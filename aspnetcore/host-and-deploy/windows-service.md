---
title: 在 Windows 服务中托管 ASP.NET Core
author: guardrex
description: 了解如何在 Windows 服务中托管 ASP.NET Core 应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 10/30/2018
uid: host-and-deploy/windows-service
ms.openlocfilehash: 11913019bfe5d06c259b806fce9cc580a8280ad5
ms.sourcegitcommit: fc2486ddbeb15ab4969168d99b3fe0fbe91e8661
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2018
ms.locfileid: "50758188"
---
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="e7a39-103">在 Windows 服务中托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e7a39-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="e7a39-104">作者：[Luke Latham](https://github.com/guardrex)、[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e7a39-104">By [Luke Latham](https://github.com/guardrex) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="e7a39-105">不将 IIS 用作 [Windows 服务](/dotnet/framework/windows-services/introduction-to-windows-service-applications)时，可在 Windows 上托管 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="e7a39-105">An ASP.NET Core app can be hosted on Windows without using IIS as a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="e7a39-106">作为 Windows 服务进行托管时，应用将在重新启动后自动启动。</span><span class="sxs-lookup"><span data-stu-id="e7a39-106">When hosted as a Windows Service, the app automatically starts after reboots.</span></span>

<span data-ttu-id="e7a39-107">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="e7a39-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="convert-a-project-into-a-windows-service"></a><span data-ttu-id="e7a39-108">将项目转换为 Windows 服务</span><span class="sxs-lookup"><span data-stu-id="e7a39-108">Convert a project into a Windows Service</span></span>

<span data-ttu-id="e7a39-109">要将现有 ASP.NET Core 项目设置为作为服务运行，至少需要执行以下更改：</span><span class="sxs-lookup"><span data-stu-id="e7a39-109">The following minimum changes are required to set up an existing ASP.NET Core project to run as a service:</span></span>

1. <span data-ttu-id="e7a39-110">在项目文件中：</span><span class="sxs-lookup"><span data-stu-id="e7a39-110">In the project file:</span></span>

   * <span data-ttu-id="e7a39-111">确认是否存在 Windows [运行时标识符 (RID)](/dotnet/core/rid-catalog)，或将其添加到包含目标框架的 `<PropertyGroup>` 中：</span><span class="sxs-lookup"><span data-stu-id="e7a39-111">Confirm the presence of a Windows [Runtime Identifier (RID)](/dotnet/core/rid-catalog) or add it to the `<PropertyGroup>` that contains the target framework:</span></span>

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp2.2</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      <span data-ttu-id="e7a39-112">要发布多个 RID：</span><span class="sxs-lookup"><span data-stu-id="e7a39-112">To publish for multiple RIDs:</span></span>

      * <span data-ttu-id="e7a39-113">通过以分号分隔的列表提供 RID。</span><span class="sxs-lookup"><span data-stu-id="e7a39-113">Provide the RIDs in a semicolon-delimited list.</span></span>
      * <span data-ttu-id="e7a39-114">使用属性名称 `<RuntimeIdentifiers>`（复数）。</span><span class="sxs-lookup"><span data-stu-id="e7a39-114">Use the property name `<RuntimeIdentifiers>` (plural).</span></span>

      <span data-ttu-id="e7a39-115">有关详细信息，请参阅 [.NET Core RID 目录](/dotnet/core/rid-catalog)。</span><span class="sxs-lookup"><span data-stu-id="e7a39-115">For more information, see [.NET Core RID Catalog](/dotnet/core/rid-catalog).</span></span>

   * <span data-ttu-id="e7a39-116">为 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices) 添加包引用。</span><span class="sxs-lookup"><span data-stu-id="e7a39-116">Add a package reference for [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices).</span></span>

