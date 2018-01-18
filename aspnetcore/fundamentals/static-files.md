---
title: "使用 ASP.NET Core 中的静态文件"
author: rick-anderson
description: "了解如何处理和保护静态文件，并配置承载 ASP.NET 核心 web 应用中的中间件行为的静态文件。"
keywords: "ASP.NET 核心，静态文件、 静态资产，HTML、 CSS、 JavaScript"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/18/2018
ms.devlang: csharp
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/static-files
ms.openlocfilehash: 912923860939a1d1dd91ccc79862e23f9095d161
ms.sourcegitcommit: a3e88639a6bcf8fb4d634036dac93130c464a097
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="work-with-static-files-in-aspnet-core"></a><span data-ttu-id="86624-104">使用 ASP.NET Core 中的静态文件</span><span class="sxs-lookup"><span data-stu-id="86624-104">Work with static files in ASP.NET Core</span></span>

<span data-ttu-id="86624-105">通过[Rick Anderson](https://twitter.com/RickAndMSFT)和[Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="86624-105">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="86624-106">静态文件，如 HTML、 CSS、 映像和 JavaScript，作为的资产直接向客户端提供 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="86624-106">Static files, such as HTML, CSS, images, and JavaScript, are assets an ASP.NET Core app serves directly to clients.</span></span> <span data-ttu-id="86624-107">不需要若要启用对这些文件提供一些配置。</span><span class="sxs-lookup"><span data-stu-id="86624-107">Some configuration is required to enable to serving of these files.</span></span>

<span data-ttu-id="86624-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/static-files/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="86624-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/static-files/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="serve-static-files"></a><span data-ttu-id="86624-109">为静态文件服务</span><span class="sxs-lookup"><span data-stu-id="86624-109">Serve static files</span></span>

<span data-ttu-id="86624-110">静态文件存储在你的项目的 web 根目录。</span><span class="sxs-lookup"><span data-stu-id="86624-110">Static files are stored within your project's web root directory.</span></span> <span data-ttu-id="86624-111">默认目录是 *\<content_root > / wwwroot*，但它可以通过更改[UseWebRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usewebroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseWebRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_)方法。</span><span class="sxs-lookup"><span data-stu-id="86624-111">The default directory is *\<content_root>/wwwroot*, but it can be changed via the [UseWebRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usewebroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseWebRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) method.</span></span> <span data-ttu-id="86624-112">请参阅[内容根](xref:fundamentals/index#content-root)和[Web 根](xref:fundamentals/index#web-root)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="86624-112">See [Content root](xref:fundamentals/index#content-root) and [Web root](xref:fundamentals/index#web-root) for more information.</span></span>

<span data-ttu-id="86624-113">应用程序的 web 主机必须让知道的内容的根目录。</span><span class="sxs-lookup"><span data-stu-id="86624-113">The app's web host must be made aware of the content root directory.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="86624-114">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="86624-114">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="86624-115">`WebHost.CreateDefaultBuilder`方法设置的内容的根到当前目录：</span><span class="sxs-lookup"><span data-stu-id="86624-115">The `WebHost.CreateDefaultBuilder` method sets the content root to the current directory:</span></span>

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=9)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="86624-116">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="86624-116">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="86624-117">设置为当前目录的内容的根，通过调用[UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseContentRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_)内`Program.Main`:</span><span class="sxs-lookup"><span data-stu-id="86624-117">Set the content root to the current directory by invoking [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseContentRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) inside of `Program.Main`:</span></span>

[!code-csharp[](static-files/samples/1x/Program.cs?name=snippet_ProgramClass&highlight=7)]

---

<span data-ttu-id="86624-118">静态文件都可以访问通过相对于 web 根的路径。</span><span class="sxs-lookup"><span data-stu-id="86624-118">Static files are accessible via a path relative to the web root.</span></span> <span data-ttu-id="86624-119">例如， **Web 应用程序**项目模板包含多个文件夹内的*wwwroot*文件夹：</span><span class="sxs-lookup"><span data-stu-id="86624-119">For example, the **Web Application** project template contains several folders within the *wwwroot* folder:</span></span>

* <span data-ttu-id="86624-120">**wwwroot**</span><span class="sxs-lookup"><span data-stu-id="86624-120">**wwwroot**</span></span>
  * <span data-ttu-id="86624-121">**css**</span><span class="sxs-lookup"><span data-stu-id="86624-121">**css**</span></span>
  * <span data-ttu-id="86624-122">**images**</span><span class="sxs-lookup"><span data-stu-id="86624-122">**images**</span></span>
  * <span data-ttu-id="86624-123">**js**</span><span class="sxs-lookup"><span data-stu-id="86624-123">**js**</span></span>

