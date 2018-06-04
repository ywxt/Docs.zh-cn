---
title: ASP.NET 核心项目中的基架标识
author: rick-anderson
description: 了解如何创建标识的基架 ASP.NET Core 项目中。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 5/16/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/scaffold-identity
ms.openlocfilehash: a43b7bbaf1f90d3373b3846bc3f4f32be6b80bd4
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34729605"
---
# <a name="scaffold-identity-in-aspnet-core-projects"></a><span data-ttu-id="0f9ab-103">ASP.NET 核心项目中的基架标识</span><span class="sxs-lookup"><span data-stu-id="0f9ab-103">Scaffold Identity in ASP.NET Core projects</span></span>

<span data-ttu-id="0f9ab-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0f9ab-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="0f9ab-105">ASP.NET 核心 2.1 及更高版本提供了[ASP.NET 核心标识](xref:security/authentication/identity)作为[Razor 类库](xref:mvc/razor-pages/ui-class)。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-105">ASP.NET Core 2.1 and later provides [ASP.NET Core Identity](xref:security/authentication/identity) as a [Razor Class Library](xref:mvc/razor-pages/ui-class).</span></span> <span data-ttu-id="0f9ab-106">包含标识的应用程序可以应用基架以有选择地添加包含在标识 Razor 类库 (RCL) 的源代码。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-106">Applications that include Identity can apply the scaffolder to selectively add the source code contained in the Identity Razor Class Library (RCL).</span></span> <span data-ttu-id="0f9ab-107">你可能想要生成源代码，因此你可以修改的代码和更改的行为。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-107">You might want to generate source code so you can modify the code and change the behavior.</span></span> <span data-ttu-id="0f9ab-108">例如，你可以指示 scaffolder 生成在注册中使用的代码。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-108">For example, you could instruct the scaffolder to generate the code used in registration.</span></span> <span data-ttu-id="0f9ab-109">生成的代码将优先于标识 RCL 中的相同代码。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-109">Generated code takes precedence over the same code in the Identity RCL.</span></span>

<span data-ttu-id="0f9ab-110">应用程序执行**不**包括身份验证可以应用基架添加 RCL 标识包。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-110">Applications that do **not** include authentication can apply the scaffolder to add the RCL Identity package.</span></span> <span data-ttu-id="0f9ab-111">必须选择标识代码生成的选项。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-111">You have the option of selecting Identity code to be generated.</span></span>

<span data-ttu-id="0f9ab-112">虽然 scaffolder 生成大部分所需的代码，但你将需要更新你的项目以完成该过程。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-112">Although the scaffolder generates most of the necessary code, you'll have to update your project to complete the process.</span></span> <span data-ttu-id="0f9ab-113">本文档说明完成标识基架更新所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-113">This document explains the steps needed to complete an Identity scaffolding update.</span></span>

<span data-ttu-id="0f9ab-114">当运行时标识 scaffolder 时， *ScaffoldingReadme.txt*在项目目录中创建文件。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-114">When the Identity scaffolder is run, a *ScaffoldingReadme.txt* file is created in the project directory.</span></span> <span data-ttu-id="0f9ab-115">*ScaffoldingReadme.txt*文件包含有关需要哪些条件完成标识基架更新的常规说明。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-115">The *ScaffoldingReadme.txt* file contains general instructions on what's needed to complete the Identity scaffolding update.</span></span> <span data-ttu-id="0f9ab-116">本文档包含比读取的更完整说明*ScaffoldingReadme.txt*文件。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-116">This document contains more complete instructions than the read the *ScaffoldingReadme.txt* file.</span></span>

<span data-ttu-id="0f9ab-117">我们建议使用源代码管理系统，它显示文件的差异，并允许你地将带外更改。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-117">We recommend using a source control system that shows file differences and allows you to back out of changes.</span></span> <span data-ttu-id="0f9ab-118">运行标识 scaffolder 后检查所做的更改。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-118">Inspect the changes after running the Identity scaffolder.</span></span>

## <a name="scaffold-identity-into-an-empty-project"></a><span data-ttu-id="0f9ab-119">为一个空的项目的基架标识</span><span class="sxs-lookup"><span data-stu-id="0f9ab-119">Scaffold identity into an empty project</span></span>

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="0f9ab-120">添加对以下突出显示的调用`Startup`类：</span><span class="sxs-lookup"><span data-stu-id="0f9ab-120">Add the following highlighted calls to the `Startup` class:</span></span>