1. <span data-ttu-id="e7a39-117">在 `Program.Main` 中，进行下列更改：</span><span class="sxs-lookup"><span data-stu-id="e7a39-117">Make the following changes in `Program.Main`:</span></span>

   * <span data-ttu-id="e7a39-118">调用 [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)，而不是 `host.Run`。</span><span class="sxs-lookup"><span data-stu-id="e7a39-118">Call [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice) instead of `host.Run`.</span></span>

   * <span data-ttu-id="e7a39-119">调用 [UseContentRoot](xref:fundamentals/host/web-host#content-root) 并使用应用的发布位置路径，而不是 `Directory.GetCurrentDirectory()`。</span><span class="sxs-lookup"><span data-stu-id="e7a39-119">Call [UseContentRoot](xref:fundamentals/host/web-host#content-root) and use a path to the app's published location instead of `Directory.GetCurrentDirectory()`.</span></span>

     [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=8-9,16)]

1. <span data-ttu-id="e7a39-120">使用 [dotnet publish](/dotnet/articles/core/tools/dotnet-publish)、[Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles) 或 Visual Studio Code 发布应用。</span><span class="sxs-lookup"><span data-stu-id="e7a39-120">Publish the app using [dotnet publish](/dotnet/articles/core/tools/dotnet-publish), a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles), or Visual Studio Code.</span></span> <span data-ttu-id="e7a39-121">使用 Visual Studio 时，先选择“FolderProfile”并配置“目标位置”，再选择“发布”按钮。</span><span class="sxs-lookup"><span data-stu-id="e7a39-121">When using Visual Studio, select the **FolderProfile** and configure the **Target Location** before selecting the **Publish** button.</span></span>

   <span data-ttu-id="e7a39-122">要使用命令行接口 (CLI) 工具发布示例应用，请在项目文件夹的命令提示符处运行 [dotnet publish](/dotnet/core/tools/dotnet-publish) 命令。</span><span class="sxs-lookup"><span data-stu-id="e7a39-122">To publish the sample app using command-line interface (CLI) tools, run the [dotnet publish](/dotnet/core/tools/dotnet-publish) command at a command prompt from the project folder.</span></span> <span data-ttu-id="e7a39-123">必须在项目文件的 `<RuntimeIdenfifier>`（或 `<RuntimeIdentifiers>`）属性中指定 RID。</span><span class="sxs-lookup"><span data-stu-id="e7a39-123">The RID must be specified in the `<RuntimeIdenfifier>` (or `<RuntimeIdentifiers>`) property of the project file.</span></span> <span data-ttu-id="e7a39-124">在下面的示例中，应用是通过 `win7-x64` 运行时的“发布”配置发布到在 c:\\svc 中创建的文件夹：</span><span class="sxs-lookup"><span data-stu-id="e7a39-124">In the following example, the app is published in Release configuration for the `win7-x64` runtime to a folder created at *c:\\svc*:</span></span>

   ```console
   dotnet publish --configuration Release --runtime win7-x64 --output c:\svc
   ```

1. <span data-ttu-id="e7a39-125">运行 `net user` 命令，创建服务用户帐户：</span><span class="sxs-lookup"><span data-stu-id="e7a39-125">Create a user account for the service using the `net user` command:</span></span>

   ```console
   net user {USER ACCOUNT} {PASSWORD} /add
   ```

   <span data-ttu-id="e7a39-126">对于示例应用，使用用户名 `ServiceUser` 和密码创建用户帐户。</span><span class="sxs-lookup"><span data-stu-id="e7a39-126">For the sample app, create a user account with the name `ServiceUser` and a password.</span></span> <span data-ttu-id="e7a39-127">在下面的命令中，将 `{PASSWORD}` 替换为[强密码](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements)。</span><span class="sxs-lookup"><span data-stu-id="e7a39-127">In the following command, replace `{PASSWORD}` with a [strong password](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements).</span></span>

   ```console
   net user ServiceUser {PASSWORD} /add
   ```

   <span data-ttu-id="e7a39-128">如果需要将用户添加到组中，请运行 `net localgroup` 命令（其中 `{GROUP}` 是组名称）：</span><span class="sxs-lookup"><span data-stu-id="e7a39-128">If you need to add the user to a group, use the `net localgroup` command, where `{GROUP}` is the name of the group:</span></span>

   ```console
   net localgroup {GROUP} {USER ACCOUNT} /add
   ```

   <span data-ttu-id="e7a39-129">有关详细信息，请参阅[服务用户帐户](/windows/desktop/services/service-user-accounts)。</span><span class="sxs-lookup"><span data-stu-id="e7a39-129">For more information, see [Service User Accounts](/windows/desktop/services/service-user-accounts).</span></span>

