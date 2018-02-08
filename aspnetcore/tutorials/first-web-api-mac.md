---
title: "使用 ASP.NET Core 和 Visual Studio for Mac 创建 Web API"
author: rick-anderson
description: "使用 ASP.NET Core MVC 和 Visual Studio for Mac 创建 Web API"
helpviewer_heywords: ASP.NET Core, WebAPI, Web API, REST, mac, macOS, HTTP, Service, HTTP Service
manager: wpickett
ms.author: riande
ms.date: 09/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-web-api-mac
ms.openlocfilehash: b0e1a331fe3229119f4669fa336b6af4822785bf
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="create-a-web-api-with-aspnet-core-mvc-and-visual-studio-for-mac"></a><span data-ttu-id="d3182-103">使用 ASP.NET Core MVC 和 Visual Studio for Mac 创建 Web API</span><span class="sxs-lookup"><span data-stu-id="d3182-103">Create a Web API with ASP.NET Core MVC and Visual Studio for Mac</span></span>

<span data-ttu-id="d3182-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="d3182-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

<span data-ttu-id="d3182-105">本教程将生成一个用于管理“待办事项”列表的 Web API。</span><span class="sxs-lookup"><span data-stu-id="d3182-105">In this tutorial, build a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="d3182-106">不构造 UI。</span><span class="sxs-lookup"><span data-stu-id="d3182-106">The UI isn't constructed.</span></span>

<span data-ttu-id="d3182-107">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="d3182-107">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="d3182-108">macOS：使用 Visual Studio for Mac 创建 Web API（本教程）</span><span class="sxs-lookup"><span data-stu-id="d3182-108">macOS: Web API with Visual Studio for Mac (This tutorial)</span></span>
* <span data-ttu-id="d3182-109">Windows：[使用 Visual Studio for Windows 创建 Web API](xref:tutorials/first-web-api)</span><span class="sxs-lookup"><span data-stu-id="d3182-109">Windows: [Web API with Visual Studio for Windows](xref:tutorials/first-web-api)</span></span>
* <span data-ttu-id="d3182-110">macOS、Linux、Windows：[使用 Visual Studio Code 创建 Web API](xref:tutorials/web-api-vsc)</span><span class="sxs-lookup"><span data-stu-id="d3182-110">macOS, Linux, Windows: [Web API with Visual Studio Code](xref:tutorials/web-api-vsc)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[template files](../includes/webApi/intro.md)]

* <span data-ttu-id="d3182-111">请参阅 [Mac 或 Linux 上的 ASP.NET Core MVC 介绍](xref:tutorials/first-mvc-app-xplat/index)，获取使用永久数据库的示例。</span><span class="sxs-lookup"><span data-stu-id="d3182-111">See [Introduction to ASP.NET Core MVC on Mac or Linux](xref:tutorials/first-mvc-app-xplat/index) for an example that uses a persistent database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3182-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="d3182-112">Prerequisites</span></span>

<span data-ttu-id="d3182-113">安装以下组件：</span><span class="sxs-lookup"><span data-stu-id="d3182-113">Install the following:</span></span>