<span data-ttu-id="86624-124">要访问中的文件的 URI 格式*映像*子文件夹是*http://\<server_address > /images/\<image_file_name >*。</span><span class="sxs-lookup"><span data-stu-id="86624-124">The URI format to access a file in the *images* subfolder is *http://\<server_address>/images/\<image_file_name>*.</span></span> <span data-ttu-id="86624-125">例如， *http://localhost:9189/images/banner3.svg*。</span><span class="sxs-lookup"><span data-stu-id="86624-125">For example, *http://localhost:9189/images/banner3.svg*.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="86624-126">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="86624-126">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="86624-127">如果面向.NET Framework，添加[Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/)包到你的项目。</span><span class="sxs-lookup"><span data-stu-id="86624-127">If targeting .NET Framework, add the [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) package to your project.</span></span> <span data-ttu-id="86624-128">如果面向的.NET 核心[Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage)包括此包。</span><span class="sxs-lookup"><span data-stu-id="86624-128">If targeting .NET Core, the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) includes this package.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="86624-129">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="86624-129">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="86624-130">添加[Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/)包到你的项目。</span><span class="sxs-lookup"><span data-stu-id="86624-130">Add the [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) package to your project.</span></span>

---

<span data-ttu-id="86624-131">配置[中间件](xref:fundamentals/middleware)这样的静态文件提供服务。</span><span class="sxs-lookup"><span data-stu-id="86624-131">Configure the [middleware](xref:fundamentals/middleware) which enables the serving of static files.</span></span>

### <a name="serve-files-inside-of-web-root"></a><span data-ttu-id="86624-132">为在 web 根目录内的文件服务</span><span class="sxs-lookup"><span data-stu-id="86624-132">Serve files inside of web root</span></span>

<span data-ttu-id="86624-133">调用[UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_)方法内的`Startup.Configure`:</span><span class="sxs-lookup"><span data-stu-id="86624-133">Invoke the [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) method within `Startup.Configure`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupStaticFiles.cs?name=snippet_ConfigureMethod&highlight=3)]

<span data-ttu-id="86624-134">无参数`UseStaticFiles`方法重载将标记为 servable web 根目录中的文件。</span><span class="sxs-lookup"><span data-stu-id="86624-134">The parameterless `UseStaticFiles` method overload marks the files in web root as servable.</span></span> <span data-ttu-id="86624-135">以下标记引用*wwwroot/images/banner1.svg*:</span><span class="sxs-lookup"><span data-stu-id="86624-135">The following markup references *wwwroot/images/banner1.svg*:</span></span>

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_wwwroot)]

### <a name="serve-files-outside-of-web-root"></a><span data-ttu-id="86624-136">为在 web 根目录之外的文件服务</span><span class="sxs-lookup"><span data-stu-id="86624-136">Serve files outside of web root</span></span>

<span data-ttu-id="86624-137">请考虑在 web 根目录之外的静态文件提供驻留在其中的目录层次结构：</span><span class="sxs-lookup"><span data-stu-id="86624-137">Consider a directory hierarchy in which the static files to be served reside outside of the web root:</span></span>

* <span data-ttu-id="86624-138">**wwwroot**</span><span class="sxs-lookup"><span data-stu-id="86624-138">**wwwroot**</span></span>
  * <span data-ttu-id="86624-139">**css**</span><span class="sxs-lookup"><span data-stu-id="86624-139">**css**</span></span>
  * <span data-ttu-id="86624-140">**images**</span><span class="sxs-lookup"><span data-stu-id="86624-140">**images**</span></span>
  * <span data-ttu-id="86624-141">**js**</span><span class="sxs-lookup"><span data-stu-id="86624-141">**js**</span></span>
* <span data-ttu-id="86624-142">**MyStaticFiles**</span><span class="sxs-lookup"><span data-stu-id="86624-142">**MyStaticFiles**</span></span>
  * <span data-ttu-id="86624-143">**images**</span><span class="sxs-lookup"><span data-stu-id="86624-143">**images**</span></span>
      * <span data-ttu-id="86624-144">*banner1.svg*</span><span class="sxs-lookup"><span data-stu-id="86624-144">*banner1.svg*</span></span>

<span data-ttu-id="86624-145">请求可以访问*banner1.svg*文件通过配置静态文件中间件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="86624-145">A request can access the *banner1.svg* file by configuring the static file middleware as follows:</span></span>

[!code-csharp[](static-files/samples/1x/StartupTwoStaticFiles.cs?name=snippet_ConfigureMethod&highlight=5-10)]

<span data-ttu-id="86624-146">在前面的代码中， *MyStaticFiles*通过公开公开目录层次结构*StaticFiles* URI 段。</span><span class="sxs-lookup"><span data-stu-id="86624-146">In the preceding code, the *MyStaticFiles* directory hierarchy is exposed publicly via the *StaticFiles* URI segment.</span></span> <span data-ttu-id="86624-147">对请求*http://\<server_address > /StaticFiles/images/banner1.svg*提供*banner1.svg*文件。</span><span class="sxs-lookup"><span data-stu-id="86624-147">A request to *http://\<server_address>/StaticFiles/images/banner1.svg* serves the *banner1.svg* file.</span></span>