1. <span data-ttu-id="e7a39-130">运行 [icacls](/windows-server/administration/windows-commands/icacls) 命令，授予对应用文件夹的写入/读取/执行权限：</span><span class="sxs-lookup"><span data-stu-id="e7a39-130">Grant write/read/execute access to the app's folder using the [icacls](/windows-server/administration/windows-commands/icacls) command:</span></span>

   ```console
   icacls "{PATH}" /grant {USER ACCOUNT}:(OI)(CI){PERMISSION FLAGS} /t
   ```

   * <span data-ttu-id="e7a39-131">`{PATH}` &ndash; 应用文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="e7a39-131">`{PATH}` &ndash; Path to the app's folder.</span></span>
   * <span data-ttu-id="e7a39-132">`{USER ACCOUNT}` &ndash; 用户帐户 (SID)。</span><span class="sxs-lookup"><span data-stu-id="e7a39-132">`{USER ACCOUNT}` &ndash; The user account (SID).</span></span>
   * <span data-ttu-id="e7a39-133">`(OI)` &ndash; 对象继承标志将权限传播给从属文件。</span><span class="sxs-lookup"><span data-stu-id="e7a39-133">`(OI)` &ndash; The Object Inherit flag propagates permissions to subordinate files.</span></span>
   * <span data-ttu-id="e7a39-134">`(CI)` &ndash; 容器继承标志将权限传播给从属文件夹。</span><span class="sxs-lookup"><span data-stu-id="e7a39-134">`(CI)` &ndash; The Container Inherit flag propagates permissions to subordinate folders.</span></span>
   * <span data-ttu-id="e7a39-135">`{PERMISSION FLAGS}` &ndash; 设置应用的访问权限。</span><span class="sxs-lookup"><span data-stu-id="e7a39-135">`{PERMISSION FLAGS}` &ndash; Sets the app's access permissions.</span></span>
     * <span data-ttu-id="e7a39-136">写入 (`W`)</span><span class="sxs-lookup"><span data-stu-id="e7a39-136">Write (`W`)</span></span>
     * <span data-ttu-id="e7a39-137">读取 (`R`)</span><span class="sxs-lookup"><span data-stu-id="e7a39-137">Read (`R`)</span></span>
     * <span data-ttu-id="e7a39-138">执行 (`X`)</span><span class="sxs-lookup"><span data-stu-id="e7a39-138">Execute (`X`)</span></span>
     * <span data-ttu-id="e7a39-139">完全 (`F`)</span><span class="sxs-lookup"><span data-stu-id="e7a39-139">Full (`F`)</span></span>
     * <span data-ttu-id="e7a39-140">修改 (`M`)</span><span class="sxs-lookup"><span data-stu-id="e7a39-140">Modify (`M`)</span></span>
   * <span data-ttu-id="e7a39-141">`/t` &ndash; 以递归方式应用于现有从属文件夹和文件。</span><span class="sxs-lookup"><span data-stu-id="e7a39-141">`/t` &ndash; Apply recursively to existing subordinate folders and files.</span></span>

   <span data-ttu-id="e7a39-142">对于发布到 c:\\sv 文件夹的示例应用，以及拥有写入/读取/执行权限的 `ServiceUser` 帐户，请运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="e7a39-142">For the sample app published to the *c:\\svc* folder and the `ServiceUser` account with write/read/execute permissions, use the following command:</span></span>

   ```console
   icacls "c:\svc" /grant ServiceUser:(OI)(CI)WRX /t
   ```

   <span data-ttu-id="e7a39-143">有关详细信息，请参阅 [icacls](/windows-server/administration/windows-commands/icacls)。</span><span class="sxs-lookup"><span data-stu-id="e7a39-143">For more information, see [icacls](/windows-server/administration/windows-commands/icacls).</span></span>