- <span data-ttu-id="d3182-114">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) 或更高版本</span><span class="sxs-lookup"><span data-stu-id="d3182-114">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later</span></span>
- [<span data-ttu-id="d3182-115">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="d3182-115">Visual Studio for Mac</span></span>](https://www.visualstudio.com/vs/visual-studio-mac/)

## <a name="create-the-project"></a><span data-ttu-id="d3182-116">创建项目</span><span class="sxs-lookup"><span data-stu-id="d3182-116">Create the project</span></span>

<span data-ttu-id="d3182-117">在 Visual Studio 中，选择“文件”>“新建解决方案”。</span><span class="sxs-lookup"><span data-stu-id="d3182-117">From Visual Studio, select **File > New Solution**.</span></span>

![macOS“新建解决方案”](first-web-api-mac/_static/sln.png)

<span data-ttu-id="d3182-119">选择“.NET Core App”>“ASP.NET Core Web API”>“下一步”。</span><span class="sxs-lookup"><span data-stu-id="d3182-119">Select **.NET Core App >  ASP.NET Core Web API > Next**.</span></span>

![macOS“新建项目”对话框](first-web-api-mac/_static/1.png)

<span data-ttu-id="d3182-121">输入“TodoApi”作为“项目名称”，然后选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="d3182-121">Enter **TodoApi** for the **Project Name**, and then select Create.</span></span>

![配置对话框](first-web-api-mac/_static/2.png)

### <a name="launch-the-app"></a><span data-ttu-id="d3182-123">启动应用</span><span class="sxs-lookup"><span data-stu-id="d3182-123">Launch the app</span></span>

<span data-ttu-id="d3182-124">在 Visual Studio 中，选择“运行”>“开始执行(调试)”启动应用。</span><span class="sxs-lookup"><span data-stu-id="d3182-124">In Visual Studio, select **Run > Start With Debugging** to launch the app.</span></span> <span data-ttu-id="d3182-125">Visual Studio 启动浏览器并导航到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="d3182-125">Visual Studio launches a browser and navigates to `http://localhost:5000`.</span></span> <span data-ttu-id="d3182-126">将收到 HTTP 404（未找到）错误。</span><span class="sxs-lookup"><span data-stu-id="d3182-126">You get an HTTP 404 (Not Found) error.</span></span>  <span data-ttu-id="d3182-127">将 URL 更改为 `http://localhost:port/api/values`。</span><span class="sxs-lookup"><span data-stu-id="d3182-127">Change the URL to `http://localhost:port/api/values`.</span></span> <span data-ttu-id="d3182-128">将显示 `ValuesController` 数据：</span><span class="sxs-lookup"><span data-stu-id="d3182-128">The `ValuesController` data will be displayed:</span></span>

```
["value1","value2"]
```

### <a name="add-support-for-entity-framework-core"></a><span data-ttu-id="d3182-129">添加对 Entity Framework Core 的支持</span><span class="sxs-lookup"><span data-stu-id="d3182-129">Add support for Entity Framework Core</span></span>

<span data-ttu-id="d3182-130">安装 [Entity Framework Core InMemory](https://docs.microsoft.com/ef/core/providers/in-memory/) 数据库提供程序。</span><span class="sxs-lookup"><span data-stu-id="d3182-130">Install the [Entity Framework Core InMemory](https://docs.microsoft.com/ef/core/providers/in-memory/) database provider.</span></span> <span data-ttu-id="d3182-131">此数据库提供程序允许将 Entity Framework Core 和内存数据库一起使用。</span><span class="sxs-lookup"><span data-stu-id="d3182-131">This database provider allows Entity Framework Core to be used with an in-memory database.</span></span>

* <span data-ttu-id="d3182-132">从“项目”菜单中，选择“添加 NuGet 包”。</span><span class="sxs-lookup"><span data-stu-id="d3182-132">From the **Project** menu, select **Add NuGet Packages**.</span></span> 

  *  <span data-ttu-id="d3182-133">或者，可以右键单击“依赖项”，然后选择“添加包”。</span><span class="sxs-lookup"><span data-stu-id="d3182-133">Alternately, you can right-click **Dependencies**, and then select **Add Packages**.</span></span>

* <span data-ttu-id="d3182-134">在搜索框中输入 `EntityFrameworkCore.InMemory`。</span><span class="sxs-lookup"><span data-stu-id="d3182-134">Enter `EntityFrameworkCore.InMemory` in the search box.</span></span>
* <span data-ttu-id="d3182-135">选择 `Microsoft.EntityFrameworkCore.InMemory`，然后选择“添加包”。</span><span class="sxs-lookup"><span data-stu-id="d3182-135">Select `Microsoft.EntityFrameworkCore.InMemory`, and then select **Add Package**.</span></span>

### <a name="add-a-model-class"></a><span data-ttu-id="d3182-136">添加模型类</span><span class="sxs-lookup"><span data-stu-id="d3182-136">Add a model class</span></span>

<span data-ttu-id="d3182-137">模型是表示应用程序中的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="d3182-137">A model is an object that represents the data in your application.</span></span> <span data-ttu-id="d3182-138">在此示例中，唯一的模型是待办事项。</span><span class="sxs-lookup"><span data-stu-id="d3182-138">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="d3182-139">添加名为“模型”的文件夹。</span><span class="sxs-lookup"><span data-stu-id="d3182-139">Add a folder named *Models*.</span></span> <span data-ttu-id="d3182-140">在解决方案资源管理器中，右键单击项目。</span><span class="sxs-lookup"><span data-stu-id="d3182-140">In Solution Explorer, right-click the project.</span></span> <span data-ttu-id="d3182-141">选择“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="d3182-141">Select **Add** > **New Folder**.</span></span> <span data-ttu-id="d3182-142">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="d3182-142">Name the folder *Models*.</span></span>

![新建文件夹](first-web-api-mac/_static/folder.png)

<span data-ttu-id="d3182-144">注意：可将模型类置于项目的任意位置，但按照惯例会使用“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="d3182-144">Note: You can put model classes anywhere in your project, but the *Models* folder is used by convention.</span></span>

<span data-ttu-id="d3182-145">添加 `TodoItem` 类。</span><span class="sxs-lookup"><span data-stu-id="d3182-145">Add a `TodoItem` class.</span></span> <span data-ttu-id="d3182-146">右键单击“Models”文件夹，然后选择“添加”>“新建文件”>“常规”>“空类”。</span><span class="sxs-lookup"><span data-stu-id="d3182-146">Right-click the *Models* folder and select **Add > New File > General > Empty Class**.</span></span> <span data-ttu-id="d3182-147">将此类命名为 `TodoItem`，然后选择“新建”。</span><span class="sxs-lookup"><span data-stu-id="d3182-147">Name the class `TodoItem`, and then select **New**.</span></span>

<span data-ttu-id="d3182-148">将生成的代码替换为：</span><span class="sxs-lookup"><span data-stu-id="d3182-148">Replace the generated code with:</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoItem.cs)]