<span data-ttu-id="86624-148">以下标记引用*MyStaticFiles/images/banner1.svg*:</span><span class="sxs-lookup"><span data-stu-id="86624-148">The following markup references *MyStaticFiles/images/banner1.svg*:</span></span>

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_outside)]

### <a name="set-http-response-headers"></a><span data-ttu-id="86624-149">设置 HTTP 响应标头</span><span class="sxs-lookup"><span data-stu-id="86624-149">Set HTTP response headers</span></span>

<span data-ttu-id="86624-150">A [StaticFileOptions](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions)对象可以用于设置 HTTP 响应标头。</span><span class="sxs-lookup"><span data-stu-id="86624-150">A [StaticFileOptions](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions) object can be used to set HTTP response headers.</span></span> <span data-ttu-id="86624-151">除了配置从 web 根的静态文件服务，以下代码将设置`Cache-Control`标头：</span><span class="sxs-lookup"><span data-stu-id="86624-151">In addition to configuring static file serving from the web root, the following code sets the `Cache-Control` header:</span></span>

[!code-csharp[](static-files/samples/1x/StartupAddHeader.cs?name=snippet_ConfigureMethod)]

<span data-ttu-id="86624-152">[HeaderDictionaryExtensions.Append](/dotnet/api/microsoft.aspnetcore.http.headerdictionaryextensions.append)方法中存在[Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/)包。</span><span class="sxs-lookup"><span data-stu-id="86624-152">The [HeaderDictionaryExtensions.Append](/dotnet/api/microsoft.aspnetcore.http.headerdictionaryextensions.append) method exists in the [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) package.</span></span>

<span data-ttu-id="86624-153">文件进行了公开可缓存 10 分钟 （600 秒）：</span><span class="sxs-lookup"><span data-stu-id="86624-153">The files have been made publicly cacheable for 10 minutes (600 seconds):</span></span>

![已添加显示的缓存控制标头的响应标头](static-files/_static/add-header.png)

## <a name="static-file-authorization"></a><span data-ttu-id="86624-155">静态文件授权</span><span class="sxs-lookup"><span data-stu-id="86624-155">Static file authorization</span></span>

<span data-ttu-id="86624-156">静态文件中间件不提供授权检查。</span><span class="sxs-lookup"><span data-stu-id="86624-156">The static file middleware doesn't provide authorization checks.</span></span> <span data-ttu-id="86624-157">由它提供任何文件包括正在*wwwroot*，是可公开访问。</span><span class="sxs-lookup"><span data-stu-id="86624-157">Any files served by it, including those under *wwwroot*, are publicly accessible.</span></span> <span data-ttu-id="86624-158">若要为文件服务基于授权：</span><span class="sxs-lookup"><span data-stu-id="86624-158">To serve files based on authorization:</span></span>

* <span data-ttu-id="86624-159">将其外部存储*wwwroot*和访问静态文件中间件任何目录**和**</span><span class="sxs-lookup"><span data-stu-id="86624-159">Store them outside of *wwwroot* and any directory accessible to the static file middleware **and**</span></span>
* <span data-ttu-id="86624-160">通过向其应用授权的操作方法提供它们。</span><span class="sxs-lookup"><span data-stu-id="86624-160">Serve them via an action method to which authorization is applied.</span></span> <span data-ttu-id="86624-161">返回[FileResult](/dotnet/api/microsoft.aspnetcore.mvc.fileresult)对象：</span><span class="sxs-lookup"><span data-stu-id="86624-161">Return a [FileResult](/dotnet/api/microsoft.aspnetcore.mvc.fileresult) object:</span></span>

[!code-csharp[](static-files/samples/1x/Controllers/HomeController.cs?name=snippet_BannerImageAction)]

## <a name="enable-directory-browsing"></a><span data-ttu-id="86624-162">启用目录浏览</span><span class="sxs-lookup"><span data-stu-id="86624-162">Enable directory browsing</span></span>

