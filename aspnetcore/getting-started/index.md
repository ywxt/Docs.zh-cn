---
title: ASP.NET Core 入门
author: rick-anderson
description: 介绍如何使用 ASP.NET Core 创建并运行简单的 Hello World 应用的快速教程。
ms.author: riande
ms.custom: mvc
ms.date: 05/31/2018
uid: getting-started
ms.openlocfilehash: 22e9c982921cc03d89506e18ff99bf481027dda6
ms.sourcegitcommit: b8a2f14bf8dd346d7592977642b610bbcb0b0757
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38216208"
---
# <a name="get-started-with-aspnet-core"></a><span data-ttu-id="11141-103">ASP.NET Core 入门</span><span class="sxs-lookup"><span data-stu-id="11141-103">Get started with ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

1. <span data-ttu-id="11141-104">安装 [!INCLUDE [](~/includes/2.1-SDK.md)]。</span><span class="sxs-lookup"><span data-stu-id="11141-104">Install the [!INCLUDE [](~/includes/2.1-SDK.md)].</span></span>

2. <span data-ttu-id="11141-105">创建 ASP.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="11141-105">Create an ASP.NET Core project.</span></span> <span data-ttu-id="11141-106">打开命令行界面，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="11141-106">Open a command shell and enter the following command:</span></span>

    ```console
    dotnet new webapp -o aspnetcoreapp
    ```

    <span data-ttu-id="11141-107">[!INCLUDE [](~/includes/webapp-alias-notice.md) [](~/includes/webapp-alias-notice.md)]</span><span class="sxs-lookup"><span data-stu-id="11141-107">[!INCLUDE [](~/includes/webapp-alias-notice.md) [](~/includes/webapp-alias-notice.md)]</span></span>

3. <span data-ttu-id="11141-108">信任 HTTPS 开发证书：</span><span class="sxs-lookup"><span data-stu-id="11141-108">Trust the HTTPS development certificate:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="11141-109">Windows</span><span class="sxs-lookup"><span data-stu-id="11141-109">Windows</span></span>](#tab/windows)

    ```console
    dotnet dev-certs https --trust
    ```

    The preceding command displays the following dialog:

    ![Security warning dialog](_static/cert.png)

    Select **Yes** if you agree to trust the development certificate.

# <a name="macostabmacos"></a>[<span data-ttu-id="11141-110">macOS</span><span class="sxs-lookup"><span data-stu-id="11141-110">macOS</span></span>](#tab/macos)

    ```console
    dotnet dev-certs https --trust
    ```

    The preceding command displays the following message:

    *Trusting the HTTPS development certificate was requested. If the certificate is not already trusted we will run the following command:*
    `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`
    *This command might prompt you for your password to install the certificate on the system keychain.
    Password:*

    Enter your password if you agree to trust the development certificate.

# <a name="linuxtablinux"></a>[<span data-ttu-id="11141-111">Linux</span><span class="sxs-lookup"><span data-stu-id="11141-111">Linux</span></span>](#tab/linux)

    See the documentation for your Linux distribution on how to trust the HTTPS development certificate
---

4. <span data-ttu-id="11141-112">运行应用：</span><span class="sxs-lookup"><span data-stu-id="11141-112">Run the app:</span></span>

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

5. <span data-ttu-id="11141-113">浏览到 [http://localhost:5001](http://localhost:5001)。</span><span class="sxs-lookup"><span data-stu-id="11141-113">Browse to [http://localhost:5001](http://localhost:5001).</span></span>  <span data-ttu-id="11141-114">单击“接受”，接受隐私和 cookie 政策。</span><span class="sxs-lookup"><span data-stu-id="11141-114">Click **Accept** to accept the privacy and cookie policy.</span></span> <span data-ttu-id="11141-115">此应用不保留个人信息。</span><span class="sxs-lookup"><span data-stu-id="11141-115">This app doesn't keep personal information.</span></span>

6. <span data-ttu-id="11141-116">打开 Pages/About.cshtml，使用以下突出显示标记修改该页面：</span><span class="sxs-lookup"><span data-stu-id="11141-116">Open *Pages/About.cshtml* and modify the page with the following highlighted markup:</span></span>

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9)]

