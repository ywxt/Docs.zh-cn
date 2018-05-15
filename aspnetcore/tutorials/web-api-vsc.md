---
title: 使用 ASP.NET Core 和 Visual Studio Code 创建 Web API
author: rick-anderson
description: 在 macOS、Linux 或 Windows 上使用 ASP.NET Core MVC 和 Visual Studio Code 构建 Web API
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 04/27/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/web-api-vsc
ms.openlocfilehash: f991aeadbaa3f7696d6fd6b8791d26248e7560a6
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio-code"></a><span data-ttu-id="e2324-103">使用 ASP.NET Core 和 Visual Studio Code 创建 Web API</span><span class="sxs-lookup"><span data-stu-id="e2324-103">Create a Web API with ASP.NET Core and Visual Studio Code</span></span>

<span data-ttu-id="e2324-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="e2324-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

::: moniker range="= aspnetcore-2.1"
[!INCLUDE[](~/includes/2.1.md)]
::: moniker-end

<span data-ttu-id="e2324-106">本教程将生成一个用于管理“待办事项”列表的 Web API。</span><span class="sxs-lookup"><span data-stu-id="e2324-106">In this tutorial, build a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="e2324-107">不构造 UI。</span><span class="sxs-lookup"><span data-stu-id="e2324-107">A UI isn't constructed.</span></span>

<span data-ttu-id="e2324-108">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="e2324-108">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="e2324-109">macOS、Linux、Windows：使用 Visual Studio Code 创建 Web API（本教程）</span><span class="sxs-lookup"><span data-stu-id="e2324-109">macOS, Linux, Windows: Web API with Visual Studio Code (This tutorial)</span></span>
* <span data-ttu-id="e2324-110">macOS：[使用 Visual Studio for Mac 创建 Web API](xref:tutorials/first-web-api-mac)</span><span class="sxs-lookup"><span data-stu-id="e2324-110">macOS: [Web API with Visual Studio for Mac](xref:tutorials/first-web-api-mac)</span></span>
* <span data-ttu-id="e2324-111">Windows：[使用 Visual Studio for Windows 创建 Web API](xref:tutorials/first-web-api)</span><span class="sxs-lookup"><span data-stu-id="e2324-111">Windows: [Web API with Visual Studio for Windows](xref:tutorials/first-web-api)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[template files](../includes/webApi/intro.md)]

## <a name="prerequisites"></a><span data-ttu-id="e2324-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="e2324-112">Prerequisites</span></span>

[!INCLUDE[prerequisites](~/includes/net-core-prereqs-vscode.md)]

## <a name="create-the-project"></a><span data-ttu-id="e2324-113">创建项目</span><span class="sxs-lookup"><span data-stu-id="e2324-113">Create the project</span></span>

<span data-ttu-id="e2324-114">从控制台运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="e2324-114">From a console, run the following commands:</span></span>

```console
dotnet new webapi -o TodoApi
code TodoApi
```

<span data-ttu-id="e2324-115">在 Visual Studio Code (VS Code) 中打开 TodoApi 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2324-115">The *TodoApi* folder opens in Visual Studio Code (VS Code).</span></span> <span data-ttu-id="e2324-116">选择 Startup.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="e2324-116">Select the *Startup.cs* file.</span></span>

* <span data-ttu-id="e2324-117">对于警告消息 -“"TodoApi" 中缺少进行生成和调试所需的资产。是否添加它们?”，。</span><span class="sxs-lookup"><span data-stu-id="e2324-117">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'TodoApi'.</span></span> <span data-ttu-id="e2324-118">请选择“是”</span><span class="sxs-lookup"><span data-stu-id="e2324-118">Add them?"</span></span>
* <span data-ttu-id="e2324-119">对于信息性消息 -“存在未解析的依赖项”，请选择“还原”。</span><span class="sxs-lookup"><span data-stu-id="e2324-119">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

<!-- uid: tutorials/first-mvc-app-xplat/start-mvc uses the pic below. If you change it, make sure it's consistent -->

![带有“"TodoApi" 中缺少进行生成和调试所需的资产。是否添加它们?”](web-api-vsc/_static/vsc_restore.png)

