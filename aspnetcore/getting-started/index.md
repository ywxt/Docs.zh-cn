---
title: ASP.NET Core 入门
author: rick-anderson
description: 介绍如何使用 ASP.NET Core 创建并运行简单的 Hello World 应用的快速教程。
ms.author: riande
ms.custom: mvc
ms.date: 05/31/2018
uid: getting-started
ms.openlocfilehash: 7ab9f303d74786c4ac76f002d0f2c66371e78cb8
ms.sourcegitcommit: b4c7b1a4c48dec0865f27874275c73da1f75e918
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2018
ms.locfileid: "39228577"
---
# <a name="get-started-with-aspnet-core"></a><span data-ttu-id="a31f2-103">ASP.NET Core 入门</span><span class="sxs-lookup"><span data-stu-id="a31f2-103">Get started with ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

1. <span data-ttu-id="a31f2-104">安装 [!INCLUDE [](~/includes/2.1-SDK.md)]。</span><span class="sxs-lookup"><span data-stu-id="a31f2-104">Install the [!INCLUDE [](~/includes/2.1-SDK.md)].</span></span>

2. <span data-ttu-id="a31f2-105">创建 ASP.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="a31f2-105">Create an ASP.NET Core project.</span></span> <span data-ttu-id="a31f2-106">打开命令行界面，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="a31f2-106">Open a command shell and enter the following command:</span></span>

    ```console
    dotnet new webapp -o aspnetcoreapp
    ```

    [!INCLUDE [](~/includes/webapp-alias-notice.md)]

3. <span data-ttu-id="a31f2-107">信任 HTTPS 开发证书：</span><span class="sxs-lookup"><span data-stu-id="a31f2-107">Trust the HTTPS development certificate:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="a31f2-108">Windows</span><span class="sxs-lookup"><span data-stu-id="a31f2-108">Windows</span></span>](#tab/windows)

    ```console
    dotnet dev-certs https --trust
    ```

   <span data-ttu-id="a31f2-109">以上命令会显示以下对话：</span><span class="sxs-lookup"><span data-stu-id="a31f2-109">The preceding command displays the following dialog:</span></span>

   ![安全警告对话](_static/cert.png)

   <span data-ttu-id="a31f2-111">如果你同意信任开发证书，请选择“是”。</span><span class="sxs-lookup"><span data-stu-id="a31f2-111">Select **Yes** if you agree to trust the development certificate.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="a31f2-112">macOS</span><span class="sxs-lookup"><span data-stu-id="a31f2-112">macOS</span></span>](#tab/macos)

    ```console
    dotnet dev-certs https --trust
    ```

   <span data-ttu-id="a31f2-113">以上命令会显示以下消息：</span><span class="sxs-lookup"><span data-stu-id="a31f2-113">The preceding command displays the following message:</span></span>

   <span data-ttu-id="a31f2-114">*请求信任 HTTPS 开发证书。如果尚未信任该证书，将运行以下命令：*`'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`*此命令可能提醒你输入密码，已在系统密钥链上安装该证书。  密码：*</span><span class="sxs-lookup"><span data-stu-id="a31f2-114">*Trusting the HTTPS development certificate was requested. If the certificate is not already trusted we will run the following command:* `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'` *This command might prompt you for your password to install the certificate on the system keychain.    Password:*</span></span>

   <span data-ttu-id="a31f2-115">如果你同意信任开发证书，请输入密码。</span><span class="sxs-lookup"><span data-stu-id="a31f2-115">Enter your password if you agree to trust the development certificate.</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="a31f2-116">Linux</span><span class="sxs-lookup"><span data-stu-id="a31f2-116">Linux</span></span>](#tab/linux)

   <a name="see-the-documentation-for-your-linux-distribution-on-how-to-trust-the-https-development-certificate"></a><span data-ttu-id="a31f2-117">查看你的 Linux 分发对应的文档，了解如何信任 HTTPS 开发证书</span><span class="sxs-lookup"><span data-stu-id="a31f2-117">See the documentation for your Linux distribution on how to trust the HTTPS development certificate</span></span>
---

4. <span data-ttu-id="a31f2-118">运行应用：</span><span class="sxs-lookup"><span data-stu-id="a31f2-118">Run the app:</span></span>

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

5. <span data-ttu-id="a31f2-119">浏览到 [http://localhost:5001](http://localhost:5001)。</span><span class="sxs-lookup"><span data-stu-id="a31f2-119">Browse to [http://localhost:5001](http://localhost:5001).</span></span>  <span data-ttu-id="a31f2-120">单击“接受”，接受隐私和 cookie 政策。</span><span class="sxs-lookup"><span data-stu-id="a31f2-120">Click **Accept** to accept the privacy and cookie policy.</span></span> <span data-ttu-id="a31f2-121">此应用不保留个人信息。</span><span class="sxs-lookup"><span data-stu-id="a31f2-121">This app doesn't keep personal information.</span></span>

6. <span data-ttu-id="a31f2-122">打开 Pages/About.cshtml，使用以下突出显示标记修改该页面：</span><span class="sxs-lookup"><span data-stu-id="a31f2-122">Open *Pages/About.cshtml* and modify the page with the following highlighted markup:</span></span>

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9)]

