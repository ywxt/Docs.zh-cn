---
title: "ASP.NET 核心中的文件提供程序"
author: ardalis
description: "了解如何 ASP.NET Core 提取通过文件提供程序使用的文件系统访问权限。"
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/file-providers
ms.openlocfilehash: db207f19b7ddc24dea36009138840be6efebdb84
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="file-providers-in-aspnet-core"></a><span data-ttu-id="c568e-103">ASP.NET 核心中的文件提供程序</span><span class="sxs-lookup"><span data-stu-id="c568e-103">File Providers in ASP.NET Core</span></span>

<span data-ttu-id="c568e-104">通过[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="c568e-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="c568e-105">ASP.NET 核心抽象化通过文件提供程序使用的文件系统访问权限。</span><span class="sxs-lookup"><span data-stu-id="c568e-105">ASP.NET Core abstracts file system access through the use of File Providers.</span></span>

<span data-ttu-id="c568e-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="c568e-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="file-provider-abstractions"></a><span data-ttu-id="c568e-107">文件提供程序抽象</span><span class="sxs-lookup"><span data-stu-id="c568e-107">File Provider abstractions</span></span>

<span data-ttu-id="c568e-108">文件提供程序通过文件系统是一种抽象。</span><span class="sxs-lookup"><span data-stu-id="c568e-108">File Providers are an abstraction over file systems.</span></span> <span data-ttu-id="c568e-109">主界面是`IFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="c568e-109">The main interface is `IFileProvider`.</span></span> <span data-ttu-id="c568e-110">`IFileProvider`公开一些方法以获取文件信息 (`IFileInfo`)，目录信息 (`IDirectoryContents`)，并设置更改通知 (使用`IChangeToken`)。</span><span class="sxs-lookup"><span data-stu-id="c568e-110">`IFileProvider` exposes methods to get file information (`IFileInfo`), directory information (`IDirectoryContents`), and to set up change notifications (using an `IChangeToken`).</span></span>

<span data-ttu-id="c568e-111">`IFileInfo`提供方法和属性有关单个文件或目录。</span><span class="sxs-lookup"><span data-stu-id="c568e-111">`IFileInfo` provides methods and properties about individual files or directories.</span></span> <span data-ttu-id="c568e-112">它具有两个布尔属性，`Exists`和`IsDirectory`，描述文件的属性以及`Name`， `Length` （以字节为单位），和`LastModified`日期。</span><span class="sxs-lookup"><span data-stu-id="c568e-112">It has two boolean properties, `Exists` and `IsDirectory`, as well as properties describing the file's `Name`, `Length` (in bytes), and `LastModified` date.</span></span> <span data-ttu-id="c568e-113">你可以从文件使用读取其`CreateReadStream`方法。</span><span class="sxs-lookup"><span data-stu-id="c568e-113">You can read from the file using its `CreateReadStream` method.</span></span>

## <a name="file-provider-implementations"></a><span data-ttu-id="c568e-114">文件提供程序实现</span><span class="sxs-lookup"><span data-stu-id="c568e-114">File Provider implementations</span></span>

<span data-ttu-id="c568e-115">三种实现`IFileProvider`可用： 物理、 嵌入和复合。</span><span class="sxs-lookup"><span data-stu-id="c568e-115">Three implementations of `IFileProvider` are available: Physical, Embedded, and Composite.</span></span> <span data-ttu-id="c568e-116">物理提供程序用于访问实际系统文件。</span><span class="sxs-lookup"><span data-stu-id="c568e-116">The physical provider is used to access the actual system's files.</span></span> <span data-ttu-id="c568e-117">嵌入的提供程序用于访问嵌入在程序集中的文件。</span><span class="sxs-lookup"><span data-stu-id="c568e-117">The embedded provider is used to access files embedded in assemblies.</span></span> <span data-ttu-id="c568e-118">复合的提供程序用于提供一个或多个其他提供商组合对文件和目录的访问权限。</span><span class="sxs-lookup"><span data-stu-id="c568e-118">The composite provider is used to provide combined access to files and directories from one or more other providers.</span></span>

### <a name="physicalfileprovider"></a><span data-ttu-id="c568e-119">PhysicalFileProvider</span><span class="sxs-lookup"><span data-stu-id="c568e-119">PhysicalFileProvider</span></span>

<span data-ttu-id="c568e-120">`PhysicalFileProvider`提供对物理文件系统的访问。</span><span class="sxs-lookup"><span data-stu-id="c568e-120">The `PhysicalFileProvider` provides access to the physical file system.</span></span> <span data-ttu-id="c568e-121">它所包装`System.IO.File`类型 （用于物理提供程序），作用域到一个目录及其子级的所有路径。</span><span class="sxs-lookup"><span data-stu-id="c568e-121">It wraps the `System.IO.File` type (for the physical provider), scoping all paths to a directory and its children.</span></span> <span data-ttu-id="c568e-122">此作用域限制对特定目录及其子级，防止对在此边界之外的文件系统的访问的访问。</span><span class="sxs-lookup"><span data-stu-id="c568e-122">This scoping limits access to a certain directory and its children, preventing access to the file system outside of this boundary.</span></span> <span data-ttu-id="c568e-123">时实例化此提供程序，你必须向它提供可用作对此提供程序所做的所有请求的基路径 （限制外部此路径的访问） 的目录路径。</span><span class="sxs-lookup"><span data-stu-id="c568e-123">When instantiating this provider, you must provide it with a directory path, which serves as the base path for all requests made to this provider (and which restricts access outside of this path).</span></span> <span data-ttu-id="c568e-124">在 ASP.NET Core 应用程序，你可以实例化`PhysicalFileProvider`直接，提供程序，也可以请求`IFileProvider`中的控制器或服务的构造函数通过[依赖关系注入](dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="c568e-124">In an ASP.NET Core app, you can instantiate a `PhysicalFileProvider` provider directly, or you can request an `IFileProvider` in a Controller or service's constructor through [dependency injection](dependency-injection.md).</span></span> <span data-ttu-id="c568e-125">后一种方法通常会产生更加灵活和可测试解决方案。</span><span class="sxs-lookup"><span data-stu-id="c568e-125">The latter approach will typically yield a more flexible and testable solution.</span></span>

<span data-ttu-id="c568e-126">下面的示例演示如何创建`PhysicalFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="c568e-126">The sample below shows how to create a `PhysicalFileProvider`.</span></span>


```csharp
IFileProvider provider = new PhysicalFileProvider(applicationRoot);
IDirectoryContents contents = provider.GetDirectoryContents(""); // the applicationRoot contents
IFileInfo fileInfo = provider.GetFileInfo("wwwroot/js/site.js"); // a file under applicationRoot
```

<span data-ttu-id="c568e-127">可以循环访问其目录内容，也可以通过提供子路径获取特定文件的信息。</span><span class="sxs-lookup"><span data-stu-id="c568e-127">You can iterate through its directory contents or get a specific file's information by providing a subpath.</span></span>

<span data-ttu-id="c568e-128">若要从控制器请求提供程序，指定控制器的构造函数中，并将其分配给本地字段。</span><span class="sxs-lookup"><span data-stu-id="c568e-128">To request a provider from a controller, specify it in the controller's constructor and assign it to a local field.</span></span> <span data-ttu-id="c568e-129">使用你的操作方法中的本地实例：</span><span class="sxs-lookup"><span data-stu-id="c568e-129">Use the local instance from your action methods:</span></span>

[!code-csharp[Main](file-providers/sample/src/FileProviderSample/Controllers/HomeController.cs?highlight=5,7,12&range=6-19)]

<span data-ttu-id="c568e-130">然后，在应用程序的创建提供程序`Startup`类：</span><span class="sxs-lookup"><span data-stu-id="c568e-130">Then, create the provider in the app's `Startup` class:</span></span>

[!code-csharp[Main](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=35,40&range=1-43)]

<span data-ttu-id="c568e-131">在*Index.cshtml*视图中，循环访问`IDirectoryContents`提供：</span><span class="sxs-lookup"><span data-stu-id="c568e-131">In the *Index.cshtml* view, iterate through the `IDirectoryContents` provided:</span></span>

[!code-html[Main](file-providers/sample/src/FileProviderSample/Views/Home/Index.cshtml?highlight=2,7,9,11,15)]

<span data-ttu-id="c568e-132">结果：</span><span class="sxs-lookup"><span data-stu-id="c568e-132">The result:</span></span>

![文件提供程序示例应用程序列表物理文件和文件夹](file-providers/_static/physical-directory-listing.png)

### <a name="embeddedfileprovider"></a><span data-ttu-id="c568e-134">EmbeddedFileProvider</span><span class="sxs-lookup"><span data-stu-id="c568e-134">EmbeddedFileProvider</span></span>

<span data-ttu-id="c568e-135">`EmbeddedFileProvider`用于访问嵌入在程序集中的文件。</span><span class="sxs-lookup"><span data-stu-id="c568e-135">The `EmbeddedFileProvider` is used to access files embedded in assemblies.</span></span> <span data-ttu-id="c568e-136">在.NET 核心中要将文件嵌入程序集中`<EmbeddedResource>`中的元素*.csproj*文件：</span><span class="sxs-lookup"><span data-stu-id="c568e-136">In .NET Core, you embed files in an assembly with the `<EmbeddedResource>` element in the *.csproj* file:</span></span>

[!code-json[Main](file-providers/sample/src/FileProviderSample/FileProviderSample.csproj?range=13-18)]

<span data-ttu-id="c568e-137">你可以使用[组合模式](#globbing-patterns)时指定要嵌入到程序集中的文件。</span><span class="sxs-lookup"><span data-stu-id="c568e-137">You can use [globbing patterns](#globbing-patterns) when specifying files to embed in the assembly.</span></span> <span data-ttu-id="c568e-138">这些模式可用于以匹配一个或多个文件。</span><span class="sxs-lookup"><span data-stu-id="c568e-138">These patterns can be used to match one or more files.</span></span>

> [!NOTE]
> <span data-ttu-id="c568e-139">不太可能会想要实际上将每个.js 文件嵌入在其程序集; 中的项目上面的示例是仅供演示。</span><span class="sxs-lookup"><span data-stu-id="c568e-139">It's unlikely you would ever want to actually embed every .js file in your project in its assembly; the above sample is for demo purposes only.</span></span>

<span data-ttu-id="c568e-140">在创建时`EmbeddedFileProvider`，传递给其构造函数将读取它的程序集。</span><span class="sxs-lookup"><span data-stu-id="c568e-140">When creating an `EmbeddedFileProvider`, pass the assembly it will read to its constructor.</span></span>

```csharp
var embeddedProvider = new EmbeddedFileProvider(Assembly.GetEntryAssembly());
```

<span data-ttu-id="c568e-141">上述代码段演示如何创建`EmbeddedFileProvider`有权访问当前正在执行的程序集。</span><span class="sxs-lookup"><span data-stu-id="c568e-141">The snippet above demonstrates how to create an `EmbeddedFileProvider` with access to the currently executing assembly.</span></span>

<span data-ttu-id="c568e-142">更新示例应用程序以使用`EmbeddedFileProvider`导致生成以下输出：</span><span class="sxs-lookup"><span data-stu-id="c568e-142">Updating the sample app to use an `EmbeddedFileProvider` results in the following output:</span></span>

![列出嵌入的文件的文件提供程序示例应用程序](file-providers/_static/embedded-directory-listing.png)

> [!NOTE]
> <span data-ttu-id="c568e-144">嵌入的资源不会公开目录。</span><span class="sxs-lookup"><span data-stu-id="c568e-144">Embedded resources do not expose directories.</span></span> <span data-ttu-id="c568e-145">相反，（通过其命名空间） 的资源路径嵌入在其文件名使用`.`分隔符。</span><span class="sxs-lookup"><span data-stu-id="c568e-145">Rather, the path to the resource (via its namespace) is embedded in its filename using `.` separators.</span></span>

> [!TIP]
> <span data-ttu-id="c568e-146">`EmbeddedFileProvider`构造函数接受一个可选`baseNamespace`参数。</span><span class="sxs-lookup"><span data-stu-id="c568e-146">The `EmbeddedFileProvider` constructor accepts an optional `baseNamespace` parameter.</span></span> <span data-ttu-id="c568e-147">指定此将作用域调用`GetDirectoryContents`对这些资源在提供的命名空间。</span><span class="sxs-lookup"><span data-stu-id="c568e-147">Specifying this will scope calls to `GetDirectoryContents` to those resources under the provided namespace.</span></span>

### <a name="compositefileprovider"></a><span data-ttu-id="c568e-148">CompositeFileProvider</span><span class="sxs-lookup"><span data-stu-id="c568e-148">CompositeFileProvider</span></span>

<span data-ttu-id="c568e-149">`CompositeFileProvider`将合并`IFileProvider`情况下，公开一个接口用于处理从多个提供程序的文件。</span><span class="sxs-lookup"><span data-stu-id="c568e-149">The `CompositeFileProvider` combines `IFileProvider` instances, exposing a single interface for working with files from multiple providers.</span></span> <span data-ttu-id="c568e-150">在创建时`CompositeFileProvider`，传递一个或多个`IFileProvider`给其构造函数的实例：</span><span class="sxs-lookup"><span data-stu-id="c568e-150">When creating the `CompositeFileProvider`, you pass one or more `IFileProvider` instances to its constructor:</span></span>

[!code-csharp[Main](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=3&range=35-37)]

<span data-ttu-id="c568e-151">更新示例应用程序以使用`CompositeFileProvider`包括这两个物理和嵌入配置提供程序之前，请在下面的输出结果：</span><span class="sxs-lookup"><span data-stu-id="c568e-151">Updating the sample app to use a `CompositeFileProvider` that includes both the physical and embedded providers configured previously, results in the following output:</span></span>

![列出的物理文件和文件夹以及嵌入的文件的文件提供程序示例应用程序](file-providers/_static/composite-directory-listing.png)

## <a name="watching-for-changes"></a><span data-ttu-id="c568e-153">监视的更改</span><span class="sxs-lookup"><span data-stu-id="c568e-153">Watching for changes</span></span>

<span data-ttu-id="c568e-154">`IFileProvider` `Watch`方法使您能够监视一个或多个文件或目录的更改。</span><span class="sxs-lookup"><span data-stu-id="c568e-154">The `IFileProvider` `Watch` method provides a way to watch one or more files or directories for changes.</span></span> <span data-ttu-id="c568e-155">此方法接受路径字符串，可以使用该对话框[组合模式](#globbing-patterns)来指定多个文件，并返回`IChangeToken`。</span><span class="sxs-lookup"><span data-stu-id="c568e-155">This method accepts a path string, which can use [globbing patterns](#globbing-patterns) to specify multiple files, and returns an `IChangeToken`.</span></span> <span data-ttu-id="c568e-156">此令牌公开`HasChanged`属性，可以检查和`RegisterChangeCallback`为指定的路径字符串检测到更改时调用的方法。</span><span class="sxs-lookup"><span data-stu-id="c568e-156">This token exposes a `HasChanged` property that can be inspected, and a `RegisterChangeCallback` method that is called when changes are detected to the specified path string.</span></span> <span data-ttu-id="c568e-157">请注意每个更改令牌仅在响应的单个更改调用其关联的回调。</span><span class="sxs-lookup"><span data-stu-id="c568e-157">Note that each change token only calls its associated callback in response to a single change.</span></span> <span data-ttu-id="c568e-158">若要启用持续的监视，你可以使用`TaskCompletionSource`如下所示，或重新创建`IChangeToken`实例以响应更改。</span><span class="sxs-lookup"><span data-stu-id="c568e-158">To enable constant monitoring, you can use a `TaskCompletionSource` as shown below, or re-create `IChangeToken` instances in response to changes.</span></span>

<span data-ttu-id="c568e-159">在本文中的示例中，一个控制台应用程序配置为每当修改文本文件时显示一条消息：</span><span class="sxs-lookup"><span data-stu-id="c568e-159">In this article's sample, a console application is configured to display a message whenever a text file is modified:</span></span>

[!code-csharp[Main](file-providers/sample/src/WatchConsole/Program.cs?name=snippet1&highlight=1-2,16,19-20)]

<span data-ttu-id="c568e-160">保存此文件若干次后的结果：</span><span class="sxs-lookup"><span data-stu-id="c568e-160">The result, after saving the file several times:</span></span>

![命令窗口后执行 dotnet 运行显示监视 quotes.txt 文件的更改的应用程序和文件已更改五次。](file-providers/_static/watch-console.png)

> [!NOTE]
> <span data-ttu-id="c568e-162">某些文件系统，例如 Docker 容器和网络共享，可能会不可靠地发送更改通知。</span><span class="sxs-lookup"><span data-stu-id="c568e-162">Some file systems, such as Docker containers and network shares, may not reliably send change notifications.</span></span> <span data-ttu-id="c568e-163">设置`DOTNET_USE_POLLINGFILEWATCHER`环境变量`1`或`true`轮询每 4 秒的文件系统更改。</span><span class="sxs-lookup"><span data-stu-id="c568e-163">Set the `DOTNET_USE_POLLINGFILEWATCHER` environment variable to `1` or `true` to poll the file system for changes every 4 seconds.</span></span>

## <a name="globbing-patterns"></a><span data-ttu-id="c568e-164">组合模式</span><span class="sxs-lookup"><span data-stu-id="c568e-164">Globbing patterns</span></span>

<span data-ttu-id="c568e-165">文件系统路径中使用通配符模式调用*组合模式*。</span><span class="sxs-lookup"><span data-stu-id="c568e-165">File system paths use wildcard patterns called *globbing patterns*.</span></span> <span data-ttu-id="c568e-166">这些简单的模式可以用于指定的文件组。</span><span class="sxs-lookup"><span data-stu-id="c568e-166">These simple patterns can be used to specify groups of files.</span></span> <span data-ttu-id="c568e-167">两个通配符字符都是`*`和`**`。</span><span class="sxs-lookup"><span data-stu-id="c568e-167">The two wildcard characters are `*` and `**`.</span></span>

**`*`**

   <span data-ttu-id="c568e-168">匹配任何内容在当前文件夹级别，或任何文件名或任何文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="c568e-168">Matches anything at the current folder level, or any filename, or any file extension.</span></span> <span data-ttu-id="c568e-169">匹配项即可终止`/`和`.`文件路径中的字符。</span><span class="sxs-lookup"><span data-stu-id="c568e-169">Matches are terminated by `/` and `.` characters in the file path.</span></span>

<strong><code>**</code></strong>

   <span data-ttu-id="c568e-170">跨多个目录级别匹配任何内容。</span><span class="sxs-lookup"><span data-stu-id="c568e-170">Matches anything across multiple directory levels.</span></span> <span data-ttu-id="c568e-171">可用于以递归方式与在目录层次结构中的许多文件匹配。</span><span class="sxs-lookup"><span data-stu-id="c568e-171">Can be used to recursively match many files within a directory hierarchy.</span></span>

### <a name="globbing-pattern-examples"></a><span data-ttu-id="c568e-172">组合模式示例</span><span class="sxs-lookup"><span data-stu-id="c568e-172">Globbing pattern examples</span></span>

**`directory/file.txt`**

   <span data-ttu-id="c568e-173">匹配特定的目录中的特定文件。</span><span class="sxs-lookup"><span data-stu-id="c568e-173">Matches a specific file in a specific directory.</span></span>

**<code>directory/*.txt</code>**

   <span data-ttu-id="c568e-174">匹配的所有文件的`.txt`特定目录中的扩展。</span><span class="sxs-lookup"><span data-stu-id="c568e-174">Matches all files with `.txt` extension in a specific directory.</span></span>

**`directory/*/bower.json`**

   <span data-ttu-id="c568e-175">匹配所有`bower.json`目录恰好一个级别中的文件`directory`目录。</span><span class="sxs-lookup"><span data-stu-id="c568e-175">Matches all `bower.json` files in directories exactly one level below the `directory` directory.</span></span>

**<code>directory/&#42;&#42;/&#42;.txt</code>**

   <span data-ttu-id="c568e-176">匹配的所有文件的`.txt`下的任何位置找到扩展`directory`目录。</span><span class="sxs-lookup"><span data-stu-id="c568e-176">Matches all files with `.txt` extension found anywhere under the `directory` directory.</span></span>

## <a name="file-provider-usage-in-aspnet-core"></a><span data-ttu-id="c568e-177">在 ASP.NET Core 文件提供程序使用情况</span><span class="sxs-lookup"><span data-stu-id="c568e-177">File Provider usage in ASP.NET Core</span></span>

<span data-ttu-id="c568e-178">ASP.NET 核心的多个部分利用文件提供程序。</span><span class="sxs-lookup"><span data-stu-id="c568e-178">Several parts of ASP.NET Core utilize file providers.</span></span> <span data-ttu-id="c568e-179">`IHostingEnvironment`公开应用程序的内容的根和 web 根与`IFileProvider`类型。</span><span class="sxs-lookup"><span data-stu-id="c568e-179">`IHostingEnvironment` exposes the app's content root and web root as `IFileProvider` types.</span></span> <span data-ttu-id="c568e-180">静态文件中间件使用文件提供程序查找静态文件。</span><span class="sxs-lookup"><span data-stu-id="c568e-180">The static files middleware uses file providers to locate static files.</span></span> <span data-ttu-id="c568e-181">Razor 使大量使用`IFileProvider`定位视图。</span><span class="sxs-lookup"><span data-stu-id="c568e-181">Razor makes heavy use of `IFileProvider` in locating views.</span></span> <span data-ttu-id="c568e-182">Dotnet 的发布功能使用文件提供程序和组合模式，以指定应发布哪些文件。</span><span class="sxs-lookup"><span data-stu-id="c568e-182">Dotnet's publish functionality uses file providers and globbing patterns to specify which files should be published.</span></span>

## <a name="recommendations-for-use-in-apps"></a><span data-ttu-id="c568e-183">用在应用程序的建议</span><span class="sxs-lookup"><span data-stu-id="c568e-183">Recommendations for use in apps</span></span>

<span data-ttu-id="c568e-184">ASP.NET Core 应用程序需要文件系统访问权限，你可以请求的实例`IFileProvider`通过依赖关系注入，然后使用其方法来执行权限，此示例中所示。</span><span class="sxs-lookup"><span data-stu-id="c568e-184">If your ASP.NET Core app requires file system access, you can request an instance of `IFileProvider` through dependency injection, and then use its methods to perform the access, as shown in this sample.</span></span> <span data-ttu-id="c568e-185">这可以一次，配置提供程序，当应用程序启动，并减少你的应用程序实例化的实现类型的数目。</span><span class="sxs-lookup"><span data-stu-id="c568e-185">This allows you to configure the provider once, when the app starts up, and reduces the number of implementation types your app instantiates.</span></span>
