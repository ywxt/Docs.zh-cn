---
title: 使用 ASP.NET Core 和 Visual Studio for Windows 创建 Web API
author: rick-anderson
description: 使用 ASP.NET Core MVC 和 Visual Studio for Windows 生成 Web API
ms.author: riande
ms.custom: mvc
ms.date: 05/17/2018
uid: tutorials/first-web-api
ms.openlocfilehash: 3da22cbbbe0db7771656997a13587521e182fb2a
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277395"
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio-for-windows"></a><span data-ttu-id="6e75f-103">使用 ASP.NET Core 和 Visual Studio for Windows 创建 Web API</span><span class="sxs-lookup"><span data-stu-id="6e75f-103">Create a Web API with ASP.NET Core and Visual Studio for Windows</span></span>

<span data-ttu-id="6e75f-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="6e75f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

<span data-ttu-id="6e75f-105">本教程构建了用于管理“待办事项”列表的 Web API。</span><span class="sxs-lookup"><span data-stu-id="6e75f-105">This tutorial builds a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="6e75f-106">未创建用户界面 (UI)。</span><span class="sxs-lookup"><span data-stu-id="6e75f-106">A user interface (UI) isn't created.</span></span>

<span data-ttu-id="6e75f-107">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="6e75f-107">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="6e75f-108">Windows：使用 Visual Studio for Windows 创建 Web API（本教程）</span><span class="sxs-lookup"><span data-stu-id="6e75f-108">Windows: Web API with Visual Studio for Windows (This tutorial)</span></span>
* <span data-ttu-id="6e75f-109">macOS：[使用 Visual Studio for Mac 创建 Web API](xref:tutorials/first-web-api-mac)</span><span class="sxs-lookup"><span data-stu-id="6e75f-109">macOS: [Web API with Visual Studio for Mac](xref:tutorials/first-web-api-mac)</span></span>
* <span data-ttu-id="6e75f-110">macOS、Linux、Windows：[使用 Visual Studio Code 创建 Web API](xref:tutorials/web-api-vsc)</span><span class="sxs-lookup"><span data-stu-id="6e75f-110">macOS, Linux, Windows: [Web API with Visual Studio Code](xref:tutorials/web-api-vsc)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[intro to web API](../includes/webApi/intro.md)]

## <a name="prerequisites"></a><span data-ttu-id="6e75f-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="6e75f-111">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="create-the-project"></a><span data-ttu-id="6e75f-112">创建项目</span><span class="sxs-lookup"><span data-stu-id="6e75f-112">Create the project</span></span>

<span data-ttu-id="6e75f-113">在 Visual Studio 中执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="6e75f-113">Follow these steps in Visual Studio:</span></span>

* <span data-ttu-id="6e75f-114">从“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="6e75f-114">From the **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="6e75f-115">选择“ASP.NET Core Web 应用程序”模板。</span><span class="sxs-lookup"><span data-stu-id="6e75f-115">Select the **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="6e75f-116">将项目命名为 TodoApi，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="6e75f-116">Name the project *TodoApi* and click **OK**.</span></span>
* <span data-ttu-id="6e75f-117">在“新建 ASP.NET Core Web 应用程序 - TodoApi”对话框中，选择 ASP.NET Core 版本。</span><span class="sxs-lookup"><span data-stu-id="6e75f-117">In the **New ASP.NET Core Web Application - TodoApi** dialog, choose the ASP.NET Core version.</span></span> <span data-ttu-id="6e75f-118">选择“API”模板，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="6e75f-118">Select the **API** template and click **OK**.</span></span> <span data-ttu-id="6e75f-119">请不要选择“启用 Docker 支持”。</span><span class="sxs-lookup"><span data-stu-id="6e75f-119">Do **not** select **Enable Docker Support**.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="6e75f-120">启动应用</span><span class="sxs-lookup"><span data-stu-id="6e75f-120">Launch the app</span></span>

<span data-ttu-id="6e75f-121">在 Visual Studio 中，按 CTRL+F5 启动应用。</span><span class="sxs-lookup"><span data-stu-id="6e75f-121">In Visual Studio, press CTRL+F5 to launch the app.</span></span> <span data-ttu-id="6e75f-122">Visual Studio 启动浏览器并导航到 `http://localhost:<port>/api/values`，其中 `<port>` 是随机选择的端口号。</span><span class="sxs-lookup"><span data-stu-id="6e75f-122">Visual Studio launches a browser and navigates to `http://localhost:<port>/api/values`, where `<port>` is a randomly chosen port number.</span></span> <span data-ttu-id="6e75f-123">Chrome、Microsoft Edge 和 Firefox 将显示以下输出：</span><span class="sxs-lookup"><span data-stu-id="6e75f-123">Chrome, Microsoft Edge, and Firefox display the following output:</span></span>

```json
["value1","value2"]
```

<span data-ttu-id="6e75f-124">如果使用 Internet Explorer，系统将提示你保存 values.json 文件。</span><span class="sxs-lookup"><span data-stu-id="6e75f-124">If using Internet Explorer, you'll be prompted to save a *values.json* file.</span></span>

### <a name="add-a-model-class"></a><span data-ttu-id="6e75f-125">添加模型类</span><span class="sxs-lookup"><span data-stu-id="6e75f-125">Add a model class</span></span>