<span data-ttu-id="d3182-149">创建 `TodoItem` 时，数据库将生成 `Id`。</span><span class="sxs-lookup"><span data-stu-id="d3182-149">The database generates the `Id` when a `TodoItem` is created.</span></span>

### <a name="create-the-database-context"></a><span data-ttu-id="d3182-150">创建数据库上下文</span><span class="sxs-lookup"><span data-stu-id="d3182-150">Create the database context</span></span>

<span data-ttu-id="d3182-151">数据库上下文是为给定数据模型协调 Entity Framework 功能的主类。</span><span class="sxs-lookup"><span data-stu-id="d3182-151">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="d3182-152">将通过从 `Microsoft.EntityFrameworkCore.DbContext` 类派生的方式创建此类。</span><span class="sxs-lookup"><span data-stu-id="d3182-152">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="d3182-153">将 `TodoContext` 类添加到“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="d3182-153">Add a `TodoContext` class to the *Models* folder.</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

## <a name="add-a-controller"></a><span data-ttu-id="d3182-154">添加控制器</span><span class="sxs-lookup"><span data-stu-id="d3182-154">Add a controller</span></span>

<span data-ttu-id="d3182-155">在解决方案资源管理器的“控制器”文件夹中，添加 `TodoController` 类。</span><span class="sxs-lookup"><span data-stu-id="d3182-155">In Solution Explorer, in the *Controllers* folder, add the class `TodoController`.</span></span>

<span data-ttu-id="d3182-156">将生成的代码替换为以下内容（并添加右大括号）：</span><span class="sxs-lookup"><span data-stu-id="d3182-156">Replace the generated code with the following (and add closing braces):</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a><span data-ttu-id="d3182-157">启动应用</span><span class="sxs-lookup"><span data-stu-id="d3182-157">Launch the app</span></span>

<span data-ttu-id="d3182-158">在 Visual Studio 中，选择“运行”>“开始执行(调试)”启动应用。</span><span class="sxs-lookup"><span data-stu-id="d3182-158">In Visual Studio, select **Run > Start With Debugging** to launch the app.</span></span> <span data-ttu-id="d3182-159">Visual Studio 启动浏览器并导航到 `http://localhost:port`，其中“端口”是随机选择的端口号。</span><span class="sxs-lookup"><span data-stu-id="d3182-159">Visual Studio launches a browser and navigates to `http://localhost:port`, where *port* is a randomly chosen port number.</span></span> <span data-ttu-id="d3182-160">将收到 HTTP 404（未找到）错误。</span><span class="sxs-lookup"><span data-stu-id="d3182-160">You get an HTTP 404 (Not Found) error.</span></span>  <span data-ttu-id="d3182-161">将 URL 更改为 `http://localhost:port/api/values`。</span><span class="sxs-lookup"><span data-stu-id="d3182-161">Change the URL to `http://localhost:port/api/values`.</span></span> <span data-ttu-id="d3182-162">将显示 `ValuesController` 数据：</span><span class="sxs-lookup"><span data-stu-id="d3182-162">The `ValuesController` data will be displayed:</span></span>

```
["value1","value2"]
```

<span data-ttu-id="d3182-163">导航到 `http://localhost:port/api/todo` 处的 `Todo` 控制器：</span><span class="sxs-lookup"><span data-stu-id="d3182-163">Navigate to the `Todo` controller at`http://localhost:port/api/todo`:</span></span>

