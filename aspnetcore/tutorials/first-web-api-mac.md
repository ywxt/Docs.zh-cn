---
title: 使用 ASP.NET Core 和 Visual Studio for Mac 创建 Web API
author: rick-anderson
description: 使用 ASP.NET Core MVC 和 Visual Studio for Mac 创建 Web API
helpviewer_heywords: ASP.NET Core, WebAPI, Web API, REST, mac, macOS, HTTP, Service, HTTP Service
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/08/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-web-api-mac
ms.openlocfilehash: 699fbbf54abf1dc5c4156c559761110cdb375558
ms.sourcegitcommit: c867d7427bd4a88a78b2322e156367733b532730
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2018
ms.locfileid: "33923199"
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio-for-mac"></a><span data-ttu-id="3d1bb-103">使用 ASP.NET Core 和 Visual Studio for Mac 创建 Web API</span><span class="sxs-lookup"><span data-stu-id="3d1bb-103">Create a Web API with ASP.NET Core and Visual Studio for Mac</span></span>

<span data-ttu-id="3d1bb-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="3d1bb-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

<span data-ttu-id="3d1bb-105">本教程将生成一个用于管理“待办事项”列表的 Web API。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-105">In this tutorial, build a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="3d1bb-106">不构造 UI。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-106">The UI isn't constructed.</span></span>

<span data-ttu-id="3d1bb-107">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="3d1bb-107">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="3d1bb-108">macOS：使用 Visual Studio for Mac 创建 Web API（本教程）</span><span class="sxs-lookup"><span data-stu-id="3d1bb-108">macOS: Web API with Visual Studio for Mac (This tutorial)</span></span>
* <span data-ttu-id="3d1bb-109">Windows：[使用 Visual Studio for Windows 创建 Web API](xref:tutorials/first-web-api)</span><span class="sxs-lookup"><span data-stu-id="3d1bb-109">Windows: [Web API with Visual Studio for Windows](xref:tutorials/first-web-api)</span></span>
* <span data-ttu-id="3d1bb-110">macOS、Linux、Windows：[使用 Visual Studio Code 创建 Web API](xref:tutorials/web-api-vsc)</span><span class="sxs-lookup"><span data-stu-id="3d1bb-110">macOS, Linux, Windows: [Web API with Visual Studio Code](xref:tutorials/web-api-vsc)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[template files](../includes/webApi/intro.md)]

<span data-ttu-id="3d1bb-111">请参阅 [macOS 或 Linux 上的 ASP.NET Core MVC 介绍](xref:tutorials/first-mvc-app-xplat/index)，获取使用永久数据库的示例。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-111">See [Introduction to ASP.NET Core MVC on macOS or Linux](xref:tutorials/first-mvc-app-xplat/index) for an example that uses a persistent database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d1bb-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="3d1bb-112">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-macos.md)]

## <a name="create-the-project"></a><span data-ttu-id="3d1bb-113">创建项目</span><span class="sxs-lookup"><span data-stu-id="3d1bb-113">Create the project</span></span>

<span data-ttu-id="3d1bb-114">在 Visual Studio 中，选择“文件” > “新建解决方案”。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-114">From Visual Studio, select **File** > **New Solution**.</span></span>

![macOS 新建解决方案](first-web-api-mac/_static/sln.png)

<span data-ttu-id="3d1bb-116">选择“.NET Core App” > “ASP.NET Core Web API” > “下一步”。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-116">Select **.NET Core App** > **ASP.NET Core Web API** > **Next**.</span></span>

![macOS“新建项目”对话框](first-web-api-mac/_static/1.png)

<span data-ttu-id="3d1bb-118">输入“TodoApi”作为“项目名称”，然后选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-118">Enter *TodoApi* for the **Project Name**, and then click **Create**.</span></span>

![配置对话框](first-web-api-mac/_static/2.png)

### <a name="launch-the-app"></a><span data-ttu-id="3d1bb-120">启动应用</span><span class="sxs-lookup"><span data-stu-id="3d1bb-120">Launch the app</span></span>

