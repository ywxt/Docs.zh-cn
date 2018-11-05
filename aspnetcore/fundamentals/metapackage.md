---
title: ASP.NET Core 2.0 的 Microsoft.AspNetCore.All 元包
author: Rick-Anderson
description: 不建议在 ASP.NET Core 2.1 及更高版本中使用 Microsoft.AspNetCore.All 元数据包。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 10/25/2018
uid: fundamentals/metapackage
ms.openlocfilehash: d95bafd412969bb8db38499bd2ff01af510d872c
ms.sourcegitcommit: 54655f1e1abf0b64d19506334d94cfdb0caf55f6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148845"
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-20"></a><span data-ttu-id="515e0-103">ASP.NET Core 2.0 的 Microsoft.AspNetCore.All 元包</span><span class="sxs-lookup"><span data-stu-id="515e0-103">Microsoft.AspNetCore.All metapackage for ASP.NET Core 2.0</span></span>

> [!NOTE]
> <span data-ttu-id="515e0-104">对于面向 ASP.NET Core 2.1 及更高版本的应用程序，建议使用 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)而不是此包。</span><span class="sxs-lookup"><span data-stu-id="515e0-104">We recommend applications targeting ASP.NET Core 2.1 and later use the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) rather than this package.</span></span> <span data-ttu-id="515e0-105">请参阅本文中的[从 Microsoft.AspNetCore.All 迁移到 Microsoft.AspNetCore.App](#migrate)。</span><span class="sxs-lookup"><span data-stu-id="515e0-105">See [Migrating from Microsoft.AspNetCore.All to Microsoft.AspNetCore.App](#migrate) in this article.</span></span>

<span data-ttu-id="515e0-106">此功能需要面向 .NET Core 2.x 的 ASP.NET Core 2.x。</span><span class="sxs-lookup"><span data-stu-id="515e0-106">This feature requires ASP.NET Core 2.x targeting .NET Core 2.x.</span></span>

<span data-ttu-id="515e0-107">ASP.NET Core 的 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 元包包括：</span><span class="sxs-lookup"><span data-stu-id="515e0-107">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="515e0-108">ASP.NET Core 团队支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="515e0-108">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="515e0-109">Entity Framework Core 支持的所有包。</span><span class="sxs-lookup"><span data-stu-id="515e0-109">All supported packages by the Entity Framework Core.</span></span>
* <span data-ttu-id="515e0-110">ASP.NET Core 和 Entity Framework Core 使用的内部和第三方依赖关系。</span><span class="sxs-lookup"><span data-stu-id="515e0-110">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span>

<span data-ttu-id="515e0-111">`Microsoft.AspNetCore.All` 包中包含了 ASP.NET Core 2.x 和 Entity Framework Core 2.x 的所有功能。</span><span class="sxs-lookup"><span data-stu-id="515e0-111">All the features of ASP.NET Core 2.x and Entity Framework Core 2.x are included in the `Microsoft.AspNetCore.All` package.</span></span> <span data-ttu-id="515e0-112">定目标到 ASP.NET Core 2.0 的默认项目模板使用此包。</span><span class="sxs-lookup"><span data-stu-id="515e0-112">The default project templates targeting ASP.NET Core 2.0 use this package.</span></span>

<span data-ttu-id="515e0-113">`Microsoft.AspNetCore.All` 元包的版本号表示 ASP.NET Core 版本和 Entity Framework Core 版本。</span><span class="sxs-lookup"><span data-stu-id="515e0-113">The version number of the `Microsoft.AspNetCore.All` metapackage represents the ASP.NET Core version and Entity Framework Core version.</span></span>

<span data-ttu-id="515e0-114">使用 `Microsoft.AspNetCore.All` 元包的应用程序会自动使用 [.NET Core 运行时存储](/dotnet/core/deploying/runtime-store)。</span><span class="sxs-lookup"><span data-stu-id="515e0-114">Applications that use the `Microsoft.AspNetCore.All` metapackage automatically take advantage of the [.NET Core Runtime Store](/dotnet/core/deploying/runtime-store).</span></span> <span data-ttu-id="515e0-115">此运行时存储包含运行 ASP.NET Core 2.x 应用程序所需的所有运行时资产。</span><span class="sxs-lookup"><span data-stu-id="515e0-115">The Runtime Store contains all the runtime assets needed to run ASP.NET Core 2.x applications.</span></span> <span data-ttu-id="515e0-116">使用 `Microsoft.AspNetCore.All` 元包时，应用程序不会部署引用的 ASP.NET Core NuGet 包中的任何资产&mdash;.NET Core 运行时存储包含这些资产。</span><span class="sxs-lookup"><span data-stu-id="515e0-116">When you use the `Microsoft.AspNetCore.All` metapackage, **no** assets from the referenced ASP.NET Core NuGet packages are deployed with the application &mdash; the .NET Core Runtime Store contains these assets.</span></span> <span data-ttu-id="515e0-117">运行时存储中的资产已经过预编译，以便缩短应用程序启动时间。</span><span class="sxs-lookup"><span data-stu-id="515e0-117">The assets in the Runtime Store are precompiled to improve application startup time.</span></span>

<span data-ttu-id="515e0-118">可使用包修整过程来删除不使用的包。</span><span class="sxs-lookup"><span data-stu-id="515e0-118">You can use the package trimming process to remove packages that you don't use.</span></span> <span data-ttu-id="515e0-119">已发布的应用程序输出中排除了修整的包。</span><span class="sxs-lookup"><span data-stu-id="515e0-119">Trimmed packages are excluded in published application output.</span></span>

<span data-ttu-id="515e0-120">以下 .csproj 文件引用了 ASP.NET Core 的 `Microsoft.AspNetCore.All` 元包：</span><span class="sxs-lookup"><span data-stu-id="515e0-120">The following *.csproj* file references the `Microsoft.AspNetCore.All` metapackage for ASP.NET Core:</span></span>

[!code-xml[](metapackage/samples/Metapackage.All.Example.csproj?highlight=8)]

::: moniker range=">= aspnetcore-2.1"

## <a name="implicit-versioning"></a><span data-ttu-id="515e0-121">隐式版本控制</span><span class="sxs-lookup"><span data-stu-id="515e0-121">Implicit versioning</span></span>

<span data-ttu-id="515e0-122">在 ASP.NET Core 2.1 或更高版本中，可以指定 `Microsoft.AspNetCore.All` 包引用但不指定版本。</span><span class="sxs-lookup"><span data-stu-id="515e0-122">In ASP.NET Core 2.1 or later, you can specify the `Microsoft.AspNetCore.All` package reference without a version.</span></span> <span data-ttu-id="515e0-123">如果未指定版本，SDK 会指定隐式版本 (`Microsoft.NET.Sdk.Web`)。</span><span class="sxs-lookup"><span data-stu-id="515e0-123">When the version isn't specified, an implicit version is specified by the SDK (`Microsoft.NET.Sdk.Web`).</span></span> <span data-ttu-id="515e0-124">建议使用 SDK 指定的隐式版本，而不是在包引用上显式设置版本号。</span><span class="sxs-lookup"><span data-stu-id="515e0-124">We recommend relying on the implicit version specified by the SDK and not explicitly setting the version number on the package reference.</span></span> <span data-ttu-id="515e0-125">如果对这种方法有任何疑问，可以在 [Microsoft.AspNetCore.App 隐式版本讨论](https://github.com/aspnet/Docs/issues/6430)上发表 GitHub 评论。</span><span class="sxs-lookup"><span data-stu-id="515e0-125">If you have questions about this approach, leave a GitHub comment at the [Discussion for the Microsoft.AspNetCore.App implicit version](https://github.com/aspnet/Docs/issues/6430).</span></span>

<span data-ttu-id="515e0-126">对于便携式应用，隐式版本设置为 `major.minor.0`。</span><span class="sxs-lookup"><span data-stu-id="515e0-126">The implicit version is set to `major.minor.0` for portable apps.</span></span> <span data-ttu-id="515e0-127">共享框架前滚机制在安装的共享框架的最新兼容版本上运行应用。</span><span class="sxs-lookup"><span data-stu-id="515e0-127">The shared framework roll-forward mechanism runs the app on the latest compatible version among the installed shared frameworks.</span></span> <span data-ttu-id="515e0-128">为确保在开发、测试和生产中使用相同的版本，请确保在所有环境中都安装相同版本的共享框架。</span><span class="sxs-lookup"><span data-stu-id="515e0-128">To guarantee the same version is used in development, test, and production, ensure the same version of the shared framework is installed in all environments.</span></span> <span data-ttu-id="515e0-129">对于独立应用，将隐式版本号设置为在已安装的 SDK 中捆绑的共享框架的 `major.minor.patch`。</span><span class="sxs-lookup"><span data-stu-id="515e0-129">For self-contained apps, the implicit version number is set to the `major.minor.patch` of the shared framework bundled in the installed SDK.</span></span>

<span data-ttu-id="515e0-130">在 `Microsoft.AspNetCore.All` 包引用上指定版本号，不能保证会选择该共享框架版本。</span><span class="sxs-lookup"><span data-stu-id="515e0-130">Specifying a version number on the `Microsoft.AspNetCore.All` package reference does **not** guarantee that version of the shared framework is chosen.</span></span> <span data-ttu-id="515e0-131">例如，假设指定的版本是“2.1.1”，但安装的是“2.1.3”。</span><span class="sxs-lookup"><span data-stu-id="515e0-131">For example, suppose version "2.1.1" is specified, but "2.1.3" is installed.</span></span> <span data-ttu-id="515e0-132">这种情况下，应用将使用"2.1.3"。</span><span class="sxs-lookup"><span data-stu-id="515e0-132">In that case, the app will use "2.1.3".</span></span> <span data-ttu-id="515e0-133">不过不建议这样做，你可以禁用前滚（修补程序和/或次要版本）。</span><span class="sxs-lookup"><span data-stu-id="515e0-133">Although not recommended, you can disable roll forward (patch and/or minor).</span></span> <span data-ttu-id="515e0-134">有关 dotnet 主机前滚以及如何配置其行为的详细信息，请参阅 [dotnet 主机前滚](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md)。</span><span class="sxs-lookup"><span data-stu-id="515e0-134">For more information regarding dotnet host roll-forward and how to configure its behavior, see [dotnet host roll forward](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md).</span></span>

<span data-ttu-id="515e0-135">必须在项目文件中将项目的 SDK 设置为 `Microsoft.NET.Sdk.Web`，这样才能使用隐式版本的 `Microsoft.AspNetCore.All`。</span><span class="sxs-lookup"><span data-stu-id="515e0-135">The project's SDK must be set to `Microsoft.NET.Sdk.Web` in the project file to use the implicit version of `Microsoft.AspNetCore.All`.</span></span> <span data-ttu-id="515e0-136">指定 `Microsoft.NET.Sdk` SDK（项目文件顶部的 `<Project Sdk="Microsoft.NET.Sdk">`）时，将生成以下警告：</span><span class="sxs-lookup"><span data-stu-id="515e0-136">When the `Microsoft.NET.Sdk` SDK is specified (`<Project Sdk="Microsoft.NET.Sdk">` at the top of the project file), the following warning is generated:</span></span>

<span data-ttu-id="515e0-137">警告 NU1604：项目依赖项 Microsoft.AspNetCore.All 不包括包含下限。请在依赖项版本中包括下限，以确保一致的还原结果。</span><span class="sxs-lookup"><span data-stu-id="515e0-137">*Warning NU1604: Project dependency Microsoft.AspNetCore.All does not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span>

<span data-ttu-id="515e0-138">这是 .NET Core 2.1 SDK 的一个已知问题，将在 .NET Core 2.2 SDK 中修复。</span><span class="sxs-lookup"><span data-stu-id="515e0-138">This is a known issue with the .NET Core 2.1 SDK and will be fixed in the .NET Core 2.2 SDK.</span></span>

::: moniker-end

<a name="migrate"></a>

## <a name="migrating-from-microsoftaspnetcoreall-to-microsoftaspnetcoreapp"></a><span data-ttu-id="515e0-139">从 Microsoft.AspNetCore.All 迁移到 Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="515e0-139">Migrating from Microsoft.AspNetCore.All to Microsoft.AspNetCore.App</span></span>

<span data-ttu-id="515e0-140">`Microsoft.AspNetCore.All` 包中包含以下包，而 `Microsoft.AspNetCore.App` 包中不包含以下包。</span><span class="sxs-lookup"><span data-stu-id="515e0-140">The following packages are included in `Microsoft.AspNetCore.All` but not the `Microsoft.AspNetCore.App` package.</span></span>

* `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServices.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServicesIntegration`
* `Microsoft.AspNetCore.DataProtection.AzureKeyVault`
* `Microsoft.AspNetCore.DataProtection.AzureStorage`
* `Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv`
* `Microsoft.AspNetCore.SignalR.Redis`
* `Microsoft.Data.Sqlite`
* `Microsoft.Data.Sqlite.Core`
* `Microsoft.EntityFrameworkCore.Sqlite`
* `Microsoft.EntityFrameworkCore.Sqlite.Core`
* `Microsoft.Extensions.Caching.Redis`
* `Microsoft.Extensions.Configuration.AzureKeyVault`
* `Microsoft.Extensions.Logging.AzureAppServices`
* `Microsoft.VisualStudio.Web.BrowserLink`

<span data-ttu-id="515e0-141">要从 `Microsoft.AspNetCore.All` 移到 `Microsoft.AspNetCore.App`，如果应用使用上述包或由这些包引入的包中的任何 API，请在项目中添加对这些包的引用。</span><span class="sxs-lookup"><span data-stu-id="515e0-141">To move from `Microsoft.AspNetCore.All` to `Microsoft.AspNetCore.App`, if your app uses any APIs from the above packages, or packages brought in by those packages, add references to those packages in your project.</span></span>

<span data-ttu-id="515e0-142">不会隐式包含非 `Microsoft.AspNetCore.App` 依赖项的上述包的任何依赖项。</span><span class="sxs-lookup"><span data-stu-id="515e0-142">Any dependencies of the preceding packages that otherwise aren't dependencies of `Microsoft.AspNetCore.App` are not included implicitly.</span></span> <span data-ttu-id="515e0-143">例如:</span><span class="sxs-lookup"><span data-stu-id="515e0-143">For example:</span></span>

* <span data-ttu-id="515e0-144">`StackExchange.Redis` 作为 `Microsoft.Extensions.Caching.Redis` 的依赖项</span><span class="sxs-lookup"><span data-stu-id="515e0-144">`StackExchange.Redis` as a dependency of `Microsoft.Extensions.Caching.Redis`</span></span>
* <span data-ttu-id="515e0-145">`Microsoft.ApplicationInsights` 作为 `Microsoft.AspNetCore.ApplicationInsights.HostingStartup` 的依赖项</span><span class="sxs-lookup"><span data-stu-id="515e0-145">`Microsoft.ApplicationInsights` as a dependency of `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`</span></span>

## <a name="update-aspnet-core-21"></a><span data-ttu-id="515e0-146">更新 ASP.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="515e0-146">Update ASP.NET Core 2.1</span></span>

<span data-ttu-id="515e0-147">建议迁移到 2.1 及更高版本的 `Microsoft.AspNetCore.App` 元数据包。</span><span class="sxs-lookup"><span data-stu-id="515e0-147">We recommend migrating to the `Microsoft.AspNetCore.App` metapackage for 2.1 and later.</span></span> <span data-ttu-id="515e0-148">要继续使用 `Microsoft.AspNetCore.All` 元数据包并确保部署最新的补丁版本，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="515e0-148">To keep using the `Microsoft.AspNetCore.All` metapackage and ensure the latest patch version is deployed:</span></span>

* <span data-ttu-id="515e0-149">在开发计算机和生成服务器上：安装最新的 [.NET Core SDK](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="515e0-149">On development machines and build servers: Install the latest [.NET Core SDK](https://www.microsoft.com/net/download).</span></span>
* <span data-ttu-id="515e0-150">在部署服务器上：安装最新的 [.NET Core 运行时](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="515e0-150">On deployment servers: Install the latest [.NET Core runtime](https://www.microsoft.com/net/download).</span></span>
 <span data-ttu-id="515e0-151">在应用程序重启时，应用将前滚到最新安装的版本。</span><span class="sxs-lookup"><span data-stu-id="515e0-151">Your app will roll forward to the latest installed version on an application restart.</span></span>