```
[{"key":1,"name":"Item1","isComplete":false}]
```

## <a name="implement-the-other-crud-operations"></a><span data-ttu-id="d3182-164">实现其他的 CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="d3182-164">Implement the other CRUD operations</span></span>

<span data-ttu-id="d3182-165">我们将向控制器添加 `Create`、`Update` 和 `Delete` 方法。</span><span class="sxs-lookup"><span data-stu-id="d3182-165">We'll add `Create`, `Update`, and `Delete` methods to the controller.</span></span> <span data-ttu-id="d3182-166">这些是主题的变体，因此在这里只提供代码并突出显示主要的差异。</span><span class="sxs-lookup"><span data-stu-id="d3182-166">These are variations on a theme, so I'll just show the code and highlight the main differences.</span></span> <span data-ttu-id="d3182-167">添加或更改代码后生成项目。</span><span class="sxs-lookup"><span data-stu-id="d3182-167">Build the project after adding or changing code.</span></span>

### <a name="create"></a><span data-ttu-id="d3182-168">创建</span><span class="sxs-lookup"><span data-stu-id="d3182-168">Create</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

<span data-ttu-id="d3182-169">这是 HTTP POST 方法，由 [`[HttpPost]`](/aspnet/core/api/microsoft.aspnetcore.mvc.httppostattribute) 特性指示的。</span><span class="sxs-lookup"><span data-stu-id="d3182-169">This is an HTTP POST method, indicated by the [`[HttpPost]`](/aspnet/core/api/microsoft.aspnetcore.mvc.httppostattribute) attribute.</span></span> <span data-ttu-id="d3182-170">[`[FromBody]`](/aspnet/core/api/microsoft.aspnetcore.mvc.frombodyattribute) 特性告诉 MVC 从 HTTP 请求正文获取待办事项的值。</span><span class="sxs-lookup"><span data-stu-id="d3182-170">The [`[FromBody]`](/aspnet/core/api/microsoft.aspnetcore.mvc.frombodyattribute) attribute tells MVC to get the value of the to-do item from the body of the HTTP request.</span></span>