<span data-ttu-id="86624-163">目录浏览使你的 web 应用的用户看到的目录列表，以及在指定的目录内文件。</span><span class="sxs-lookup"><span data-stu-id="86624-163">Directory browsing allows users of your web app to see a directory listing and files within a specified directory.</span></span> <span data-ttu-id="86624-164">默认情况下，出于安全原因禁用目录浏览 (请参阅[注意事项](#considerations))。</span><span class="sxs-lookup"><span data-stu-id="86624-164">Directory browsing is disabled by default for security reasons (see [Considerations](#considerations)).</span></span> <span data-ttu-id="86624-165">启用目录浏览通过调用[UseDirectoryBrowser](/dotnet/api/microsoft.aspnetcore.builder.directorybrowserextensions.usedirectorybrowser#Microsoft_AspNetCore_Builder_DirectoryBrowserExtensions_UseDirectoryBrowser_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_DirectoryBrowserOptions_)中的方法`Startup.Configure`:</span><span class="sxs-lookup"><span data-stu-id="86624-165">Enable directory browsing by invoking the [UseDirectoryBrowser](/dotnet/api/microsoft.aspnetcore.builder.directorybrowserextensions.usedirectorybrowser#Microsoft_AspNetCore_Builder_DirectoryBrowserExtensions_UseDirectoryBrowser_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_DirectoryBrowserOptions_) method in `Startup.Configure`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=12-17)]

<span data-ttu-id="86624-166">添加所需的服务通过调用[AddDirectoryBrowser](/dotnet/api/microsoft.extensions.dependencyinjection.directorybrowserserviceextensions.adddirectorybrowser#Microsoft_Extensions_DependencyInjection_DirectoryBrowserServiceExtensions_AddDirectoryBrowser_Microsoft_Extensions_DependencyInjection_IServiceCollection_)方法从`Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="86624-166">Add required services by invoking the [AddDirectoryBrowser](/dotnet/api/microsoft.extensions.dependencyinjection.directorybrowserserviceextensions.adddirectorybrowser#Microsoft_Extensions_DependencyInjection_DirectoryBrowserServiceExtensions_AddDirectoryBrowser_Microsoft_Extensions_DependencyInjection_IServiceCollection_) method from `Startup.ConfigureServices`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureServicesMethod&highlight=3)]

<span data-ttu-id="86624-167">前面的代码中允许目录浏览的*wwwroot/images*文件夹使用 URL *http://\<server_address > / MyImages*，以链接到每个文件和文件夹：</span><span class="sxs-lookup"><span data-stu-id="86624-167">The preceding code allows directory browsing of the *wwwroot/images* folder using the URL *http://\<server_address>/MyImages*, with links to each file and folder:</span></span>

![目录浏览](static-files/_static/dir-browse.png)

<span data-ttu-id="86624-169">请参阅[注意事项](#considerations)上启用浏览时安全风险。</span><span class="sxs-lookup"><span data-stu-id="86624-169">See [Considerations](#considerations) on the security risks when enabling browsing.</span></span>

<span data-ttu-id="86624-170">请注意两个`UseStaticFiles`调用在下面的示例。</span><span class="sxs-lookup"><span data-stu-id="86624-170">Note the two `UseStaticFiles` calls in the following example.</span></span> <span data-ttu-id="86624-171">第一次调用启用中的静态文件提供*wwwroot*文件夹。</span><span class="sxs-lookup"><span data-stu-id="86624-171">The first call enables the serving of static files in the *wwwroot* folder.</span></span> <span data-ttu-id="86624-172">第二个调用启用目录浏览的*wwwroot/images*文件夹使用 URL *http://\<server_address > / MyImages*:</span><span class="sxs-lookup"><span data-stu-id="86624-172">The second call enables directory browsing of the *wwwroot/images* folder using the URL *http://\<server_address>/MyImages*:</span></span>

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=3,5)]

## <a name="serve-a-default-document"></a><span data-ttu-id="86624-173">服务默认的文档</span><span class="sxs-lookup"><span data-stu-id="86624-173">Serve a default document</span></span>

<span data-ttu-id="86624-174">设置默认主页上提供了访问者的逻辑起点时访问您的网站。</span><span class="sxs-lookup"><span data-stu-id="86624-174">Setting a default home page provides visitors a logical starting point when visiting your site.</span></span> <span data-ttu-id="86624-175">若要为默认页上，而用户完全限定 URI 提供服务，调用[UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_)方法从`Startup.Configure`:</span><span class="sxs-lookup"><span data-stu-id="86624-175">To serve a default page without the user fully qualifying the URI, call the [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) method from `Startup.Configure`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupEmpty.cs?name=snippet_ConfigureMethod&highlight=3)]

> [!IMPORTANT]
> <span data-ttu-id="86624-176">`UseDefaultFiles`前必须调用`UseStaticFiles`用于默认文件。</span><span class="sxs-lookup"><span data-stu-id="86624-176">`UseDefaultFiles` must be called before `UseStaticFiles` to serve the default file.</span></span> <span data-ttu-id="86624-177">`UseDefaultFiles`是不实际处理该文件 URL 重写者。</span><span class="sxs-lookup"><span data-stu-id="86624-177">`UseDefaultFiles` is a URL rewriter that doesn't actually serve the file.</span></span> <span data-ttu-id="86624-178">启用通过静态文件中间件`UseStaticFiles`来处理该文件。</span><span class="sxs-lookup"><span data-stu-id="86624-178">Enable the static file middleware via `UseStaticFiles` to serve the file.</span></span>