<span data-ttu-id="3d1bb-121">在 Visual Studio 中，选择“运行” > “开始执行(调试)”启动应用。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-121">In Visual Studio, select **Run** > **Start With Debugging** to launch the app.</span></span> <span data-ttu-id="3d1bb-122">Visual Studio 启动浏览器并导航到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-122">Visual Studio launches a browser and navigates to `http://localhost:5000`.</span></span> <span data-ttu-id="3d1bb-123">将收到 HTTP 404（未找到）错误。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-123">You get an HTTP 404 (Not Found) error.</span></span> <span data-ttu-id="3d1bb-124">将 URL 更改为 `http://localhost:<port>/api/values`。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-124">Change the URL to `http://localhost:<port>/api/values`.</span></span> <span data-ttu-id="3d1bb-125">`ValuesController` 数据已显示：</span><span class="sxs-lookup"><span data-stu-id="3d1bb-125">The `ValuesController` data is displayed:</span></span>

```json
["value1","value2"]
```

### <a name="add-support-for-entity-framework-core"></a><span data-ttu-id="3d1bb-126">添加对 Entity Framework Core 的支持</span><span class="sxs-lookup"><span data-stu-id="3d1bb-126">Add support for Entity Framework Core</span></span>

<span data-ttu-id="3d1bb-127">安装 [Entity Framework Core InMemory](/ef/core/providers/in-memory/) 数据库提供程序。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-127">Install the [Entity Framework Core InMemory](/ef/core/providers/in-memory/) database provider.</span></span> <span data-ttu-id="3d1bb-128">此数据库提供程序允许将 Entity Framework Core 和内存数据库一起使用。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-128">This database provider allows Entity Framework Core to be used with an in-memory database.</span></span>

* <span data-ttu-id="3d1bb-129">从“项目”菜单中，选择“添加 NuGet 包”。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-129">From the **Project** menu, select **Add NuGet Packages**.</span></span>

  * <span data-ttu-id="3d1bb-130">或者，可以右键单击“依赖项”，然后选择“添加包”。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-130">Alternatively, you can right-click **Dependencies**, and then select **Add Packages**.</span></span>

* <span data-ttu-id="3d1bb-131">在搜索框中输入 `EntityFrameworkCore.InMemory`。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-131">Enter `EntityFrameworkCore.InMemory` in the search box.</span></span>
* <span data-ttu-id="3d1bb-132">选择 `Microsoft.EntityFrameworkCore.InMemory`，然后选择“添加包”。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-132">Select `Microsoft.EntityFrameworkCore.InMemory`, and then select **Add Package**.</span></span>

### <a name="add-a-model-class"></a><span data-ttu-id="3d1bb-133">添加模型类</span><span class="sxs-lookup"><span data-stu-id="3d1bb-133">Add a model class</span></span>

<span data-ttu-id="3d1bb-134">模型是表示应用中的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-134">A model is an object representing the data in your app.</span></span> <span data-ttu-id="3d1bb-135">在此示例中，唯一的模型是待办事项。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-135">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="3d1bb-136">在解决方案资源管理器中，右键单击项目。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-136">In Solution Explorer, right-click the project.</span></span> <span data-ttu-id="3d1bb-137">选择“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-137">Select **Add** > **New Folder**.</span></span> <span data-ttu-id="3d1bb-138">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-138">Name the folder *Models*.</span></span>

![新建文件夹](first-web-api-mac/_static/folder.png)

> [!NOTE]
> <span data-ttu-id="3d1bb-140">可将模型类置于项目的任意位置，但按照惯例会使用“模型”文件夹。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-140">You can put model classes anywhere in your project, but the *Models* folder is used by convention.</span></span>

<span data-ttu-id="3d1bb-141">右键单击“Models”文件夹，然后选择“添加” > “新建文件” > “常规” > “空类”。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-141">Right-click the *Models* folder, and select **Add** > **New File** > **General** > **Empty Class**.</span></span> <span data-ttu-id="3d1bb-142">将类命名为“TodoItem”，然后单击“新建”。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-142">Name the class *TodoItem*, and then click **New**.</span></span>