1. <span data-ttu-id="e7a39-144">使用 [sc.exe](https://technet.microsoft.com/library/bb490995) 命令行工具创建服务。</span><span class="sxs-lookup"><span data-stu-id="e7a39-144">Use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create the service.</span></span> <span data-ttu-id="e7a39-145">`binPath` 值是应用的可执行文件的路径，其中包括可执行文件的文件名。</span><span class="sxs-lookup"><span data-stu-id="e7a39-145">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span> <span data-ttu-id="e7a39-146">每个参数和值的等于号和引号字符之间必须有空格。</span><span class="sxs-lookup"><span data-stu-id="e7a39-146">**The space between the equal sign and the quote character of each parameter and value is required.**</span></span>

   ```console
   sc create {SERVICE NAME} binPath= "{PATH}" obj= "{DOMAIN}\{USER ACCOUNT}" password= "{PASSWORD}"
   ```

   * <span data-ttu-id="e7a39-147">`{SERVICE NAME}` &ndash; 要在[服务控制管理器](/windows/desktop/services/service-control-manager)中分配给服务的名称。</span><span class="sxs-lookup"><span data-stu-id="e7a39-147">`{SERVICE NAME}` &ndash; The name to assign to the service in [Service Control Manager](/windows/desktop/services/service-control-manager).</span></span>
   * <span data-ttu-id="e7a39-148">`{PATH}` &ndash; 可执行服务的路径。</span><span class="sxs-lookup"><span data-stu-id="e7a39-148">`{PATH}` &ndash; The path to the service executable.</span></span>
   * <span data-ttu-id="e7a39-149">`{DOMAIN}`（或为本地计算机名称，如果计算机不是域加入的话）；以及 `{USER ACCOUNT}` &ndash; 域（或为本地计算机名称）和运行服务所用的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="e7a39-149">`{DOMAIN}` (or if the machine isn't domain joined, the local machine name) and `{USER ACCOUNT}` &ndash; The domain (or local machine name) and user account under which the service runs.</span></span> <span data-ttu-id="e7a39-150">请勿省略 `obj` 参数。</span><span class="sxs-lookup"><span data-stu-id="e7a39-150">Do **not** omit the `obj` parameter.</span></span> <span data-ttu-id="e7a39-151">`obj` 的默认值为 [LocalSystem 帐户](/windows/desktop/services/localsystem-account)。</span><span class="sxs-lookup"><span data-stu-id="e7a39-151">The default value for `obj` is the [LocalSystem account](/windows/desktop/services/localsystem-account) account.</span></span> <span data-ttu-id="e7a39-152">使用 `LocalSystem` 帐户运行服务会带来重大安全风险。</span><span class="sxs-lookup"><span data-stu-id="e7a39-152">Running a service under the `LocalSystem` account presents a significant security risk.</span></span> <span data-ttu-id="e7a39-153">请始终使用在服务器上拥有有限权限的用户帐户运行服务。</span><span class="sxs-lookup"><span data-stu-id="e7a39-153">Always run a service under a user account with restricted privileges on the server.</span></span>
   * <span data-ttu-id="e7a39-154">`{PASSWORD}` &ndash; 用户帐户密码。</span><span class="sxs-lookup"><span data-stu-id="e7a39-154">`{PASSWORD}` &ndash; The user account password.</span></span>

   <span data-ttu-id="e7a39-155">如下示例中：</span><span class="sxs-lookup"><span data-stu-id="e7a39-155">In the following example:</span></span>

   * <span data-ttu-id="e7a39-156">服务名为 MyService。</span><span class="sxs-lookup"><span data-stu-id="e7a39-156">The service is named **MyService**.</span></span>
   * <span data-ttu-id="e7a39-157">已发布的服务驻留在 c:\\svc 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e7a39-157">The published service resides in the *c:\\svc* folder.</span></span> <span data-ttu-id="e7a39-158">应用可执行文件名为 AspNetCoreService.exe。</span><span class="sxs-lookup"><span data-stu-id="e7a39-158">The app executable is named *AspNetCoreService.exe*.</span></span> <span data-ttu-id="e7a39-159">`binPath` 值是放在半角双引号 (") 中。</span><span class="sxs-lookup"><span data-stu-id="e7a39-159">The `binPath` value is enclosed in straight quotation marks (").</span></span>
   * <span data-ttu-id="e7a39-160">服务是使用 `ServiceUser` 帐户运行。</span><span class="sxs-lookup"><span data-stu-id="e7a39-160">The service runs under the `ServiceUser` account.</span></span> <span data-ttu-id="e7a39-161">将 `{DOMAIN}` 替换为用户帐户的域或本地计算机名称。</span><span class="sxs-lookup"><span data-stu-id="e7a39-161">Replace `{DOMAIN}` with the user account's domain or local machine name.</span></span> <span data-ttu-id="e7a39-162">将 `obj` 值放在半角双引号 (") 中。</span><span class="sxs-lookup"><span data-stu-id="e7a39-162">Enclose the `obj` value in straight quotation marks (").</span></span> <span data-ttu-id="e7a39-163">例如，如果托管系统是名为 `MairaPC` 的本地计算机，请将 `obj` 设置为 `"MairaPC\ServiceUser"`。</span><span class="sxs-lookup"><span data-stu-id="e7a39-163">Example: If the hosting system is a local machine named `MairaPC`, set `obj` to `"MairaPC\ServiceUser"`.</span></span>
   * <span data-ttu-id="e7a39-164">将 `{PASSWORD}` 替换为用户帐户密码。</span><span class="sxs-lookup"><span data-stu-id="e7a39-164">Replace `{PASSWORD}` with the user account's password.</span></span> <span data-ttu-id="e7a39-165">`password` 值是放在半角双引号 (") 中。</span><span class="sxs-lookup"><span data-stu-id="e7a39-165">The `password` value is enclosed in straight quotation marks (").</span></span>

   ```console
   sc create MyService binPath= "c:\svc\aspnetcoreservice.exe" obj= "{DOMAIN}\ServiceUser" password= "{PASSWORD}"
   ```

   > [!IMPORTANT]
   > <span data-ttu-id="e7a39-166">请确保参数的等于号和参数值之间有空格。</span><span class="sxs-lookup"><span data-stu-id="e7a39-166">Make sure that the spaces between the parameters' equal signs and the parameters' values are present.</span></span>

1. <span data-ttu-id="e7a39-167">使用 `sc start {SERVICE NAME}` 命令启动服务。</span><span class="sxs-lookup"><span data-stu-id="e7a39-167">Start the service with the `sc start {SERVICE NAME}` command.</span></span>

   <span data-ttu-id="e7a39-168">要启动示例应用服务，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="e7a39-168">To start the sample app service, use the following command:</span></span>

   ```console
   sc start MyService
   ```

   <span data-ttu-id="e7a39-169">此命令需要几秒钟才能启动服务。</span><span class="sxs-lookup"><span data-stu-id="e7a39-169">The command takes a few seconds to start the service.</span></span>

1. <span data-ttu-id="e7a39-170">要检查服务的状态，请使用 `sc query {SERVICE NAME}` 命令。</span><span class="sxs-lookup"><span data-stu-id="e7a39-170">To check the status of the service, use the `sc query {SERVICE NAME}` command.</span></span> <span data-ttu-id="e7a39-171">状态报告为以下值之一：</span><span class="sxs-lookup"><span data-stu-id="e7a39-171">The status is reported as one of the following values:</span></span>

   * `START_PENDING`
   * `RUNNING`
   * `STOP_PENDING`
   * `STOPPED`

   <span data-ttu-id="e7a39-172">使用以下命令检查示例应用服务的状态：</span><span class="sxs-lookup"><span data-stu-id="e7a39-172">Use the following command to check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

1. <span data-ttu-id="e7a39-173">当服务处于 `RUNNING` 状态并且服务是 Web 应用时，在应用所在路径中浏览应用（默认路径为 `http://localhost:5000`；在使用 [HTTPS 重定向中间件](xref:security/enforcing-ssl)时，它将重定向到 `https://localhost:5001`）。</span><span class="sxs-lookup"><span data-stu-id="e7a39-173">When the service is in the `RUNNING` state and if the service is a web app, browse the app at its path (by default, `http://localhost:5000`, which redirects to `https://localhost:5001` when using [HTTPS Redirection Middleware](xref:security/enforcing-ssl)).</span></span>

   <span data-ttu-id="e7a39-174">对于示例应用服务，请在 `http://localhost:5000` 浏览应用。</span><span class="sxs-lookup"><span data-stu-id="e7a39-174">For the sample app service, browse the app at `http://localhost:5000`.</span></span>

1. <span data-ttu-id="e7a39-175">使用 `sc stop {SERVICE NAME}` 命令停止服务。</span><span class="sxs-lookup"><span data-stu-id="e7a39-175">Stop the service with the `sc stop {SERVICE NAME}` command.</span></span>

   <span data-ttu-id="e7a39-176">以下命令可停止示例应用服务：</span><span class="sxs-lookup"><span data-stu-id="e7a39-176">The following command stops the sample app service:</span></span>

   ```console
   sc stop MyService
   ```

1. <span data-ttu-id="e7a39-177">停止服务并经过短暂延迟后，使用 `sc delete {SERVICE NAME}` 命令卸载服务。</span><span class="sxs-lookup"><span data-stu-id="e7a39-177">After a short delay to stop a service, uninstall the service with the `sc delete {SERVICE NAME}` command.</span></span>

   <span data-ttu-id="e7a39-178">检查示例应用服务的状态：</span><span class="sxs-lookup"><span data-stu-id="e7a39-178">Check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

   <span data-ttu-id="e7a39-179">当示例应用服务处于 `STOPPED` 状态时，使用以下命令卸载示例应用服务：</span><span class="sxs-lookup"><span data-stu-id="e7a39-179">When the sample app service is in the `STOPPED` state, use the following command to uninstall the sample app service:</span></span>

   ```console
   sc delete MyService
   ```

## <a name="run-the-app-outside-of-a-service"></a><span data-ttu-id="e7a39-180">在服务之外运行应用</span><span class="sxs-lookup"><span data-stu-id="e7a39-180">Run the app outside of a service</span></span>

<span data-ttu-id="e7a39-181">在服务之外运行时更便于进行测试和调试，因此通常仅在特定情况下添加调用 `RunAsService` 的代码。</span><span class="sxs-lookup"><span data-stu-id="e7a39-181">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `RunAsService` only under certain conditions.</span></span> <span data-ttu-id="e7a39-182">例如，应用可以使用 `--console` 命令行参数或在已附加调试器时作为控制台应用运行：</span><span class="sxs-lookup"><span data-stu-id="e7a39-182">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached:</span></span>

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOrConsole)]

