---
title: 安全存储中 ASP.NET Core 中开发的应用程序机密
author: rick-anderson
description: 了解如何存储和检索在 ASP.NET Core 应用程序开发期间为应用程序机密的敏感信息。
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 05/16/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/app-secrets
ms.openlocfilehash: 4db09d3d41b705597f93d05af91077f2b9236b7e
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="safe-storage-of-app-secrets-in-development-in-aspnet-core"></a><span data-ttu-id="d05b4-103">安全存储中 ASP.NET Core 中开发的应用程序机密</span><span class="sxs-lookup"><span data-stu-id="d05b4-103">Safe storage of app secrets in development in ASP.NET Core</span></span>

<span data-ttu-id="d05b4-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)， [Daniel Roth](https://github.com/danroth27)，和[Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="d05b4-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Daniel Roth](https://github.com/danroth27), and [Scott Addie](https://github.com/scottaddie)</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="d05b4-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples/1.1)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="d05b4-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples/1.1) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="d05b4-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples/2.1)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="d05b4-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples/2.1) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>
::: moniker-end

<span data-ttu-id="d05b4-107">本文档介绍用于存储和检索敏感数据的 ASP.NET Core 应用程序开发过程的技术。</span><span class="sxs-lookup"><span data-stu-id="d05b4-107">This document explains techniques for storing and retrieving sensitive data during the development of an ASP.NET Core app.</span></span> <span data-ttu-id="d05b4-108">你应永远不会将密码或其他敏感数据存储在源代码中，并且你不应在开发过程中使用生产机密或测试模式。</span><span class="sxs-lookup"><span data-stu-id="d05b4-108">You should never store passwords or other sensitive data in source code, and you shouldn't use production secrets in development or test mode.</span></span> <span data-ttu-id="d05b4-109">你可以存储和保护与 Azure 的测试和生产机密[Azure 密钥保管库配置提供程序](xref:security/key-vault-configuration)。</span><span class="sxs-lookup"><span data-stu-id="d05b4-109">You can store and protect Azure test and production secrets with the [Azure Key Vault configuration provider](xref:security/key-vault-configuration).</span></span>

## <a name="environment-variables"></a><span data-ttu-id="d05b4-110">环境变量</span><span class="sxs-lookup"><span data-stu-id="d05b4-110">Environment variables</span></span>

<span data-ttu-id="d05b4-111">使用环境变量以避免在代码中或在本地配置文件中的应用程序机密存储。</span><span class="sxs-lookup"><span data-stu-id="d05b4-111">Environment variables are used to avoid storage of app secrets in code or in local configuration files.</span></span> <span data-ttu-id="d05b4-112">环境变量重写所有以前指定的配置源的配置的值。</span><span class="sxs-lookup"><span data-stu-id="d05b4-112">Environment variables override configuration values for all previously specified configuration sources.</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="d05b4-113">通过调用配置的环境变量值读取[AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables)中`Startup`构造函数：</span><span class="sxs-lookup"><span data-stu-id="d05b4-113">Configure the reading of environment variable values by calling [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) in the `Startup` constructor:</span></span>

<span data-ttu-id="d05b4-114">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=10)]</span><span class="sxs-lookup"><span data-stu-id="d05b4-114">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=10)]</span></span>
::: moniker-end

<span data-ttu-id="d05b4-115">请考虑在其中一个 ASP.NET 核心 web 应用**单个用户帐户**已启用安全性。</span><span class="sxs-lookup"><span data-stu-id="d05b4-115">Consider an ASP.NET Core web app in which **Individual User Accounts** security is enabled.</span></span> <span data-ttu-id="d05b4-116">默认数据库连接字符串包含在项目的*appsettings.json*文件与键`DefaultConnection`。</span><span class="sxs-lookup"><span data-stu-id="d05b4-116">A default database connection string is included in the project's *appsettings.json* file with the key `DefaultConnection`.</span></span> <span data-ttu-id="d05b4-117">默认连接字符串用于 LocalDB，在用户模式下运行，而且不需要密码。</span><span class="sxs-lookup"><span data-stu-id="d05b4-117">The default connection string is for LocalDB, which runs in user mode and doesn't require a password.</span></span> <span data-ttu-id="d05b4-118">应用程序在部署期间，`DefaultConnection`密钥值可以用环境变量的值重写。</span><span class="sxs-lookup"><span data-stu-id="d05b4-118">During app deployment, the `DefaultConnection` key value can be overridden with an environment variable's value.</span></span> <span data-ttu-id="d05b4-119">环境变量可以存储敏感的凭据与完整的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d05b4-119">The environment variable may store the complete connection string with sensitive credentials.</span></span>

