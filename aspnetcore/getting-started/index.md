---
title: ASP.NET Core 入门
author: rick-anderson
description: 介绍如何使用 ASP.NET Core 创建并运行简单的 Hello World 应用的快速教程。
ms.author: riande
ms.custom: mvc
ms.date: 12/01/2018
uid: getting-started
ms.openlocfilehash: 29a328b610b0a6e1616cd6ebc70a8fa3e515eb92
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861701"
---
# <a name="tutorial-get-started-with-aspnet-core"></a><span data-ttu-id="87d64-103">教程：ASP.NET Core 入门</span><span class="sxs-lookup"><span data-stu-id="87d64-103">Tutorial: Get started with ASP.NET Core</span></span>

<span data-ttu-id="87d64-104">本教程演示如何使用 .NET Core 命令行接口创建 ASP.NET Core Web 应用。</span><span class="sxs-lookup"><span data-stu-id="87d64-104">This tutorial shows how to use the .NET Core command-line interface to create an ASP.NET Core web app.</span></span>

<span data-ttu-id="87d64-105">你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="87d64-105">You'll learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="87d64-106">创建 Web 应用项目。</span><span class="sxs-lookup"><span data-stu-id="87d64-106">Create a web app project.</span></span>
> * <span data-ttu-id="87d64-107">启用本地 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="87d64-107">Enable local HTTPS.</span></span>
> * <span data-ttu-id="87d64-108">运行应用。</span><span class="sxs-lookup"><span data-stu-id="87d64-108">Run the app.</span></span>
> * <span data-ttu-id="87d64-109">编辑 Razor 页面。</span><span class="sxs-lookup"><span data-stu-id="87d64-109">Edit a Razor page.</span></span>

<span data-ttu-id="87d64-110">最后，在本地计算机上运行工作 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="87d64-110">At the end, you'll have a working web app running on your local machine.</span></span>

![Web 应用主页](_static/home-page.png)

## <a name="prerequisites"></a><span data-ttu-id="87d64-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="87d64-112">Prerequisites</span></span>

<span data-ttu-id="87d64-113">安装 [!INCLUDE [](~/includes/2.1-SDK.md)]。</span><span class="sxs-lookup"><span data-stu-id="87d64-113">Install the [!INCLUDE [](~/includes/2.1-SDK.md)].</span></span>

## <a name="create-a-web-app-project"></a><span data-ttu-id="87d64-114">创建 Web 应用项目</span><span class="sxs-lookup"><span data-stu-id="87d64-114">Create a web app project</span></span>

<span data-ttu-id="87d64-115">打开命令行界面，然后输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="87d64-115">Open a command shell, and enter the following command:</span></span>

```console
dotnet new webapp -o aspnetcoreapp
```

## <a name="enable-local-https"></a><span data-ttu-id="87d64-116">启用本地 HTTPS</span><span class="sxs-lookup"><span data-stu-id="87d64-116">Enable local HTTPS</span></span>

