---
title: "使用 ASP.NET Core 和 VS Code 创建 Web API"
description: "在 macOS、Linux 或 Windows 上使用 ASP.NET Core MVC 和 Visual Studio Code 构建 Web API"
author: rick-anderson
ms.author: riande
ms.date: 09/22/2017
ms.topic: get-started-article
ms.prod: asp.net-core
ms.technology: aspnet
keywords: "ASP.NET Core, WebAPI, Web API, REST, Mac, Linux, HTTP, 服务, HTTP 服务, VS Code"
manager: wpickett
ms.assetid: 830b4bf5-dd14-423e-9f59-764a6f13a8f6
uid: tutorials/web-api-vsc
ms.openlocfilehash: 40f9259101e5d006378562a27e97948641e29450
ms.sourcegitcommit: 281f0c614543a6c3db565ea4655b70fe49b61d84
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2018
---
# <a name="create-a-web-api-with-aspnet-core-mvc-and-visual-studio-code-on-linux-macos-and-windows"></a><span data-ttu-id="d01bb-104">在Linux、macOS 或 Windows 上使用 ASP.NET Core MVC 和 Visual Studio Code 创建 Web API</span><span class="sxs-lookup"><span data-stu-id="d01bb-104">Create a Web API with ASP.NET Core MVC and Visual Studio Code on Linux, macOS, and Windows</span></span>

<span data-ttu-id="d01bb-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="d01bb-105">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

<span data-ttu-id="d01bb-106">在本教程中，将生成用于管理“待办事项”列表的 Web API。</span><span class="sxs-lookup"><span data-stu-id="d01bb-106">In this tutorial, you’ll build a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="d01bb-107">不会生成 UI。</span><span class="sxs-lookup"><span data-stu-id="d01bb-107">You won’t build a UI.</span></span>

<span data-ttu-id="d01bb-108">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="d01bb-108">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="d01bb-109">macOS、Linux、Windows：使用 Visual Studio Code 创建 Web API（本教程）</span><span class="sxs-lookup"><span data-stu-id="d01bb-109">macOS, Linux, Windows: Web API with Visual Studio Code (This tutorial)</span></span>
* <span data-ttu-id="d01bb-110">macOS：[使用 Visual Studio for Mac 创建 Web API](xref:tutorials/first-web-api-mac)</span><span class="sxs-lookup"><span data-stu-id="d01bb-110">macOS: [Web API with Visual Studio for Mac](xref:tutorials/first-web-api-mac)</span></span>
* <span data-ttu-id="d01bb-111">Windows：[使用 Visual Studio for Windows 创建 Web API](xref:tutorials/first-web-api)</span><span class="sxs-lookup"><span data-stu-id="d01bb-111">Windows: [Web API with Visual Studio for Windows](xref:tutorials/first-web-api)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[template files](../includes/webApi/intro.md)]

## <a name="set-up-your-development-environment"></a><span data-ttu-id="d01bb-112">设置开发环境</span><span class="sxs-lookup"><span data-stu-id="d01bb-112">Set up your development environment</span></span>