<span data-ttu-id="d3182-171">`CreatedAtRoute` 方法返回 201 响应，这是在服务器上创建新资源的 HTTP POST 方法的标准响应。</span><span class="sxs-lookup"><span data-stu-id="d3182-171">The `CreatedAtRoute` method returns a 201 response, which is the standard response for an HTTP POST method that creates a new resource on the server.</span></span> <span data-ttu-id="d3182-172">`CreatedAtRoute` 还会向响应添加位置标头。</span><span class="sxs-lookup"><span data-stu-id="d3182-172">`CreatedAtRoute` also adds a Location header to the response.</span></span> <span data-ttu-id="d3182-173">位置标头指定新建的待办事项的 URI。</span><span class="sxs-lookup"><span data-stu-id="d3182-173">The Location header specifies the URI of the newly created to-do item.</span></span> <span data-ttu-id="d3182-174">请参阅 [10.2.2 201 已创建](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)。</span><span class="sxs-lookup"><span data-stu-id="d3182-174">See [10.2.2 201 Created](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>

### <a name="use-postman-to-send-a-create-request"></a><span data-ttu-id="d3182-175">使用 Postman 发送创建请求</span><span class="sxs-lookup"><span data-stu-id="d3182-175">Use Postman to send a Create request</span></span>

* <span data-ttu-id="d3182-176">启动应用（“运行”>“开始执行(调试)”）。</span><span class="sxs-lookup"><span data-stu-id="d3182-176">Start the app (**Run > Start With Debugging**).</span></span>
* <span data-ttu-id="d3182-177">启动 Postman。</span><span class="sxs-lookup"><span data-stu-id="d3182-177">Start Postman.</span></span>

![Postman 控制台](first-web-api/_static/pmc.png)

* <span data-ttu-id="d3182-179">将 HTTP 方法设置为 `POST`</span><span class="sxs-lookup"><span data-stu-id="d3182-179">Set the HTTP method to `POST`</span></span>
* <span data-ttu-id="d3182-180">选择“正文”单选按钮</span><span class="sxs-lookup"><span data-stu-id="d3182-180">Select the **Body** radio button</span></span>
* <span data-ttu-id="d3182-181">选择“原始”单选按钮</span><span class="sxs-lookup"><span data-stu-id="d3182-181">Select the **raw** radio button</span></span>
* <span data-ttu-id="d3182-182">将类型设置为 JSON</span><span class="sxs-lookup"><span data-stu-id="d3182-182">Set the type to JSON</span></span>
* <span data-ttu-id="d3182-183">在键值编辑器中，输入一个待办事项，例如</span><span class="sxs-lookup"><span data-stu-id="d3182-183">In the key-value editor, enter a Todo item such as</span></span>

```json
{
    "name":"walk dog",
    "isComplete":true
}
```

* <span data-ttu-id="d3182-184">选择“发送”</span><span class="sxs-lookup"><span data-stu-id="d3182-184">Select **Send**</span></span>

* <span data-ttu-id="d3182-185">选择下窗格中的“标头”选项卡，然后复制“位置”标头：</span><span class="sxs-lookup"><span data-stu-id="d3182-185">Select the Headers tab in the lower pane and copy the **Location** header:</span></span>

![Postman 控制台的“标头”选项卡](first-web-api/_static/pmget.png)

<span data-ttu-id="d3182-187">可以使用此位置标头 URI 访问刚刚创建的资源。</span><span class="sxs-lookup"><span data-stu-id="d3182-187">You can use the Location header URI to access the resource you just created.</span></span> <span data-ttu-id="d3182-188">重新调用创建名为 `"GetTodo"` 路由时使用的 `GetById` 方法：</span><span class="sxs-lookup"><span data-stu-id="d3182-188">Recall the `GetById` method created the `"GetTodo"` named route:</span></span>

```csharp
[HttpGet("{id}", Name = "GetTodo")]
public IActionResult GetById(string id)
```

### <a name="update"></a><span data-ttu-id="d3182-189">更新</span><span class="sxs-lookup"><span data-stu-id="d3182-189">Update</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]

<span data-ttu-id="d3182-190">`Update` 与 `Create` 类似，但是使用的是 HTTP PUT。</span><span class="sxs-lookup"><span data-stu-id="d3182-190">`Update` is similar to `Create`, but uses HTTP PUT.</span></span> <span data-ttu-id="d3182-191">响应是 [204（无内容）](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。</span><span class="sxs-lookup"><span data-stu-id="d3182-191">The response is [204 (No Content)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span> <span data-ttu-id="d3182-192">根据 HTTP 规范，PUT 请求需要客户端发送整个更新的实体，而不仅仅是增量。</span><span class="sxs-lookup"><span data-stu-id="d3182-192">According to the HTTP spec, a PUT request requires the client to send the entire updated entity, not just the deltas.</span></span> <span data-ttu-id="d3182-193">若要支持部分更新，请使用 HTTP PATCH。</span><span class="sxs-lookup"><span data-stu-id="d3182-193">To support partial updates, use HTTP PATCH.</span></span>

```json
{
  "key": 1,
  "name": "walk dog",
  "isComplete": true
}
```

![显示 204（无内容）响应的 Postman 控制台](first-web-api/_static/pmcput.png)

### <a name="delete"></a><span data-ttu-id="d3182-195">删除</span><span class="sxs-lookup"><span data-stu-id="d3182-195">Delete</span></span>

[!code-csharp[Main](first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_Delete)]

<span data-ttu-id="d3182-196">响应是 [204（无内容）](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。</span><span class="sxs-lookup"><span data-stu-id="d3182-196">The response is [204 (No Content)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span>

![显示 204（无内容）响应的 Postman 控制台](first-web-api/_static/pmd.png)

## <a name="next-steps"></a><span data-ttu-id="d3182-198">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d3182-198">Next steps</span></span>

* [<span data-ttu-id="d3182-199">路由到控制器操作</span><span class="sxs-lookup"><span data-stu-id="d3182-199">Routing to Controller Actions</span></span>](xref:mvc/controllers/routing)
* <span data-ttu-id="d3182-200">有关部署 API 的信息，请参阅[托管和部署](xref:host-and-deploy/index)。</span><span class="sxs-lookup"><span data-stu-id="d3182-200">For information about deploying your API, see [Host and deploy](xref:host-and-deploy/index).</span></span>
* <span data-ttu-id="d3182-201">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/first-web-api/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="d3182-201">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/first-web-api/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>
* [<span data-ttu-id="d3182-202">Postman</span><span class="sxs-lookup"><span data-stu-id="d3182-202">Postman</span></span>](https://www.getpostman.com/)
* [<span data-ttu-id="d3182-203">Fiddler</span><span class="sxs-lookup"><span data-stu-id="d3182-203">Fiddler</span></span>](https://www.telerik.com/download/fiddler)
