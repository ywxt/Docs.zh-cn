---
title: ASP.NET Core 入门
author: rick-anderson
description: 介绍如何使用 ASP.NET Core 创建并运行简单的 Hello World 应用的快速教程。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/10/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: getting-started
ms.openlocfilehash: e814277663ff5a964171a71ebb6e0f094e0ddc60
ms.sourcegitcommit: 3d071fabaf90e32906df97b08a8d00e602db25c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="get-started-with-aspnet-core"></a><span data-ttu-id="da1bc-103">ASP.NET Core 入门</span><span class="sxs-lookup"><span data-stu-id="da1bc-103">Get started with ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.0"

1. <span data-ttu-id="da1bc-104">安装 [!INCLUDE[](~/includes/net-core-sdk-download-link.md)]。</span><span class="sxs-lookup"><span data-stu-id="da1bc-104">Install the [!INCLUDE[](~/includes/net-core-sdk-download-link.md)].</span></span>

2. <span data-ttu-id="da1bc-105">创建新的 .NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="da1bc-105">Create a new .NET Core project.</span></span>

   <span data-ttu-id="da1bc-106">在 macOS 和 Linux 上，打开终端窗口。</span><span class="sxs-lookup"><span data-stu-id="da1bc-106">On macOS and Linux, open a terminal window.</span></span> <span data-ttu-id="da1bc-107">在 Windows 上，打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="da1bc-107">On Windows, open a command prompt.</span></span> <span data-ttu-id="da1bc-108">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="da1bc-108">Enter the following command:</span></span>

    ```terminal
    dotnet new razor -o aspnetcoreapp
    ```

3. <span data-ttu-id="da1bc-109">使用以下命令运行应用：</span><span class="sxs-lookup"><span data-stu-id="da1bc-109">Run the app with the following commands:</span></span>

    ```terminal
    cd aspnetcoreapp
    dotnet run
    ```

4. <span data-ttu-id="da1bc-110">浏览到 [http://localhost:5000](http://localhost:5000)。</span><span class="sxs-lookup"><span data-stu-id="da1bc-110">Browse to [http://localhost:5000](http://localhost:5000).</span></span>

5. <span data-ttu-id="da1bc-111">打开 Pages/About.cshtml 并将页面修改为显示消息“Hello, world!</span><span class="sxs-lookup"><span data-stu-id="da1bc-111">Open *Pages/About.cshtml* and modify the page to display the message "Hello, world!</span></span> <span data-ttu-id="da1bc-112">The time on the server is @DateTime.Now” ：</span><span class="sxs-lookup"><span data-stu-id="da1bc-112">The time on the server is @DateTime.Now":</span></span>

    <span data-ttu-id="da1bc-113">[!code-cshtml[](getting-started/sample/getting-started/about.cshtml?highlight=9&range=1-9)]</span><span class="sxs-lookup"><span data-stu-id="da1bc-113">[!code-cshtml[](getting-started/sample/getting-started/about.cshtml?highlight=9&range=1-9)]</span></span>

6. <span data-ttu-id="da1bc-114">浏览到 [http://localhost:5000/About](http://localhost:5000/About) 并验证更改。</span><span class="sxs-lookup"><span data-stu-id="da1bc-114">Browse to [http://localhost:5000/About](http://localhost:5000/About) and verify the changes.</span></span>

[!INCLUDE[next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. <span data-ttu-id="da1bc-115">从 [.NET Core 所有下载页面](https://www.microsoft.com/net/download/all)安装 SDK 1.0.4 的 .NET Core SDK 安装程序。</span><span class="sxs-lookup"><span data-stu-id="da1bc-115">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>

2. <span data-ttu-id="da1bc-116">为新 .NET Core 项目创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="da1bc-116">Create a folder for a new .NET Core project.</span></span>

   <span data-ttu-id="da1bc-117">在 macOS 和 Linux 上，打开终端窗口。</span><span class="sxs-lookup"><span data-stu-id="da1bc-117">On macOS and Linux, open a terminal window.</span></span> <span data-ttu-id="da1bc-118">在 Windows 上，打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="da1bc-118">On Windows, open a command prompt.</span></span>

   ```terminal
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. <span data-ttu-id="da1bc-119">如果已计算机上安装了 SDK 的更高版本，则创建一个 global.json 文件以选择 1.0.4 SDK。</span><span class="sxs-lookup"><span data-stu-id="da1bc-119">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. <span data-ttu-id="da1bc-120">创建新的 .NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="da1bc-120">Create a new .NET Core project.</span></span>

   ```terminal
   dotnet new web
   ```

5. <span data-ttu-id="da1bc-121">还原程序包。</span><span class="sxs-lookup"><span data-stu-id="da1bc-121">Restore the packages.</span></span>

    ```terminal
    dotnet restore
    ```

6. <span data-ttu-id="da1bc-122">运行应用。</span><span class="sxs-lookup"><span data-stu-id="da1bc-122">Run the app.</span></span>

   ```terminal
   dotnet run
   ```

   <span data-ttu-id="da1bc-123">如有需要，[dotnet run](/dotnet/core/tools/dotnet-run) 命令会首先生成应用。</span><span class="sxs-lookup"><span data-stu-id="da1bc-123">The [dotnet run](/dotnet/core/tools/dotnet-run) command builds the app first, if needed.</span></span>

7. <span data-ttu-id="da1bc-124">浏览到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="da1bc-124">Browse to `http://localhost:5000`.</span></span>

[!INCLUDE[next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end