> [!WARNING]
> <span data-ttu-id="d05b4-120">环境变量通常存储在未加密的纯文本。</span><span class="sxs-lookup"><span data-stu-id="d05b4-120">Environment variables are generally stored in plain, unencrypted text.</span></span> <span data-ttu-id="d05b4-121">如果计算机或进程受到攻击，则可以通过不受信任方访问环境变量。</span><span class="sxs-lookup"><span data-stu-id="d05b4-121">If the machine or process is compromised, environment variables can be accessed by untrusted parties.</span></span> <span data-ttu-id="d05b4-122">可能需要更多措施，防止用户的机密信息泄露。</span><span class="sxs-lookup"><span data-stu-id="d05b4-122">Additional measures to prevent disclosure of user secrets may be required.</span></span>

## <a name="secret-manager"></a><span data-ttu-id="d05b4-123">密码管理器</span><span class="sxs-lookup"><span data-stu-id="d05b4-123">Secret Manager</span></span>

<span data-ttu-id="d05b4-124">密码管理器工具在 ASP.NET Core 项目的开发过程中存储敏感数据。</span><span class="sxs-lookup"><span data-stu-id="d05b4-124">The Secret Manager tool stores sensitive data during the development of an ASP.NET Core project.</span></span> <span data-ttu-id="d05b4-125">在此上下文中，一种敏感数据是应用程序密钥。</span><span class="sxs-lookup"><span data-stu-id="d05b4-125">In this context, a piece of sensitive data is an app secret.</span></span> <span data-ttu-id="d05b4-126">应用程序机密存储在单独的位置，从项目树中。</span><span class="sxs-lookup"><span data-stu-id="d05b4-126">App secrets are stored in a separate location from the project tree.</span></span> <span data-ttu-id="d05b4-127">应用程序机密是与特定项目关联，或共享跨多个项目。</span><span class="sxs-lookup"><span data-stu-id="d05b4-127">The app secrets are associated with a specific project or shared across several projects.</span></span> <span data-ttu-id="d05b4-128">应用程序机密不签入源控件。</span><span class="sxs-lookup"><span data-stu-id="d05b4-128">The app secrets aren't checked into source control.</span></span>

> [!WARNING]
> <span data-ttu-id="d05b4-129">密码管理器工具不加密存储的机密信息，并不应被视为受信任存储区。</span><span class="sxs-lookup"><span data-stu-id="d05b4-129">The Secret Manager tool doesn't encrypt the stored secrets and shouldn't be treated as a trusted store.</span></span> <span data-ttu-id="d05b4-130">它是仅限开发目的。</span><span class="sxs-lookup"><span data-stu-id="d05b4-130">It's for development purposes only.</span></span> <span data-ttu-id="d05b4-131">键和值存储在用户配置文件目录中的 JSON 配置文件中。</span><span class="sxs-lookup"><span data-stu-id="d05b4-131">The keys and values are stored in a JSON configuration file in the user profile directory.</span></span>

## <a name="how-the-secret-manager-tool-works"></a><span data-ttu-id="d05b4-132">密码管理器工具的工作原理</span><span class="sxs-lookup"><span data-stu-id="d05b4-132">How the Secret Manager tool works</span></span>