<span data-ttu-id="d01bb-113">下载和安装：</span><span class="sxs-lookup"><span data-stu-id="d01bb-113">Download and install:</span></span>
- <span data-ttu-id="d01bb-114">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="d01bb-114">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later.</span></span>
- [<span data-ttu-id="d01bb-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d01bb-115">Visual Studio Code</span></span>](https://code.visualstudio.com)
- <span data-ttu-id="d01bb-116">Visual Studio Code [C# 扩展](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span><span class="sxs-lookup"><span data-stu-id="d01bb-116">Visual Studio Code [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span></span>

## <a name="create-the-project"></a><span data-ttu-id="d01bb-117">创建项目</span><span class="sxs-lookup"><span data-stu-id="d01bb-117">Create the project</span></span>

<span data-ttu-id="d01bb-118">从控制台运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="d01bb-118">From a console, run the following commands:</span></span>

```console
mkdir TodoApi
cd TodoApi
dotnet new webapi
```

<span data-ttu-id="d01bb-119">在 Visual Studio Code (VS Code) 中打开“TodoApi”文件夹并选择“Startup.cs”文件。</span><span class="sxs-lookup"><span data-stu-id="d01bb-119">Open the *TodoApi* folder in Visual Studio Code (VS Code) and select the *Startup.cs* file.</span></span>

- <span data-ttu-id="d01bb-120">对于警告消息 -“"TodoApi" 中缺少进行生成和调试所需的资产。是否添加它们?”，。</span><span class="sxs-lookup"><span data-stu-id="d01bb-120">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'TodoApi'.</span></span> <span data-ttu-id="d01bb-121">请选择“是”</span><span class="sxs-lookup"><span data-stu-id="d01bb-121">Add them?"</span></span>
- <span data-ttu-id="d01bb-122">对于信息性消息 -“存在未解析的依赖项”，请选择“还原”。</span><span class="sxs-lookup"><span data-stu-id="d01bb-122">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

<!-- uid: tutorials/first-mvc-app-xplat/start-mvc uses the pic below. If you change it, make sure it's consistent -->

![带有“"TodoApi" 中缺少进行生成和调试所需的资产。是否添加它们?”](web-api-vsc/_static/vsc_restore.png)

<span data-ttu-id="d01bb-126">按“调试”(F5) 生成并运行程序。</span><span class="sxs-lookup"><span data-stu-id="d01bb-126">Press **Debug** (F5) to build and run the program.</span></span> <span data-ttu-id="d01bb-127">在浏览器中，导航到 http://localhost:5000/api/values。</span><span class="sxs-lookup"><span data-stu-id="d01bb-127">In a browser navigate to http://localhost:5000/api/values .</span></span> <span data-ttu-id="d01bb-128">将显示以下内容：</span><span class="sxs-lookup"><span data-stu-id="d01bb-128">The following is displayed:</span></span>

`["value1","value2"]`

<span data-ttu-id="d01bb-129">有关 VS Code 的使用技巧，请参阅 [Visual Studio Code 帮助](#visual-studio-code-help)。</span><span class="sxs-lookup"><span data-stu-id="d01bb-129">See [Visual Studio Code help](#visual-studio-code-help) for tips on using VS Code.</span></span>

## <a name="add-support-for-entity-framework-core"></a><span data-ttu-id="d01bb-130">添加对 Entity Framework Core 的支持</span><span class="sxs-lookup"><span data-stu-id="d01bb-130">Add support for Entity Framework Core</span></span>

<span data-ttu-id="d01bb-131">在 .NET Core 2.0 中创建新项目会在 TodoApi.csproj 文件中添加“Microsoft.AspNetCore.All”提供程序。</span><span class="sxs-lookup"><span data-stu-id="d01bb-131">Creating a new project in .NET Core 2.0 adds the 'Microsoft.AspNetCore.All' provider in the *TodoApi.csproj* file.</span></span> <span data-ttu-id="d01bb-132">无需单独安装 [Entity Framework Core InMemory](https://docs.microsoft.com/ef/core/providers/in-memory/) 数据库提供程序。</span><span class="sxs-lookup"><span data-stu-id="d01bb-132">There is no need to install the [Entity Framework Core InMemory](https://docs.microsoft.com/ef/core/providers/in-memory/) database provider separately.</span></span> <span data-ttu-id="d01bb-133">此数据库提供程序允许将 Entity Framework Core 和内存数据库一起使用。</span><span class="sxs-lookup"><span data-stu-id="d01bb-133">This database provider allows Entity Framework Core to be used with an in-memory database.</span></span>

[!code-xml[Main](web-api-vsc/sample/TodoApi/TodoApi.csproj?highlight=12)]

## <a name="add-a-model-class"></a><span data-ttu-id="d01bb-134">添加模型类</span><span class="sxs-lookup"><span data-stu-id="d01bb-134">Add a model class</span></span>

<span data-ttu-id="d01bb-135">模型是表示应用程序中的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="d01bb-135">A model is an object that represents the data in your application.</span></span> <span data-ttu-id="d01bb-136">在此示例中，唯一的模型是待办事项。</span><span class="sxs-lookup"><span data-stu-id="d01bb-136">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="d01bb-137">添加名为“模型”的文件夹。</span><span class="sxs-lookup"><span data-stu-id="d01bb-137">Add a folder named *Models*.</span></span> <span data-ttu-id="d01bb-138">可将模型类置于项目的任意位置，但按照惯例会使用“模型”文件夹。</span><span class="sxs-lookup"><span data-stu-id="d01bb-138">You can put model classes anywhere in your project, but the *Models* folder is used by convention.</span></span>

<span data-ttu-id="d01bb-139">添加带有以下代码的 `TodoItem` 类：</span><span class="sxs-lookup"><span data-stu-id="d01bb-139">Add a `TodoItem` class with the following code:</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="d01bb-140">创建 `TodoItem` 时，数据库将生成 `Id`。</span><span class="sxs-lookup"><span data-stu-id="d01bb-140">The database generates the `Id` when a `TodoItem` is created.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="d01bb-141">创建数据库上下文</span><span class="sxs-lookup"><span data-stu-id="d01bb-141">Create the database context</span></span>

<span data-ttu-id="d01bb-142">数据库上下文是为给定数据模型协调 Entity Framework 功能的主类。</span><span class="sxs-lookup"><span data-stu-id="d01bb-142">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="d01bb-143">将通过从 `Microsoft.EntityFrameworkCore.DbContext` 类派生的方式创建此类。</span><span class="sxs-lookup"><span data-stu-id="d01bb-143">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="d01bb-144">在“模型”文件夹中添加 `TodoContext` 类：</span><span class="sxs-lookup"><span data-stu-id="d01bb-144">Add a `TodoContext` class in the *Models* folder:</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

## <a name="add-a-controller"></a><span data-ttu-id="d01bb-145">添加控制器</span><span class="sxs-lookup"><span data-stu-id="d01bb-145">Add a controller</span></span>

<span data-ttu-id="d01bb-146">在“控制器”文件夹中，创建名为 `TodoController` 的类。</span><span class="sxs-lookup"><span data-stu-id="d01bb-146">In the *Controllers* folder, create a class named `TodoController`.</span></span> <span data-ttu-id="d01bb-147">添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="d01bb-147">Add the following code:</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="d01bb-148">启动应用</span><span class="sxs-lookup"><span data-stu-id="d01bb-148">Launch the app</span></span>

<span data-ttu-id="d01bb-149">在 VS Code 中，按 F5 启动应用。</span><span class="sxs-lookup"><span data-stu-id="d01bb-149">In VS Code, press F5 to launch the app.</span></span> <span data-ttu-id="d01bb-150">导航到 http://localhost:5000/api/todo（之前创建的 `Todo` 控制器）。</span><span class="sxs-lookup"><span data-stu-id="d01bb-150">Navigate to  http://localhost:5000/api/todo   (The `Todo` controller we just created).</span></span>

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

## <a name="visual-studio-code-help"></a><span data-ttu-id="d01bb-151">Visual Studio Code 帮助</span><span class="sxs-lookup"><span data-stu-id="d01bb-151">Visual Studio Code help</span></span>

- [<span data-ttu-id="d01bb-152">入门</span><span class="sxs-lookup"><span data-stu-id="d01bb-152">Getting started</span></span>](https://code.visualstudio.com/docs)
- [<span data-ttu-id="d01bb-153">调试</span><span class="sxs-lookup"><span data-stu-id="d01bb-153">Debugging</span></span>](https://code.visualstudio.com/docs/editor/debugging)
- [<span data-ttu-id="d01bb-154">集成终端</span><span class="sxs-lookup"><span data-stu-id="d01bb-154">Integrated terminal</span></span>](https://code.visualstudio.com/docs/editor/integrated-terminal)
- [<span data-ttu-id="d01bb-155">键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="d01bb-155">Keyboard shortcuts</span></span>](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference)

  - [<span data-ttu-id="d01bb-156">Mac 键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="d01bb-156">Mac keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
  - [<span data-ttu-id="d01bb-157">Linux 键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="d01bb-157">Linux keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
  - [<span data-ttu-id="d01bb-158">Windows 键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="d01bb-158">Windows keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)

[!INCLUDE[next steps](../includes/webApi/next.md)]