<span data-ttu-id="3d1bb-143">将生成的代码替换为：</span><span class="sxs-lookup"><span data-stu-id="3d1bb-143">Replace the generated code with:</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="3d1bb-144">创建 `TodoItem` 时，数据库将生成 `Id`。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-144">The database generates the `Id` when a `TodoItem` is created.</span></span>

### <a name="create-the-database-context"></a><span data-ttu-id="3d1bb-145">创建数据库上下文</span><span class="sxs-lookup"><span data-stu-id="3d1bb-145">Create the database context</span></span>

<span data-ttu-id="3d1bb-146">数据库上下文是为给定数据模型协调 Entity Framework 功能的主类。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-146">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="3d1bb-147">可以通过继承 `Microsoft.EntityFrameworkCore.DbContext` 类的方式创建此类。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-147">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="3d1bb-148">将 `TodoContext` 类添加到“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-148">Add a `TodoContext` class to the *Models* folder.</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

## <a name="add-a-controller"></a><span data-ttu-id="3d1bb-149">添加控制器</span><span class="sxs-lookup"><span data-stu-id="3d1bb-149">Add a controller</span></span>

<span data-ttu-id="3d1bb-150">在解决方案资源管理器的“控制器”文件夹中，添加 `TodoController` 类。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-150">In Solution Explorer, in the *Controllers* folder, add the class `TodoController`.</span></span>

<span data-ttu-id="3d1bb-151">将生成的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="3d1bb-151">Replace the generated code with the following:</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="3d1bb-152">启动应用</span><span class="sxs-lookup"><span data-stu-id="3d1bb-152">Launch the app</span></span>

<span data-ttu-id="3d1bb-153">在 Visual Studio 中，选择“运行” > “开始执行(调试)”启动应用。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-153">In Visual Studio, select **Run** > **Start With Debugging** to launch the app.</span></span> <span data-ttu-id="3d1bb-154">Visual Studio 启动浏览器并导航到 `http://localhost:<port>`，其中 `<port>` 是随机选择的端口号。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-154">Visual Studio launches a browser and navigates to `http://localhost:<port>`, where `<port>` is a randomly chosen port number.</span></span> <span data-ttu-id="3d1bb-155">将收到 HTTP 404（未找到）错误。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-155">You get an HTTP 404 (Not Found) error.</span></span> <span data-ttu-id="3d1bb-156">将 URL 更改为 `http://localhost:<port>/api/values`。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-156">Change the URL to `http://localhost:<port>/api/values`.</span></span> <span data-ttu-id="3d1bb-157">`ValuesController` 数据已显示：</span><span class="sxs-lookup"><span data-stu-id="3d1bb-157">The `ValuesController` data is displayed:</span></span>

```json
["value1","value2"]
```

<span data-ttu-id="3d1bb-158">导航到位于 `http://localhost:<port>/api/todo` 的 `Todo` 控制器。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-158">Navigate to the `Todo` controller at `http://localhost:<port>/api/todo`.</span></span> <span data-ttu-id="3d1bb-159">会返回以下 JSON：</span><span class="sxs-lookup"><span data-stu-id="3d1bb-159">The following JSON is returned:</span></span>

```json
[{"key":1,"name":"Item1","isComplete":false}]
```

## <a name="implement-the-other-crud-operations"></a><span data-ttu-id="3d1bb-160">实现其他的 CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="3d1bb-160">Implement the other CRUD operations</span></span>

<span data-ttu-id="3d1bb-161">我们将向控制器添加 `Create`、`Update` 和 `Delete` 方法。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-161">We'll add `Create`, `Update`, and `Delete` methods to the controller.</span></span> <span data-ttu-id="3d1bb-162">这些方法是主题的变体，因此在这里只提供代码并突出显示主要的差异。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-162">These methods are variations on a theme, so I'll just show the code and highlight the main differences.</span></span> <span data-ttu-id="3d1bb-163">添加或更改代码后生成项目。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-163">Build the project after adding or changing code.</span></span>