7. <span data-ttu-id="a31f2-123">浏览到 [http://localhost:5001/About](http://localhost:5001/About) 并验证是否显示更改。</span><span class="sxs-lookup"><span data-stu-id="a31f2-123">Browse to [http://localhost:5001/About](http://localhost:5001/About) and verify the changes are displayed.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

1. <span data-ttu-id="a31f2-124">安装 [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]。</span><span class="sxs-lookup"><span data-stu-id="a31f2-124">Install the [!INCLUDE [](~/includes/net-core-sdk-download-link.md)].</span></span>

2. <span data-ttu-id="a31f2-125">创建新的 ASP.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="a31f2-125">Create a new ASP.NET Core project.</span></span>

   <span data-ttu-id="a31f2-126">打开命令行界面。</span><span class="sxs-lookup"><span data-stu-id="a31f2-126">Open a command shell.</span></span> <span data-ttu-id="a31f2-127">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="a31f2-127">Enter the following command:</span></span>

    ```console
    dotnet new razor -o aspnetcoreapp
    ```

3. <span data-ttu-id="a31f2-128">使用以下命令运行应用：</span><span class="sxs-lookup"><span data-stu-id="a31f2-128">Run the app with the following commands:</span></span>

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

4. <span data-ttu-id="a31f2-129">浏览到 [http://localhost:5000](http://localhost:5000)。</span><span class="sxs-lookup"><span data-stu-id="a31f2-129">Browse to [http://localhost:5000](http://localhost:5000).</span></span>

5. <span data-ttu-id="a31f2-130">打开 Pages/About.cshtml 并将页面修改为显示消息“Hello, world!</span><span class="sxs-lookup"><span data-stu-id="a31f2-130">Open *Pages/About.cshtml* and modify the page to display the message "Hello, world!</span></span> <span data-ttu-id="a31f2-131">The time on the server is @DateTime.Now” ：</span><span class="sxs-lookup"><span data-stu-id="a31f2-131">The time on the server is @DateTime.Now":</span></span>

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. <span data-ttu-id="a31f2-132">浏览到 [http://localhost:5000/About](http://localhost:5000/About) 并验证更改。</span><span class="sxs-lookup"><span data-stu-id="a31f2-132">Browse to [http://localhost:5000/About](http://localhost:5000/About) and verify the changes.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. <span data-ttu-id="a31f2-133">从 [.NET Core 所有下载页面](https://www.microsoft.com/net/download/all)安装 SDK 1.0.4 的 .NET Core SDK 安装程序。</span><span class="sxs-lookup"><span data-stu-id="a31f2-133">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>

2. <span data-ttu-id="a31f2-134">为新 ASP.NET Core 项目创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="a31f2-134">Create a folder for a new ASP.NET Core project.</span></span>

   <span data-ttu-id="a31f2-135">打开命令行界面。</span><span class="sxs-lookup"><span data-stu-id="a31f2-135">Open a command shell.</span></span> <span data-ttu-id="a31f2-136">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="a31f2-136">Enter the following commands:</span></span>

   ```console
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. <span data-ttu-id="a31f2-137">如果已计算机上安装了 SDK 的更高版本，则创建一个 global.json 文件以选择 1.0.4 SDK。</span><span class="sxs-lookup"><span data-stu-id="a31f2-137">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. <span data-ttu-id="a31f2-138">创建新的 ASP.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="a31f2-138">Create a new ASP.NET Core project.</span></span>

   ```console
   dotnet new web
   ```

5. <span data-ttu-id="a31f2-139">还原程序包。</span><span class="sxs-lookup"><span data-stu-id="a31f2-139">Restore the packages.</span></span>

    ```console
    dotnet restore
    ```

6. <span data-ttu-id="a31f2-140">运行应用。</span><span class="sxs-lookup"><span data-stu-id="a31f2-140">Run the app.</span></span>

   ```console
   dotnet run
   ```

   <span data-ttu-id="a31f2-141">如有需要，[dotnet run](/dotnet/core/tools/dotnet-run) 命令会首先生成应用。</span><span class="sxs-lookup"><span data-stu-id="a31f2-141">The [dotnet run](/dotnet/core/tools/dotnet-run) command builds the app first, if needed.</span></span>

7. <span data-ttu-id="a31f2-142">浏览到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="a31f2-142">Browse to `http://localhost:5000`.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end