<span data-ttu-id="e7a39-183">由于 ASP.NET Core 配置需要命令行参数的名称/值对，因此将先删除 `--console` 开关，然后再将参数传递到 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)。</span><span class="sxs-lookup"><span data-stu-id="e7a39-183">Because ASP.NET Core configuration requires name-value pairs for command-line arguments, the `--console` switch is removed before the arguments are passed to [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder).</span></span>

> [!NOTE]
> <span data-ttu-id="e7a39-184">不将 `Main` 中的 `isService` 传递到 `CreateWebHostBuilder`，因为 `CreateWebHostBuilder` 的签名必须是 `CreateWebHostBuilder(string[])`才能使[集成测试](xref:test/integration-tests)正常运行。</span><span class="sxs-lookup"><span data-stu-id="e7a39-184">`isService` isn't passed from `Main` into `CreateWebHostBuilder` because the signature of `CreateWebHostBuilder` must be `CreateWebHostBuilder(string[])` in order for [integration testing](xref:test/integration-tests) to work properly.</span></span>

## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="e7a39-185">处理停止和启动事件</span><span class="sxs-lookup"><span data-stu-id="e7a39-185">Handle stopping and starting events</span></span>

<span data-ttu-id="e7a39-186">要处理 [OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting)、[OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted) 和 [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) 事件，请执行以下额外更改：</span><span class="sxs-lookup"><span data-stu-id="e7a39-186">To handle [OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting), [OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted), and [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) events, make the following additional changes:</span></span>

