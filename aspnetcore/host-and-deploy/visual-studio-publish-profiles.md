---
title: 用于 ASP.NET Core 应用部署的 Visual Studio 发布配置文件
author: rick-anderson
description: 了解如何在 Visual Studio 中创建发布配置文件，并将它们用于管理针对各种目标的 ASP.NET Core 应用部署。
ms.author: riande
ms.custom: mvc
ms.date: 04/10/2018
uid: host-and-deploy/visual-studio-publish-profiles
ms.openlocfilehash: 751f25f74a0e24eb9ce4f2bd6b2fa462ccb03ecb
ms.sourcegitcommit: a742b55e4b8276a48b8b4394784554fecd883c84
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2018
ms.locfileid: "45538396"
---
# <a name="visual-studio-publish-profiles-for-aspnet-core-app-deployment"></a>用于 ASP.NET Core 应用部署的 Visual Studio 发布配置文件

作者：[Sayed Ibrahim Hashimi](https://github.com/sayedihashimi) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)

本文档重点介绍如何使用 Visual Studio 2017 创建并使用发布配置文件。 可以从 MSBuild 和 Visual Studio 2017 运行使用 Visual Studio 创建的发布配置文件。 有关发布到 Azure 的说明，请参阅[使用 Visual Studio 将 ASP.NET Core Web 应用发布到 Azure App Service](xref:tutorials/publish-to-azure-webapp-using-vs)。

使用命令 `dotnet new mvc` 创建以下项目文件：

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.All" Version="2.1.4" />
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

`<Project>` 元素的 `Sdk` 属性完成以下任务：

* 在开始时从 $(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.Props 导入属性文件。
* 在结束时从 $(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.targets 导入目标文件。

`MSBuildSDKsPath`（装有 Visual Studio 2017 Enterprise）的默认位置是 %programfiles(x86)%\Microsoft Visual Studio\2017\Enterprise\MSBuild\Sdks 文件夹。

`Microsoft.NET.Sdk.Web` SDK 依赖于：

* *Microsoft.NET.Sdk.Web.ProjectSystem*
* *Microsoft.NET.Sdk.Publish*

它们会导致导入以下属性和目标：

* $(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.Props
* $(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.targets
* $(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.Props
* $(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.targets

发布目标将根据使用的发布方法，导入正确的目标集。

MSBuild 或 Visual Studio 加载项目时，执行下列高级别操作：

* 生成项目
* 计算要发布的文件
* 将文件发布到目标

## <a name="compute-project-items"></a>计算项目项

加载项目时，将计算项目项（文件）。 `item type` 属性确定如何处理该文件。 默认情况下，.cs 文件包含在 `Compile` 项列表内。 会对 `Compile` 项列表中的文件进行编译。

除了生成输出，`Content` 项列表还包含已发布的文件。 默认情况下，匹配模式 `wwwroot/**` 的文件将包含在 `Content` 项内。 `wwwroot/\*\*` [glob 模式](https://gruntjs.com/configuring-tasks#globbing-patterns) 匹配 wwwroot 文件夹及其子文件夹中的所有文件。 若要将文件显式添加到发布列表，请直接在 .csproj 文件中添加文件，如[包含文件](#include-files)中所示。

在 Visual Studio 中选择“发布”按钮时或从命令行发布时：

* 计算属性/项目（需要生成的文件）。
* 仅限 Visual Studio：还原 NuGet 包。 （用户需要在 CLI 上执行显式还原。）
* 生成项目。
* 计算发布项（需要发布的文件）。
* 文件已发布（计算的文件将被复制到发布目标）。

当 ASP.NET Core 项目在项目文件中引用 `Microsoft.NET.Sdk.Web` 时，会将 app_offline.htm 文件放在 Web 应用目录的根目录下。 该文件存在时，ASP.NET Core 模块会在部署过程中正常关闭该应用并提供 app_offline.htm 文件。 有关详细信息，请参阅 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module#app_offlinehtm)。

## <a name="basic-command-line-publishing"></a>基本命令行发布

命令行发布适用于所有支持 .NET Core 的平台，而且不需要 Visual Studio。 在下面的示例中，从项目目录（其中包含 .csproj 文件）运行 [dotnet publish](/dotnet/core/tools/dotnet-publish) 命令。 如果不在项目文件夹中，则可以在项目文件路径中显式传递。 例如:

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

[dotnet publish](/dotnet/core/tools/dotnet-publish) 命令生成类似下面的输出：

```console
C:\Webs\Web1>dotnet publish
Microsoft (R) Build Engine version 15.3.409.57025 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\Web1.dll
  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\publish\
```

默认发布文件夹为 `bin\$(Configuration)\netcoreapp<version>\publish`。 `$(Configuration)` 的默认值为 Debug。 在上述示例中，`<TargetFramework>` 是 `netcoreapp2.0`。

`dotnet publish -h` 显示用于发布的帮助信息。

以下命令指定 `Release` 生成和发布目录：

```console
dotnet publish -c Release -o C:\MyWebs\test
```

[dotnet publish](/dotnet/core/tools/dotnet-publish) 命令调用 MSBuild，它调用 `Publish` 目标。 任何传递给 `dotnet publish` 的参数都将传递给 MSBuild。 `-c` 参数映射到 `Configuration` MSBuild 属性。 `-o` 参数映射到 `OutputPath`。

可以使用以下任一格式来传递 MSBuild 属性：

* ` p:<NAME>=<VALUE>`
* `/p:<NAME>=<VALUE>`

以下命令将 `Release` 版本发布到网络共享：

`dotnet publish -c Release /p:PublishDir=//r8/release/AdminWeb`

网络共享通过正斜杠指定 (//r8/) 并适用于所有支持 .NET Core 的平台。

确认用于部署的发布应用未在运行。 如果应用正在运行，publish 文件夹中的文件会被锁定。 部署不会发生，因为无法复制锁定的文件。

## <a name="publish-profiles"></a>发布配置文件

本部分使用 Visual Studio 2017 创建发布配置文件。 创建后，可以从 Visual Studio 或命令行中发布。

发布配置文件可以简化发布过程，并且可以存在任意数量的配置文件。 通过选择以下路径之一在 Visual Studio 中创建发布配置文件：

* 在解决方案资源管理器中右键单击该项目，然后选择“发布”。
* 可以从“生成”菜单中选择发布 &lt;project_name&gt;。

随即显示应用程序容量页的“发布”选项卡。 如果项目缺少发布配置文件，将显示以下页面：

![随即显示应用程序容量页的“发布”选项卡](visual-studio-publish-profiles/_static/az.png)

当选择“文件夹”时，指定一个文件夹路径来存储发布的资产。 默认文件夹是 bin\Release\PublishOutput。 单击“创建配置文件”按钮即可完成。

创建发布配置文件后，“发布”选项卡将更改。 新创建的配置文件显示在下拉列表中。 单击“创建新配置文件”以创建其他新配置文件。

![显示 FolderProfile 的应用程序容量页的“发布”选项卡](visual-studio-publish-profiles/_static/create_new.png)

发布向导支持以下发布目标：

* Azure 应用服务
* Azure 虚拟机
* IIS、FTP 等（适用于任何 Web 服务器）
* 文件夹
* 导入配置文件

有关详细信息，请参阅[哪些发布选项适合我](/visualstudio/ide/not-in-toc/web-publish-options)。

使用 Visual Studio 创建发布配置文件时，将创建 Properties/PublishProfiles/&lt;profile_name&gt;.pubxml MSBuild 文件。 此 .pubxml 文件为 MSBuild 文件，包含发布配置设置。 可以更改此文件以自定义生成和发布过程。 通过发布过程读取此文件。 `<LastUsedBuildConfiguration>` 比较特殊，因为它是一个全局属性，不应出现在导入生成的任何文件中。 有关详细信息，请参阅 [MSBuild：如何设置配置属性](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)。

发布到 Azure 目标时，.pubxml 文件包含 Azure 订阅标识符。 不建议使用该目标类型将此文件添加到源代码管理。 发布到非 Azure 目标时，签入 .pubxml 文件是安全的。

敏感信息（如发布密码）在每个用户/机器级别均进行加密。 它存储在 Properties/PublishProfiles/&lt;profile_name&gt;.pubxml.user 文件中。 由于此文件可以存储敏感信息，因此不应将其签入源代码管理。

有关如何在 ASP.NET Core 上发布 Web 应用的概述，请参阅[托管和部署](xref:host-and-deploy/index)。 发布 ASP.NET Core 应用程序所需的 MSBuild 任务和目标是开放源代码，位于： https://github.com/aspnet/websdk。

`dotnet publish` 可以使用文件夹、MSDeploy 和 [Kudu](https://github.com/projectkudu/kudu/wiki) 发布配置文件：

文件夹（跨平台工作）：

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<FolderProfileName>
```

MSDeploy（当前仅适用于 Windows，因为 MSDeploy 不是跨平台的）：

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployProfileName> /p:Password=<DeploymentPassword>
```

MSDeploy 包（当前仅适用于 Windows，因为 MSDeploy 不是跨平台的）：

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployPackageProfileName>
```

在前面示例中，不会将 `deployonbuild` 传递到 `dotnet publish`。

有关详细信息，请参阅 [Microsoft.NET.Sdk.Publish](https://github.com/aspnet/websdk#microsoftnetsdkpublish)。

`dotnet publish` 支持 Kudu API 从任何平台发布到 Azure。 Visual Studio 发布支持 Kudu API，但 WebSDK 支持其跨平台发布到 Azure。

向“属性/发布配置文件”文件夹添加包含以下内容的发布配置文件：

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

运行以下命令将会压缩发布内容并将其发布到使用 Kudu API 的 Azure：

```console
dotnet publish /p:PublishProfile=Azure /p:Configuration=Release
```

使用发布配置文件时，请设置以下 MSBuild 属性：

* `DeployOnBuild=true`
* `PublishProfile=<Publish profile name>`

发布名为 FolderProfile 的配置文件时，可以执行以下命令之一：

* `dotnet build /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`
* `msbuild      /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`

调用 [dotnet build](/dotnet/core/tools/dotnet-build) 时，它调用 `msbuild` 来运行生成和发布过程。 当传递到文件夹配置文件中时，调用 `dotnet build` 或 `msbuild` 的作用是相同的。 在 Windows 上直接调用 MSBuild 时，将使用 MSBuild 的 .NET Framework 版本。 MSDeploy 目前仅限于在 Windows 计算机上进行发布。 在非文件夹配置文件上调用 `dotnet build` 时，会调用 MSBuild，并且 MSBuild 在非文件夹配置文件上使用 MSDeploy。 在非文件夹配置文件上调用 `dotnet build` 时，会调用 MSBuild（使用 MSDeploy）并导致失败（即使在 Windows 平台上运行也是如此）。 若要使用非文件夹配置文件进行发布，请直接调用 MSBuild。

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

请注意，`<LastUsedBuildConfiguration>` 已设置为 `Release`。 从 Visual Studio 发布时，在启动发布过程后将使用该值设置 `<LastUsedBuildConfiguration>` 配置属性值。 `<LastUsedBuildConfiguration>` 配置属性比较特殊，不应在导入的 MSBuild 文件中覆盖该属性。 可以从命令行覆盖此属性。

使用 .NET Core CLI：

```console
dotnet build -c Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile
```

使用 MSBuild：

```console
msbuild /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile
```

## <a name="publish-to-an-msdeploy-endpoint-from-the-command-line"></a>从命令行发布到 MSDeploy 终结点

可以使用 .NET Core CLI 或 MSBuild 完成发布。 `dotnet publish` 在 .NET Core 的上下文中运行。 `msbuild` 命令需要 .NET Framework，它将该命令限制到 Windows 环境。

使用 MSDeploy 发布的最简单的方法是，首先在 Visual Studio 2017 中创建发布配置文件，然后从命令行中使用配置文件。

下面的示例中创建了一个 ASP.NET Core Web应用（使用 `dotnet new mvc`），并且通过 Visual Studio 添加了一个 Azure 发布配置文件。

从 VS 2017 开发人员命令提示符中运行 `msbuild`。 开发人员命令提示符在其路径中将具有正确的 msbuild.exe，并会设置一些 MSBuild 变量。

MSBuild 使用以下语法：

```console
msbuild <path-to-project-file> /p:DeployOnBuild=true /p:PublishProfile=<Publish Profile> /p:Username=<USERNAME> /p:Password=<PASSWORD>
```

可以从 \<Publish name>.PublishSettings 文件获取 `Password`。 可以从以下位置下载 .PublishSettings 文件：

* 解决方案资源管理器：右键单击 Web 应用并选择“下载发布配置文件”。
* Azure 门户：单击 Web 应用“概述”面板上的“获取发布配置文件”。

可在发布配置文件中找到 `Username`。

以下示例使用“Web11112 - Web 部署”发布配置文件：

```console
msbuild "C:\Webs\Web1\Web1.csproj" /p:DeployOnBuild=true
 /p:PublishProfile="Web11112 - Web Deploy"  /p:Username="$Web11112"
 /p:Password="<password removed>"
```

## <a name="exclude-files"></a>排除文件

在发布 ASP.NET Core Web 应用时，生成项目和 wwwroot 文件夹的内容包括在内。 `msbuild` 支持[通配模式](https://gruntjs.com/configuring-tasks#globbing-patterns)。 例如，以下 `<Content>` 元素将从 wwwroot/content 文件夹及其所有子文件夹中排除所有文本 (.txt) 文件。

```xml
<ItemGroup>
  <Content Update="wwwroot/content/**/*.txt" CopyToPublishDirectory="Never" />
</ItemGroup>
```

可以将上面的标记添加到发布配置文件或 .csproj 文件。 添加到 .csproj 文件时，会将该规则添加到项目中的所有发布配置文件中。

以下 `<MsDeploySkipRules>` 元素排除 wwwroot/content 文件夹中的所有文件：

```xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFolder">
    <ObjectName>dirPath</ObjectName>
    <AbsolutePath>wwwroot\\content</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

`<MsDeploySkipRules>` 不会从部署站点删除跳过目标。 从部署站点中删除 `<Content>` 目标文件和文件夹。 例如，假设部署的 Web 应用具有以下文件：

* *Views/Home/About1.cshtml*
* *Views/Home/About2.cshtml*
* *Views/Home/About3.cshtml*

如果添加了以下 `<MsDeploySkipRules>` 元素，则不会在部署站点上删除这些文件。

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

之前的 `<MsDeploySkipRules>` 元素阻止部署跳过的文件。 一旦部署这些文件就不会删除它们。

以下 `<Content>` 元素将在部署站点中删除目标文件：

```xml
<ItemGroup>
  <Content Update="Views/Home/About?.cshtml" CopyToPublishDirectory="Never" />
</ItemGroup>
```

使用具有上述 `<Content>` 元素的命令行部署可生成以下输出：

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

以下标记将项目目录外的 images 文件夹包含到发布站点的 wwwroot/images 文件夹中：

```xml
<ItemGroup>
  <_CustomFiles Include="$(MSBuildProjectDirectory)/../images/**/*" />
  <DotnetPublishFiles Include="@(_CustomFiles)">
    <DestinationRelativePath>wwwroot/images/%(RecursiveDir)%(Filename)%(Extension)</DestinationRelativePath>
  </DotnetPublishFiles>
</ItemGroup>
```

可以将标记添加到 .csproj 文件或发布配置文件。 如果将其添加到 .csproj 文件，它会包含在项目的每个发布配置文件中。

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

内置 `BeforePublish` 和 `AfterPublish` 目标在发布目标前/后执行目标。 将以下元素添加到发布配置文件，以在发布前/后均记录控制台消息：

```xml
<Target Name="CustomActionsBeforePublish" BeforeTargets="BeforePublish">
    <Message Text="Inside BeforePublish" Importance="high" />
  </Target>
  <Target Name="CustomActionsAfterPublish" AfterTargets="AfterPublish">
    <Message Text="Inside AfterPublish" Importance="high" />
</Target>
```

## <a name="publish-to-a-server-using-an-untrusted-certificate"></a>使用不受信任的证书发布到服务器

将值为 `True` 的 `<AllowUntrustedCertificate>` 属性添加到发布配置文件：

```xml
<PropertyGroup>
  <AllowUntrustedCertificate>True</AllowUntrustedCertificate>
</PropertyGroup>
```

## <a name="the-kudu-service"></a>Kudu 服务

要查看 Azure 应用服务 Web 应用部署中的文件，请使用 [Kudu 服务](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service)。 将 `scm` 令牌追加到 Web 应用名称。 例如:

| URL                                    | 结果       |
| -------------------------------------- | ------------ |
| `http://mysite.azurewebsites.net/`     | Web 应用      |
| `http://mysite.scm.azurewebsites.net/` | Kudu 服务 |

选择[调试控制台](https://github.com/projectkudu/kudu/wiki/Kudu-console)菜单项来查看、编辑、删除或添加文件。

## <a name="additional-resources"></a>其他资源

* [Web 部署](https://www.iis.net/downloads/microsoft/web-deploy) (MSDeploy) 简化了 Web 应用和网站到 IIS 服务器的部署。
* [https://github.com/aspnet/websdk](https://github.com/aspnet/websdk/issues)：文件问题和部署的请求功能。
* [从 Visual Studio 将 ASP.NET Web 应用发布到 Azure VM](/azure/virtual-machines/windows/publish-web-app-from-visual-studio)