### <a name="create"></a><span data-ttu-id="3d1bb-164">创建</span><span class="sxs-lookup"><span data-stu-id="3d1bb-164">Create</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="3d1bb-165">[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]</span><span class="sxs-lookup"><span data-stu-id="3d1bb-165">[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]</span></span>

<span data-ttu-id="3d1bb-166">上述方法响应至 HTTP POST，由 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 属性指示。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-166">The preceding method responds to an HTTP POST, as indicated by the [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) attribute.</span></span> <span data-ttu-id="3d1bb-167">[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) 特性告诉 MVC 从 HTTP 请求正文获取待办事项的值。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-167">The [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) attribute tells MVC to get the value of the to-do item from the body of the HTTP request.</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="3d1bb-168">[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]</span><span class="sxs-lookup"><span data-stu-id="3d1bb-168">[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]</span></span>

<span data-ttu-id="3d1bb-169">上述方法响应至 HTTP POST，由 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 属性指示。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-169">The preceding method responds to an HTTP POST, as indicated by the [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) attribute.</span></span> <span data-ttu-id="3d1bb-170">MVC 从 HTTP 请求正文获取待办事项的值。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-170">MVC gets the value of the to-do item from the body of the HTTP request.</span></span>
::: moniker-end

<span data-ttu-id="3d1bb-171">`CreatedAtRoute` 方法返回 201 响应。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-171">The `CreatedAtRoute` method returns a 201 response.</span></span> <span data-ttu-id="3d1bb-172">201 响应是在服务器上创建新资源的 HTTP POST 方法的标准响应。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-172">It's the standard response for an HTTP POST method that creates a new resource on the server.</span></span> <span data-ttu-id="3d1bb-173">`CreatedAtRoute` 还会向响应添加位置标头。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-173">`CreatedAtRoute` also adds a Location header to the response.</span></span> <span data-ttu-id="3d1bb-174">位置标头指定新建的待办事项的 URI。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-174">The Location header specifies the URI of the newly created to-do item.</span></span> <span data-ttu-id="3d1bb-175">请参阅 [10.2.2 201 已创建](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-175">See [10.2.2 201 Created](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>

### <a name="use-postman-to-send-a-create-request"></a><span data-ttu-id="3d1bb-176">使用 Postman 发送创建请求</span><span class="sxs-lookup"><span data-stu-id="3d1bb-176">Use Postman to send a Create request</span></span>

* <span data-ttu-id="3d1bb-177">启动应用（“运行” > “开始执行(调试)”）。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-177">Start the app (**Run** > **Start With Debugging**).</span></span>
* <span data-ttu-id="3d1bb-178">打开 Postman。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-178">Open Postman.</span></span>

![Postman 控制台](first-web-api/_static/pmc.png)

* <span data-ttu-id="3d1bb-180">更新 localhost URL 中的端口号。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-180">Update the port number in the localhost URL.</span></span>
* <span data-ttu-id="3d1bb-181">将 HTTP 方法设置为 POST。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-181">Set the HTTP method to *POST*.</span></span>
* <span data-ttu-id="3d1bb-182">单击“正文”选项卡。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-182">Click the **Body** tab.</span></span>
* <span data-ttu-id="3d1bb-183">选择“原始”单选按钮。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-183">Select the **raw** radio button.</span></span>
* <span data-ttu-id="3d1bb-184">将类型设置为 JSON (application/json)</span><span class="sxs-lookup"><span data-stu-id="3d1bb-184">Set the type to *JSON (application/json)*.</span></span>
* <span data-ttu-id="3d1bb-185">输入包含待办事项的请求正文，类似以下 JSON：</span><span class="sxs-lookup"><span data-stu-id="3d1bb-185">Enter a request body with a to-do item resembling the following JSON:</span></span>

```json
{
  "name":"walk dog",
  "isComplete":true
}
```

* <span data-ttu-id="3d1bb-186">单击“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-186">Click the **Send** button.</span></span>

