---
title: NSwag 和 ASP.NET Core 入门
author: zuckerthoben
description: 了解如何使用 NSwag 为 ASP.NET Core Web API 生成文档和帮助页面。
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 05/08/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: tutorials/get-started-with-nswag
ms.openlocfilehash: 0f0aa0eeaa174ef40f03aab2500a8b3ce37e9448
ms.sourcegitcommit: 9bc34b8269d2a150b844c3b8646dcb30278a95ea
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2018
ms.locfileid: "34094887"
---
# <a name="get-started-with-nswag-and-aspnet-core"></a><span data-ttu-id="456ec-103">NSwag 和 ASP.NET Core 入门</span><span class="sxs-lookup"><span data-stu-id="456ec-103">Get started with NSwag and ASP.NET Core</span></span>

<span data-ttu-id="456ec-104">作者：[Christoph Nienaber](https://twitter.com/zuckerthoben) 和 [Rico Suter](https://rsuter.com)</span><span class="sxs-lookup"><span data-stu-id="456ec-104">By [Christoph Nienaber](https://twitter.com/zuckerthoben) and [Rico Suter](https://rsuter.com)</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="456ec-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="456ec-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="456ec-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="456ec-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>
::: moniker-end

<span data-ttu-id="456ec-107">在 ASP.NET Core 中间件中使用 [NSwag](https://github.com/RSuter/NSwag) 需要 [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="456ec-107">Using [NSwag](https://github.com/RSuter/NSwag) with ASP.NET Core middleware requires the [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/) NuGet package.</span></span> <span data-ttu-id="456ec-108">该包由 Swagger 生成器、Swagger UI（v2 和 v3）和 [ReDoc UI](https://github.com/Rebilly/ReDoc) 组成。</span><span class="sxs-lookup"><span data-stu-id="456ec-108">The package consists of a Swagger generator, Swagger UI (v2 and v3), and [ReDoc UI](https://github.com/Rebilly/ReDoc).</span></span>

<span data-ttu-id="456ec-109">强烈建议使用 NSwag 的代码生成功能。</span><span class="sxs-lookup"><span data-stu-id="456ec-109">It's highly recommended to make use of NSwag's code generation capabilities.</span></span> <span data-ttu-id="456ec-110">请为代码生成选择下列选项之一：</span><span class="sxs-lookup"><span data-stu-id="456ec-110">Choose one of the following options for code generation:</span></span>

* <span data-ttu-id="456ec-111">使用 [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio)，这是一款 Windows 桌面应用，用于在 C# 和 TypeScript 中为 API 生成客户端代码。</span><span class="sxs-lookup"><span data-stu-id="456ec-111">Use [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio), a Windows desktop app for generating client code in C# and TypeScript for your API.</span></span>
* <span data-ttu-id="456ec-112">使用 [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) 或 [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) NuGet 包在项目中执行代码生成。</span><span class="sxs-lookup"><span data-stu-id="456ec-112">Use the [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) or [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) NuGet packages to do code generation inside your project.</span></span>
* <span data-ttu-id="456ec-113">使用[命令行](https://github.com/NSwag/NSwag/wiki/CommandLine)中的 NSwag。</span><span class="sxs-lookup"><span data-stu-id="456ec-113">Use NSwag from the [command line](https://github.com/NSwag/NSwag/wiki/CommandLine).</span></span>
* <span data-ttu-id="456ec-114">使用 [NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="456ec-114">Use the [NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild) NuGet package.</span></span>

## <a name="features"></a><span data-ttu-id="456ec-115">功能</span><span class="sxs-lookup"><span data-stu-id="456ec-115">Features</span></span>

<span data-ttu-id="456ec-116">使用 NSwag 的主要原因是它不仅能引入 Swagger UI 和 Swagger 生成器，还能利用灵活的代码生成功能。</span><span class="sxs-lookup"><span data-stu-id="456ec-116">The main reason to use NSwag is the ability to not only introduce the Swagger UI and Swagger generator, but to make use of the flexible code generation capabilities.</span></span> <span data-ttu-id="456ec-117">无需现有API &mdash; 可使用包含 Swagger 的第三方 API 并让 NSwag 生成客户端实现。</span><span class="sxs-lookup"><span data-stu-id="456ec-117">You don't need an existing API&mdash;you can use third-party APIs that incorporate Swagger and let NSwag generate a client implementation.</span></span> <span data-ttu-id="456ec-118">无论哪种方式，开发周期都会加快，可以更轻松地适应 API 更改。</span><span class="sxs-lookup"><span data-stu-id="456ec-118">Either way, the development cycle is expedited and you can more easily adapt to API changes.</span></span>

## <a name="package-installation"></a><span data-ttu-id="456ec-119">包安装</span><span class="sxs-lookup"><span data-stu-id="456ec-119">Package installation</span></span>

<span data-ttu-id="456ec-120">可使用以下方法添加 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="456ec-120">The NSwag NuGet package can be added with the following approaches:</span></span>

### <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="456ec-121">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="456ec-121">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="456ec-122">从“程序包管理器控制台”窗口：</span><span class="sxs-lookup"><span data-stu-id="456ec-122">From the **Package Manager Console** window:</span></span>
  * <span data-ttu-id="456ec-123">转到“视图” > “其他窗口” > “程序包管理器控制台”</span><span class="sxs-lookup"><span data-stu-id="456ec-123">Go to **View** > **Other Windows** > **Package Manager Console**</span></span>
  * <span data-ttu-id="456ec-124">导航到包含 TodoApi.csproj 文件的目录</span><span class="sxs-lookup"><span data-stu-id="456ec-124">Navigate to the directory in which the *TodoApi.csproj* file exists</span></span>
  * <span data-ttu-id="456ec-125">请执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="456ec-125">Execute the following command:</span></span>

    ```powershell
    Install-Package NSwag.AspNetCore
    ```

* <span data-ttu-id="456ec-126">从“管理 NuGet 程序包”对话框中：</span><span class="sxs-lookup"><span data-stu-id="456ec-126">From the **Manage NuGet Packages** dialog:</span></span>
  * <span data-ttu-id="456ec-127">右键单击“解决方案资源管理器” > “管理 NuGet 包”中的项目</span><span class="sxs-lookup"><span data-stu-id="456ec-127">Right-click the project in **Solution Explorer** > **Manage NuGet Packages**</span></span>
  * <span data-ttu-id="456ec-128">将“包源”设置为“nuget.org”</span><span class="sxs-lookup"><span data-stu-id="456ec-128">Set the **Package source** to "nuget.org"</span></span>
  * <span data-ttu-id="456ec-129">在搜索框中输入“NSwag.AspNetCore”</span><span class="sxs-lookup"><span data-stu-id="456ec-129">Enter "NSwag.AspNetCore" in the search box</span></span>
  * <span data-ttu-id="456ec-130">从“浏览”选项卡中选择“NSwag.AspNetCore”包，然后单击“安装”</span><span class="sxs-lookup"><span data-stu-id="456ec-130">Select the "NSwag.AspNetCore" package from the **Browse** tab and click **Install**</span></span>

### <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="456ec-131">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="456ec-131">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="456ec-132">右键单击“Solution Pad” > “添加包...”中的“包”文件夹</span><span class="sxs-lookup"><span data-stu-id="456ec-132">Right-click the *Packages* folder in **Solution Pad** > **Add Packages...**</span></span>
* <span data-ttu-id="456ec-133">将“添加包”窗口的“源”下拉列表设置为“nuget.org”</span><span class="sxs-lookup"><span data-stu-id="456ec-133">Set the **Add Packages** window's **Source** drop-down to "nuget.org"</span></span>
* <span data-ttu-id="456ec-134">在搜索框中输入“NSwag.AspNetCore”</span><span class="sxs-lookup"><span data-stu-id="456ec-134">Enter "NSwag.AspNetCore" in the search box</span></span>
* <span data-ttu-id="456ec-135">从结果窗格中选择“NSwag.AspNetCore”包，然后单击“添加包”</span><span class="sxs-lookup"><span data-stu-id="456ec-135">Select the "NSwag.AspNetCore" package from the results pane and click **Add Package**</span></span>

### <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="456ec-136">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="456ec-136">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="456ec-137">从“集成终端”中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="456ec-137">Run the following command from the **Integrated Terminal**:</span></span>

```console
dotnet add TodoApi.csproj package NSwag.AspNetCore
```

### <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="456ec-138">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="456ec-138">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="456ec-139">运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="456ec-139">Run the following command:</span></span>

```console
dotnet add TodoApi.csproj package NSwag.AspNetCore
```

---

## <a name="add-and-configure-swagger-middleware"></a><span data-ttu-id="456ec-140">添加并配置 Swagger 中间件</span><span class="sxs-lookup"><span data-stu-id="456ec-140">Add and configure Swagger middleware</span></span>

<span data-ttu-id="456ec-141">在 `Startup` 类中导入以下命名空间：</span><span class="sxs-lookup"><span data-stu-id="456ec-141">Import the following namespaces in the `Startup` class:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup.cs?name=snippet_StartupConfigureImports)]

<span data-ttu-id="456ec-142">在 `Startup.Configure` 方法中，启用中间件为生成的 Swagger 规范和 Swagger UI 提供服务：</span><span class="sxs-lookup"><span data-stu-id="456ec-142">In the `Startup.Configure` method, enable the middleware for serving the generated Swagger specification and the Swagger UI:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup.cs?name=snippet_Configure&highlight=6-10)]

