---
title: ASP.NET Core 入门
author: rick-anderson
description: 介绍如何使用 ASP.NET Core 创建并运行简单的 Hello World 应用的快速教程。
ms.author: riande
ms.custom: mvc
ms.date: 05/31/2018
uid: getting-started
ms.openlocfilehash: a6a5023594aec01370143e7d1f35fb45c109122a
ms.sourcegitcommit: 13940eb53c68664b11a2d685ee17c78faab1945d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47860935"
---
# <a name="get-started-with-aspnet-core"></a><span data-ttu-id="e0146-103">ASP.NET Core 入门</span><span class="sxs-lookup"><span data-stu-id="e0146-103">Get started with ASP.NET Core</span></span>

<span data-ttu-id="e0146-104">本文档提供了用于创建和运行 ASP.NET Core 应用的步骤。</span><span class="sxs-lookup"><span data-stu-id="e0146-104">This document provides steps for creating and running an ASP.NET Core app.</span></span>

::: moniker range=">= aspnetcore-2.1"

1. <span data-ttu-id="e0146-105">安装 [!INCLUDE [](~/includes/2.1-SDK.md)]。</span><span class="sxs-lookup"><span data-stu-id="e0146-105">Install the [!INCLUDE [](~/includes/2.1-SDK.md)].</span></span>

2. <span data-ttu-id="e0146-106">创建 ASP.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="e0146-106">Create an ASP.NET Core project.</span></span> <span data-ttu-id="e0146-107">打开命令行界面，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="e0146-107">Open a command shell and enter the following command:</span></span>

   ```console
   dotnet new webapp -o aspnetcoreapp
   ```