1. <span data-ttu-id="e7a39-187">创建从 [WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice) 派生的类：</span><span class="sxs-lookup"><span data-stu-id="e7a39-187">Create a class that derives from [WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=NoLogging)]

2. <span data-ttu-id="e7a39-188">创建可将自定义 `WebHostService` 传递给 [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run) 的 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) 的扩展方法：</span><span class="sxs-lookup"><span data-stu-id="e7a39-188">Create an extension method for [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) that passes the custom `WebHostService` to [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="e7a39-189">在 `Program.Main` 中，调用新扩展方法 `RunAsCustomService`，而不是 [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)：</span><span class="sxs-lookup"><span data-stu-id="e7a39-189">In `Program.Main`, call the new extension method, `RunAsCustomService`, instead of [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=17)]

   > [!NOTE]
   > <span data-ttu-id="e7a39-190">不将 `Main` 中的 `isService` 传递到 `CreateWebHostBuilder`，因为 `CreateWebHostBuilder` 的签名必须是 `CreateWebHostBuilder(string[])`才能使[集成测试](xref:test/integration-tests)正常运行。</span><span class="sxs-lookup"><span data-stu-id="e7a39-190">`isService` isn't passed from `Main` into `CreateWebHostBuilder` because the signature of `CreateWebHostBuilder` must be `CreateWebHostBuilder(string[])` in order for [integration testing](xref:test/integration-tests) to work properly.</span></span>

