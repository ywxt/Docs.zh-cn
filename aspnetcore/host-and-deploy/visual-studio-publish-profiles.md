---
title: Visual Studio 发布 ASP.NET 核心应用程序部署的配置文件
author: rick-anderson
description: 了解如何创建 Visual Studio 中发布配置文件，并使用它们来管理 ASP.NET Core 应用程序部署到各种目标。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 04/10/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/visual-studio-publish-profiles
ms.openlocfilehash: 3dc858793cd4ddb2630d05a5084f4b7caeaa30eb
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="visual-studio-publish-profiles-for-aspnet-core-app-deployment"></a>Visual Studio 发布 ASP.NET 核心应用程序部署的配置文件

作者：[Sayed Ibrahim Hashimi](https://github.com/sayedihashimi) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)

本文档重点介绍使用 Visual Studio 2017 创建和使用发布配置文件。 可以从 MSBuild 和 Visual Studio 2017 运行使用 Visual Studio 创建的发布配置文件。 有关发布到 Azure 的说明，请参阅[使用 Visual Studio 将 ASP.NET Core Web 应用发布到 Azure App Service](xref:tutorials/publish-to-azure-webapp-using-vs)。

以下项目文件已使用命令创建`dotnet new mvc`:

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.0" />
  </ItemGroup>

  <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.0" />
  </ItemGroup>

</Project>
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp1.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore" Version="1.1.5" />
    <PackageReference Include="Microsoft.AspNetCore.Mvc" Version="1.1.6" />
    <PackageReference Include="Microsoft.AspNetCore.StaticFiles" Version="1.1.3" />
  </ItemGroup>

</Project>
```

---

`<Project>`元素的`Sdk`属性完成以下任务：

* 导入中的属性文件 *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.Props*开头。
* 在结束时从 $(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.targets 导入目标文件。

`MSBuildSDKsPath`（装有 Visual Studio 2017 Enterprise）的默认位置是 %programfiles(x86)%\Microsoft Visual Studio\2017\Enterprise\MSBuild\Sdks 文件夹。

`Microsoft.NET.Sdk.Web` SDK 依赖于：

* *Microsoft.NET.Sdk.Web.ProjectSystem*
* *Microsoft.NET.Sdk.Publish*

这将导致产生以下属性和要导入的目标：

* *$ (MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.Props*
* *$ (MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.targets*
* *$ (MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.Props*
* *$ (MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.targets*

发布目标导入右侧集的目标根据使用的发布方法。

MSBuild 或 Visual Studio 将项目加载，出现以下高级操作：

* 生成项目
* 计算要发布的文件
* 将文件发布到目标

## <a name="compute-project-items"></a>计算项目项

加载项目时，将计算项目项（文件）。 `item type` 属性确定如何处理该文件。 默认情况下，.cs 文件包含在 `Compile` 项列表内。 会对 `Compile` 项列表中的文件进行编译。

`Content`项列表包含发布除了生成输出的文件。 默认情况下，文件与模式匹配的`wwwroot/**`都将纳入`Content`项。 `wwwroot/\*\*` [组合模式](https://gruntjs.com/configuring-tasks#globbing-patterns)匹配中的所有文件*wwwroot*文件夹**和**子文件夹。 若要显式将文件添加到发布列表中，添加文件直接在 *.csproj*文件中所示[包含文件](#include-files)。

选择时**发布**Visual Studio 中或从命令行发布时的按钮：

* 计算属性/项目（需要生成的文件）。
* **Visual Studio 仅**： 还原 NuGet 包。 （用户需要在 CLI 上执行显式还原。）
* 生成项目。
* 计算发布项（需要发布的文件）。
* 该项目发布 （计算的文件复制到发布目标）。

当 ASP.NET Core 项目引用`Microsoft.NET.Sdk.Web`在项目文件中， *app_offline.htm*文件放置在 web 应用程序目录的根目录。 该文件存在时，ASP.NET Core 模块会在部署过程中正常关闭该应用并提供 app_offline.htm 文件。 有关详细信息，请参阅 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module#app_offlinehtm)。

## <a name="basic-command-line-publishing"></a>基本的命令行发布

命令行发布适用于所有.NET 核心支持的平台，而且不需要 Visual Studio。 在下面的示例中[dotnet 发布](/dotnet/core/tools/dotnet-publish)从项目目录运行命令 (其中包含 *.csproj*文件)。 如果未在项目文件夹中，显式传入的项目文件路径。 例如：

```console
dotnet publish C:\Webs\Web1
```

运行以下命令以创建并发布 Web 应用：

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```console
dotnet new mvc
dotnet publish
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```console
dotnet new mvc
dotnet restore
dotnet publish
```

---

[Dotnet 发布](/dotnet/core/tools/dotnet-publish)命令生成类似于以下输出：

```console
C:\Webs\Web1>dotnet publish
Microsoft (R) Build Engine version 15.3.409.57025 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\Web1.dll
  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\publish\
```

默认发布文件夹为 `bin\$(Configuration)\netcoreapp<version>\publish`。 默认值为`$(Configuration)`是*调试*。 在前面的示例中，`<TargetFramework>`是`netcoreapp2.0`。

`dotnet publish -h` 显示用于发布的帮助信息。

以下命令指定 `Release` 生成和发布目录：

```console
dotnet publish -c Release -o C:\MyWebs\test
```

[Dotnet 发布](/dotnet/core/tools/dotnet-publish)命令调用 MSBuild，调用`Publish`目标。 任何参数传递给`dotnet publish`传递到 MSBuild。 `-c` 参数映射到 `Configuration` MSBuild 属性。 `-o` 参数映射到 `OutputPath`。

可以使用以下格式之一传递 MSBuild 属性：

* ` p:<NAME>=<VALUE>`
* `/p:<NAME>=<VALUE>`

以下命令将 `Release` 版本发布到网络共享：

`dotnet publish -c Release /p:PublishDir=//r8/release/AdminWeb`

网络共享通过正斜杠指定 (//r8/) 并适用于所有支持 .NET Core 的平台。

确认用于部署的发布应用未在运行。 如果应用正在运行，publish 文件夹中的文件会被锁定。 部署不会发生，因为无法复制锁定的文件。

## <a name="publish-profiles"></a>发布配置文件

本部分使用 Visual Studio 2017 创建发布配置文件。 创建后，从 Visual Studio 或命令行发布是可用。

发布配置文件可以简化发布的过程中，并可以存在任意数量的配置文件。 在 Visual Studio 中创建的发布配置文件，通过选择以下路径之一：

* 右键单击解决方案资源管理器中的项目并选择**发布**。
* 选择**发布&lt;文件的内容&gt;** 从**生成**菜单。

**发布**显示在应用程序容量页的选项卡。 如果项目缺少的发布配置文件，将显示的以下页面：

![应用程序容量页的发布选项卡](visual-studio-publish-profiles/_static/az.png)

当**文件夹**是选中，请指定文件夹路径来存储已发布的资产。 默认文件夹是*bin\Release\PublishOutput*。 单击**创建配置文件**按钮以完成。

发布配置文件创建后，**发布**选项卡上更改。 下拉列表中显示新创建的配置文件。 单击**创建新的配置文件**创建另一个新的配置文件。

![显示 FolderProfile 应用容量页的发布选项卡](visual-studio-publish-profiles/_static/create_new.png)

发布向导支持以下发布目标：

* Azure 应用服务
* Azure 虚拟机
* IIS、 FTP、 等 （适用于任何 web 服务器）
* 文件夹
* 导入配置文件

有关详细信息，请参阅[哪些发布选项是适合我](/visualstudio/ide/not-in-toc/web-publish-options)。

使用 Visual Studio 中，创建的发布配置文件时*属性/PublishProfiles/&lt;profile_name&gt;.pubxml*创建 MSBuild 文件。 *.Pubxml*文件是 MSBuild 文件，包含发布配置设置。 可以更改此文件为自定义生成和发布过程。 通过发布过程读取此文件。 `<LastUsedBuildConfiguration>` 是特殊的因为它的全局属性，且不应是在生成中导入任何文件中。 请参阅[MSBuild： 如何设置配置属性](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)有关详细信息。

当发布到 Azure 的目标， *.pubxml*文件包含你的 Azure 订阅标识符。 与该目标类型，不建议将此文件添加到源代码管理。 在发布到非 Azure 目标时，则可以安全地签入 *.pubxml*文件。

敏感信息 （如发布密码） 在上加密每用户/计算机级别。 存储在*属性/PublishProfiles/&lt;profile_name&gt;。 pubxml.user*文件。 此文件可以存储敏感信息，因为它不应签入源控件。

有关如何发布 web 应用程序在 ASP.NET Core 上的概述，请参阅[主机并将其部署](xref:host-and-deploy/index)。 MSBuild 任务和发布 ASP.NET Core 应用所需的目标是开放源代码在https://github.com/aspnet/websdk。

`dotnet publish` 可以使用文件夹，MSDeploy，和[Kudu](https://github.com/projectkudu/kudu/wiki)发布配置文件：

（可跨平台运行） 的文件夹：

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<FolderProfileName>
```

MSDeploy （当前此仅适用于 Windows 由于 MSDeploy 不跨平台中）：

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployProfileName> /p:Password=<DeploymentPassword>
```

MSDeploy 包 （当前此仅适用于 Windows 由于 MSDeploy 不跨平台中）：

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployPackageProfileName>
```

在前面的示例中，**不**传递`deployonbuild`到`dotnet publish`。

有关详细信息，请参阅[Microsoft.NET.Sdk.Publish](https://github.com/aspnet/websdk#microsoftnetsdkpublish)。

`dotnet publish` 支持 Kudu Api 从任何平台发布到 Azure。 Visual Studio 发布 Kudu Api，但它支持通过 WebSDK 发布到 Azure 的跨平台的支持。

添加到的发布配置文件*属性/PublishProfiles*文件夹使用以下内容：

```xml
<Project>
  <PropertyGroup>
    <PublishProtocol>Kudu</PublishProtocol>
    <PublishSiteName>nodewebapp</PublishSiteName>
    <UserName>username</UserName>
    <Password>password</Password>
  </PropertyGroup>
</Project>
```

运行以下命令以压缩发布内容，然后将其发布到 Azure 中使用 Kudu Api:

```console
dotnet publish /p:PublishProfile=Azure /p:Configuration=Release
```

使用发布配置文件时，请设置以下 MSBuild 属性：

* `DeployOnBuild=true`
* `PublishProfile=<Publish profile name>`

发布与名为配置文件时*FolderProfile*，可以执行以下命令之一：

* `dotnet build /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`
* `msbuild      /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`

在调用时[dotnet 生成](/dotnet/core/tools/dotnet-build)，它调用`msbuild`来运行生成和发布过程。 调用`dotnet build`或`msbuild`相当时传递文件夹配置文件中。 调用时 MSBuild 直接在 Windows 上，使用 MSBuild 的.NET Framework 版本。 MSDeploy 目前仅限于在 Windows 计算机上进行发布。 在非文件夹配置文件上调用 `dotnet build` 时，会调用 MSBuild，并且 MSBuild 在非文件夹配置文件上使用 MSDeploy。 在非文件夹配置文件上调用 `dotnet build` 时，会调用 MSBuild（使用 MSDeploy）并导致失败（即使在 Windows 平台上运行也是如此）。 若要使用非文件夹配置文件进行发布，请直接调用 MSBuild。

以下文件夹发布配置文件通过 Visual Studio 创建，并被发布到网络共享：

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
This file is used by the publish/package process of your Web project.
You can customize the behavior of this process by editing this 
MSBuild file.
-->
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <PublishProvider>FileSystem</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish />
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <ExcludeApp_Data>False</ExcludeApp_Data>
    <PublishFramework>netcoreapp1.1</PublishFramework>
    <ProjectGuid>c30c453c-312e-40c4-aec9-394a145dee0b</ProjectGuid>
    <publishUrl>\\r8\Release\AdminWeb</publishUrl>
    <DeleteExistingFiles>False</DeleteExistingFiles>
  </PropertyGroup>
</Project>
```

请注意，`<LastUsedBuildConfiguration>` 已设置为 `Release`。 从 Visual Studio 发布时，在启动发布过程后将使用该值设置 `<LastUsedBuildConfiguration>` 配置属性值。 `<LastUsedBuildConfiguration>`配置属性是特殊，并且不应在导入的 MSBuild 文件中重写。 从命令行，可以重写此属性。

使用.NET Core CLI:

```console
dotnet build -c Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile
```

使用 MSBuild：

```console
msbuild /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile
```

## <a name="publish-to-an-msdeploy-endpoint-from-the-command-line"></a>从命令行发布到 MSDeploy 终结点

可以使用 MSBuild 的.NET 核心 CLI 完成发布。 `dotnet publish` 在 .NET Core 的上下文中运行。 `msbuild`命令需要.NET Framework，限制为 Windows 环境。

使用 MSDeploy 发布的最简单的方法是，首先在 Visual Studio 2017 中创建发布配置文件，然后从命令行中使用配置文件。

在下面的示例中，创建一个 ASP.NET 核心 web 应用 (使用`dotnet new mvc`)，并使用 Visual Studio 添加 Azure 发布配置文件。

运行`msbuild`从**VS 2017 的开发人员命令提示符**。 开发人员命令提示已正确*msbuild.exe*在与某些 MSBuild 变量集其路径中。

MSBuild 使用以下语法：

```console
msbuild <path-to-project-file> /p:DeployOnBuild=true /p:PublishProfile=<Publish Profile> /p:Username=<USERNAME> /p:Password=<PASSWORD>
```

获取`Password`从*\<发布名称 >。PublishSettings*文件。 下载*。PublishSettings*从文件：

* 解决方案资源管理器： 在 Web 应用上右键单击并选择**下载发布配置文件**。
* Azure 门户： 单击**Get 发布配置文件**Web 应用上**概述**面板。

可在发布配置文件中找到 `Username`。

下面的示例使用*Web11112-Web 部署*发布配置文件：

```console
msbuild "C:\Webs\Web1\Web1.csproj" /p:DeployOnBuild=true
 /p:PublishProfile="Web11112 - Web Deploy"  /p:Username="$Web11112"
 /p:Password="<password removed>"
```

## <a name="exclude-files"></a>排除文件

在发布 ASP.NET Core Web 应用时，生成项目和 wwwroot 文件夹的内容包括在内。 `msbuild` 支持[通配模式](https://gruntjs.com/configuring-tasks#globbing-patterns)。 例如，以下`<Content>`元素排除的所有文本 (*.txt*) 从文件*wwwroot/content*文件夹和所有子文件夹。

```xml
<ItemGroup>
  <Content Update="wwwroot/content/**/*.txt" CopyToPublishDirectory="Never" />
</ItemGroup>
```

前面的标记可以添加到发布配置文件或 *.csproj*文件。 添加到 .csproj 文件时，会将该规则添加到项目中的所有发布配置文件中。

以下`<MsDeploySkipRules>`元素排除中的所有文件*wwwroot/content*文件夹：

```xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFolder">
    <ObjectName>dirPath</ObjectName>
    <AbsolutePath>wwwroot\\content</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

`<MsDeploySkipRules>` 不会删除*跳过*部署站点中的目标。 `<Content>` 从部署站点删除目标的文件和文件夹。 例如，假设已部署的 web 应用程序有以下文件：

* *Views/Home/About1.cshtml*
* *Views/Home/About2.cshtml*
* *Views/Home/About3.cshtml*

如果以下`<MsDeploySkipRules>`添加元素，不会在部署站点上删除这些文件。

```xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About1.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About2.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About3.cshtml</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

前面`<MsDeploySkipRules>`元素防止*跳过*不会部署的文件。 它们在部署后，它不会删除这些文件。

以下`<Content>`元素删除在部署站点的目标的文件：

```xml
<ItemGroup>
  <Content Update="Views/Home/About?.cshtml" CopyToPublishDirectory="Never" />
</ItemGroup>
```

使用命令行部署前面`<Content>`元素生成下面的输出：

```console
MSDeployPublish:
  Starting Web deployment task from source: manifest(C:\Webs\Web1\obj\Release\netcoreapp1.1\PubTmp\Web1.SourceManifest.
  xml) to Destination: auto().
  Deleting file (Web11112\Views\Home\About1.cshtml).
  Deleting file (Web11112\Views\Home\About2.cshtml).
  Deleting file (Web11112\Views\Home\About3.cshtml).
  Updating file (Web11112\web.config).
  Updating file (Web11112\Web1.deps.json).
  Updating file (Web11112\Web1.dll).
  Updating file (Web11112\Web1.pdb).
  Updating file (Web11112\Web1.runtimeconfig.json).
  Successfully executed Web deployment task.
  Publish Succeeded.
Done Building Project "C:\Webs\Web1\Web1.csproj" (default targets).
```

## <a name="include-files"></a>包含文件

以下标记包括*映像*文件夹到在项目目录外的*wwwroot/images*发布站点文件夹：

```xml
<ItemGroup>
  <_CustomFiles Include="$(MSBuildProjectDirectory)/../images/**/*" />
  <DotnetPublishFiles Include="@(_CustomFiles)">
    <DestinationRelativePath>wwwroot/images/%(RecursiveDir)%(Filename)%(Extension)</DestinationRelativePath>
  </DotnetPublishFiles>
</ItemGroup>
```

可以将标记添加到 .csproj 文件或发布配置文件。 如果将其添加到 *.csproj*文件，它包含在项目中每个发布配置文件中。

以下突出显示的标记显示如何：

* 将文件从项目外部复制到 wwwroot 文件夹。
* 排除 wwwroot\Content 文件夹。
* 排除 Views\Home\About2.cshtml。

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
This file is used by the publish/package process of your Web project.
You can customize the behavior of this process by editing this 
MSBuild file.
-->
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <PublishProvider>FileSystem</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish />
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <ExcludeApp_Data>False</ExcludeApp_Data>
    <PublishFramework />
    <ProjectGuid>afa9f185-7ce0-4935-9da1-ab676229d68a</ProjectGuid>
    <publishUrl>bin\Release\PublishOutput</publishUrl>
    <DeleteExistingFiles>False</DeleteExistingFiles>
  </PropertyGroup>
  <ItemGroup>
    <ResolvedFileToPublish Include="..\ReadMe2.MD">
      <RelativePath>wwwroot\ReadMe2.MD</RelativePath>
    </ResolvedFileToPublish>

    <Content Update="wwwroot\Content\**\*" CopyToPublishDirectory="Never" />
    <Content Update="Views\Home\About2.cshtml" CopyToPublishDirectory="Never" />

  </ItemGroup>
</Project>
```

请参阅 [WebSDK 自述文件](https://github.com/aspnet/websdk)，了解更多部署示例。

## <a name="run-a-target-before-or-after-publishing"></a>在发布前或发布后运行目标

内置`BeforePublish`和`AfterPublish`目标执行目标之前或之后发布目标。 将以下元素添加到要记录控制台消息之前和之后发布的发布配置文件：

```xml
<Target Name="CustomActionsBeforePublish" BeforeTargets="BeforePublish">
    <Message Text="Inside BeforePublish" Importance="high" />
  </Target>
  <Target Name="CustomActionsAfterPublish" AfterTargets="AfterPublish">
    <Message Text="Inside AfterPublish" Importance="high" />
</Target>
```

## <a name="publish-to-a-server-using-an-untrusted-certificate"></a>将发布到使用不受信任的证书的服务器

添加`<AllowUntrustedCertificate>`属性值为`True`到发布配置文件：

```xml
<PropertyGroup>
  <AllowUntrustedCertificate>True</AllowUntrustedCertificate>
</PropertyGroup>
```

## <a name="the-kudu-service"></a>Kudu 服务

若要在 Azure App Service web 应用程序部署中查看的文件，使用[Kudu 服务](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service)。 追加`scm`令牌 web 应用名。 例如：

| URL                                    | 结果       |
| -------------------------------------- | ------------ |
| `http://mysite.azurewebsites.net/`     | Web 应用      |
| `http://mysite.scm.azurewebsites.net/` | Kudu 服务 |

选择[调试控制台](https://github.com/projectkudu/kudu/wiki/Kudu-console)菜单项以查看、 编辑、 删除或添加文件。

## <a name="additional-resources"></a>其他资源

* [Web 部署](https://www.iis.net/downloads/microsoft/web-deploy)(MSDeploy) 简化了部署 web 应用和到 IIS 服务器的网站。
* [https://github.com/aspnet/websdk](https://github.com/aspnet/websdk/issues)： 文件的问题并请求适用于部署的功能。
