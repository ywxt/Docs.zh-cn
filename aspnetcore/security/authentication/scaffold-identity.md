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
ms.openlocfilehash: 8933cf9c4063bd94f7f3a9ba53b5372b443eb7c8
ms.sourcegitcommit: d4cefc0c63550c64a8040b11867cc05efcfb7e86
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34758747"
---
# <a name="scaffold-identity-in-aspnet-core-projects"></a>ASP.NET 核心项目中的基架标识

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET 核心 2.1 及更高版本提供了[ASP.NET 核心标识](xref:security/authentication/identity)作为[Razor 类库](xref:mvc/razor-pages/ui-class)。 包含标识的应用程序可以应用基架以有选择地添加包含在标识 Razor 类库 (RCL) 的源代码。 你可能想要生成源代码，因此你可以修改的代码和更改的行为。 例如，你可以指示 scaffolder 生成在注册中使用的代码。 生成的代码将优先于标识 RCL 中的相同代码。

应用程序执行**不**包括身份验证可以应用基架添加 RCL 标识包。 必须选择标识代码生成的选项。

虽然 scaffolder 生成大部分所需的代码，但你将需要更新你的项目以完成该过程。 本文档说明完成标识基架更新所需的步骤。

当运行时标识 scaffolder 时， *ScaffoldingReadme.txt*在项目目录中创建文件。 *ScaffoldingReadme.txt*文件包含有关需要哪些条件完成标识基架更新的常规说明。 本文档包含比读取的更完整说明*ScaffoldingReadme.txt*文件。

我们建议使用源代码管理系统，它显示文件的差异，并允许你地将带外更改。 运行标识 scaffolder 后检查所做的更改。

## <a name="scaffold-identity-into-an-empty-project"></a>为一个空的项目的基架标识

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

添加对以下突出显示的调用`Startup`类：

[!code-csharp[Main](scaffold-identity/sample/StartupEmpty.cs?name=snippet1&highlight=5,20-23)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

## <a name="scaffold-identity-into-a-razor-project-without-existing-authorization"></a>到未包含现有的授权 Razor 项目的基架标识

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

在中配置标识*Areas/Identity/IdentityHostingStartup.cs*。 有关详细信息，请参阅[IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)。

<a name="efm"></a>

### <a name="migrations-useauthentication-and-layout"></a>迁移、 UseAuthentication 和布局

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

在`Configure`方法`Startup`类中，调用[UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_)后`UseStaticFiles`:

[!code-csharp[Main](scaffold-identity/sample/StartupRPnoAuth.cs?name=snippet1&highlight=29)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

### <a name="layout-changes"></a>布局更改

可选： 添加部分的登录名 (`_LoginPartial`) 到布局文件：

[!code-html[Main](scaffold-identity/sample/_Layout.cshtml?highlight=37)]

## <a name="scaffold-identity-into-a-razor-project-with-authorization"></a>到与授权 Razor 项目的基架标识

<!--
Use >=2.1: dotnet new webapp -au Individual -o RPauth
Use = 2.0: dotnet new razor -au Individual -o RPauth
cd RPauth
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
dotnet aspnet-codegenerator identity -dc RPauth.Data.ApplicationDbContext --files Account.Register
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg-auth.md)]
某些标识选项配置中*Areas/Identity/IdentityHostingStartup.cs*。 有关详细信息，请参阅[IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)。

## <a name="scaffold-identity-into-an-mvc-project-without-existing-authorization"></a>到未包含现有的授权 MVC 项目的基架标识

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

可选： 添加部分的登录名 (`_LoginPartial`) 到*Views/Shared/_Layout.cshtml*文件：

[!code-html[Main](scaffold-identity/sample/_LayoutMvc.cshtml?highlight=37)]

* 移动*Pages/Shared/_LoginPartial.cshtml*文件为*Views/Shared/_LoginPartial.cshtml*

在中配置标识*Areas/Identity/IdentityHostingStartup.cs*。 有关详细信息，请参阅 IHostingStartup。

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

调用[UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_)后`UseStaticFiles`:

[!code-csharp[Main](scaffold-identity/sample/StartupMvcNoAuth.cs?name=snippet1&highlight=23)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

## <a name="scaffold-identity-into-an-mvc-project-with-authorization"></a>到具有授权的 MVC 项目的基架标识

<!--
dotnet new mvc -au Individual -o MvcAuth
cd MvcAuth
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
dotnet aspnet-codegenerator identity -dc MvcAuth.Data.ApplicationDbContext --files Account.Register
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg-auth.md)]

删除*页/共享*文件夹和该文件夹中的文件。