<span data-ttu-id="456ec-143">启动应用。</span><span class="sxs-lookup"><span data-stu-id="456ec-143">Launch the app.</span></span> <span data-ttu-id="456ec-144">导航到 `http://localhost:<port>/swagger` 查看 Swagger UI。</span><span class="sxs-lookup"><span data-stu-id="456ec-144">Navigate to `http://localhost:<port>/swagger` to view the Swagger UI.</span></span> <span data-ttu-id="456ec-145">导航到 `http://localhost:<port>/swagger/v1/swagger.json` 查看 Swagger 规范。</span><span class="sxs-lookup"><span data-stu-id="456ec-145">Navigate to `http://localhost:<port>/swagger/v1/swagger.json` to view the Swagger specification.</span></span>

## <a name="code-generation"></a><span data-ttu-id="456ec-146">代码生成</span><span class="sxs-lookup"><span data-stu-id="456ec-146">Code generation</span></span>

### <a name="via-nswagstudio"></a><span data-ttu-id="456ec-147">通过 NSwagStudio</span><span class="sxs-lookup"><span data-stu-id="456ec-147">Via NSwagStudio</span></span>

* <span data-ttu-id="456ec-148">从官方 [GitHub 存储库](https://github.com/RSuter/NSwag/wiki/NSwagStudio)安装 NSwagStudio。</span><span class="sxs-lookup"><span data-stu-id="456ec-148">Install NSwagStudio from the official [GitHub repository](https://github.com/RSuter/NSwag/wiki/NSwagStudio).</span></span>
* <span data-ttu-id="456ec-149">启动 NSwagStudio。</span><span class="sxs-lookup"><span data-stu-id="456ec-149">Launch NSwagStudio.</span></span> <span data-ttu-id="456ec-150">在“Swagger 规范 URL”文本框中输入 swagger.json 文件 URL，然后单击“创建本地副本”按钮。</span><span class="sxs-lookup"><span data-stu-id="456ec-150">Enter the *swagger.json* file URL in the **Swagger Specification URL** textbox, and click the **Create local Copy** button.</span></span>
* <span data-ttu-id="456ec-151">选择“CSharp 客户端”作为客户端输出类型。</span><span class="sxs-lookup"><span data-stu-id="456ec-151">Select the **CSharp Client** client output type.</span></span> <span data-ttu-id="456ec-152">其他选项包括“TypeScript 客户端”和“CSharp Web API 控制器”。</span><span class="sxs-lookup"><span data-stu-id="456ec-152">Other options include **TypeScript Client** and **CSharp Web API Controller**.</span></span> <span data-ttu-id="456ec-153">使用 Web API 控制器基本上是一种反向生成。</span><span class="sxs-lookup"><span data-stu-id="456ec-153">Using a Web API Controller is basically a reverse generation.</span></span> <span data-ttu-id="456ec-154">它使用服务的规范来重新生成服务。</span><span class="sxs-lookup"><span data-stu-id="456ec-154">It uses a specification of a service to rebuild the service.</span></span>
* <span data-ttu-id="456ec-155">单击“生成输出”按钮。</span><span class="sxs-lookup"><span data-stu-id="456ec-155">Click the **Generate Outputs** button.</span></span> <span data-ttu-id="456ec-156">随即生成完整的 TodoApi.NSwag 项目 C# 客户端实现。</span><span class="sxs-lookup"><span data-stu-id="456ec-156">A complete C# client implementation of the *TodoApi.NSwag* project is produced.</span></span> <span data-ttu-id="456ec-157">单击“输出”部分的“CSharp 客户端”选项卡，查看生成的客户端代码：</span><span class="sxs-lookup"><span data-stu-id="456ec-157">Click the **CSharp Client** tab of the **Outputs** section to see the generated client code:</span></span>

```csharp
//----------------------
// <auto-generated>
//     Generated using the NSwag toolchain v11.17.3.0 (NJsonSchema v9.10.46.0 (Newtonsoft.Json v9.0.0.0)) (http://NSwag.org)
// </auto-generated>
//----------------------

namespace MyNamespace
{
    #pragma warning disable // Disable all warnings

    [System.CodeDom.Compiler.GeneratedCode("NSwag",
        "11.17.3.0 (NJsonSchema v9.10.46.0 (Newtonsoft.Json v9.0.0.0))")]
    public partial class TodoClient
    {
        private string _baseUrl = "http://localhost:50499";
        private System.Lazy<Newtonsoft.Json.JsonSerializerSettings> _settings;

        public TodoClient()
        {
            _settings = new System.Lazy
                <Newtonsoft.Json.JsonSerializerSettings>(() =>
            {
                var settings = new Newtonsoft.Json.JsonSerializerSettings();
                UpdateJsonSerializerSettings(settings);
                return settings;
            });
        }

        public string BaseUrl
        {
            get { return _baseUrl; }
            set { _baseUrl = value; }
        }

        // code omitted for brevity
```

> [!TIP]
> <span data-ttu-id="456ec-158">基于“CSharp 客户端”选项卡的“设置”选项卡中定义的设置，生成 C# 客户端代码。修改设置以执行任务，例如默认命名空间重命名和同步方法生成。</span><span class="sxs-lookup"><span data-stu-id="456ec-158">The C# client code is generated based on settings defined in the **Settings** tab of the **CSharp Client** tab. Modify the settings to perform tasks such as default namespace renaming and synchronous method generation.</span></span>

* <span data-ttu-id="456ec-159">将生成的 C# 代码复制到客户端项目的某个文件中（例如，[Xamarin.Forms](/xamarin/xamarin-forms/) 应用）。</span><span class="sxs-lookup"><span data-stu-id="456ec-159">Copy the generated C# code into a file in a client project (for example, a [Xamarin.Forms](/xamarin/xamarin-forms/) app).</span></span>
* <span data-ttu-id="456ec-160">开始使用 Web API：</span><span class="sxs-lookup"><span data-stu-id="456ec-160">Start consuming the web API:</span></span>

```csharp
var todoClient = new TodoClient();

// Gets all to-dos from the API
var allTodos = await todoClient.GetAllAsync();

// Create a new TodoItem, and save it in the API
var createdTodo = await todoClient.CreateAsync(new TodoItem());

// Get a single to-do by ID
var foundTodo = await todoClient.GetByIdAsync(1);
```

> [!NOTE]
> <span data-ttu-id="456ec-161">可将基 URL 和/或 HTTP 客户端注入 API 客户端。</span><span class="sxs-lookup"><span data-stu-id="456ec-161">You can inject a base URL and/or a HTTP client into the API client.</span></span> <span data-ttu-id="456ec-162">最佳做法是始终[重复使用 HttpClient](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/)。</span><span class="sxs-lookup"><span data-stu-id="456ec-162">The best practice is to always [reuse the HttpClient](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/).</span></span>

### <a name="other-ways-to-generate-client-code"></a><span data-ttu-id="456ec-163">生成客户端代码的其他方法</span><span class="sxs-lookup"><span data-stu-id="456ec-163">Other ways to generate client code</span></span>

<span data-ttu-id="456ec-164">可通过其他更适合你的工作流的方式生成客户端代码：</span><span class="sxs-lookup"><span data-stu-id="456ec-164">You can generate the client code in other ways, more suited to your workflow:</span></span>

* [<span data-ttu-id="456ec-165">MSBuild</span><span class="sxs-lookup"><span data-stu-id="456ec-165">MSBuild</span></span>](https://www.nuget.org/packages/NSwag.MSBuild/)

* [<span data-ttu-id="456ec-166">在代码中生成</span><span class="sxs-lookup"><span data-stu-id="456ec-166">In code</span></span>](https://github.com/NSwag/NSwag/wiki/SwaggerToCSharpClientGenerator)

* [<span data-ttu-id="456ec-167">通过 T4 模板生成</span><span class="sxs-lookup"><span data-stu-id="456ec-167">T4 templates</span></span>](https://github.com/NSwag/NSwag/wiki/T4)

## <a name="customize"></a><span data-ttu-id="456ec-168">自定义</span><span class="sxs-lookup"><span data-stu-id="456ec-168">Customize</span></span>

<span data-ttu-id="456ec-169">Swagger 提供用于记录对象模型以便于使用 Web API 的选项。</span><span class="sxs-lookup"><span data-stu-id="456ec-169">Swagger provides options for documenting the object model to ease consumption of the web API.</span></span>

### <a name="api-info-and-description"></a><span data-ttu-id="456ec-170">API 信息和说明</span><span class="sxs-lookup"><span data-stu-id="456ec-170">API info and description</span></span>

<span data-ttu-id="456ec-171">在 `Startup.Configure` 方法中，传递给 `UseSwagger` 方法的配置操作会添加诸如作者、许可证和说明的信息：</span><span class="sxs-lookup"><span data-stu-id="456ec-171">In the `Startup.Configure` method, a configuration action passed to the `UseSwagger` method adds information such as the author, license, and description:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup2.cs?name=snippet_UseSwagger)]

<span data-ttu-id="456ec-172">Swagger UI 显示版本的信息：</span><span class="sxs-lookup"><span data-stu-id="456ec-172">The Swagger UI displays the version's information:</span></span>

![带有版本信息的 Swagger UI](web-api-help-pages-using-swagger/_static/custom-info-nswag.png)

### <a name="xml-comments"></a><span data-ttu-id="456ec-174">XML 注释</span><span class="sxs-lookup"><span data-stu-id="456ec-174">XML comments</span></span>

<span data-ttu-id="456ec-175">可使用以下方法启用 XML 注释：</span><span class="sxs-lookup"><span data-stu-id="456ec-175">XML comments are enabled with the following approaches:</span></span>

# <a name="visual-studiotabvisual-studio-xml"></a>[<span data-ttu-id="456ec-176">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="456ec-176">Visual Studio</span></span>](#tab/visual-studio-xml/)

* <span data-ttu-id="456ec-177">右键单击“解决方案资源管理器”中的项目，然后选择“属性”</span><span class="sxs-lookup"><span data-stu-id="456ec-177">Right-click the project in **Solution Explorer** and select **Properties**</span></span>
* <span data-ttu-id="456ec-178">查看“生成”选项卡的“输出”部分下的“XML 文档文件”框</span><span class="sxs-lookup"><span data-stu-id="456ec-178">Check the **XML documentation file** box under the **Output** section of the **Build** tab</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac-xml"></a>[<span data-ttu-id="456ec-179">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="456ec-179">Visual Studio for Mac</span></span>](#tab/visual-studio-mac-xml/)

* <span data-ttu-id="456ec-180">打开“项目选项”对话框 >“生成” > “编译器”</span><span class="sxs-lookup"><span data-stu-id="456ec-180">Open the **Project Options** dialog > **Build** > **Compiler**</span></span>
* <span data-ttu-id="456ec-181">查看“常规选项”部分下的“生成 xml 文档”框</span><span class="sxs-lookup"><span data-stu-id="456ec-181">Check the **Generate xml documentation** box under the **General Options** section</span></span>

# <a name="visual-studio-codetabvisual-studio-code-xml"></a>[<span data-ttu-id="456ec-182">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="456ec-182">Visual Studio Code</span></span>](#tab/visual-studio-code-xml/)

<span data-ttu-id="456ec-183">将以下代码片段手动添加到 .csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="456ec-183">Manually add the following snippet to the *.csproj* file:</span></span>

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement)]