<span data-ttu-id="e2324-123">按“调试”(F5) 生成并运行程序。</span><span class="sxs-lookup"><span data-stu-id="e2324-123">Press **Debug** (F5) to build and run the program.</span></span> <span data-ttu-id="e2324-124">在浏览器中导航到 http://localhost:5000/api/values。</span><span class="sxs-lookup"><span data-stu-id="e2324-124">In a browser, navigate to http://localhost:5000/api/values.</span></span> <span data-ttu-id="e2324-125">显示以下输出：</span><span class="sxs-lookup"><span data-stu-id="e2324-125">The following output is displayed:</span></span>

```json
["value1","value2"]
```

<span data-ttu-id="e2324-126">有关 VS Code 的使用技巧，请参阅 [Visual Studio Code 帮助](#visual-studio-code-help)。</span><span class="sxs-lookup"><span data-stu-id="e2324-126">See [Visual Studio Code help](#visual-studio-code-help) for tips on using VS Code.</span></span>

## <a name="add-support-for-entity-framework-core"></a><span data-ttu-id="e2324-127">添加对 Entity Framework Core 的支持</span><span class="sxs-lookup"><span data-stu-id="e2324-127">Add support for Entity Framework Core</span></span>

:::moniker range="<= aspnetcore-2.0"
<span data-ttu-id="e2324-128">在 ASP.NET Core 2.0 中创建新项目会在 TodoApi.csproj 文件中添加 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 包引用：</span><span class="sxs-lookup"><span data-stu-id="e2324-128">Creating a new project in ASP.NET Core 2.0 adds the [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) package reference to the *TodoApi.csproj* file:</span></span>

<span data-ttu-id="e2324-129">[!code-xml[](first-web-api/samples/2.0/TodoApi/TodoApi.csproj?name=snippet_Metapackage&highlight=2)]</span><span class="sxs-lookup"><span data-stu-id="e2324-129">[!code-xml[](first-web-api/samples/2.0/TodoApi/TodoApi.csproj?name=snippet_Metapackage&highlight=2)]</span></span>
:::moniker-end
:::moniker range=">= aspnetcore-2.1"
<span data-ttu-id="e2324-130">在 ASP.NET Core 2.1 或更改版本中创建新项目会在 TodoApi.csproj 文件中添加 [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App) 包引用：</span><span class="sxs-lookup"><span data-stu-id="e2324-130">Creating a new project in ASP.NET Core 2.1 or later adds the [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App) package reference to the *TodoApi.csproj* file:</span></span>

<span data-ttu-id="e2324-131">[!code-xml[](first-web-api/samples/2.1/TodoApi/TodoApi.csproj?name=snippet_Metapackage&highlight=2)]</span><span class="sxs-lookup"><span data-stu-id="e2324-131">[!code-xml[](first-web-api/samples/2.1/TodoApi/TodoApi.csproj?name=snippet_Metapackage&highlight=2)]</span></span>
:::moniker-end

<span data-ttu-id="e2324-132">无需单独安装 [Entity Framework Core InMemory](/ef/core/providers/in-memory/) 数据库提供程序。</span><span class="sxs-lookup"><span data-stu-id="e2324-132">There's no need to install the [Entity Framework Core InMemory](/ef/core/providers/in-memory/) database provider separately.</span></span> <span data-ttu-id="e2324-133">此数据库提供程序允许将 Entity Framework Core 和内存数据库一起使用。</span><span class="sxs-lookup"><span data-stu-id="e2324-133">This database provider allows Entity Framework Core to be used with an in-memory database.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="e2324-134">添加模型类</span><span class="sxs-lookup"><span data-stu-id="e2324-134">Add a model class</span></span>

<span data-ttu-id="e2324-135">模型是表示应用中的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="e2324-135">A model is an object representing the data in your app.</span></span> <span data-ttu-id="e2324-136">在此示例中，唯一的模型是待办事项。</span><span class="sxs-lookup"><span data-stu-id="e2324-136">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="e2324-137">添加名为“模型”的文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2324-137">Add a folder named *Models*.</span></span> <span data-ttu-id="e2324-138">可将模型类置于项目的任意位置，但按照惯例会使用“模型”文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2324-138">You can put model classes anywhere in your project, but the *Models* folder is used by convention.</span></span>

<span data-ttu-id="e2324-139">添加带有以下代码的 `TodoItem` 类：</span><span class="sxs-lookup"><span data-stu-id="e2324-139">Add a `TodoItem` class with the following code:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="e2324-140">创建 `TodoItem` 时，数据库将生成 `Id`。</span><span class="sxs-lookup"><span data-stu-id="e2324-140">The database generates the `Id` when a `TodoItem` is created.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="e2324-141">创建数据库上下文</span><span class="sxs-lookup"><span data-stu-id="e2324-141">Create the database context</span></span>

<span data-ttu-id="e2324-142">数据库上下文是为给定数据模型协调 Entity Framework 功能的主类。</span><span class="sxs-lookup"><span data-stu-id="e2324-142">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="e2324-143">将通过从 `Microsoft.EntityFrameworkCore.DbContext` 类派生的方式创建此类。</span><span class="sxs-lookup"><span data-stu-id="e2324-143">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="e2324-144">在“模型”文件夹中添加 `TodoContext` 类：</span><span class="sxs-lookup"><span data-stu-id="e2324-144">Add a `TodoContext` class in the *Models* folder:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

## <a name="add-a-controller"></a><span data-ttu-id="e2324-145">添加控制器</span><span class="sxs-lookup"><span data-stu-id="e2324-145">Add a controller</span></span>

<span data-ttu-id="e2324-146">在“控制器”文件夹中，创建名为 `TodoController` 的类。</span><span class="sxs-lookup"><span data-stu-id="e2324-146">In the *Controllers* folder, create a class named `TodoController`.</span></span> <span data-ttu-id="e2324-147">用以下代码替代其内容：</span><span class="sxs-lookup"><span data-stu-id="e2324-147">Replace its contents with the following code:</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="e2324-148">启动应用</span><span class="sxs-lookup"><span data-stu-id="e2324-148">Launch the app</span></span>

<span data-ttu-id="e2324-149">在 VS Code 中，按 F5 启动应用。</span><span class="sxs-lookup"><span data-stu-id="e2324-149">In VS Code, press F5 to launch the app.</span></span> <span data-ttu-id="e2324-150">导航到 http://localhost:5000/api/todo（我们刚刚创建的 `Todo` 控制器）。</span><span class="sxs-lookup"><span data-stu-id="e2324-150">Navigate to http://localhost:5000/api/todo (the `Todo` controller we created).</span></span>

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

## <a name="visual-studio-code-help"></a><span data-ttu-id="e2324-151">Visual Studio Code 帮助</span><span class="sxs-lookup"><span data-stu-id="e2324-151">Visual Studio Code help</span></span>

* [<span data-ttu-id="e2324-152">入门</span><span class="sxs-lookup"><span data-stu-id="e2324-152">Getting started</span></span>](https://code.visualstudio.com/docs)
* [<span data-ttu-id="e2324-153">调试</span><span class="sxs-lookup"><span data-stu-id="e2324-153">Debugging</span></span>](https://code.visualstudio.com/docs/editor/debugging)
* [<span data-ttu-id="e2324-154">集成终端</span><span class="sxs-lookup"><span data-stu-id="e2324-154">Integrated terminal</span></span>](https://code.visualstudio.com/docs/editor/integrated-terminal)
* [<span data-ttu-id="e2324-155">键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="e2324-155">Keyboard shortcuts</span></span>](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference)

  * [<span data-ttu-id="e2324-156">macOS 键盘快捷方式</span><span class="sxs-lookup"><span data-stu-id="e2324-156">macOS keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
  * [<span data-ttu-id="e2324-157">Linux 键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="e2324-157">Linux keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
  * [<span data-ttu-id="e2324-158">Windows 键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="e2324-158">Windows keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)

[!INCLUDE[next steps](../includes/webApi/next.md)]