[!code-csharp[Main](scaffold-identity/sample/StartupEmpty.cs?name=snippet1&highlight=5,20-23)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

## <a name="scaffold-identity-into-a-razor-project-without-existing-authorization"></a><span data-ttu-id="0f9ab-121">到未包含现有的授权 Razor 项目的基架标识</span><span class="sxs-lookup"><span data-stu-id="0f9ab-121">Scaffold identity into a Razor project without existing authorization</span></span>

<!--
set projNam=RPnoAuth
set projType=razor
set version=2.1.0

dotnet new %projType% -o %projNam%
cd %projNam%
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design -v %version%
dotnet restore
dotnet aspnet-codegenerator identity --useDefaultUI
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="0f9ab-122">在中配置标识*Areas/Identity/IdentityHostingStartup.cs*。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-122">Identity is configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="0f9ab-123">有关详细信息，请参阅[IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-123">for more information, see [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span></span>

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

<span data-ttu-id="0f9ab-124">在`Configure`方法`Startup`类中，调用[UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_)后`UseStaticFiles`:</span><span class="sxs-lookup"><span data-stu-id="0f9ab-124">In the `Configure` method of the `Startup` class, call [UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) after `UseStaticFiles`:</span></span>

[!code-csharp[Main](scaffold-identity/sample/StartupRPnoAuth.cs?name=snippet1&highlight=29)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

### <a name="layout-changes"></a><span data-ttu-id="0f9ab-125">布局更改</span><span class="sxs-lookup"><span data-stu-id="0f9ab-125">Layout changes</span></span>

<span data-ttu-id="0f9ab-126">可选： 添加部分的登录名 (`_LoginPartial`) 到布局文件：</span><span class="sxs-lookup"><span data-stu-id="0f9ab-126">Optional: Add the login partial (`_LoginPartial`) to the layout file:</span></span>

[!code-html[Main](scaffold-identity/sample/_Layout.cshtml?highlight=37)]

## <a name="scaffold-identity-into-a-razor-project-with-authorization"></a><span data-ttu-id="0f9ab-127">到与授权 Razor 项目的基架标识</span><span class="sxs-lookup"><span data-stu-id="0f9ab-127">Scaffold identity into a Razor project with authorization</span></span>

<!--
Use >=2.1: dotnet new webapp -au Individual -o RPauth
Use = 2.0: dotnet new razor -au Individual -o RPauth
cd RPauth
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design --version 2.1.0
dotnet restore
dotnet aspnet-codegenerator identity -dc RPauth.Data.ApplicationDbContext --files Account.Register
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg-auth.md)]
<span data-ttu-id="0f9ab-128">某些标识选项配置中*Areas/Identity/IdentityHostingStartup.cs*。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-128">Some Identity options are configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="0f9ab-129">有关详细信息，请参阅[IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-129">For more information, see [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span></span>

## <a name="scaffold-identity-into-an-mvc-project-without-existing-authorization"></a><span data-ttu-id="0f9ab-130">到未包含现有的授权 MVC 项目的基架标识</span><span class="sxs-lookup"><span data-stu-id="0f9ab-130">Scaffold identity into an MVC project without existing authorization</span></span>

<!--
set projNam=MvcNoAuth
set projType=mvc
set version=2.1.0

dotnet new %projType% -o %projNam%
cd %projNam%
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design -v %version%
dotnet restore
dotnet aspnet-codegenerator identity --useDefaultUI
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="0f9ab-131">可选： 添加部分的登录名 (`_LoginPartial`) 到*Views/Shared/_Layout.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="0f9ab-131">Optional: Add the login partial (`_LoginPartial`) to the *Views/Shared/_Layout.cshtml* file:</span></span>

[!code-html[Main](scaffold-identity/sample/_LayoutMvc.cshtml?highlight=37)]

* <span data-ttu-id="0f9ab-132">移动*Pages/Shared/_LoginPartial.cshtml*文件为*Views/Shared/_LoginPartial.cshtml*</span><span class="sxs-lookup"><span data-stu-id="0f9ab-132">Move the *Pages/Shared/_LoginPartial.cshtml* file to *Views/Shared/_LoginPartial.cshtml*</span></span>

<span data-ttu-id="0f9ab-133">在中配置标识*Areas/Identity/IdentityHostingStartup.cs*。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-133">Identity is configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="0f9ab-134">有关详细信息，请参阅 IHostingStartup。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-134">For more information, see IHostingStartup.</span></span>

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

<span data-ttu-id="0f9ab-135">调用[UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_)后`UseStaticFiles`:</span><span class="sxs-lookup"><span data-stu-id="0f9ab-135">Call [UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) after `UseStaticFiles`:</span></span>

[!code-csharp[Main](scaffold-identity/sample/StartupMvcNoAuth.cs?name=snippet1&highlight=23)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

## <a name="scaffold-identity-into-an-mvc-project-with-authorization"></a><span data-ttu-id="0f9ab-136">到具有授权的 MVC 项目的基架标识</span><span class="sxs-lookup"><span data-stu-id="0f9ab-136">Scaffold identity into an MVC project with authorization</span></span>

<!--
dotnet new mvc -au Individual -o MvcAuth
cd MvcAuth
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design --version 2.1.0
dotnet restore
dotnet aspnet-codegenerator identity -dc MvcAuth.Data.ApplicationDbContext --files Account.Register
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg-auth.md)]

<span data-ttu-id="0f9ab-137">删除*页/共享*文件夹和该文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="0f9ab-137">Delete the *Pages/Shared* folder and the files in that folder.</span></span>