---

### <a name="data-annotations"></a><span data-ttu-id="456ec-184">数据注释</span><span class="sxs-lookup"><span data-stu-id="456ec-184">Data annotations</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="456ec-185">NSwag 使用[反射](/dotnet/csharp/programming-guide/concepts/reflection)，建议使用 [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult) 作为 Web API 操作的返回类型。</span><span class="sxs-lookup"><span data-stu-id="456ec-185">NSwag uses [Reflection](/dotnet/csharp/programming-guide/concepts/reflection), and the recommended return type for web API actions is [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult).</span></span> <span data-ttu-id="456ec-186">因此，NSwag 无法推断正在执行的操作和返回的结果。</span><span class="sxs-lookup"><span data-stu-id="456ec-186">Consequently, NSwag can't infer what your action is doing and what it returns.</span></span> <span data-ttu-id="456ec-187">请看下面的示例：</span><span class="sxs-lookup"><span data-stu-id="456ec-187">Consider the following example:</span></span>

<span data-ttu-id="456ec-188">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateAction)]</span><span class="sxs-lookup"><span data-stu-id="456ec-188">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateAction)]</span></span>

<span data-ttu-id="456ec-189">上述操作返回 `IActionResult`，但在操作内部返回 [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute) 或 [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest)。</span><span class="sxs-lookup"><span data-stu-id="456ec-189">The preceding action returns `IActionResult`, but inside the action it's returning either [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute) or [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest).</span></span> <span data-ttu-id="456ec-190">使用数据注释告知客户端此操作会返回哪些 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="456ec-190">Data annotations are used to tell clients which HTTP status codes this action is known to return.</span></span> <span data-ttu-id="456ec-191">使用以下属性修饰该操作：</span><span class="sxs-lookup"><span data-stu-id="456ec-191">Decorate the action with the following attributes:</span></span>