::: moniker range=">= aspnetcore-2.1"
> [!TIP]
> <span data-ttu-id="3d1bb-187">如果单击“发送”后没有响应，则禁用“SSL 证书验证”选项。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-187">If no response displays after clicking **Send**, disable the **SSL certification verification** option.</span></span> <span data-ttu-id="3d1bb-188">在“文件” > “设置”下可以找到该选项</span><span class="sxs-lookup"><span data-stu-id="3d1bb-188">This is found under **File** > **Settings**.</span></span> <span data-ttu-id="3d1bb-189">在禁用该设置后，再次单击“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-189">Click the **Send** button again after disabling the setting.</span></span>
::: moniker-end

<span data-ttu-id="3d1bb-190">单击“响应”窗格中的“标头”选项卡，然后复制位置标头值：</span><span class="sxs-lookup"><span data-stu-id="3d1bb-190">Click the **Headers** tab in the **Response** pane and copy the **Location** header value:</span></span>

![Postman 控制台的“标头”选项卡](first-web-api/_static/pmc2.png)

<span data-ttu-id="3d1bb-192">可以使用此位置标头 URI 访问创建的资源。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-192">You can use the Location header URI to access the resource you created.</span></span> <span data-ttu-id="3d1bb-193">`Create` 方法返回 [CreatedAtRoute](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdatroute#Microsoft_AspNetCore_Mvc_ControllerBase_CreatedAtRoute_System_String_System_Object_System_Object_)。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-193">The `Create` method returns [CreatedAtRoute](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdatroute#Microsoft_AspNetCore_Mvc_ControllerBase_CreatedAtRoute_System_String_System_Object_System_Object_).</span></span> <span data-ttu-id="3d1bb-194">传递至 `CreatedAtRoute` 的第一个参数代表用于生成 URL 的命名路由。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-194">The first parameter passed to `CreatedAtRoute` represents the named route to use for generating the URL.</span></span> <span data-ttu-id="3d1bb-195">请回想一下，`GetById` 方法创建的 `"GetTodo"` 命令路由：</span><span class="sxs-lookup"><span data-stu-id="3d1bb-195">Recall that the `GetById` method created the `"GetTodo"` named route:</span></span>

```csharp
[HttpGet("{id}", Name = "GetTodo")]
```

### <a name="update"></a><span data-ttu-id="3d1bb-196">更新</span><span class="sxs-lookup"><span data-stu-id="3d1bb-196">Update</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="3d1bb-197">[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]</span><span class="sxs-lookup"><span data-stu-id="3d1bb-197">[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="3d1bb-198">[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]</span><span class="sxs-lookup"><span data-stu-id="3d1bb-198">[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]</span></span>
::: moniker-end

<span data-ttu-id="3d1bb-199">`Update` 与 `Create` 类似，但是使用的是 HTTP PUT。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-199">`Update` is similar to `Create`, but uses HTTP PUT.</span></span> <span data-ttu-id="3d1bb-200">响应是 [204（无内容）](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-200">The response is [204 (No Content)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span> <span data-ttu-id="3d1bb-201">根据 HTTP 规范，PUT 请求需要客户端发送整个更新的实体，而不仅仅是增量。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-201">According to the HTTP spec, a PUT request requires the client to send the entire updated entity, not just the deltas.</span></span> <span data-ttu-id="3d1bb-202">若要支持部分更新，请使用 HTTP PATCH。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-202">To support partial updates, use HTTP PATCH.</span></span>

```json
{
  "key": 1,
  "name": "walk dog",
  "isComplete": true
}
```

![显示 204（无内容）响应的 Postman 控制台](first-web-api/_static/pmcput.png)

### <a name="delete"></a><span data-ttu-id="3d1bb-204">删除</span><span class="sxs-lookup"><span data-stu-id="3d1bb-204">Delete</span></span>

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Delete)]

<span data-ttu-id="3d1bb-205">响应是 [204（无内容）](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。</span><span class="sxs-lookup"><span data-stu-id="3d1bb-205">The response is [204 (No Content)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span>

![显示 204（无内容）响应的 Postman 控制台](first-web-api/_static/pmd.png)

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]