7. <span data-ttu-id="11141-117">浏览到 [http://localhost:5001/About](http://localhost:5001/About) 并验证是否显示更改。</span><span class="sxs-lookup"><span data-stu-id="11141-117">Browse to [http://localhost:5001/About](http://localhost:5001/About) and verify the changes are displayed.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

1. <span data-ttu-id="11141-118">安装 [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]。</span><span class="sxs-lookup"><span data-stu-id="11141-118">Install the [!INCLUDE [](~/includes/net-core-sdk-download-link.md)].</span></span>

2. <span data-ttu-id="11141-119">创建新的 ASP.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="11141-119">Create a new ASP.NET Core project.</span></span>

   <span data-ttu-id="11141-120">打开命令行界面。</span><span class="sxs-lookup"><span data-stu-id="11141-120">Open a command shell.</span></span> <span data-ttu-id="11141-121">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="11141-121">Enter the following command:</span></span>

    ```console
    dotnet new razor -o aspnetcoreapp
    ```

3. <span data-ttu-id="11141-122">使用以下命令运行应用：</span><span class="sxs-lookup"><span data-stu-id="11141-122">Run the app with the following commands:</span></span>

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

4. <span data-ttu-id="11141-123">浏览到 [http://localhost:5000](http://localhost:5000)。</span><span class="sxs-lookup"><span data-stu-id="11141-123">Browse to [http://localhost:5000](http://localhost:5000).</span></span>

5. <span data-ttu-id="11141-124">打开 Pages/About.cshtml 并将页面修改为显示消息“Hello, world!</span><span class="sxs-lookup"><span data-stu-id="11141-124">Open *Pages/About.cshtml* and modify the page to display the message "Hello, world!</span></span> <span data-ttu-id="11141-125">The time on the server is @DateTime.Now” ：</span><span class="sxs-lookup"><span data-stu-id="11141-125">The time on the server is @DateTime.Now":</span></span>

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. <span data-ttu-id="11141-126">浏览到 [http://localhost:5000/About](http://localhost:5000/About) 并验证更改。</span><span class="sxs-lookup"><span data-stu-id="11141-126">Browse to [http://localhost:5000/About](http://localhost:5000/About) and verify the changes.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. <span data-ttu-id="11141-127">从 [.NET Core 所有下载页面](https://www.microsoft.com/net/download/all)安装 SDK 1.0.4 的 .NET Core SDK 安装程序。</span><span class="sxs-lookup"><span data-stu-id="11141-127">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>

2. <span data-ttu-id="11141-128">为新 ASP.NET Core 项目创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="11141-128">Create a folder for a new ASP.NET Core project.</span></span>

   <span data-ttu-id="11141-129">打开命令行界面。</span><span class="sxs-lookup"><span data-stu-id="11141-129">Open a command shell.</span></span> <span data-ttu-id="11141-130">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="11141-130">Enter the following commands:</span></span>

   ```console
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. <span data-ttu-id="11141-131">如果已计算机上安装了 SDK 的更高版本，则创建一个 global.json 文件以选择 1.0.4 SDK。</span><span class="sxs-lookup"><span data-stu-id="11141-131">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. <span data-ttu-id="11141-132">创建新的 ASP.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="11141-132">Create a new ASP.NET Core project.</span></span>

   ```console
   dotnet new web
   ```

5. <span data-ttu-id="11141-133">还原程序包。</span><span class="sxs-lookup"><span data-stu-id="11141-133">Restore the packages.</span></span>

    ```console
    dotnet restore
    ```

6. <span data-ttu-id="11141-134">运行应用。</span><span class="sxs-lookup"><span data-stu-id="11141-134">Run the app.</span></span>

   ```console
   dotnet run
   ```

   <span data-ttu-id="11141-135">如有需要，[dotnet run](/dotnet/core/tools/dotnet-run) 命令会首先生成应用。</span><span class="sxs-lookup"><span data-stu-id="11141-135">The [dotnet run](/dotnet/core/tools/dotnet-run) command builds the app first, if needed.</span></span>

7. <span data-ttu-id="11141-136">浏览到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="11141-136">Browse to `http://localhost:5000`.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end