<span data-ttu-id="456ec-192">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateActionAttributes)]</span><span class="sxs-lookup"><span data-stu-id="456ec-192">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateActionAttributes)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="456ec-193">NSwag 使用[反射](/dotnet/csharp/programming-guide/concepts/reflection)，建议的 Web API 操作返回类型为 [ActionResult\<T>](/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1)。</span><span class="sxs-lookup"><span data-stu-id="456ec-193">NSwag uses [Reflection](/dotnet/csharp/programming-guide/concepts/reflection), and the recommended return type for web API actions is [ActionResult\<T>](/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1).</span></span> <span data-ttu-id="456ec-194">因此，NSwag 仅可以推断 `T` 定义的返回类型。</span><span class="sxs-lookup"><span data-stu-id="456ec-194">Consequently, NSwag can only infer the return type defined by `T`.</span></span> <span data-ttu-id="456ec-195">无法推断操作中其他可能的返回类型。</span><span class="sxs-lookup"><span data-stu-id="456ec-195">Other possible return types in the action cannot be inferred.</span></span> <span data-ttu-id="456ec-196">请看下面的示例：</span><span class="sxs-lookup"><span data-stu-id="456ec-196">Consider the following example:</span></span>

<span data-ttu-id="456ec-197">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateAction)]</span><span class="sxs-lookup"><span data-stu-id="456ec-197">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateAction)]</span></span>

