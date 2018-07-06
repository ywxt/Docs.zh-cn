---
title: 安全存储中 ASP.NET Core 中开发的应用程序机密
author: rick-anderson
description: 了解如何存储和检索在 ASP.NET Core 应用程序开发期间为应用程序机密的敏感信息。
ms.author: scaddie
ms.custom: mvc
ms.date: 06/21/2018
uid: security/app-secrets
ms.openlocfilehash: d3b2de1a17012986ef8dea7aaf8636dd35d10fa1
ms.sourcegitcommit: e22097b84d26a812cd1380a6b2d12c93e522c125
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2018
ms.locfileid: "36314170"
---
# <a name="safe-storage-of-app-secrets-in-development-in-aspnet-core"></a><span data-ttu-id="19e5f-103">安全存储中 ASP.NET Core 中开发的应用程序机密</span><span class="sxs-lookup"><span data-stu-id="19e5f-103">Safe storage of app secrets in development in ASP.NET Core</span></span>

<span data-ttu-id="19e5f-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)， [Daniel Roth](https://github.com/danroth27)，和[Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="19e5f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Daniel Roth](https://github.com/danroth27), and [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="19e5f-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="19e5f-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="19e5f-106">本文档介绍用于存储和检索敏感数据的 ASP.NET Core 应用程序开发过程的技术。</span><span class="sxs-lookup"><span data-stu-id="19e5f-106">This document explains techniques for storing and retrieving sensitive data during the development of an ASP.NET Core app.</span></span> <span data-ttu-id="19e5f-107">你应永远不会将密码或其他敏感数据存储在源代码中，并且你不应在开发过程中使用生产机密或测试模式。</span><span class="sxs-lookup"><span data-stu-id="19e5f-107">You should never store passwords or other sensitive data in source code, and you shouldn't use production secrets in development or test mode.</span></span> <span data-ttu-id="19e5f-108">你可以存储和保护与 Azure 的测试和生产机密[Azure 密钥保管库配置提供程序](xref:security/key-vault-configuration)。</span><span class="sxs-lookup"><span data-stu-id="19e5f-108">You can store and protect Azure test and production secrets with the [Azure Key Vault configuration provider](xref:security/key-vault-configuration).</span></span>

## <a name="environment-variables"></a><span data-ttu-id="19e5f-109">环境变量</span><span class="sxs-lookup"><span data-stu-id="19e5f-109">Environment variables</span></span>

<span data-ttu-id="19e5f-110">使用环境变量以避免在代码中或在本地配置文件中的应用程序机密存储。</span><span class="sxs-lookup"><span data-stu-id="19e5f-110">Environment variables are used to avoid storage of app secrets in code or in local configuration files.</span></span> <span data-ttu-id="19e5f-111">环境变量重写所有以前指定的配置源的配置的值。</span><span class="sxs-lookup"><span data-stu-id="19e5f-111">Environment variables override configuration values for all previously specified configuration sources.</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="19e5f-112">通过调用配置的环境变量值读取[AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables)中`Startup`构造函数：</span><span class="sxs-lookup"><span data-stu-id="19e5f-112">Configure the reading of environment variable values by calling [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) in the `Startup` constructor:</span></span>

<span data-ttu-id="19e5f-113">[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=10)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-113">[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=10)]</span></span>
::: moniker-end

<span data-ttu-id="19e5f-114">请考虑在其中一个 ASP.NET Core web 应用**单个用户帐户**已启用安全性。</span><span class="sxs-lookup"><span data-stu-id="19e5f-114">Consider an ASP.NET Core web app in which **Individual User Accounts** security is enabled.</span></span> <span data-ttu-id="19e5f-115">默认数据库连接字符串包含在项目的*appsettings.json*文件与键`DefaultConnection`。</span><span class="sxs-lookup"><span data-stu-id="19e5f-115">A default database connection string is included in the project's *appsettings.json* file with the key `DefaultConnection`.</span></span> <span data-ttu-id="19e5f-116">默认连接字符串用于 LocalDB，在用户模式下运行，而且不需要密码。</span><span class="sxs-lookup"><span data-stu-id="19e5f-116">The default connection string is for LocalDB, which runs in user mode and doesn't require a password.</span></span> <span data-ttu-id="19e5f-117">应用程序在部署期间，`DefaultConnection`密钥值可以用环境变量的值重写。</span><span class="sxs-lookup"><span data-stu-id="19e5f-117">During app deployment, the `DefaultConnection` key value can be overridden with an environment variable's value.</span></span> <span data-ttu-id="19e5f-118">环境变量可以存储敏感的凭据与完整的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="19e5f-118">The environment variable may store the complete connection string with sensitive credentials.</span></span>

> [!WARNING]
> <span data-ttu-id="19e5f-119">环境变量通常存储在未加密的纯文本。</span><span class="sxs-lookup"><span data-stu-id="19e5f-119">Environment variables are generally stored in plain, unencrypted text.</span></span> <span data-ttu-id="19e5f-120">如果计算机或进程受到攻击，则可以通过不受信任方访问环境变量。</span><span class="sxs-lookup"><span data-stu-id="19e5f-120">If the machine or process is compromised, environment variables can be accessed by untrusted parties.</span></span> <span data-ttu-id="19e5f-121">可能需要更多措施，防止用户的机密信息泄露。</span><span class="sxs-lookup"><span data-stu-id="19e5f-121">Additional measures to prevent disclosure of user secrets may be required.</span></span>

## <a name="secret-manager"></a><span data-ttu-id="19e5f-122">密码管理器</span><span class="sxs-lookup"><span data-stu-id="19e5f-122">Secret Manager</span></span>

<span data-ttu-id="19e5f-123">密码管理器工具在 ASP.NET Core 项目的开发过程中存储敏感数据。</span><span class="sxs-lookup"><span data-stu-id="19e5f-123">The Secret Manager tool stores sensitive data during the development of an ASP.NET Core project.</span></span> <span data-ttu-id="19e5f-124">在此上下文中，一种敏感数据是应用程序密钥。</span><span class="sxs-lookup"><span data-stu-id="19e5f-124">In this context, a piece of sensitive data is an app secret.</span></span> <span data-ttu-id="19e5f-125">应用程序机密存储在单独的位置，从项目树中。</span><span class="sxs-lookup"><span data-stu-id="19e5f-125">App secrets are stored in a separate location from the project tree.</span></span> <span data-ttu-id="19e5f-126">应用程序机密是与特定项目关联，或共享跨多个项目。</span><span class="sxs-lookup"><span data-stu-id="19e5f-126">The app secrets are associated with a specific project or shared across several projects.</span></span> <span data-ttu-id="19e5f-127">应用程序机密不签入源控件。</span><span class="sxs-lookup"><span data-stu-id="19e5f-127">The app secrets aren't checked into source control.</span></span>

> [!WARNING]
> <span data-ttu-id="19e5f-128">密码管理器工具不加密存储的机密信息，并不应被视为受信任存储区。</span><span class="sxs-lookup"><span data-stu-id="19e5f-128">The Secret Manager tool doesn't encrypt the stored secrets and shouldn't be treated as a trusted store.</span></span> <span data-ttu-id="19e5f-129">它是仅限开发目的。</span><span class="sxs-lookup"><span data-stu-id="19e5f-129">It's for development purposes only.</span></span> <span data-ttu-id="19e5f-130">键和值存储在用户配置文件目录中的 JSON 配置文件中。</span><span class="sxs-lookup"><span data-stu-id="19e5f-130">The keys and values are stored in a JSON configuration file in the user profile directory.</span></span>

## <a name="how-the-secret-manager-tool-works"></a><span data-ttu-id="19e5f-131">密码管理器工具的工作原理</span><span class="sxs-lookup"><span data-stu-id="19e5f-131">How the Secret Manager tool works</span></span>

<span data-ttu-id="19e5f-132">密码管理器工具避开实现详细信息，例如哪里和如何存储值。</span><span class="sxs-lookup"><span data-stu-id="19e5f-132">The Secret Manager tool abstracts away the implementation details, such as where and how the values are stored.</span></span> <span data-ttu-id="19e5f-133">无需知道这些实现的详细信息，可以使用该工具。</span><span class="sxs-lookup"><span data-stu-id="19e5f-133">You can use the tool without knowing these implementation details.</span></span> <span data-ttu-id="19e5f-134">值存储在本地计算机上的 JSON 配置文件受系统保护用户配置文件文件夹中：</span><span class="sxs-lookup"><span data-stu-id="19e5f-134">The values are stored in a JSON configuration file in a system-protected user profile folder on the local machine:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="19e5f-135">Windows</span><span class="sxs-lookup"><span data-stu-id="19e5f-135">Windows</span></span>](#tab/windows)

<span data-ttu-id="19e5f-136">文件系统路径：</span><span class="sxs-lookup"><span data-stu-id="19e5f-136">File system path:</span></span>

`%APPDATA%\Microsoft\UserSecrets\<user_secrets_id>\secrets.json`

# <a name="macostabmacos"></a>[<span data-ttu-id="19e5f-137">macOS</span><span class="sxs-lookup"><span data-stu-id="19e5f-137">macOS</span></span>](#tab/macos)

<span data-ttu-id="19e5f-138">文件系统路径：</span><span class="sxs-lookup"><span data-stu-id="19e5f-138">File system path:</span></span>

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

# <a name="linuxtablinux"></a>[<span data-ttu-id="19e5f-139">Linux</span><span class="sxs-lookup"><span data-stu-id="19e5f-139">Linux</span></span>](#tab/linux)

<span data-ttu-id="19e5f-140">文件系统路径：</span><span class="sxs-lookup"><span data-stu-id="19e5f-140">File system path:</span></span>

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

---

<span data-ttu-id="19e5f-141">在前面文件路径中，将`<user_secrets_id>`与`UserSecretsId`中指定的值 *.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="19e5f-141">In the preceding file paths, replace `<user_secrets_id>` with the `UserSecretsId` value specified in the *.csproj* file.</span></span>

<span data-ttu-id="19e5f-142">不编写代码所依赖的位置或使用密码管理器工具中保存的数据的格式。</span><span class="sxs-lookup"><span data-stu-id="19e5f-142">Don't write code that depends on the location or format of data saved with the Secret Manager tool.</span></span> <span data-ttu-id="19e5f-143">这些实现的详细信息如有更改。</span><span class="sxs-lookup"><span data-stu-id="19e5f-143">These implementation details may change.</span></span> <span data-ttu-id="19e5f-144">例如，密钥值不加密，但是可能在将来。</span><span class="sxs-lookup"><span data-stu-id="19e5f-144">For example, the secret values aren't encrypted, but could be in the future.</span></span>

::: moniker range="<= aspnetcore-2.0"
## <a name="install-the-secret-manager-tool"></a><span data-ttu-id="19e5f-145">安装机密管理器工具</span><span class="sxs-lookup"><span data-stu-id="19e5f-145">Install the Secret Manager tool</span></span>

<span data-ttu-id="19e5f-146">密钥管理器工具是与.NET Core CLI 截至.NET Core SDK 2.1.300 捆绑。</span><span class="sxs-lookup"><span data-stu-id="19e5f-146">The Secret Manager tool is bundled with the .NET Core CLI as of .NET Core SDK 2.1.300.</span></span> <span data-ttu-id="19e5f-147">有关.NET Core SDK 2.1.300 之前的版本中，工具安装是必需的。</span><span class="sxs-lookup"><span data-stu-id="19e5f-147">For .NET Core SDK versions before 2.1.300, tool installation is necessary.</span></span>

> [!TIP]
> <span data-ttu-id="19e5f-148">运行`dotnet --version`从命令行界面中，若要查看已安装的.NET Core SDK 版本号。</span><span class="sxs-lookup"><span data-stu-id="19e5f-148">Run `dotnet --version` from a command shell to see the installed .NET Core SDK version number.</span></span>

<span data-ttu-id="19e5f-149">如果正在使用的.NET Core SDK 包括的工具，将显示警告：</span><span class="sxs-lookup"><span data-stu-id="19e5f-149">A warning is displayed if the .NET Core SDK being used includes the tool:</span></span>

```console
The tool 'Microsoft.Extensions.SecretManager.Tools' is now included in the .NET Core SDK. Information on resolving this warning is available at (https://aka.ms/dotnetclitools-in-box).
```

<span data-ttu-id="19e5f-150">安装[Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) ASP.NET Core 项目中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="19e5f-150">Install the [Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) NuGet package in your ASP.NET Core project.</span></span> <span data-ttu-id="19e5f-151">例如：</span><span class="sxs-lookup"><span data-stu-id="19e5f-151">For example:</span></span>

<span data-ttu-id="19e5f-152">[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_CsprojFile&highlight=13-14)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-152">[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_CsprojFile&highlight=13-14)]</span></span>

<span data-ttu-id="19e5f-153">在验证工具的安装命令行界面中执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="19e5f-153">Execute the following command in a command shell to validate the tool installation:</span></span>

```console
dotnet user-secrets -h
```

<span data-ttu-id="19e5f-154">密码管理器工具显示示例用法、 选项和命令帮助：</span><span class="sxs-lookup"><span data-stu-id="19e5f-154">The Secret Manager tool displays sample usage, options, and command help:</span></span>

```console
Usage: dotnet user-secrets [options] [command]

Options:
  -?|-h|--help                        Show help information
  --version                           Show version information
  -v|--verbose                        Show verbose output
  -p|--project <PROJECT>              Path to project. Defaults to searching the current directory.
  -c|--configuration <CONFIGURATION>  The project configuration to use. Defaults to 'Debug'.
  --id                                The user secret ID to use.

Commands:
  clear   Deletes all the application secrets
  list    Lists all the application secrets
  remove  Removes the specified user secret
  set     Sets the user secret to the specified value

Use "dotnet user-secrets [command] --help" for more information about a command.
```

> [!NOTE]
> <span data-ttu-id="19e5f-155">你必须在与位于同一目录 *.csproj*文件以运行中定义的工具 *.csproj*文件的`DotNetCliToolReference`元素。</span><span class="sxs-lookup"><span data-stu-id="19e5f-155">You must be in the same directory as the *.csproj* file to run tools defined in the *.csproj* file's `DotNetCliToolReference` elements.</span></span>
::: moniker-end

## <a name="set-a-secret"></a><span data-ttu-id="19e5f-156">设置机密</span><span class="sxs-lookup"><span data-stu-id="19e5f-156">Set a secret</span></span>

<span data-ttu-id="19e5f-157">密码管理器工具进行存储用户配置文件中的特定于项目的配置设置操作。</span><span class="sxs-lookup"><span data-stu-id="19e5f-157">The Secret Manager tool operates on project-specific configuration settings stored in your user profile.</span></span> <span data-ttu-id="19e5f-158">若要使用用户的机密信息，定义`UserSecretsId`中的元素`PropertyGroup`的 *.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="19e5f-158">To use user secrets, define a `UserSecretsId` element within a `PropertyGroup` of the *.csproj* file.</span></span> <span data-ttu-id="19e5f-159">值`UserSecretsId`任意的但是唯一到项目。</span><span class="sxs-lookup"><span data-stu-id="19e5f-159">The value of `UserSecretsId` is arbitrary, but is unique to the project.</span></span> <span data-ttu-id="19e5f-160">开发人员通常应生成的 GUID `UserSecretsId`。</span><span class="sxs-lookup"><span data-stu-id="19e5f-160">Developers typically generate a GUID for the `UserSecretsId`.</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="19e5f-161">[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-161">[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="19e5f-162">[!code-xml[](app-secrets/samples/2.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-162">[!code-xml[](app-secrets/samples/2.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span></span>
::: moniker-end

> [!TIP]
> <span data-ttu-id="19e5f-163">在 Visual Studio 中，右键单击解决方案资源管理器中的项目，然后选择**管理用户的机密信息**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="19e5f-163">In Visual Studio, right-click the project in Solution Explorer, and select **Manage User Secrets** from the context menu.</span></span> <span data-ttu-id="19e5f-164">此手势添加`UserSecretsId`元素，为填充 GUID， *.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="19e5f-164">This gesture adds a `UserSecretsId` element, populated with a GUID, to the *.csproj* file.</span></span> <span data-ttu-id="19e5f-165">Visual Studio 将打开*secrets.json*在文本编辑器中的文件。</span><span class="sxs-lookup"><span data-stu-id="19e5f-165">Visual Studio opens a *secrets.json* file in the text editor.</span></span> <span data-ttu-id="19e5f-166">内容替换*secrets.json*要存储的键 / 值对。</span><span class="sxs-lookup"><span data-stu-id="19e5f-166">Replace the contents of *secrets.json* with the key-value pairs to be stored.</span></span> <span data-ttu-id="19e5f-167">例如：[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file.md)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-167">For example: [!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file.md)]</span></span>

<span data-ttu-id="19e5f-168">定义一个键和其值组成应用程序密钥。</span><span class="sxs-lookup"><span data-stu-id="19e5f-168">Define an app secret consisting of a key and its value.</span></span> <span data-ttu-id="19e5f-169">密钥是与项目的关联`UserSecretsId`值。</span><span class="sxs-lookup"><span data-stu-id="19e5f-169">The secret is associated with the project's `UserSecretsId` value.</span></span> <span data-ttu-id="19e5f-170">例如，从在其中的目录运行以下命令 *.csproj*文件存在：</span><span class="sxs-lookup"><span data-stu-id="19e5f-170">For example, run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345"
```

<span data-ttu-id="19e5f-171">在前面的示例中，冒号表示`Movies`是一个对象文本替换`ServiceApiKey`属性。</span><span class="sxs-lookup"><span data-stu-id="19e5f-171">In the preceding example, the colon denotes that `Movies` is an object literal with a `ServiceApiKey` property.</span></span>

<span data-ttu-id="19e5f-172">密码管理器工具可以过使用从其他目录。</span><span class="sxs-lookup"><span data-stu-id="19e5f-172">The Secret Manager tool can be used from other directories too.</span></span> <span data-ttu-id="19e5f-173">使用`--project`选项提供文件系统路径，在此处 *.csproj*文件存在。</span><span class="sxs-lookup"><span data-stu-id="19e5f-173">Use the `--project` option to supply the file system path at which the *.csproj* file exists.</span></span> <span data-ttu-id="19e5f-174">例如：</span><span class="sxs-lookup"><span data-stu-id="19e5f-174">For example:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345" --project "C:\apps\WebApp1\src\WebApp1"
```

## <a name="set-multiple-secrets"></a><span data-ttu-id="19e5f-175">设置多个机密</span><span class="sxs-lookup"><span data-stu-id="19e5f-175">Set multiple secrets</span></span>

<span data-ttu-id="19e5f-176">可以通过管道传递到的 JSON 设置机密一批`set`命令。</span><span class="sxs-lookup"><span data-stu-id="19e5f-176">A batch of secrets can be set by piping JSON to the `set` command.</span></span> <span data-ttu-id="19e5f-177">在下面的示例中， *input.json*文件的内容通过管道传递给`set`命令。</span><span class="sxs-lookup"><span data-stu-id="19e5f-177">In the following example, the *input.json* file's contents are piped to the `set` command.</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="19e5f-178">Windows</span><span class="sxs-lookup"><span data-stu-id="19e5f-178">Windows</span></span>](#tab/windows)

<span data-ttu-id="19e5f-179">打开命令 shell，并执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="19e5f-179">Open a command shell, and execute the following command:</span></span>

  ```console
  type .\input.json | dotnet user-secrets set
  ```

# <a name="macostabmacos"></a>[<span data-ttu-id="19e5f-180">macOS</span><span class="sxs-lookup"><span data-stu-id="19e5f-180">macOS</span></span>](#tab/macos)

<span data-ttu-id="19e5f-181">打开命令 shell，并执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="19e5f-181">Open a command shell, and execute the following command:</span></span>

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

# <a name="linuxtablinux"></a>[<span data-ttu-id="19e5f-182">Linux</span><span class="sxs-lookup"><span data-stu-id="19e5f-182">Linux</span></span>](#tab/linux)

<span data-ttu-id="19e5f-183">打开命令 shell，并执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="19e5f-183">Open a command shell, and execute the following command:</span></span>

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

---

## <a name="access-a-secret"></a><span data-ttu-id="19e5f-184">访问机密</span><span class="sxs-lookup"><span data-stu-id="19e5f-184">Access a secret</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="19e5f-185">[ASP.NET Core 配置 API](xref:fundamentals/configuration/index)提供对机密 Manager 机密的访问。</span><span class="sxs-lookup"><span data-stu-id="19e5f-185">The [ASP.NET Core Configuration API](xref:fundamentals/configuration/index) provides access to Secret Manager secrets.</span></span> <span data-ttu-id="19e5f-186">安装[Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="19e5f-186">Install the [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet package.</span></span>

<span data-ttu-id="19e5f-187">添加用户机密配置源通过调用[AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets)中`Startup`构造函数：</span><span class="sxs-lookup"><span data-stu-id="19e5f-187">Add the user secrets configuration source with a call to [AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets) in the `Startup` constructor:</span></span>

<span data-ttu-id="19e5f-188">[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=5-8)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-188">[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=5-8)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="19e5f-189">[ASP.NET Core 配置 API](xref:fundamentals/configuration/index)提供对机密 Manager 机密的访问。</span><span class="sxs-lookup"><span data-stu-id="19e5f-189">The [ASP.NET Core Configuration API](xref:fundamentals/configuration/index) provides access to Secret Manager secrets.</span></span> <span data-ttu-id="19e5f-190">如果你的项目面向.NET Framework，安装[Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="19e5f-190">If your project targets the .NET Framework, install the [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet package.</span></span>

<span data-ttu-id="19e5f-191">在 ASP.NET Core 2.0 或更高版本，用户机密配置源时，自动添加在开发模式下项目调用[CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)初始化带有预配置的默认值的主机的新实例。</span><span class="sxs-lookup"><span data-stu-id="19e5f-191">In ASP.NET Core 2.0 or later, the user secrets configuration source is automatically added in development mode when the project calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to initialize a new instance of the host with preconfigured defaults.</span></span> <span data-ttu-id="19e5f-192">`CreateDefaultBuilder` 调用[AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets)时[EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname)是[开发](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development):</span><span class="sxs-lookup"><span data-stu-id="19e5f-192">`CreateDefaultBuilder` calls [AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets) when the [EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname) is [Development](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development):</span></span>

<span data-ttu-id="19e5f-193">[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Program.cs?name=snippet_CreateWebHostBuilder&highlight=2)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-193">[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Program.cs?name=snippet_CreateWebHostBuilder&highlight=2)]</span></span>

<span data-ttu-id="19e5f-194">当`CreateDefaultBuilder`不在主机构造过程中调用，将通过调用该用户机密配置源添加[AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets)中`Startup`构造函数：</span><span class="sxs-lookup"><span data-stu-id="19e5f-194">When `CreateDefaultBuilder` isn't called during host construction, add the user secrets configuration source with a call to [AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets) in the `Startup` constructor:</span></span>

<span data-ttu-id="19e5f-195">[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=5-8)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-195">[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=5-8)]</span></span>
::: moniker-end

<span data-ttu-id="19e5f-196">可以通过检索用户的机密信息`Configuration`API:</span><span class="sxs-lookup"><span data-stu-id="19e5f-196">User secrets can be retrieved via the `Configuration` API:</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="19e5f-197">[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=23)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-197">[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=23)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="19e5f-198">[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=14)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-198">[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=14)]</span></span>
::: moniker-end

## <a name="string-replacement-with-secrets"></a><span data-ttu-id="19e5f-199">包含密码的字符串替换</span><span class="sxs-lookup"><span data-stu-id="19e5f-199">String replacement with secrets</span></span>

<span data-ttu-id="19e5f-200">以纯文本格式存储密码是不安全的。</span><span class="sxs-lookup"><span data-stu-id="19e5f-200">Storing passwords in plain text is insecure.</span></span> <span data-ttu-id="19e5f-201">例如，数据库连接字符串存储在*appsettings.json*可能包括指定用户的密码：</span><span class="sxs-lookup"><span data-stu-id="19e5f-201">For example, a database connection string stored in *appsettings.json* may include a password for the specified user:</span></span>

[!code-json[](app-secrets/samples/2.x/UserSecrets/appsettings-unsecure.json?highlight=3)]

<span data-ttu-id="19e5f-202">更安全的方法是将密码存储的机密形式。</span><span class="sxs-lookup"><span data-stu-id="19e5f-202">A more secure approach is to store the password as a secret.</span></span> <span data-ttu-id="19e5f-203">例如：</span><span class="sxs-lookup"><span data-stu-id="19e5f-203">For example:</span></span>

```console
dotnet user-secrets set "DbPassword" "pass123"
```

<span data-ttu-id="19e5f-204">删除`Password`中的连接字符串中的键 / 值对*appsettings.json*。</span><span class="sxs-lookup"><span data-stu-id="19e5f-204">Remove the `Password` key-value pair from the connection string in *appsettings.json*.</span></span> <span data-ttu-id="19e5f-205">例如：</span><span class="sxs-lookup"><span data-stu-id="19e5f-205">For example:</span></span>

[!code-json[](app-secrets/samples/2.x/UserSecrets/appsettings.json?highlight=3)]

<span data-ttu-id="19e5f-206">机密的值可以设置上[SqlConnectionStringBuilder](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder)对象的[密码](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.password)属性来完成连接字符串：</span><span class="sxs-lookup"><span data-stu-id="19e5f-206">The secret's value can be set on a [SqlConnectionStringBuilder](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder) object's [Password](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.password) property to complete the connection string:</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="19e5f-207">[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=26-29)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-207">[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=26-29)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="19e5f-208">[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=14-17)]</span><span class="sxs-lookup"><span data-stu-id="19e5f-208">[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=14-17)]</span></span>
::: moniker-end

## <a name="list-the-secrets"></a><span data-ttu-id="19e5f-209">列出机密</span><span class="sxs-lookup"><span data-stu-id="19e5f-209">List the secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="19e5f-210">从在其中的目录运行以下命令 *.csproj*文件存在：</span><span class="sxs-lookup"><span data-stu-id="19e5f-210">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets list
```

<span data-ttu-id="19e5f-211">显示以下输出：</span><span class="sxs-lookup"><span data-stu-id="19e5f-211">The following output appears:</span></span>

```console
Movies:ServiceApiKey = 12345
Movies:ConnectionString = Server=(localdb)\mssqllocaldb;Database=Movie-1;Trusted_Connection=True;MultipleActiveResultSets=true
```

<span data-ttu-id="19e5f-212">在前面的示例中，在项名称中的冒号表示内的对象层次结构*secrets.json*。</span><span class="sxs-lookup"><span data-stu-id="19e5f-212">In the preceding example, a colon in the key names denotes the object hierarchy within *secrets.json*.</span></span>

## <a name="remove-a-single-secret"></a><span data-ttu-id="19e5f-213">删除单个机密</span><span class="sxs-lookup"><span data-stu-id="19e5f-213">Remove a single secret</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="19e5f-214">从在其中的目录运行以下命令 *.csproj*文件存在：</span><span class="sxs-lookup"><span data-stu-id="19e5f-214">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets remove "Movies:ConnectionString"
```

<span data-ttu-id="19e5f-215">应用程序的*secrets.json*已修改文件，以删除与关联的键 / 值对`MoviesConnectionString`密钥：</span><span class="sxs-lookup"><span data-stu-id="19e5f-215">The app's *secrets.json* file was modified to remove the key-value pair associated with the `MoviesConnectionString` key:</span></span>

```json
{
  "Movies": {
    "ServiceApiKey": "12345"
  }
}
```

<span data-ttu-id="19e5f-216">运行`dotnet user-secrets list`显示以下消息：</span><span class="sxs-lookup"><span data-stu-id="19e5f-216">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
Movies:ServiceApiKey = 12345
```

## <a name="remove-all-secrets"></a><span data-ttu-id="19e5f-217">删除所有机密</span><span class="sxs-lookup"><span data-stu-id="19e5f-217">Remove all secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="19e5f-218">从在其中的目录运行以下命令 *.csproj*文件存在：</span><span class="sxs-lookup"><span data-stu-id="19e5f-218">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets clear
```

<span data-ttu-id="19e5f-219">已从删除应用程序的所有用户机密*secrets.json*文件：</span><span class="sxs-lookup"><span data-stu-id="19e5f-219">All user secrets for the app have been deleted from the *secrets.json* file:</span></span>

```json
{}
```

<span data-ttu-id="19e5f-220">运行`dotnet user-secrets list`显示以下消息：</span><span class="sxs-lookup"><span data-stu-id="19e5f-220">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
No secrets configured for this application.
```

## <a name="additional-resources"></a><span data-ttu-id="19e5f-221">其他资源</span><span class="sxs-lookup"><span data-stu-id="19e5f-221">Additional resources</span></span>

* <xref:fundamentals/configuration/index>
* <xref:security/key-vault-configuration>