<span data-ttu-id="86624-179">与`UseDefaultFiles`，文件夹搜索到的请求：</span><span class="sxs-lookup"><span data-stu-id="86624-179">With `UseDefaultFiles`, requests to a folder search for:</span></span>

* <span data-ttu-id="86624-180">*default.htm*</span><span class="sxs-lookup"><span data-stu-id="86624-180">*default.htm*</span></span>
* <span data-ttu-id="86624-181">*default.html*</span><span class="sxs-lookup"><span data-stu-id="86624-181">*default.html*</span></span>
* <span data-ttu-id="86624-182">*index.htm*</span><span class="sxs-lookup"><span data-stu-id="86624-182">*index.htm*</span></span>
* <span data-ttu-id="86624-183">*index.html*</span><span class="sxs-lookup"><span data-stu-id="86624-183">*index.html*</span></span>

<span data-ttu-id="86624-184">从列表中找到的第一个文件，就好像该请求是完全限定的 URI 提供服务。</span><span class="sxs-lookup"><span data-stu-id="86624-184">The first file found from the list is served as though the request were the fully qualified URI.</span></span> <span data-ttu-id="86624-185">浏览器 URL 将继续以反映所请求的 URI。</span><span class="sxs-lookup"><span data-stu-id="86624-185">The browser URL continues to reflect the URI requested.</span></span>

<span data-ttu-id="86624-186">下面的代码更改到的默认文件名称*mydefault.html*:</span><span class="sxs-lookup"><span data-stu-id="86624-186">The following code changes the default file name to *mydefault.html*:</span></span>

[!code-csharp[](static-files/samples/1x/StartupDefault.cs?name=snippet_ConfigureMethod)]

## <a name="usefileserver"></a><span data-ttu-id="86624-187">UseFileServer</span><span class="sxs-lookup"><span data-stu-id="86624-187">UseFileServer</span></span>

<span data-ttu-id="86624-188">[UseFileServer](/dotnet/api/microsoft.aspnetcore.builder.fileserverextensions.usefileserver#Microsoft_AspNetCore_Builder_FileServerExtensions_UseFileServer_Microsoft_AspNetCore_Builder_IApplicationBuilder_)将功能组合`UseStaticFiles`， `UseDefaultFiles`，和`UseDirectoryBrowser`。</span><span class="sxs-lookup"><span data-stu-id="86624-188">[UseFileServer](/dotnet/api/microsoft.aspnetcore.builder.fileserverextensions.usefileserver#Microsoft_AspNetCore_Builder_FileServerExtensions_UseFileServer_Microsoft_AspNetCore_Builder_IApplicationBuilder_) combines the functionality of `UseStaticFiles`, `UseDefaultFiles`, and `UseDirectoryBrowser`.</span></span>

<span data-ttu-id="86624-189">以下代码允许静态文件和默认的文件的服务。</span><span class="sxs-lookup"><span data-stu-id="86624-189">The following code enables the serving of static files and the default file.</span></span> <span data-ttu-id="86624-190">未启用目录浏览。</span><span class="sxs-lookup"><span data-stu-id="86624-190">Directory browsing isn't enabled.</span></span>

```csharp
app.UseFileServer();
```

<span data-ttu-id="86624-191">下面的代码基于通过启用目录浏览的无参数的重载：</span><span class="sxs-lookup"><span data-stu-id="86624-191">The following code builds upon the parameterless overload by enabling directory browsing:</span></span>

```csharp
app.UseFileServer(enableDirectoryBrowsing: true);
```

<span data-ttu-id="86624-192">请考虑以下目录层次结构：</span><span class="sxs-lookup"><span data-stu-id="86624-192">Consider the following directory hierarchy:</span></span>

* <span data-ttu-id="86624-193">**wwwroot**</span><span class="sxs-lookup"><span data-stu-id="86624-193">**wwwroot**</span></span>
  * <span data-ttu-id="86624-194">**css**</span><span class="sxs-lookup"><span data-stu-id="86624-194">**css**</span></span>
  * <span data-ttu-id="86624-195">**images**</span><span class="sxs-lookup"><span data-stu-id="86624-195">**images**</span></span>
  * <span data-ttu-id="86624-196">**js**</span><span class="sxs-lookup"><span data-stu-id="86624-196">**js**</span></span>
* <span data-ttu-id="86624-197">**MyStaticFiles**</span><span class="sxs-lookup"><span data-stu-id="86624-197">**MyStaticFiles**</span></span>
  * <span data-ttu-id="86624-198">**images**</span><span class="sxs-lookup"><span data-stu-id="86624-198">**images**</span></span>
      * <span data-ttu-id="86624-199">*banner1.svg*</span><span class="sxs-lookup"><span data-stu-id="86624-199">*banner1.svg*</span></span>
  * <span data-ttu-id="86624-200">*default.html*</span><span class="sxs-lookup"><span data-stu-id="86624-200">*default.html*</span></span>

<span data-ttu-id="86624-201">下面的代码使静态文件、 默认文件和目录浏览的`MyStaticFiles`:</span><span class="sxs-lookup"><span data-stu-id="86624-201">The following code enables static files, default files, and directory browsing of `MyStaticFiles`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureMethod&highlight=5-11)]