<span data-ttu-id="456ec-198">上述操作返回 `ActionResult<T>`，但在操作内部返回 [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute)。</span><span class="sxs-lookup"><span data-stu-id="456ec-198">The preceding action returns `ActionResult<T>`, but inside the action it's returning either [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute).</span></span> <span data-ttu-id="456ec-199">由于使用 [[ApiController]](/dotnet/api/microsoft.aspnetcore.mvc.apicontrollerattribute) 属性修饰控制器，所以也可能出现 [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest) 响应。</span><span class="sxs-lookup"><span data-stu-id="456ec-199">Since the controller is decorated with the [[ApiController]](/dotnet/api/microsoft.aspnetcore.mvc.apicontrollerattribute) attribute, a [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest) response is possible too.</span></span> <span data-ttu-id="456ec-200">有关详细信息，请参阅[自动 HTTP 400 响应](xref:web-api/index#automatic-http-400-responses)。</span><span class="sxs-lookup"><span data-stu-id="456ec-200">See [Automatic HTTP 400 responses](xref:web-api/index#automatic-http-400-responses) for more info.</span></span> <span data-ttu-id="456ec-201">使用数据注释告知客户端此操作会返回哪些 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="456ec-201">Data annotations are used to tell clients which HTTP status codes this action is known to return.</span></span> <span data-ttu-id="456ec-202">使用以下属性修饰该操作：</span><span class="sxs-lookup"><span data-stu-id="456ec-202">Decorate the action with the following attributes:</span></span>

<span data-ttu-id="456ec-203">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateActionAttributes)]</span><span class="sxs-lookup"><span data-stu-id="456ec-203">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateActionAttributes)]</span></span>
::: moniker-end

<span data-ttu-id="456ec-204">Swagger 生成器现在可准确地描述此操作，且生成的客户端知道调用终结点时收到的内容。</span><span class="sxs-lookup"><span data-stu-id="456ec-204">The Swagger generator can now accurately describe this action, and generated clients know what they receive when calling the endpoint.</span></span> <span data-ttu-id="456ec-205">强烈建议使用这些属性来修饰所有操作。</span><span class="sxs-lookup"><span data-stu-id="456ec-205">Decorating all actions with these attributes is highly recommended.</span></span> <span data-ttu-id="456ec-206">有关 API 操作应返回的 HTTP 响应的指导原则，请参阅 [RFC 7231 规范](https://tools.ietf.org/html/rfc7231#section-4.3)。</span><span class="sxs-lookup"><span data-stu-id="456ec-206">For guidelines on what HTTP responses your API actions should return, see the [RFC 7231 specification](https://tools.ietf.org/html/rfc7231#section-4.3).</span></span>