<span data-ttu-id="e7a39-191">如果自定义 `WebHostService` 代码需要来自依赖项注入（如记录器）的服务，请从 [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) 属性中获取：</span><span class="sxs-lookup"><span data-stu-id="e7a39-191">If the custom `WebHostService` code requires a service from dependency injection (such as a logger), obtain it from the [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) property:</span></span>

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=Logging&highlight=7-8)]

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="e7a39-192">代理服务器和负载均衡器方案</span><span class="sxs-lookup"><span data-stu-id="e7a39-192">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="e7a39-193">与来自 Internet 或公司网络的请求进行交互且在代理或负载均衡器后方的服务可能需要其他配置。</span><span class="sxs-lookup"><span data-stu-id="e7a39-193">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="e7a39-194">有关更多信息，请参见<xref:host-and-deploy/proxy-load-balancer>。</span><span class="sxs-lookup"><span data-stu-id="e7a39-194">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>

## <a name="configure-https"></a><span data-ttu-id="e7a39-195">配置 HTTPS</span><span class="sxs-lookup"><span data-stu-id="e7a39-195">Configure HTTPS</span></span>

<span data-ttu-id="e7a39-196">若要为服务配置安全终结点，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="e7a39-196">To configure the service with a secure endpoint:</span></span>

1. <span data-ttu-id="e7a39-197">使用平台的证书获取和部署机制，为托管系统创建 X.509 证书。</span><span class="sxs-lookup"><span data-stu-id="e7a39-197">Create an X.509 certificate for the hosting system using your platform's certificate acquisition and deployment mechanisms.</span></span>
1. <span data-ttu-id="e7a39-198">将 [Kestrel 服务器 HTTPS 终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)指定为使用此证书。</span><span class="sxs-lookup"><span data-stu-id="e7a39-198">Specify a [Kestrel server HTTPS endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) to use the certificate.</span></span>

