---
title: ASP.NET Core 中的文件提供程序
author: ardalis
description: 了解 ASP.NET Core 如何通过文件提供程序来抽象化文件系统访问。
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/file-providers
ms.openlocfilehash: cdbffdadd9616fe941809d67dc2c0bbd52149561
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2018
ms.locfileid: "29724566"
---
# <a name="file-providers-in-aspnet-core"></a><span data-ttu-id="5a2c0-103">ASP.NET Core 中的文件提供程序</span><span class="sxs-lookup"><span data-stu-id="5a2c0-103">File Providers in ASP.NET Core</span></span>

<span data-ttu-id="5a2c0-104">作者：[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="5a2c0-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="5a2c0-105">ASP.NET Core 通过文件提供程序来抽象化文件系统访问。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-105">ASP.NET Core abstracts file system access through the use of File Providers.</span></span>

<span data-ttu-id="5a2c0-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="5a2c0-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="file-provider-abstractions"></a><span data-ttu-id="5a2c0-107">文件提供程序抽象</span><span class="sxs-lookup"><span data-stu-id="5a2c0-107">File Provider abstractions</span></span>

<span data-ttu-id="5a2c0-108">文件提供程序是对文件系统的抽象。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-108">File Providers are an abstraction over file systems.</span></span> <span data-ttu-id="5a2c0-109">主接口是`IFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-109">The main interface is `IFileProvider`.</span></span> <span data-ttu-id="5a2c0-110">`IFileProvider` 公开一些方法以获取文件信息 (`IFileInfo`)、目录信息 (`IDirectoryContents`)，以及设置更改通知（使用 `IChangeToken`）。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-110">`IFileProvider` exposes methods to get file information (`IFileInfo`), directory information (`IDirectoryContents`), and to set up change notifications (using an `IChangeToken`).</span></span>

<span data-ttu-id="5a2c0-111">`IFileInfo` 提供有关单个文件或目录的方法和属性。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-111">`IFileInfo` provides methods and properties about individual files or directories.</span></span> <span data-ttu-id="5a2c0-112">它有两个布尔属性（`Exists` 和`IsDirectory`），以及描述文件 `Name``Length` （以字节为单位）、`LastModified` 日期的属性。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-112">It has two boolean properties, `Exists` and `IsDirectory`, as well as properties describing the file's `Name`, `Length` (in bytes), and `LastModified` date.</span></span> <span data-ttu-id="5a2c0-113">可使用其 `CreateReadStream` 方法从文件中读取。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-113">You can read from the file using its `CreateReadStream` method.</span></span>

## <a name="file-provider-implementations"></a><span data-ttu-id="5a2c0-114">文件提供程序实现</span><span class="sxs-lookup"><span data-stu-id="5a2c0-114">File Provider implementations</span></span>

<span data-ttu-id="5a2c0-115">`IFileProvider` 的三种实现可用：物理、嵌入和复合。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-115">Three implementations of `IFileProvider` are available: Physical, Embedded, and Composite.</span></span> <span data-ttu-id="5a2c0-116">物理提供程序用于访问实际系统的文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-116">The physical provider is used to access the actual system's files.</span></span> <span data-ttu-id="5a2c0-117">嵌入式提供程序用于访问嵌入在程序集中的文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-117">The embedded provider is used to access files embedded in assemblies.</span></span> <span data-ttu-id="5a2c0-118">复合式提供程序提供对一个或多个其他提供程序中的文件和目录的合并访问。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-118">The composite provider is used to provide combined access to files and directories from one or more other providers.</span></span>

### <a name="physicalfileprovider"></a><span data-ttu-id="5a2c0-119">PhysicalFileProvider</span><span class="sxs-lookup"><span data-stu-id="5a2c0-119">PhysicalFileProvider</span></span>

<span data-ttu-id="5a2c0-120">`PhysicalFileProvider` 提供对物理文件系统的访问。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-120">The `PhysicalFileProvider` provides access to the physical file system.</span></span> <span data-ttu-id="5a2c0-121">它包装 `System.IO.File` 类型（针对物理提供程序），将所有路径范围限定在一个目录及其子目录中。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-121">It wraps the `System.IO.File` type (for the physical provider), scoping all paths to a directory and its children.</span></span> <span data-ttu-id="5a2c0-122">此范围限制对特定目录及其子目录的访问，从而阻止对该边界外的文件系统的访问。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-122">This scoping limits access to a certain directory and its children, preventing access to the file system outside of this boundary.</span></span> <span data-ttu-id="5a2c0-123">实例化此提供程序时，用户必须向其提供一个目录路径，它可作为对该提供程序的所有请求的基本路径（并且限制此路径之外的访问）。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-123">When instantiating this provider, you must provide it with a directory path, which serves as the base path for all requests made to this provider (and which restricts access outside of this path).</span></span> <span data-ttu-id="5a2c0-124">在 ASP.NET Core 应用中，可以直接实例化 `PhysicalFileProvider` 提供程序，也可以通过 [依赖关系注入](dependency-injection.md)在控制器或服务的构造函数中请求 `IFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-124">In an ASP.NET Core app, you can instantiate a `PhysicalFileProvider` provider directly, or you can request an `IFileProvider` in a Controller or service's constructor through [dependency injection](dependency-injection.md).</span></span> <span data-ttu-id="5a2c0-125">后一种方法生成的解决方案通常更具灵活性和可测试性。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-125">The latter approach will typically yield a more flexible and testable solution.</span></span>

<span data-ttu-id="5a2c0-126">以下示例演示如何创建 `PhysicalFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-126">The sample below shows how to create a `PhysicalFileProvider`.</span></span>


```csharp
IFileProvider provider = new PhysicalFileProvider(applicationRoot);
IDirectoryContents contents = provider.GetDirectoryContents(""); // the applicationRoot contents
IFileInfo fileInfo = provider.GetFileInfo("wwwroot/js/site.js"); // a file under applicationRoot
```

<span data-ttu-id="5a2c0-127">你可以循环访问其目录内容，或通过提供子路径来获取特定文件的信息。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-127">You can iterate through its directory contents or get a specific file's information by providing a subpath.</span></span>

<span data-ttu-id="5a2c0-128">若要从控制器请求提供程序，请在控制器的构造函数中指定该提供程序，并将其分配给本地字段。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-128">To request a provider from a controller, specify it in the controller's constructor and assign it to a local field.</span></span> <span data-ttu-id="5a2c0-129">使用操作方法中的本地实例：</span><span class="sxs-lookup"><span data-stu-id="5a2c0-129">Use the local instance from your action methods:</span></span>

[!code-csharp[](file-providers/sample/src/FileProviderSample/Controllers/HomeController.cs?highlight=5,7,12&range=6-19)]

<span data-ttu-id="5a2c0-130">然后，在应用的 `Startup` 类中创建提供程序：</span><span class="sxs-lookup"><span data-stu-id="5a2c0-130">Then, create the provider in the app's `Startup` class:</span></span>

[!code-csharp[](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=35,40&range=1-43)]

<span data-ttu-id="5a2c0-131">在 Index.cshtml 视图中，循环访问提供的 `IDirectoryContents`：</span><span class="sxs-lookup"><span data-stu-id="5a2c0-131">In the *Index.cshtml* view, iterate through the `IDirectoryContents` provided:</span></span>

[!code-html[](file-providers/sample/src/FileProviderSample/Views/Home/Index.cshtml?highlight=2,7,9,11,15)]

<span data-ttu-id="5a2c0-132">结果：</span><span class="sxs-lookup"><span data-stu-id="5a2c0-132">The result:</span></span>

![列出物理文件和文件夹的文件提供程序示例应用程序](file-providers/_static/physical-directory-listing.png)

### <a name="embeddedfileprovider"></a><span data-ttu-id="5a2c0-134">EmbeddedFileProvider</span><span class="sxs-lookup"><span data-stu-id="5a2c0-134">EmbeddedFileProvider</span></span>

<span data-ttu-id="5a2c0-135">`EmbeddedFileProvider` 用于访问嵌入在程序集中的文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-135">The `EmbeddedFileProvider` is used to access files embedded in assemblies.</span></span> <span data-ttu-id="5a2c0-136">在 .NET Core 中，通过 .csproj 文件中的 `<EmbeddedResource>` 元素将各个文件嵌入程序集中：</span><span class="sxs-lookup"><span data-stu-id="5a2c0-136">In .NET Core, you embed files in an assembly with the `<EmbeddedResource>` element in the *.csproj* file:</span></span>

[!code-json[](file-providers/sample/src/FileProviderSample/FileProviderSample.csproj?range=13-18)]

<span data-ttu-id="5a2c0-137">在指定要嵌入到程序集中的文件时，你可以使用[通配模式](#globbing-patterns)。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-137">You can use [globbing patterns](#globbing-patterns) when specifying files to embed in the assembly.</span></span> <span data-ttu-id="5a2c0-138">这些模式可用于匹配一个或多个文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-138">These patterns can be used to match one or more files.</span></span>

> [!NOTE]
> <span data-ttu-id="5a2c0-139">实际上，用户不太可能会将项目中所有的 .js 文件都嵌入其程序集中；以上示例仅供演示。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-139">It's unlikely you would ever want to actually embed every .js file in your project in its assembly; the above sample is for demo purposes only.</span></span>

<span data-ttu-id="5a2c0-140">创建 `EmbeddedFileProvider` 时，将它要读取的程序集传递给其构造函数。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-140">When creating an `EmbeddedFileProvider`, pass the assembly it will read to its constructor.</span></span>

```csharp
var embeddedProvider = new EmbeddedFileProvider(Assembly.GetEntryAssembly());
```

<span data-ttu-id="5a2c0-141">以上片段演示如何创建可访问当前执行的程序集的 `EmbeddedFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-141">The snippet above demonstrates how to create an `EmbeddedFileProvider` with access to the currently executing assembly.</span></span>

<span data-ttu-id="5a2c0-142">更新要使用 `EmbeddedFileProvider` 的示例应用会导致以下输出：</span><span class="sxs-lookup"><span data-stu-id="5a2c0-142">Updating the sample app to use an `EmbeddedFileProvider` results in the following output:</span></span>

![列出嵌入的文件的文件提供程序示例应用程序](file-providers/_static/embedded-directory-listing.png)

> [!NOTE]
> <span data-ttu-id="5a2c0-144">嵌入的资源不会公开目录。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-144">Embedded resources don't expose directories.</span></span> <span data-ttu-id="5a2c0-145">而是使用 `.` 分隔符将指向资源的路径（通过其命名空间）嵌入其文件名中。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-145">Rather, the path to the resource (via its namespace) is embedded in its filename using `.` separators.</span></span>

> [!TIP]
> <span data-ttu-id="5a2c0-146">`EmbeddedFileProvider` 构造函数接受一个可选的 `baseNamespace` 参数。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-146">The `EmbeddedFileProvider` constructor accepts an optional `baseNamespace` parameter.</span></span> <span data-ttu-id="5a2c0-147">指定此操作会将到 `GetDirectoryContents` 的调用范围限制为提供的名称空间下的那些资源。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-147">Specifying this will scope calls to `GetDirectoryContents` to those resources under the provided namespace.</span></span>

### <a name="compositefileprovider"></a><span data-ttu-id="5a2c0-148">CompositeFileProvider</span><span class="sxs-lookup"><span data-stu-id="5a2c0-148">CompositeFileProvider</span></span>

<span data-ttu-id="5a2c0-149">`CompositeFileProvider` 合并 `IFileProvider` 实例，以便公开一个接口来处理多个提供程序中的文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-149">The `CompositeFileProvider` combines `IFileProvider` instances, exposing a single interface for working with files from multiple providers.</span></span> <span data-ttu-id="5a2c0-150">创建 `CompositeFileProvider` 时，将一个或多个 `IFileProvider` 实例传递给其构造函数：</span><span class="sxs-lookup"><span data-stu-id="5a2c0-150">When creating the `CompositeFileProvider`, you pass one or more `IFileProvider` instances to its constructor:</span></span>

[!code-csharp[](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=3&range=35-37)]

<span data-ttu-id="5a2c0-151">更新要使用 `CompositeFileProvider` 的示例应用（该应用包括之前配置的物理和嵌入式提供程序）会导致以下输出：</span><span class="sxs-lookup"><span data-stu-id="5a2c0-151">Updating the sample app to use a `CompositeFileProvider` that includes both the physical and embedded providers configured previously, results in the following output:</span></span>

![列出物理文件/文件夹和嵌入的文件的文件提供程序示例应用程序](file-providers/_static/composite-directory-listing.png)

## <a name="watching-for-changes"></a><span data-ttu-id="5a2c0-153">监视更改</span><span class="sxs-lookup"><span data-stu-id="5a2c0-153">Watching for changes</span></span>

<span data-ttu-id="5a2c0-154">`IFileProvider` `Watch` 方法提供一种方法来监视一个或多个文件或目录的更改。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-154">The `IFileProvider` `Watch` method provides a way to watch one or more files or directories for changes.</span></span> <span data-ttu-id="5a2c0-155">此方法接受一个路径字符串，该字符串可使用[通配模式](#globbing-patterns)来指定多个文件，并返回一个 `IChangeToken`。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-155">This method accepts a path string, which can use [globbing patterns](#globbing-patterns) to specify multiple files, and returns an `IChangeToken`.</span></span> <span data-ttu-id="5a2c0-156">此令牌公开可被检查的 `HasChanged` 属性，以及在检测到对指定路径字符串进行更改时调用的 `RegisterChangeCallback` 方法。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-156">This token exposes a `HasChanged` property that can be inspected, and a `RegisterChangeCallback` method that's called when changes are detected to the specified path string.</span></span> <span data-ttu-id="5a2c0-157">请注意，每个更改令牌仅调用其关联的回叫来响应单个更改。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-157">Note that each change token only calls its associated callback in response to a single change.</span></span> <span data-ttu-id="5a2c0-158">若要启用持续监视，可以使用如下所示的 `TaskCompletionSource`，或者重新创建 `IChangeToken` 实例来响应更改。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-158">To enable constant monitoring, you can use a `TaskCompletionSource` as shown below, or re-create `IChangeToken` instances in response to changes.</span></span>

<span data-ttu-id="5a2c0-159">在本文的示例中，控制台应用程序被配置为每当在修改文本文件时显示消息：</span><span class="sxs-lookup"><span data-stu-id="5a2c0-159">In this article's sample, a console application is configured to display a message whenever a text file is modified:</span></span>

[!code-csharp[](file-providers/sample/src/WatchConsole/Program.cs?name=snippet1&highlight=1-2,16,19-20)]

<span data-ttu-id="5a2c0-160">多次保存文件之后的结果：</span><span class="sxs-lookup"><span data-stu-id="5a2c0-160">The result, after saving the file several times:</span></span>

![执行 dotnet run 后的命令窗口（显示应用程序正在监视 quotes.txt 文件的更改，该文件已更改五次）。](file-providers/_static/watch-console.png)

> [!NOTE]
> <span data-ttu-id="5a2c0-162">某些文件系统（例如 Docker 容器和网络共享）可能无法可靠地发送更改通知。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-162">Some file systems, such as Docker containers and network shares, may not reliably send change notifications.</span></span> <span data-ttu-id="5a2c0-163">将 `DOTNET_USE_POLLINGFILEWATCHER` 环境变量设置为 `1` 或 `true`，以便每 4 秒对文件系统的更改进行轮询。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-163">Set the `DOTNET_USE_POLLINGFILEWATCHER` environment variable to `1` or `true` to poll the file system for changes every 4 seconds.</span></span>

## <a name="globbing-patterns"></a><span data-ttu-id="5a2c0-164">通配模式</span><span class="sxs-lookup"><span data-stu-id="5a2c0-164">Globbing patterns</span></span>

<span data-ttu-id="5a2c0-165">文件系统路径使用称作“通配模式”的通配符模式。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-165">File system paths use wildcard patterns called *globbing patterns*.</span></span> <span data-ttu-id="5a2c0-166">这些简单的模式可以用来指定文件组。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-166">These simple patterns can be used to specify groups of files.</span></span> <span data-ttu-id="5a2c0-167">这两个通配符为 `*` 和 `**`。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-167">The two wildcard characters are `*` and `**`.</span></span>

**`*`**

   <span data-ttu-id="5a2c0-168">匹配位于当前文件夹级别的任何内容、任何文件名或任何文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-168">Matches anything at the current folder level, or any filename, or any file extension.</span></span> <span data-ttu-id="5a2c0-169">匹配由文件路径中的 `/` 和 `.` 字符终止。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-169">Matches are terminated by `/` and `.` characters in the file path.</span></span>

<strong><code>**</code></strong>

   <span data-ttu-id="5a2c0-170">匹配多个目录级别的任何内容。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-170">Matches anything across multiple directory levels.</span></span> <span data-ttu-id="5a2c0-171">可用于以递归方式匹配目录层次结构中的许多文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-171">Can be used to recursively match many files within a directory hierarchy.</span></span>

### <a name="globbing-pattern-examples"></a><span data-ttu-id="5a2c0-172">通配模式示例</span><span class="sxs-lookup"><span data-stu-id="5a2c0-172">Globbing pattern examples</span></span>

**`directory/file.txt`**

   <span data-ttu-id="5a2c0-173">匹配特定目录中的特定文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-173">Matches a specific file in a specific directory.</span></span>

**<code>directory/*.txt</code>**

   <span data-ttu-id="5a2c0-174">匹配特定目录中带有 `.txt` 扩展名的所有文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-174">Matches all files with `.txt` extension in a specific directory.</span></span>

**`directory/*/bower.json`**

   <span data-ttu-id="5a2c0-175">匹配 `directory` 目录的下一级目录中的所有 `bower.json` 文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-175">Matches all `bower.json` files in directories exactly one level below the `directory` directory.</span></span>

**<code>directory/&#42;&#42;/&#42;.txt</code>**

   <span data-ttu-id="5a2c0-176">匹配在 `directory` 目录下带有 `.txt` 扩展名所有文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-176">Matches all files with `.txt` extension found anywhere under the `directory` directory.</span></span>

## <a name="file-provider-usage-in-aspnet-core"></a><span data-ttu-id="5a2c0-177">ASP.NET Core 中的文件提供程序使用情况</span><span class="sxs-lookup"><span data-stu-id="5a2c0-177">File Provider usage in ASP.NET Core</span></span>

<span data-ttu-id="5a2c0-178">ASP.NET Core 的多个部分使用文件提供程序。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-178">Several parts of ASP.NET Core utilize file providers.</span></span> <span data-ttu-id="5a2c0-179">`IHostingEnvironment` 将应用的内容根和 Web 根作为 `IFileProvider` 类型公开。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-179">`IHostingEnvironment` exposes the app's content root and web root as `IFileProvider` types.</span></span> <span data-ttu-id="5a2c0-180">静态文件中间件使用文件提供程序来查找静态文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-180">The static files middleware uses file providers to locate static files.</span></span> <span data-ttu-id="5a2c0-181">Razor 在查找视图时大量使用 `IFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-181">Razor makes heavy use of `IFileProvider` in locating views.</span></span> <span data-ttu-id="5a2c0-182">Dotnet 的发布功能使用文件提供程序和通配模式来指定应该发布哪些文件。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-182">Dotnet's publish functionality uses file providers and globbing patterns to specify which files should be published.</span></span>

## <a name="recommendations-for-use-in-apps"></a><span data-ttu-id="5a2c0-183">在应用中使用的建议</span><span class="sxs-lookup"><span data-stu-id="5a2c0-183">Recommendations for use in apps</span></span>

<span data-ttu-id="5a2c0-184">如果 ASP.NET Core 应用需要文件系统访问权限，那么你可以通过依赖关系注入请求 `IFileProvider` 的实例，然后使用其方法执行访问操作（如此示例中所示）。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-184">If your ASP.NET Core app requires file system access, you can request an instance of `IFileProvider` through dependency injection, and then use its methods to perform the access, as shown in this sample.</span></span> <span data-ttu-id="5a2c0-185">这样在应用启动时配置一次提供程序即可，而且可以减少应用实例化的实现类型数量。</span><span class="sxs-lookup"><span data-stu-id="5a2c0-185">This allows you to configure the provider once, when the app starts up, and reduces the number of implementation types your app instantiates.</span></span>