<span data-ttu-id="87d64-117">信任 HTTPS 开发证书：</span><span class="sxs-lookup"><span data-stu-id="87d64-117">Trust the HTTPS development certificate:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="87d64-118">Windows</span><span class="sxs-lookup"><span data-stu-id="87d64-118">Windows</span></span>](#tab/windows)

```console
dotnet dev-certs https --trust
```

<span data-ttu-id="87d64-119">以上命令会显示以下对话：</span><span class="sxs-lookup"><span data-stu-id="87d64-119">The preceding command displays the following dialog:</span></span>

![安全警告对话](_static/cert.png)

<span data-ttu-id="87d64-121">如果你同意信任开发证书，请选择“是”。</span><span class="sxs-lookup"><span data-stu-id="87d64-121">Select **Yes** if you agree to trust the development certificate.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="87d64-122">macOS</span><span class="sxs-lookup"><span data-stu-id="87d64-122">macOS</span></span>](#tab/macos)

```console
dotnet dev-certs https --trust
```

<span data-ttu-id="87d64-123">以上命令会显示以下消息：</span><span class="sxs-lookup"><span data-stu-id="87d64-123">The preceding command displays the following message:</span></span>

<span data-ttu-id="87d64-124">*请求信任 HTTPS 开发证书。如果证书尚不受信任，我们将运行以下命令：* `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`。</span><span class="sxs-lookup"><span data-stu-id="87d64-124">*Trusting the HTTPS development certificate was requested. If the certificate is not already trusted we will run the following command:* `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`.</span></span>  
<span data-ttu-id="87d64-125">\*此命令可能会提示你输入密码以在系统密钥链上安装证书。</span><span class="sxs-lookup"><span data-stu-id="87d64-125">\*This command might prompt you for your password to install the certificate on the system keychain.</span></span>

<span data-ttu-id="87d64-126">密码：\*</span><span class="sxs-lookup"><span data-stu-id="87d64-126">Password:\*</span></span>

<span data-ttu-id="87d64-127">如果你同意信任开发证书，请输入密码。</span><span class="sxs-lookup"><span data-stu-id="87d64-127">Enter your password if you agree to trust the development certificate.</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="87d64-128">Linux</span><span class="sxs-lookup"><span data-stu-id="87d64-128">Linux</span></span>](#tab/linux)

<span data-ttu-id="87d64-129">查看你的 Linux 分发对应的文档，了解如何信任 HTTPS 开发证书。</span><span class="sxs-lookup"><span data-stu-id="87d64-129">See the documentation for your Linux distribution on how to trust the HTTPS development certificate.</span></span>

---

## <a name="run-the-app"></a><span data-ttu-id="87d64-130">运行应用</span><span class="sxs-lookup"><span data-stu-id="87d64-130">Run the app</span></span>

<span data-ttu-id="87d64-131">运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="87d64-131">Run the following commands:</span></span>

```console
cd aspnetcoreapp
dotnet run
```

<span data-ttu-id="87d64-132">浏览到 [https://localhost:5001](https://localhost:5001)。</span><span class="sxs-lookup"><span data-stu-id="87d64-132">Browse to [https://localhost:5001](https://localhost:5001).</span></span> <span data-ttu-id="87d64-133">单击“接受”，接受隐私和 cookie 政策。</span><span class="sxs-lookup"><span data-stu-id="87d64-133">Click **Accept** to accept the privacy and cookie policy.</span></span> <span data-ttu-id="87d64-134">此应用不保留个人信息。</span><span class="sxs-lookup"><span data-stu-id="87d64-134">This app doesn't keep personal information.</span></span>

## <a name="edit-a-razor-page"></a><span data-ttu-id="87d64-135">编辑 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="87d64-135">Edit a Razor page</span></span>

<span data-ttu-id="87d64-136">打开 Pages/About.cshtml，使用以下突出显示标记修改该页面：</span><span class="sxs-lookup"><span data-stu-id="87d64-136">Open *Pages/About.cshtml* and modify the page with the following highlighted markup:</span></span>

[!code-cshtml[](sample/getting-started/about.cshtml?highlight=9)]

<span data-ttu-id="87d64-137">浏览到 [https://localhost:5001/About](https://localhost:5001/About) 并验证是否显示更改。</span><span class="sxs-lookup"><span data-stu-id="87d64-137">Browse to [https://localhost:5001/About](https://localhost:5001/About) and verify the changes are displayed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87d64-138">后续步骤</span><span class="sxs-lookup"><span data-stu-id="87d64-138">Next steps</span></span>

<span data-ttu-id="87d64-139">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="87d64-139">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="87d64-140">创建 Web 应用项目。</span><span class="sxs-lookup"><span data-stu-id="87d64-140">Create a web app project.</span></span>
> * <span data-ttu-id="87d64-141">启用本地 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="87d64-141">Enable local HTTPS.</span></span>
> * <span data-ttu-id="87d64-142">运行该项目。</span><span class="sxs-lookup"><span data-stu-id="87d64-142">Run the project.</span></span>
> * <span data-ttu-id="87d64-143">进行更改。</span><span class="sxs-lookup"><span data-stu-id="87d64-143">Make a change.</span></span>

<span data-ttu-id="87d64-144">若要了解有关 ASP.NET Core 的详细信息，请参阅简介：</span><span class="sxs-lookup"><span data-stu-id="87d64-144">To learn more about ASP.NET Core, see the introduction:</span></span>

> [!div class="nextstepaction"]
> <xref:index>

> [!NOTE]
> <span data-ttu-id="87d64-145">我们要测试所建议的新 ASP.NET Core 目录结构是否可用。</span><span class="sxs-lookup"><span data-stu-id="87d64-145">We're testing the usability of a proposed new structure for the ASP.NET Core table of contents.</span></span> <span data-ttu-id="87d64-146">如果有几分钟时间尝试了解当前或所建议目录中的七个不同主题，请[单击此处参与调查](https://dpk4xbh5.optimalworkshop.com/treejack/aa11wn82)。</span><span class="sxs-lookup"><span data-stu-id="87d64-146">If you have a few minutes to try an exercise of finding seven different topics in the current or proposed table of contents, please [click here to participate in the study](https://dpk4xbh5.optimalworkshop.com/treejack/aa11wn82).</span></span>