<span data-ttu-id="e7a39-199">不支持使用 ASP.NET Core HTTPS 开发证书保护服务终结点。</span><span class="sxs-lookup"><span data-stu-id="e7a39-199">Use of the ASP.NET Core HTTPS development certificate to secure a service endpoint isn't supported.</span></span>

## <a name="current-directory-and-content-root"></a><span data-ttu-id="e7a39-200">当前目录和内容根</span><span class="sxs-lookup"><span data-stu-id="e7a39-200">Current directory and content root</span></span>

<span data-ttu-id="e7a39-201">通过为 Windows 服务调用 `Directory.GetCurrentDirectory()` 返回的当前工作目录是 C:\\WINDOWS\\system32 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e7a39-201">The current working directory returned by calling `Directory.GetCurrentDirectory()` for a Windows Service is the *C:\\WINDOWS\\system32* folder.</span></span> <span data-ttu-id="e7a39-202">system32 文件夹不是存储服务文件（如设置文件）的合适位置。</span><span class="sxs-lookup"><span data-stu-id="e7a39-202">The *system32* folder isn't a suitable location to store a service's files (for example, settings files).</span></span> <span data-ttu-id="e7a39-203">使用 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) 时，通过以下某种方法使用 [FileConfigurationExtensions.SetBasePath](/dotnet/api/microsoft.extensions.configuration.fileconfigurationextensions.setbasepath) 维护和访问服务的资产和设置文件：</span><span class="sxs-lookup"><span data-stu-id="e7a39-203">Use one of the following approaches to maintain and access a service's assets and settings files with [FileConfigurationExtensions.SetBasePath](/dotnet/api/microsoft.extensions.configuration.fileconfigurationextensions.setbasepath) when using an [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder):</span></span>

* <span data-ttu-id="e7a39-204">使用内容根路径。</span><span class="sxs-lookup"><span data-stu-id="e7a39-204">Use the content root path.</span></span> <span data-ttu-id="e7a39-205">`IHostingEnvironment.ContentRootPath` 是创建服务时提供给 `binPath` 参数的同一路径。</span><span class="sxs-lookup"><span data-stu-id="e7a39-205">The `IHostingEnvironment.ContentRootPath` is the same path provided to the `binPath` argument when the service is created.</span></span> <span data-ttu-id="e7a39-206">不要使用 `Directory.GetCurrentDirectory()` 创建设置文件的路径，而是使用内容根路径并在应用的内容根中维护文件。</span><span class="sxs-lookup"><span data-stu-id="e7a39-206">Instead of using `Directory.GetCurrentDirectory()` to create paths to settings files, use the content root path and maintain the files in the app's content root.</span></span>
* <span data-ttu-id="e7a39-207">将文件存储在磁盘中的合适位置。</span><span class="sxs-lookup"><span data-stu-id="e7a39-207">Store the files in a suitable location on disk.</span></span> <span data-ttu-id="e7a39-208">使用 `SetBasePath` 指定到包含文件的文件夹的绝对路径。</span><span class="sxs-lookup"><span data-stu-id="e7a39-208">Specify an absolute path with `SetBasePath` to the folder containing the files.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7a39-209">其他资源</span><span class="sxs-lookup"><span data-stu-id="e7a39-209">Additional resources</span></span>

* <span data-ttu-id="e7a39-210">[Kestrel 终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)（包括 HTTPS 配置和 SNI 支持）</span><span class="sxs-lookup"><span data-stu-id="e7a39-210">[Kestrel endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) (includes HTTPS configuration and SNI support)</span></span>
* <xref:fundamentals/host/web-host>