<span data-ttu-id="86624-202">`AddDirectoryBrowser`时，必须调用`EnableDirectoryBrowsing`属性值是`true`:</span><span class="sxs-lookup"><span data-stu-id="86624-202">`AddDirectoryBrowser` must be called when the `EnableDirectoryBrowsing` property value is `true`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureServicesMethod)]

<span data-ttu-id="86624-203">使用的文件层次结构和前面的代码，Url 被解析为，如下所示：</span><span class="sxs-lookup"><span data-stu-id="86624-203">Using the file hierarchy and preceding code, URLs resolve as follows:</span></span>

| <span data-ttu-id="86624-204">URI</span><span class="sxs-lookup"><span data-stu-id="86624-204">URI</span></span>            |                             <span data-ttu-id="86624-205">响应</span><span class="sxs-lookup"><span data-stu-id="86624-205">Response</span></span>  |
| ------- | ------|
| <span data-ttu-id="86624-206">*http://\<server_address>/StaticFiles/images/banner1.svg*</span><span class="sxs-lookup"><span data-stu-id="86624-206">*http://\<server_address>/StaticFiles/images/banner1.svg*</span></span>    |      <span data-ttu-id="86624-207">MyStaticFiles/images/banner1.svg</span><span class="sxs-lookup"><span data-stu-id="86624-207">MyStaticFiles/images/banner1.svg</span></span> |
| <span data-ttu-id="86624-208">*http://\<server_address>/StaticFiles*</span><span class="sxs-lookup"><span data-stu-id="86624-208">*http://\<server_address>/StaticFiles*</span></span>             |     <span data-ttu-id="86624-209">MyStaticFiles/default.html</span><span class="sxs-lookup"><span data-stu-id="86624-209">MyStaticFiles/default.html</span></span> |

<span data-ttu-id="86624-210">如果没有默认已命名的文件存在于*MyStaticFiles*目录中， *http://\<server_address > / StaticFiles*返回具有可单击链接列出的目录：</span><span class="sxs-lookup"><span data-stu-id="86624-210">If no default-named file exists in the *MyStaticFiles* directory, *http://\<server_address>/StaticFiles* returns the directory listing with clickable links:</span></span>

![静态文件列表](static-files/_static/db2.png)

> [!NOTE]
> <span data-ttu-id="86624-212">`UseDefaultFiles`和`UseDirectoryBrowser`使用 URL *http://\<server_address > / StaticFiles*不尾部反斜杠来触发客户端的情况下将重定向到*http://\<server_address > /StaticFiles /*。</span><span class="sxs-lookup"><span data-stu-id="86624-212">`UseDefaultFiles` and `UseDirectoryBrowser` use the URL *http://\<server_address>/StaticFiles* without the trailing slash to trigger a client-side redirect to *http://\<server_address>/StaticFiles/*.</span></span> <span data-ttu-id="86624-213">请注意添加尾部反斜杠。</span><span class="sxs-lookup"><span data-stu-id="86624-213">Notice the addition of the trailing slash.</span></span> <span data-ttu-id="86624-214">在文档中的相对 Url 被视为无效而无需尾随斜杠。</span><span class="sxs-lookup"><span data-stu-id="86624-214">Relative URLs within the documents are deemed invalid without a trailing slash.</span></span>

## <a name="fileextensioncontenttypeprovider"></a><span data-ttu-id="86624-215">FileExtensionContentTypeProvider</span><span class="sxs-lookup"><span data-stu-id="86624-215">FileExtensionContentTypeProvider</span></span>

<span data-ttu-id="86624-216">[FileExtensionContentTypeProvider](/dotnet/api/microsoft.aspnetcore.staticfiles.fileextensioncontenttypeprovider)类包含`Mappings`充当 MIME 内容类型的文件扩展名的映射的属性。</span><span class="sxs-lookup"><span data-stu-id="86624-216">The [FileExtensionContentTypeProvider](/dotnet/api/microsoft.aspnetcore.staticfiles.fileextensioncontenttypeprovider) class contains a `Mappings` property serving as a mapping of file extensions to MIME content types.</span></span> <span data-ttu-id="86624-217">在下面的示例中，多个文件扩展名有注册到已知的 MIME 类型。</span><span class="sxs-lookup"><span data-stu-id="86624-217">In the following sample, several file extensions are registered to known MIME types.</span></span> <span data-ttu-id="86624-218">*.Rtf*替换扩展，和*.mp4*中删除。</span><span class="sxs-lookup"><span data-stu-id="86624-218">The *.rtf* extension is replaced, and *.mp4* is removed.</span></span>