<span data-ttu-id="6e75f-126">模型是表示应用中的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="6e75f-126">A model is an object representing the data in the app.</span></span> <span data-ttu-id="6e75f-127">在此示例中，唯一的模型是待办事项。</span><span class="sxs-lookup"><span data-stu-id="6e75f-127">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="6e75f-128">在解决方案资源管理器中，右键单击项目。</span><span class="sxs-lookup"><span data-stu-id="6e75f-128">In Solution Explorer, right-click the project.</span></span> <span data-ttu-id="6e75f-129">选择“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="6e75f-129">Select **Add** > **New Folder**.</span></span> <span data-ttu-id="6e75f-130">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="6e75f-130">Name the folder *Models*.</span></span>

> [!NOTE]
> <span data-ttu-id="6e75f-131">模型类可以出现在项目的任意位置。</span><span class="sxs-lookup"><span data-stu-id="6e75f-131">The model classes can go anywhere in the project.</span></span> <span data-ttu-id="6e75f-132">Models 文件夹按约定用于模型类。</span><span class="sxs-lookup"><span data-stu-id="6e75f-132">The *Models* folder is used by convention for model classes.</span></span>

<span data-ttu-id="6e75f-133">在解决方案资源管理器中右键单击“模型”文件夹，然后选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="6e75f-133">In Solution Explorer, right-click the *Models* folder and select **Add** > **Class**.</span></span> <span data-ttu-id="6e75f-134">将类命名为 TodoItem，然后单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="6e75f-134">Name the class *TodoItem* and click **Add**.</span></span>

<span data-ttu-id="6e75f-135">使用以下代码更新 `TodoItem` 类：</span><span class="sxs-lookup"><span data-stu-id="6e75f-135">Update the `TodoItem` class with the following code:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="6e75f-136">创建 `TodoItem` 时，数据库将生成 `Id`。</span><span class="sxs-lookup"><span data-stu-id="6e75f-136">The database generates the `Id` when a `TodoItem` is created.</span></span>

### <a name="create-the-database-context"></a><span data-ttu-id="6e75f-137">创建数据库上下文</span><span class="sxs-lookup"><span data-stu-id="6e75f-137">Create the database context</span></span>

<span data-ttu-id="6e75f-138">数据库上下文是为给定数据模型协调实体框架功能的主类。</span><span class="sxs-lookup"><span data-stu-id="6e75f-138">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="6e75f-139">此类由 `Microsoft.EntityFrameworkCore.DbContext` 类派生而来。</span><span class="sxs-lookup"><span data-stu-id="6e75f-139">This class is created by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="6e75f-140">在解决方案资源管理器中右键单击“模型”文件夹，然后选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="6e75f-140">In Solution Explorer, right-click the *Models* folder and select **Add** > **Class**.</span></span> <span data-ttu-id="6e75f-141">将类命名为 TodoContext，然后单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="6e75f-141">Name the class *TodoContext* and click **Add**.</span></span>

<span data-ttu-id="6e75f-142">将该类替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="6e75f-142">Replace the class with the following code:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

### <a name="add-a-controller"></a><span data-ttu-id="6e75f-143">添加控制器</span><span class="sxs-lookup"><span data-stu-id="6e75f-143">Add a controller</span></span>

<span data-ttu-id="6e75f-144">在解决方案资源管理器中，右键单击“控制器”文件夹。</span><span class="sxs-lookup"><span data-stu-id="6e75f-144">In Solution Explorer, right-click the *Controllers* folder.</span></span> <span data-ttu-id="6e75f-145">选择 **添加** > **新建项**。</span><span class="sxs-lookup"><span data-stu-id="6e75f-145">Select **Add** > **New Item**.</span></span> <span data-ttu-id="6e75f-146">在“添加新项”对话框中，选择“API 控制器类”模板。</span><span class="sxs-lookup"><span data-stu-id="6e75f-146">In the **Add New Item** dialog, select the **API Controller Class** template.</span></span> <span data-ttu-id="6e75f-147">将类命名为 TodoController，然后单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="6e75f-147">Name the class *TodoController*, and click **Add**.</span></span>

![“添加新项”对话框，“控制器”显示在搜索框中，并且“Web API 控制器”已选中](first-web-api/_static/new_controller.png)

<span data-ttu-id="6e75f-149">将该类替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="6e75f-149">Replace the class with the following code:</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="6e75f-150">启动应用</span><span class="sxs-lookup"><span data-stu-id="6e75f-150">Launch the app</span></span>

<span data-ttu-id="6e75f-151">在 Visual Studio 中，按 CTRL+F5 启动应用。</span><span class="sxs-lookup"><span data-stu-id="6e75f-151">In Visual Studio, press CTRL+F5 to launch the app.</span></span> <span data-ttu-id="6e75f-152">Visual Studio 启动浏览器并导航到 `http://localhost:<port>/api/values`，其中 `<port>` 是随机选择的端口号。</span><span class="sxs-lookup"><span data-stu-id="6e75f-152">Visual Studio launches a browser and navigates to `http://localhost:<port>/api/values`, where `<port>` is a randomly chosen port number.</span></span> <span data-ttu-id="6e75f-153">导航到位于 `http://localhost:<port>/api/todo` 的 `Todo` 控制器。</span><span class="sxs-lookup"><span data-stu-id="6e75f-153">Navigate to the `Todo` controller at `http://localhost:<port>/api/todo`.</span></span>

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]