3. <span data-ttu-id="e0146-108">信任 HTTPS 开发证书：</span><span class="sxs-lookup"><span data-stu-id="e0146-108">Trust the HTTPS development certificate:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="e0146-109">Windows</span><span class="sxs-lookup"><span data-stu-id="e0146-109">Windows</span></span>](#tab/windows)

  ```console
  dotnet dev-certs https --trust
  ```

  <span data-ttu-id="e0146-110">以上命令会显示以下对话：</span><span class="sxs-lookup"><span data-stu-id="e0146-110">The preceding command displays the following dialog:</span></span>

  ![安全警告对话](_static/cert.png)

  <span data-ttu-id="e0146-112">如果你同意信任开发证书，请选择“是”。</span><span class="sxs-lookup"><span data-stu-id="e0146-112">Select **Yes** if you agree to trust the development certificate.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="e0146-113">macOS</span><span class="sxs-lookup"><span data-stu-id="e0146-113">macOS</span></span>](#tab/macos)

  ```console
  dotnet dev-certs https --trust
  ```

  <span data-ttu-id="e0146-114">以上命令会显示以下消息：</span><span class="sxs-lookup"><span data-stu-id="e0146-114">The preceding command displays the following message:</span></span>

  <span data-ttu-id="e0146-115">*请求信任 HTTPS 开发证书。如果证书尚不受信任，我们将运行以下命令：* `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`。</span><span class="sxs-lookup"><span data-stu-id="e0146-115">*Trusting the HTTPS development certificate was requested. If the certificate is not already trusted we will run the following command:* `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`.</span></span>  
  <span data-ttu-id="e0146-116">\*此命令可能会提示你输入密码以在系统密钥链上安装证书。</span><span class="sxs-lookup"><span data-stu-id="e0146-116">\*This command might prompt you for your password to install the certificate on the system keychain.</span></span>
  
  <span data-ttu-id="e0146-117">密码：\*</span><span class="sxs-lookup"><span data-stu-id="e0146-117">Password:\*</span></span>

  <span data-ttu-id="e0146-118">如果你同意信任开发证书，请输入密码。</span><span class="sxs-lookup"><span data-stu-id="e0146-118">Enter your password if you agree to trust the development certificate.</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="e0146-119">Linux</span><span class="sxs-lookup"><span data-stu-id="e0146-119">Linux</span></span>](#tab/linux)

  <span data-ttu-id="e0146-120">查看你的 Linux 分发对应的文档，了解如何信任 HTTPS 开发证书。</span><span class="sxs-lookup"><span data-stu-id="e0146-120">See the documentation for your Linux distribution on how to trust the HTTPS development certificate.</span></span>
   
---

4. <span data-ttu-id="e0146-121">运行应用：</span><span class="sxs-lookup"><span data-stu-id="e0146-121">Run the app:</span></span>

   ```console
   cd aspnetcoreapp
   dotnet run
   ```

5. <span data-ttu-id="e0146-122">浏览到 [http://localhost:5001](http://localhost:5001)。</span><span class="sxs-lookup"><span data-stu-id="e0146-122">Browse to [http://localhost:5001](http://localhost:5001).</span></span>  <span data-ttu-id="e0146-123">单击“接受”，接受隐私和 cookie 政策。</span><span class="sxs-lookup"><span data-stu-id="e0146-123">Click **Accept** to accept the privacy and cookie policy.</span></span> <span data-ttu-id="e0146-124">此应用不保留个人信息。</span><span class="sxs-lookup"><span data-stu-id="e0146-124">This app doesn't keep personal information.</span></span>

6. <span data-ttu-id="e0146-125">打开 Pages/About.cshtml，使用以下突出显示标记修改该页面：</span><span class="sxs-lookup"><span data-stu-id="e0146-125">Open *Pages/About.cshtml* and modify the page with the following highlighted markup:</span></span>

   [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9)]

7. <span data-ttu-id="e0146-126">浏览到 [http://localhost:5001/About](http://localhost:5001/About) 并验证是否显示更改。</span><span class="sxs-lookup"><span data-stu-id="e0146-126">Browse to [http://localhost:5001/About](http://localhost:5001/About) and verify the changes are displayed.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

1. <span data-ttu-id="e0146-127">安装 [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]。</span><span class="sxs-lookup"><span data-stu-id="e0146-127">Install the [!INCLUDE [](~/includes/net-core-sdk-download-link.md)].</span></span>

2. <span data-ttu-id="e0146-128">创建新的 ASP.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="e0146-128">Create a new ASP.NET Core project.</span></span>

   <span data-ttu-id="e0146-129">打开命令行界面。</span><span class="sxs-lookup"><span data-stu-id="e0146-129">Open a command shell.</span></span> <span data-ttu-id="e0146-130">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="e0146-130">Enter the following command:</span></span>

   ```console
   dotnet new razor -o aspnetcoreapp
   ```

3. <span data-ttu-id="e0146-131">使用以下命令运行应用：</span><span class="sxs-lookup"><span data-stu-id="e0146-131">Run the app with the following commands:</span></span>

   ```console
   cd aspnetcoreapp
   dotnet run
   ```

4. <span data-ttu-id="e0146-132">浏览到 [http://localhost:5000](http://localhost:5000)。</span><span class="sxs-lookup"><span data-stu-id="e0146-132">Browse to [http://localhost:5000](http://localhost:5000).</span></span>

5. <span data-ttu-id="e0146-133">打开 Pages/About.cshtml 并将页面修改为显示消息“Hello, world!</span><span class="sxs-lookup"><span data-stu-id="e0146-133">Open *Pages/About.cshtml* and modify the page to display the message "Hello, world!</span></span> <span data-ttu-id="e0146-134">The time on the server is @DateTime.Now” ：</span><span class="sxs-lookup"><span data-stu-id="e0146-134">The time on the server is @DateTime.Now":</span></span>

   [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. <span data-ttu-id="e0146-135">浏览到 [http://localhost:5000/About](http://localhost:5000/About) 并验证更改。</span><span class="sxs-lookup"><span data-stu-id="e0146-135">Browse to [http://localhost:5000/About](http://localhost:5000/About) and verify the changes.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. <span data-ttu-id="e0146-136">从 [.NET Core 所有下载页面](https://www.microsoft.com/net/download/all)安装 SDK 1.0.4 的 .NET Core SDK 安装程序。</span><span class="sxs-lookup"><span data-stu-id="e0146-136">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>

2. <span data-ttu-id="e0146-137">为新 ASP.NET Core 项目创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="e0146-137">Create a folder for a new ASP.NET Core project.</span></span>

   <span data-ttu-id="e0146-138">打开命令行界面。</span><span class="sxs-lookup"><span data-stu-id="e0146-138">Open a command shell.</span></span> <span data-ttu-id="e0146-139">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="e0146-139">Enter the following commands:</span></span>

   ```console
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. <span data-ttu-id="e0146-140">如果已计算机上安装了 SDK 的更高版本，则创建一个 global.json 文件以选择 1.0.4 SDK。</span><span class="sxs-lookup"><span data-stu-id="e0146-140">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. <span data-ttu-id="e0146-141">创建新的 ASP.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="e0146-141">Create a new ASP.NET Core project.</span></span>

   ```console
   dotnet new web
   ```

5. <span data-ttu-id="e0146-142">还原程序包。</span><span class="sxs-lookup"><span data-stu-id="e0146-142">Restore the packages.</span></span>

   ```console
   dotnet restore
   ```

6. <span data-ttu-id="e0146-143">运行应用。</span><span class="sxs-lookup"><span data-stu-id="e0146-143">Run the app.</span></span>

   ```console
   dotnet run
   ```

   <span data-ttu-id="e0146-144">如有需要，[dotnet run](/dotnet/core/tools/dotnet-run) 命令会首先生成应用。</span><span class="sxs-lookup"><span data-stu-id="e0146-144">The [dotnet run](/dotnet/core/tools/dotnet-run) command builds the app first, if needed.</span></span>

7. <span data-ttu-id="e0146-145">浏览到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="e0146-145">Browse to `http://localhost:5000`.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end