[!code-csharp[](static-files/samples/1x/StartupFileExtensionContentTypeProvider.cs?name=snippet_ConfigureMethod&highlight=3-12,19)]

<span data-ttu-id="86624-219">请参阅[MIME 内容类型](http://www.iana.org/assignments/media-types/media-types.xhtml)。</span><span class="sxs-lookup"><span data-stu-id="86624-219">See [MIME content types](http://www.iana.org/assignments/media-types/media-types.xhtml).</span></span>

## <a name="non-standard-content-types"></a><span data-ttu-id="86624-220">非标准的内容类型</span><span class="sxs-lookup"><span data-stu-id="86624-220">Non-standard content types</span></span>

<span data-ttu-id="86624-221">静态文件中间件理解几乎 400 已知的文件内容类型。</span><span class="sxs-lookup"><span data-stu-id="86624-221">The static file middleware understands almost 400 known file content types.</span></span> <span data-ttu-id="86624-222">如果用户请求了未知的文件类型的文件，静态文件中间件将返回 HTTP 404 （未找到） 响应。</span><span class="sxs-lookup"><span data-stu-id="86624-222">If the user requests a file of an unknown file type, the static file middleware returns a HTTP 404 (Not Found) response.</span></span> <span data-ttu-id="86624-223">如果启用目录浏览，将显示文件的链接。</span><span class="sxs-lookup"><span data-stu-id="86624-223">If directory browsing is enabled, a link to the file is displayed.</span></span> <span data-ttu-id="86624-224">URI 将返回 HTTP 404 错误。</span><span class="sxs-lookup"><span data-stu-id="86624-224">The URI returns an HTTP 404 error.</span></span>

<span data-ttu-id="86624-225">下面的代码启用为未知的类型，并呈现为图像未知的文件：</span><span class="sxs-lookup"><span data-stu-id="86624-225">The following code enables serving unknown types and renders the unknown file as an image:</span></span>

[!code-csharp[](static-files/samples/1x/StartupServeUnknownFileTypes.cs?name=snippet_ConfigureMethod)]

<span data-ttu-id="86624-226">与前面的代码中，具有未知的内容类型的文件的请求返回作为映像。</span><span class="sxs-lookup"><span data-stu-id="86624-226">With the preceding code, a request for a file with an unknown content type is returned as an image.</span></span>

> [!WARNING]
> <span data-ttu-id="86624-227">启用[ServeUnknownFileTypes](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions.serveunknownfiletypes#Microsoft_AspNetCore_Builder_StaticFileOptions_ServeUnknownFileTypes)存在安全风险。</span><span class="sxs-lookup"><span data-stu-id="86624-227">Enabling [ServeUnknownFileTypes](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions.serveunknownfiletypes#Microsoft_AspNetCore_Builder_StaticFileOptions_ServeUnknownFileTypes) is a security risk.</span></span> <span data-ttu-id="86624-228">默认情况下，处于禁用状态，建议不要其使用。</span><span class="sxs-lookup"><span data-stu-id="86624-228">It's disabled by default, and its use is discouraged.</span></span> <span data-ttu-id="86624-229">[FileExtensionContentTypeProvider](#fileextensioncontenttypeprovider)提供为文件提供服务使用非标准扩展到更安全的替代方法。</span><span class="sxs-lookup"><span data-stu-id="86624-229">[FileExtensionContentTypeProvider](#fileextensioncontenttypeprovider) provides a safer alternative to serving files with non-standard extensions.</span></span>

### <a name="considerations"></a><span data-ttu-id="86624-230">注意事项</span><span class="sxs-lookup"><span data-stu-id="86624-230">Considerations</span></span>

> [!WARNING]
> <span data-ttu-id="86624-231">`UseDirectoryBrowser`和`UseStaticFiles`可能会泄漏机密。</span><span class="sxs-lookup"><span data-stu-id="86624-231">`UseDirectoryBrowser` and `UseStaticFiles` can leak secrets.</span></span> <span data-ttu-id="86624-232">强烈建议禁用目录浏览在生产环境中。</span><span class="sxs-lookup"><span data-stu-id="86624-232">Disabling directory browsing in production is highly recommended.</span></span> <span data-ttu-id="86624-233">请仔细查看的目录启用通过`UseStaticFiles`或`UseDirectoryBrowser`。</span><span class="sxs-lookup"><span data-stu-id="86624-233">Carefully review which directories are enabled via `UseStaticFiles` or `UseDirectoryBrowser`.</span></span> <span data-ttu-id="86624-234">整个目录和其子目录变得可公开访问。</span><span class="sxs-lookup"><span data-stu-id="86624-234">The entire directory and its sub-directories become publicly accessible.</span></span> <span data-ttu-id="86624-235">应用商店中的文件适用于向公众提供一个专用的目录，如 *\<content_root > / wwwroot*。</span><span class="sxs-lookup"><span data-stu-id="86624-235">Store files suitable for serving to the public in a dedicated directory, such as *\<content_root>/wwwroot*.</span></span> <span data-ttu-id="86624-236">这些文件分开 MVC 视图，Razor 页 (仅 2.x) 配置文件，等等。</span><span class="sxs-lookup"><span data-stu-id="86624-236">Separate these files from MVC views, Razor Pages (2.x only), configuration files, etc.</span></span>

* <span data-ttu-id="86624-237">通过公开的内容的 Url`UseDirectoryBrowser`和`UseStaticFiles`受到的区分大小写和基础文件系统的字符限制。</span><span class="sxs-lookup"><span data-stu-id="86624-237">The URLs for content exposed with `UseDirectoryBrowser` and `UseStaticFiles` are subject to the case sensitivity and character restrictions of the underlying file system.</span></span> <span data-ttu-id="86624-238">例如，Windows 不区分&mdash;Mac 和 Linux 不是。</span><span class="sxs-lookup"><span data-stu-id="86624-238">For example, Windows is case insensitive&mdash;Mac and Linux aren't.</span></span>

* <span data-ttu-id="86624-239">承载于 IIS 使用 ASP.NET Core 应用[ASP.NET 核心模块 (ANCM)](xref:fundamentals/servers/aspnet-core-module)转发到应用程序，包括静态文件请求的所有请求。</span><span class="sxs-lookup"><span data-stu-id="86624-239">ASP.NET Core apps hosted in IIS use the [ASP.NET Core Module (ANCM)](xref:fundamentals/servers/aspnet-core-module) to forward all requests to the app, including static file requests.</span></span> <span data-ttu-id="86624-240">IIS 静态文件处理程序未使用。</span><span class="sxs-lookup"><span data-stu-id="86624-240">The IIS static file handler isn't used.</span></span> <span data-ttu-id="86624-241">它具有没有机会之前通过 ANCM 处理这些处理请求。</span><span class="sxs-lookup"><span data-stu-id="86624-241">It has no chance to handle requests before they're handled by the ANCM.</span></span>

* <span data-ttu-id="86624-242">完成以下步骤在 IIS 管理器来删除 IIS 静态文件处理程序在服务器或网站级别：</span><span class="sxs-lookup"><span data-stu-id="86624-242">Complete the following steps in IIS Manager to remove the IIS static file handler at the server or website level:</span></span>
    1. <span data-ttu-id="86624-243">导航到**模块**功能。</span><span class="sxs-lookup"><span data-stu-id="86624-243">Navigate to the **Modules** feature.</span></span>
    1. <span data-ttu-id="86624-244">选择**StaticFileModule**列表中。</span><span class="sxs-lookup"><span data-stu-id="86624-244">Select **StaticFileModule** in the list.</span></span>
    1. <span data-ttu-id="86624-245">单击**删除**中**操作**侧栏。</span><span class="sxs-lookup"><span data-stu-id="86624-245">Click **Remove** in the **Actions** sidebar.</span></span>

> [!WARNING]
> <span data-ttu-id="86624-246">如果启用了 IIS 静态文件处理程序**和**ANCM 配置不正确，静态文件提供服务。</span><span class="sxs-lookup"><span data-stu-id="86624-246">If the IIS static file handler is enabled **and** the ANCM is configured incorrectly, static files are served.</span></span> <span data-ttu-id="86624-247">发生这种情况，例如，如果*web.config*文件未部署。</span><span class="sxs-lookup"><span data-stu-id="86624-247">This happens, for example, if the *web.config* file isn't deployed.</span></span>

* <span data-ttu-id="86624-248">放置代码文件 (包括*.cs*和*.cshtml*) 在应用程序项目的 web 根目录之外。</span><span class="sxs-lookup"><span data-stu-id="86624-248">Place code files (including *.cs* and *.cshtml*) outside of the app project's web root.</span></span> <span data-ttu-id="86624-249">因此应用程序的客户端的内容与基于服务器的代码之间创建逻辑分隔。</span><span class="sxs-lookup"><span data-stu-id="86624-249">A logical separation is therefore created between the app's client-side content and server-based code.</span></span> <span data-ttu-id="86624-250">这可防止服务器端代码被泄露。</span><span class="sxs-lookup"><span data-stu-id="86624-250">This prevents server-side code from being leaked.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86624-251">其他资源</span><span class="sxs-lookup"><span data-stu-id="86624-251">Additional resources</span></span>

* [<span data-ttu-id="86624-252">中间件</span><span class="sxs-lookup"><span data-stu-id="86624-252">Middleware</span></span>](xref:fundamentals/middleware)

* [<span data-ttu-id="86624-253">ASP.NET Core 简介</span><span class="sxs-lookup"><span data-stu-id="86624-253">Introduction to ASP.NET Core</span></span>](xref:index)