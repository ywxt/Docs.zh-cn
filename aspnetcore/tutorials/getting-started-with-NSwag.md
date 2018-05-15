---
title: NSwag 和 ASP.NET Core 入门
author: zuckerthoben
description: 了解如何使用 NSwag 为 ASP.NET Core Web API 应用生成文档和帮助页面。
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 03/15/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: tutorials/get-started-with-nswag
ms.openlocfilehash: 80e6a9e1702d8f68d139d2ff9c3a01a27c40cecb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="get-started-with-nswag-and-aspnet-core"></a><span data-ttu-id="a6d1d-103">NSwag 和 ASP.NET Core 入门</span><span class="sxs-lookup"><span data-stu-id="a6d1d-103">Get started with NSwag and ASP.NET Core</span></span>

<span data-ttu-id="a6d1d-104">作者：[Christoph Nienaber](https://twitter.com/zuckerthoben) 和 [Rico Suter](https://rsuter.com)</span><span class="sxs-lookup"><span data-stu-id="a6d1d-104">By [Christoph Nienaber](https://twitter.com/zuckerthoben) and [Rico Suter](https://rsuter.com)</span></span>

<span data-ttu-id="a6d1d-105">在 ASP.NET Core 中间件中使用 [NSwag](https://github.com/RSuter/NSwag) 需要 [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-105">Using [NSwag](https://github.com/RSuter/NSwag) with ASP.NET Core middleware requires the [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/) NuGet package.</span></span> <span data-ttu-id="a6d1d-106">该包由 Swagger 生成器、Swagger UI（v2 和 v3）和 [ReDoc UI](https://github.com/Rebilly/ReDoc) 组成。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-106">The package consists of a Swagger generator, Swagger UI (v2 and v3), and [ReDoc UI](https://github.com/Rebilly/ReDoc).</span></span>

<span data-ttu-id="a6d1d-107">强烈建议使用 NSwag 的代码生成功能。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-107">It's highly recommended to make use of NSwag's code generation capabilities.</span></span> <span data-ttu-id="a6d1d-108">请为代码生成选择下列选项之一：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-108">Choose one of the following options for code generation:</span></span>

* <span data-ttu-id="a6d1d-109">使用 [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio)，这是一款 Windows 桌面应用，用于在 C# 和 TypeScript 中为 API 生成客户端代码</span><span class="sxs-lookup"><span data-stu-id="a6d1d-109">Use [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio), a Windows desktop app for generating client code in C# and TypeScript for your API</span></span>
* <span data-ttu-id="a6d1d-110">使用 [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) 或 [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) NuGet 包在项目中执行代码生成</span><span class="sxs-lookup"><span data-stu-id="a6d1d-110">Use the [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) or [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) NuGet packages to do code generation inside your project</span></span>
* <span data-ttu-id="a6d1d-111">使用[命令行](https://github.com/NSwag/NSwag/wiki/CommandLine)中的 NSwag</span><span class="sxs-lookup"><span data-stu-id="a6d1d-111">Use NSwag from the [command line](https://github.com/NSwag/NSwag/wiki/CommandLine)</span></span>
* <span data-ttu-id="a6d1d-112">使用 [NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild) NuGet 包</span><span class="sxs-lookup"><span data-stu-id="a6d1d-112">Use the [NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild) NuGet package</span></span>

## <a name="features"></a><span data-ttu-id="a6d1d-113">功能</span><span class="sxs-lookup"><span data-stu-id="a6d1d-113">Features</span></span>

<span data-ttu-id="a6d1d-114">使用 NSwag 的主要原因是它不仅能引入 Swagger UI 和 Swagger 生成器，还能利用灵活的代码生成功能。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-114">The main reason to use NSwag is the ability to not only introduce the Swagger UI and Swagger generator, but to make use of the flexible code generation capabilities.</span></span> <span data-ttu-id="a6d1d-115">无需现有API &mdash; 可使用包含 Swagger 的第三方 API 并让 NSwag 生成客户端实现。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-115">You don't need an existing API&mdash;you can use third-party APIs that incorporate Swagger and let NSwag generate a client implementation.</span></span> <span data-ttu-id="a6d1d-116">无论哪种方式，开发周期都会加快，可以更轻松地适应 API 更改。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-116">Either way, the development cycle is expedited and you can more easily adapt to API changes.</span></span>

## <a name="package-installation"></a><span data-ttu-id="a6d1d-117">包安装</span><span class="sxs-lookup"><span data-stu-id="a6d1d-117">Package installation</span></span>

<span data-ttu-id="a6d1d-118">可使用以下方法添加 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-118">The NSwag NuGet package can be added with the following approaches:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="a6d1d-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6d1d-119">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="a6d1d-120">从“程序包管理器控制台”窗口：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-120">From the **Package Manager Console** window:</span></span>

    ```powershell
    Install-Package NSwag.AspNetCore
    ```

* <span data-ttu-id="a6d1d-121">从“管理 NuGet 程序包”对话框中：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-121">From the **Manage NuGet Packages** dialog:</span></span>
  * <span data-ttu-id="a6d1d-122">右键单击“解决方案资源管理器” > “管理 NuGet 包”中的项目</span><span class="sxs-lookup"><span data-stu-id="a6d1d-122">Right-click your project in **Solution Explorer** > **Manage NuGet Packages**</span></span>
  * <span data-ttu-id="a6d1d-123">将“包源”设置为“nuget.org”</span><span class="sxs-lookup"><span data-stu-id="a6d1d-123">Set the **Package source** to "nuget.org"</span></span>
  * <span data-ttu-id="a6d1d-124">在搜索框中输入“NSwag.AspNetCore”</span><span class="sxs-lookup"><span data-stu-id="a6d1d-124">Enter "NSwag.AspNetCore" in the search box</span></span>
  * <span data-ttu-id="a6d1d-125">从“浏览”选项卡中选择“NSwag.AspNetCore”包，然后单击“安装”</span><span class="sxs-lookup"><span data-stu-id="a6d1d-125">Select the "NSwag.AspNetCore" package from the **Browse** tab and click **Install**</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="a6d1d-126">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="a6d1d-126">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="a6d1d-127">右键单击“Solution Pad” > “添加包...”中的“包”文件夹</span><span class="sxs-lookup"><span data-stu-id="a6d1d-127">Right-click the *Packages* folder in **Solution Pad** > **Add Packages...**</span></span>
* <span data-ttu-id="a6d1d-128">将“添加包”窗口的“源”下拉列表设置为“nuget.org”</span><span class="sxs-lookup"><span data-stu-id="a6d1d-128">Set the **Add Packages** window's **Source** drop-down to "nuget.org"</span></span>
* <span data-ttu-id="a6d1d-129">在搜索框中输入 NSwag.AspNetCore</span><span class="sxs-lookup"><span data-stu-id="a6d1d-129">Enter NSwag.AspNetCore in the search box</span></span>
* <span data-ttu-id="a6d1d-130">从结果窗格中选择“NSwag.AspNetCore”包，然后单击“添加包”</span><span class="sxs-lookup"><span data-stu-id="a6d1d-130">Select the NSwag.AspNetCore package from the results pane and click **Add Package**</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="a6d1d-131">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a6d1d-131">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="a6d1d-132">从“集成终端”中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-132">Run the following command from the **Integrated Terminal**:</span></span>

```console
dotnet add TodoApi.NSwag.csproj package NSwag.AspNetCore
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="a6d1d-133">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="a6d1d-133">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="a6d1d-134">运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-134">Run the following command:</span></span>

```console
dotnet add TodoApi.NSwag.csproj package NSwag.AspNetCore
```

---

## <a name="add-and-configure-swagger-middleware"></a><span data-ttu-id="a6d1d-135">添加并配置 Swagger 中间件</span><span class="sxs-lookup"><span data-stu-id="a6d1d-135">Add and configure Swagger middleware</span></span>

<span data-ttu-id="a6d1d-136">在 `Info` 类中导入以下命名空间：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-136">Import the following namespaces in the `Info` class:</span></span>

```csharp
using NSwag.AspNetCore;
using System.Reflection;
using NJsonSchema;
```

<span data-ttu-id="a6d1d-137">在 `Startup.Configure` 方法中，启用中间件为生成的 Swagger 规范和 Swagger UI 提供服务：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-137">In the `Startup.Configure` method, enable the middleware for serving the generated Swagger specification and the Swagger UI:</span></span>

[!code-cs[](../tutorials/web-api-help-pages-using-swagger/samples/TodoApi.NSwag/Startup.cs?name=snippet_Configure&highlight=4,7-10)]

<span data-ttu-id="a6d1d-138">启动应用。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-138">Launch the app.</span></span> <span data-ttu-id="a6d1d-139">导航到 `/swagger` 查看 Swagger UI。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-139">Navigate to `/swagger` to view the Swagger UI.</span></span> <span data-ttu-id="a6d1d-140">导航到 `/swagger/v1/swagger.json` 查看 Swagger 规范。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-140">Navigate to `/swagger/v1/swagger.json` to view the Swagger specification.</span></span>

## <a name="code-generation"></a><span data-ttu-id="a6d1d-141">代码生成</span><span class="sxs-lookup"><span data-stu-id="a6d1d-141">Code generation</span></span>

### <a name="via-nswagstudio"></a><span data-ttu-id="a6d1d-142">通过 NSwagStudio</span><span class="sxs-lookup"><span data-stu-id="a6d1d-142">Via NSwagStudio</span></span>

* <span data-ttu-id="a6d1d-143">从官方 [GitHub 存储库](https://github.com/RSuter/NSwag/wiki/NSwagStudio)安装 `NSwagStudio`。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-143">Install `NSwagStudio` from the official [GitHub repository](https://github.com/RSuter/NSwag/wiki/NSwagStudio).</span></span>

* <span data-ttu-id="a6d1d-144">启动 NSwagStudio。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-144">Launch NSwagStudio.</span></span> <span data-ttu-id="a6d1d-145">输入 swagger.json 的位置或直接复制它：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-145">Enter the location of your *swagger.json* or copy it directly:</span></span>

![NSwagStudio](web-api-help-pages-using-swagger/_static/NSwagStudio.png)

* <span data-ttu-id="a6d1d-147">指示所需的客户端输出类型。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-147">Indicate the desired client output type.</span></span> <span data-ttu-id="a6d1d-148">选项包括“TypeScript 客户端”、“CSharp 客户端”或“CSharp Web API 控制器”。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-148">Options include **TypeScript Client**, **CSharp Client**, or **CSharp Web API Controller**.</span></span> <span data-ttu-id="a6d1d-149">使用 Web API 控制器基本上是一种反向生成。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-149">Using a Web API Controller is basically a reverse generation.</span></span> <span data-ttu-id="a6d1d-150">它使用服务的规范来重新生成服务。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-150">It uses a specification of a service to rebuild the service.</span></span>

* <span data-ttu-id="a6d1d-151">单击“生成输出”。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-151">Click **Generate Outputs**.</span></span>

* <span data-ttu-id="a6d1d-152">可在此处看到 C# 中的 TodoApi.NSwag 示例的完整客户端实现：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-152">Here you see a complete client implementation of the *TodoApi.NSwag* sample in C#:</span></span>

![NSwagStudio-Output](web-api-help-pages-using-swagger/_static/NSwagStudio-Output.png)

* <span data-ttu-id="a6d1d-154">将该文件放入客户端项目（例如，[Xamarin.Forms](/xamarin/xamarin-forms/) 应用）。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-154">Put the file into a client project (for example, a [Xamarin.Forms](/xamarin/xamarin-forms/) app).</span></span> <span data-ttu-id="a6d1d-155">开始使用 API：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-155">Start consuming the API:</span></span>

```csharp
var todoClient = new TodoClient();

// Gets all Todos from the Api
var allTodos = await todoClient.GetAllAsync();

// Create a new TodoItem and save it in the Api
var createdTodo = await todoClient.CreateAsync(new TodoItem);

// Get a single Todo by Id
var foundTodo = await todoClient.GetByIdAsync(1);
```

> [!NOTE]
> <span data-ttu-id="a6d1d-156">可将基 URL 和/或 HTTP 客户端注入 API 客户端。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-156">You can inject a base URL and/or a HTTP client into the API client.</span></span> <span data-ttu-id="a6d1d-157">最佳做法是始终[重复使用 HttpClient](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/)。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-157">The best practice is to always [reuse the HttpClient](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/).</span></span>

<span data-ttu-id="a6d1d-158">现在可开始轻松地将 API 实施到客户端项目中。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-158">You can now start implementing your API into client projects easily.</span></span>

### <a name="other-ways-to-generate-client-code"></a><span data-ttu-id="a6d1d-159">生成客户端代码的其他方法</span><span class="sxs-lookup"><span data-stu-id="a6d1d-159">Other ways to generate client code</span></span>

<span data-ttu-id="a6d1d-160">可通过其他更适合你的工作流的方式生成代码：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-160">You can generate the code in other ways, more suited to your workflow:</span></span>

* [<span data-ttu-id="a6d1d-161">MSBuild</span><span class="sxs-lookup"><span data-stu-id="a6d1d-161">MSBuild</span></span>](https://www.nuget.org/packages/NSwag.MSBuild/)

* [<span data-ttu-id="a6d1d-162">在代码中生成</span><span class="sxs-lookup"><span data-stu-id="a6d1d-162">In code</span></span>](https://github.com/NSwag/NSwag/wiki/SwaggerToCSharpClientGenerator)

* [<span data-ttu-id="a6d1d-163">通过 T4 模板生成</span><span class="sxs-lookup"><span data-stu-id="a6d1d-163">T4 templates</span></span>](https://github.com/NSwag/NSwag/wiki/T4)

## <a name="customization"></a><span data-ttu-id="a6d1d-164">自定义</span><span class="sxs-lookup"><span data-stu-id="a6d1d-164">Customization</span></span>

### <a name="xml-comments"></a><span data-ttu-id="a6d1d-165">XML 注释</span><span class="sxs-lookup"><span data-stu-id="a6d1d-165">XML comments</span></span>

<span data-ttu-id="a6d1d-166">可使用以下方法启用 XML 注释：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-166">XML comments are enabled with the following approaches:</span></span>

#### <a name="visual-studiotabvisual-studio-xml"></a>[<span data-ttu-id="a6d1d-167">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6d1d-167">Visual Studio</span></span>](#tab/visual-studio-xml/)
* <span data-ttu-id="a6d1d-168">右键单击“解决方案资源管理器”中的项目，然后选择“属性”</span><span class="sxs-lookup"><span data-stu-id="a6d1d-168">Right-click the project in **Solution Explorer** and select **Properties**</span></span>
* <span data-ttu-id="a6d1d-169">查看“生成”选项卡的“输出”部分下的“XML 文档文件”框：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-169">Check the **XML documentation file** box under the **Output** section of the **Build** tab:</span></span>

![项目属性的“生成”选项卡](web-api-help-pages-using-swagger/_static/swagger-xml-comments.png)

#### <a name="visual-studio-for-mactabvisual-studio-mac-xml"></a>[<span data-ttu-id="a6d1d-171">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="a6d1d-171">Visual Studio for Mac</span></span>](#tab/visual-studio-mac-xml/)
* <span data-ttu-id="a6d1d-172">打开“项目选项”对话框 >“生成” > “编译器”</span><span class="sxs-lookup"><span data-stu-id="a6d1d-172">Open the **Project Options** dialog > **Build** > **Compiler**</span></span>
* <span data-ttu-id="a6d1d-173">查看“常规选项”部分下的“生成 xml 文档”框：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-173">Check the **Generate xml documentation** box under the **General Options** section:</span></span>

![项目选项的“常规选项”部分](web-api-help-pages-using-swagger/_static/swagger-xml-comments-mac.png)

#### <a name="visual-studio-codetabvisual-studio-code-xml"></a>[<span data-ttu-id="a6d1d-175">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a6d1d-175">Visual Studio Code</span></span>](#tab/visual-studio-code-xml/)
<span data-ttu-id="a6d1d-176">将以下代码片段手动添加到 .csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-176">Manually add the following snippet to the *.csproj* file:</span></span>

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/TodoApi.NSwag/TodoApiNSwag.csproj?range=7-9)]

* * *
## <a name="data-annotations"></a><span data-ttu-id="a6d1d-177">数据注释</span><span class="sxs-lookup"><span data-stu-id="a6d1d-177">Data annotations</span></span>

<span data-ttu-id="a6d1d-178">NSwag 使用[反射](/dotnet/csharp/programming-guide/concepts/reflection)，Web API 操作的最佳做法是返回 [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult)。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-178">NSwag uses [Reflection](/dotnet/csharp/programming-guide/concepts/reflection), and the best practice for Web API actions is to return [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult).</span></span> <span data-ttu-id="a6d1d-179">因此，NSwag 无法推断正在执行的操作和返回的结果。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-179">Consequently, NSwag can't infer what your action is doing and what it returns.</span></span> <span data-ttu-id="a6d1d-180">请看下面的示例：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-180">Consider the following example:</span></span>

```csharp
public IActionResult Create([FromBody] TodoItem item)
{
    if (item == null)
    {
        return BadRequest();
    }

    _context.TodoItems.Add(item);
    _context.SaveChanges();

     return CreatedAtRoute("GetTodo", new { id = item.Id }, item);
}
```

<span data-ttu-id="a6d1d-181">上述操作返回 `IActionResult`，但在操作内部返回 [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute) 或 [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest)。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-181">The preceding action returns `IActionResult`, but inside the action it's returning either [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute) or [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest).</span></span> <span data-ttu-id="a6d1d-182">使用数据注释告知客户端此操作返回的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-182">Data annotations are used to tell clients which HTTP response this action is returning.</span></span> <span data-ttu-id="a6d1d-183">使用以下属性修饰该操作：</span><span class="sxs-lookup"><span data-stu-id="a6d1d-183">Decorate the action with the following attributes:</span></span>

```csharp
[HttpPost]
[ProducesResponseType(typeof(TodoItem), 201)] // Created
[ProducesResponseType(typeof(TodoItem), 400)] // BadRequest
public IActionResult Create([FromBody] TodoItem item)
```

<span data-ttu-id="a6d1d-184">Swagger 生成器现在可准确地描述此操作，且生成的客户端知道调用终结点时收到的内容。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-184">The Swagger generator can now accurately describe this action, and generated clients know what they receive when calling the endpoint.</span></span> <span data-ttu-id="a6d1d-185">强烈建议使用这些属性来修饰所有操作。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-185">Decorating all actions with these attributes is highly recommended.</span></span> <span data-ttu-id="a6d1d-186">有关 API 操作应返回的 HTTP 响应的指导原则，请参阅 [RFC 7231 规范](https://tools.ietf.org/html/rfc7231#section-4.3)。</span><span class="sxs-lookup"><span data-stu-id="a6d1d-186">For guidelines on what HTTP responses your API actions should return, see the [RFC 7231 specification](https://tools.ietf.org/html/rfc7231#section-4.3).</span></span>