<span data-ttu-id="d05b4-133">密码管理器工具避开实现详细信息，例如哪里和如何存储值。</span><span class="sxs-lookup"><span data-stu-id="d05b4-133">The Secret Manager tool abstracts away the implementation details, such as where and how the values are stored.</span></span> <span data-ttu-id="d05b4-134">无需知道这些实现的详细信息，可以使用该工具。</span><span class="sxs-lookup"><span data-stu-id="d05b4-134">You can use the tool without knowing these implementation details.</span></span> <span data-ttu-id="d05b4-135">这些值存储在[JSON](https://json.org/)受系统保护用户配置文件文件夹中本地计算机上的配置文件：</span><span class="sxs-lookup"><span data-stu-id="d05b4-135">The values are stored in a [JSON](https://json.org/) configuration file in a system-protected user profile folder on the local machine:</span></span>

* <span data-ttu-id="d05b4-136">Windows：`%APPDATA%\Microsoft\UserSecrets\<user_secrets_id>\secrets.json`</span><span class="sxs-lookup"><span data-stu-id="d05b4-136">Windows: `%APPDATA%\Microsoft\UserSecrets\<user_secrets_id>\secrets.json`</span></span>
* <span data-ttu-id="d05b4-137">Linux 和 macOS: `~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`</span><span class="sxs-lookup"><span data-stu-id="d05b4-137">Linux & macOS: `~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`</span></span>

<span data-ttu-id="d05b4-138">在前面文件路径中，将`<user_secrets_id>`与`UserSecretsId`中指定的值 *.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="d05b4-138">In the preceding file paths, replace `<user_secrets_id>` with the `UserSecretsId` value specified in the *.csproj* file.</span></span>

<span data-ttu-id="d05b4-139">不编写代码所依赖的位置或使用密码管理器工具中保存的数据的格式。</span><span class="sxs-lookup"><span data-stu-id="d05b4-139">Don't write code that depends on the location or format of data saved with the Secret Manager tool.</span></span> <span data-ttu-id="d05b4-140">这些实现的详细信息如有更改。</span><span class="sxs-lookup"><span data-stu-id="d05b4-140">These implementation details may change.</span></span> <span data-ttu-id="d05b4-141">例如，密钥值不加密，但是可能在将来。</span><span class="sxs-lookup"><span data-stu-id="d05b4-141">For example, the secret values aren't encrypted, but could be in the future.</span></span>

::: moniker range="<= aspnetcore-2.0"
## <a name="install-the-secret-manager-tool"></a><span data-ttu-id="d05b4-142">安装机密管理器工具</span><span class="sxs-lookup"><span data-stu-id="d05b4-142">Install the Secret Manager tool</span></span>

<span data-ttu-id="d05b4-143">密码管理器工具是与.NET 核心 SDK 2.1 中的.NET 核心 CLI 捆绑。</span><span class="sxs-lookup"><span data-stu-id="d05b4-143">The Secret Manager tool is bundled with the .NET Core CLI in .NET Core SDK 2.1.</span></span> <span data-ttu-id="d05b4-144">有关.NET 核心 SDK 2.0 及更早版本，则工具安装是必需的。</span><span class="sxs-lookup"><span data-stu-id="d05b4-144">For .NET Core SDK 2.0 and earlier, tool installation is necessary.</span></span>

<span data-ttu-id="d05b4-145">安装[Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) ASP.NET Core 项目中的 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="d05b4-145">Install the [Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) NuGet package in your ASP.NET Core project:</span></span>

<span data-ttu-id="d05b4-146">[!code-xml[](app-secrets/samples/1.1/UserSecrets/UserSecrets.csproj?name=snippet_CsprojFile&highlight=13-14)]</span><span class="sxs-lookup"><span data-stu-id="d05b4-146">[!code-xml[](app-secrets/samples/1.1/UserSecrets/UserSecrets.csproj?name=snippet_CsprojFile&highlight=13-14)]</span></span>

<span data-ttu-id="d05b4-147">在验证工具的安装命令行界面中执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="d05b4-147">Execute the following command in a command shell to validate the tool installation:</span></span>

```console
dotnet user-secrets -h
```

<span data-ttu-id="d05b4-148">密码管理器工具显示示例用法、 选项和命令帮助：</span><span class="sxs-lookup"><span data-stu-id="d05b4-148">The Secret Manager tool displays sample usage, options, and command help:</span></span>

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
> <span data-ttu-id="d05b4-149">你必须在与位于同一目录 *.csproj*文件以运行中定义的工具 *.csproj*文件的`DotNetCliToolReference`元素。</span><span class="sxs-lookup"><span data-stu-id="d05b4-149">You must be in the same directory as the *.csproj* file to run tools defined in the *.csproj* file's `DotNetCliToolReference` elements.</span></span>
::: moniker-end

## <a name="set-a-secret"></a><span data-ttu-id="d05b4-150">设置机密</span><span class="sxs-lookup"><span data-stu-id="d05b4-150">Set a secret</span></span>

<span data-ttu-id="d05b4-151">密码管理器工具进行存储用户配置文件中的特定于项目的配置设置操作。</span><span class="sxs-lookup"><span data-stu-id="d05b4-151">The Secret Manager tool operates on project-specific configuration settings stored in your user profile.</span></span> <span data-ttu-id="d05b4-152">若要使用用户的机密信息，定义`UserSecretsId`中的元素`PropertyGroup`的 *.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="d05b4-152">To use user secrets, define a `UserSecretsId` element within a `PropertyGroup` of the *.csproj* file.</span></span> <span data-ttu-id="d05b4-153">值`UserSecretsId`任意的但是唯一到项目。</span><span class="sxs-lookup"><span data-stu-id="d05b4-153">The value of `UserSecretsId` is arbitrary, but is unique to the project.</span></span> <span data-ttu-id="d05b4-154">开发人员通常应生成的 GUID `UserSecretsId`。</span><span class="sxs-lookup"><span data-stu-id="d05b4-154">Developers typically generate a GUID for the `UserSecretsId`.</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="d05b4-155">[!code-xml[](app-secrets/samples/1.1/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="d05b4-155">[!code-xml[](app-secrets/samples/1.1/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="d05b4-156">[!code-xml[](app-secrets/samples/2.1/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="d05b4-156">[!code-xml[](app-secrets/samples/2.1/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]</span></span>
::: moniker-end

> [!TIP]
> <span data-ttu-id="d05b4-157">在 Visual Studio 中，右键单击解决方案资源管理器中的项目，然后选择**管理用户的机密信息**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="d05b4-157">In Visual Studio, right-click the project in Solution Explorer, and select **Manage User Secrets** from the context menu.</span></span> <span data-ttu-id="d05b4-158">此手势添加`UserSecretsId`元素，为填充 GUID， *.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="d05b4-158">This gesture adds a `UserSecretsId` element, populated with a GUID, to the *.csproj* file.</span></span> <span data-ttu-id="d05b4-159">Visual Studio 将打开*secrets.json*在文本编辑器中的文件。</span><span class="sxs-lookup"><span data-stu-id="d05b4-159">Visual Studio opens a *secrets.json* file in the text editor.</span></span> <span data-ttu-id="d05b4-160">内容替换*secrets.json*要存储的键 / 值对。</span><span class="sxs-lookup"><span data-stu-id="d05b4-160">Replace the contents of *secrets.json* with the key-value pairs to be stored.</span></span> <span data-ttu-id="d05b4-161">例如：[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file.md)]</span><span class="sxs-lookup"><span data-stu-id="d05b4-161">For example: [!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file.md)]</span></span>

<span data-ttu-id="d05b4-162">定义一个键和其值组成应用程序密钥。</span><span class="sxs-lookup"><span data-stu-id="d05b4-162">Define an app secret consisting of a key and its value.</span></span> <span data-ttu-id="d05b4-163">密钥是与项目的关联`UserSecretsId`值。</span><span class="sxs-lookup"><span data-stu-id="d05b4-163">The secret is associated with the project's `UserSecretsId` value.</span></span> <span data-ttu-id="d05b4-164">例如，从在其中的目录运行以下命令 *.csproj*文件存在：</span><span class="sxs-lookup"><span data-stu-id="d05b4-164">For example, run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345"
```

<span data-ttu-id="d05b4-165">在前面的示例中，冒号表示`Movies`是一个对象文本替换`ServiceApiKey`属性。</span><span class="sxs-lookup"><span data-stu-id="d05b4-165">In the preceding example, the colon denotes that `Movies` is an object literal with a `ServiceApiKey` property.</span></span>

<span data-ttu-id="d05b4-166">密码管理器工具可以过使用从其他目录。</span><span class="sxs-lookup"><span data-stu-id="d05b4-166">The Secret Manager tool can be used from other directories too.</span></span> <span data-ttu-id="d05b4-167">使用`--project`选项提供文件系统路径，在此处 *.csproj*文件存在。</span><span class="sxs-lookup"><span data-stu-id="d05b4-167">Use the `--project` option to supply the file system path at which the *.csproj* file exists.</span></span> <span data-ttu-id="d05b4-168">例如：</span><span class="sxs-lookup"><span data-stu-id="d05b4-168">For example:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345" --project "C:\apps\WebApp1\src\WebApp1"
```

## <a name="set-multiple-secrets"></a><span data-ttu-id="d05b4-169">设置多个机密</span><span class="sxs-lookup"><span data-stu-id="d05b4-169">Set multiple secrets</span></span>

<span data-ttu-id="d05b4-170">可以通过管道传递到的 JSON 设置机密一批`set`命令。</span><span class="sxs-lookup"><span data-stu-id="d05b4-170">A batch of secrets can be set by piping JSON to the `set` command.</span></span> <span data-ttu-id="d05b4-171">在下面的示例中， *input.json*文件的内容通过管道传递给`set`命令在 Windows 上：</span><span class="sxs-lookup"><span data-stu-id="d05b4-171">In the following example, the *input.json* file's contents are piped to the `set` command on Windows:</span></span>

```console
type .\input.json | dotnet user-secrets set
```

<span data-ttu-id="d05b4-172">在 macOS 和 Linux 上使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="d05b4-172">Use the following command on macOS and Linux:</span></span>

```console
cat ./input.json | dotnet user-secrets set
```

## <a name="access-a-secret"></a><span data-ttu-id="d05b4-173">访问机密</span><span class="sxs-lookup"><span data-stu-id="d05b4-173">Access a secret</span></span>

<span data-ttu-id="d05b4-174">[ASP.NET 核心配置 API](xref:fundamentals/configuration/index)提供对机密 Manager 机密的访问。</span><span class="sxs-lookup"><span data-stu-id="d05b4-174">The [ASP.NET Core Configuration API](xref:fundamentals/configuration/index) provides access to Secret Manager secrets.</span></span> <span data-ttu-id="d05b4-175">如果目标.NET 核心 1.x 或.NET Framework 安装[Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="d05b4-175">If targeting .NET Core 1.x or .NET Framework, install the [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet package.</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="d05b4-176">添加到用户机密配置源`Startup`构造函数：</span><span class="sxs-lookup"><span data-stu-id="d05b4-176">Add the user secrets configuration source to the `Startup` constructor:</span></span>

<span data-ttu-id="d05b4-177">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=5-8)]</span><span class="sxs-lookup"><span data-stu-id="d05b4-177">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=5-8)]</span></span>
::: moniker-end

<span data-ttu-id="d05b4-178">可以通过检索用户的机密信息`Configuration`API:</span><span class="sxs-lookup"><span data-stu-id="d05b4-178">User secrets can be retrieved via the `Configuration` API:</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="d05b4-179">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=23)]</span><span class="sxs-lookup"><span data-stu-id="d05b4-179">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=23)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="d05b4-180">[!code-csharp[](app-secrets/samples/2.1/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=14)]</span><span class="sxs-lookup"><span data-stu-id="d05b4-180">[!code-csharp[](app-secrets/samples/2.1/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=14)]</span></span>
::: moniker-end

## <a name="string-replacement-with-secrets"></a><span data-ttu-id="d05b4-181">包含密码的字符串替换</span><span class="sxs-lookup"><span data-stu-id="d05b4-181">String replacement with secrets</span></span>

<span data-ttu-id="d05b4-182">以纯文本格式存储密码是危险的。</span><span class="sxs-lookup"><span data-stu-id="d05b4-182">Storing passwords in plain text is risky.</span></span> <span data-ttu-id="d05b4-183">例如，数据库连接字符串存储在*appsettings.json*可能包括指定用户的密码：</span><span class="sxs-lookup"><span data-stu-id="d05b4-183">For example, a database connection string stored in *appsettings.json* may include a password for the specified user:</span></span>

[!code-json[](app-secrets/samples/2.1/UserSecrets/appsettings-unsecure.json?highlight=3)]

<span data-ttu-id="d05b4-184">更安全的方法是将密码存储的机密形式。</span><span class="sxs-lookup"><span data-stu-id="d05b4-184">A more secure approach is to store the password as a secret.</span></span> <span data-ttu-id="d05b4-185">例如：</span><span class="sxs-lookup"><span data-stu-id="d05b4-185">For example:</span></span>

```console
dotnet user-secrets set "DbPassword" "pass123"
```

<span data-ttu-id="d05b4-186">替换中的密码*appsettings.json*其占位符。</span><span class="sxs-lookup"><span data-stu-id="d05b4-186">Replace the password in *appsettings.json* with a placeholder.</span></span> <span data-ttu-id="d05b4-187">在下面的示例中，`{0}`用作到窗体的占位符[复合格式字符串](/dotnet/standard/base-types/composite-formatting#composite-format-string)。</span><span class="sxs-lookup"><span data-stu-id="d05b4-187">In the following example, `{0}` is used as the placeholder to form a [Composite Format String](/dotnet/standard/base-types/composite-formatting#composite-format-string).</span></span>

[!code-json[](app-secrets/samples/2.1/UserSecrets/appsettings.json?highlight=3)]

<span data-ttu-id="d05b4-188">机密的值可以将其插入占位符以完成连接字符串：</span><span class="sxs-lookup"><span data-stu-id="d05b4-188">The secret's value can be injected into the placeholder to complete the connection string:</span></span>

::: moniker range="<= aspnetcore-1.1"
<span data-ttu-id="d05b4-189">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=23-25)]</span><span class="sxs-lookup"><span data-stu-id="d05b4-189">[!code-csharp[](app-secrets/samples/1.1/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=23-25)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.0"
<span data-ttu-id="d05b4-190">[!code-csharp[](app-secrets/samples/2.1/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=14-16)]</span><span class="sxs-lookup"><span data-stu-id="d05b4-190">[!code-csharp[](app-secrets/samples/2.1/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=14-16)]</span></span>
::: moniker-end

## <a name="list-the-secrets"></a><span data-ttu-id="d05b4-191">列出机密</span><span class="sxs-lookup"><span data-stu-id="d05b4-191">List the secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="d05b4-192">从在其中的目录运行以下命令 *.csproj*文件存在：</span><span class="sxs-lookup"><span data-stu-id="d05b4-192">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets list
```

<span data-ttu-id="d05b4-193">显示以下输出：</span><span class="sxs-lookup"><span data-stu-id="d05b4-193">The following output appears:</span></span>

```console
Movies:ServiceApiKey = 12345
Movies:ConnectionString = Server=(localdb)\mssqllocaldb;Database=Movie-1;Trusted_Connection=True;MultipleActiveResultSets=true
```

<span data-ttu-id="d05b4-194">在前面的示例中，在项名称中的冒号表示内的对象层次结构*secrets.json*。</span><span class="sxs-lookup"><span data-stu-id="d05b4-194">In the preceding example, a colon in the key names denotes the object hierarchy within *secrets.json*.</span></span>

## <a name="remove-a-single-secret"></a><span data-ttu-id="d05b4-195">删除单个机密</span><span class="sxs-lookup"><span data-stu-id="d05b4-195">Remove a single secret</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="d05b4-196">从在其中的目录运行以下命令 *.csproj*文件存在：</span><span class="sxs-lookup"><span data-stu-id="d05b4-196">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets remove "Movies:ConnectionString"
```

<span data-ttu-id="d05b4-197">应用程序的*secrets.json*已修改文件，以删除与关联的键 / 值对`MoviesConnectionString`密钥：</span><span class="sxs-lookup"><span data-stu-id="d05b4-197">The app's *secrets.json* file was modified to remove the key-value pair associated with the `MoviesConnectionString` key:</span></span>

```json
{
  "Movies": {
    "ServiceApiKey": "12345"
  }
}
```

<span data-ttu-id="d05b4-198">运行`dotnet user-secrets list`显示以下消息：</span><span class="sxs-lookup"><span data-stu-id="d05b4-198">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
Movies:ServiceApiKey = 12345
```

## <a name="remove-all-secrets"></a><span data-ttu-id="d05b4-199">删除所有机密</span><span class="sxs-lookup"><span data-stu-id="d05b4-199">Remove all secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="d05b4-200">从在其中的目录运行以下命令 *.csproj*文件存在：</span><span class="sxs-lookup"><span data-stu-id="d05b4-200">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets clear
```

<span data-ttu-id="d05b4-201">已从删除应用程序的所有用户机密*secrets.json*文件：</span><span class="sxs-lookup"><span data-stu-id="d05b4-201">All user secrets for the app have been deleted from the *secrets.json* file:</span></span>

```json
{}
```

<span data-ttu-id="d05b4-202">运行`dotnet user-secrets list`显示以下消息：</span><span class="sxs-lookup"><span data-stu-id="d05b4-202">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
No secrets configured for this application.
```

## <a name="additional-resources"></a><span data-ttu-id="d05b4-203">其他资源</span><span class="sxs-lookup"><span data-stu-id="d05b4-203">Additional resources</span></span>

* <xref:fundamentals/configuration/index>
* <xref:security/key-vault-configuration>