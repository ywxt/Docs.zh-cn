---
title: 使用 Apache 在 Linux 上托管 ASP.NET Core
description: 了解如何在 CentOS 上将 Apache 设置为反向代理服务器，以将 HTTP 流量重定向到在 Kestrel 上运行的 ASP.NET Core Web 应用。
author: spboyer
ms.author: spboyer
ms.custom: mvc
ms.date: 10/09/2018
uid: host-and-deploy/linux-apache
ms.openlocfilehash: 237646f839a4973074bb64176a024ebb3d32ee4e
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48913003"
---
# <a name="host-aspnet-core-on-linux-with-apache"></a><span data-ttu-id="c1b0b-103">使用 Apache 在 Linux 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="c1b0b-103">Host ASP.NET Core on Linux with Apache</span></span>

<span data-ttu-id="c1b0b-104">作者：[Shayne Boyer](https://github.com/spboyer)</span><span class="sxs-lookup"><span data-stu-id="c1b0b-104">By [Shayne Boyer](https://github.com/spboyer)</span></span>

<span data-ttu-id="c1b0b-105">使用本指南，了解如何在 [CentOS 7](https://www.centos.org/) 上将 [Apache](https://httpd.apache.org/) 设置为反向代理服务器，以将 HTTP 流量重定向到在 [Kestrel](xref:fundamentals/servers/kestrel) 上运行的 ASP.NET Core Web 应用。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-105">Using this guide, learn how to set up [Apache](https://httpd.apache.org/) as a reverse proxy server on [CentOS 7](https://www.centos.org/) to redirect HTTP traffic to an ASP.NET Core web app running on [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="c1b0b-106">[mod_proxy extension](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) 和相关模块可创建服务器的反向代理。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-106">The [mod_proxy extension](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) and related modules create the server's reverse proxy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1b0b-107">系统必备</span><span class="sxs-lookup"><span data-stu-id="c1b0b-107">Prerequisites</span></span>

1. <span data-ttu-id="c1b0b-108">运行 CentOS 7 的服务器，使用具有 sudo 特权的标准用户帐户。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-108">Server running CentOS 7 with a standard user account with sudo privilege.</span></span>
1. <span data-ttu-id="c1b0b-109">在服务器上安装 .NET Core 运行时。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-109">Install the .NET Core runtime on the server.</span></span>
   1. <span data-ttu-id="c1b0b-110">访问 [.NET Core“所有下载”页](https://www.microsoft.com/net/download/all)。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-110">Visit the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>
   1. <span data-ttu-id="c1b0b-111">从“运行时”下的列表中选择最新的非预览运行时。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-111">Select the latest non-preview runtime from the list under **Runtime**.</span></span>
   1. <span data-ttu-id="c1b0b-112">选择并执行适用于 CentOS/Oracle 的说明。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-112">Select and follow the instructions for CentOS/Oracle.</span></span>
1. <span data-ttu-id="c1b0b-113">一个现有 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-113">An existing ASP.NET Core app.</span></span>

## <a name="publish-and-copy-over-the-app"></a><span data-ttu-id="c1b0b-114">通过应用发布和复制</span><span class="sxs-lookup"><span data-stu-id="c1b0b-114">Publish and copy over the app</span></span>

<span data-ttu-id="c1b0b-115">配置应用以进行[依赖框架的部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-115">Configure the app for a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd).</span></span>

<span data-ttu-id="c1b0b-116">在开发环境中运行 [dotnet publish](/dotnet/core/tools/dotnet-publish)，将应用打包到可在服务器上运行的目录中（例如 bin/Release/&lt;target_framework_moniker&gt;/publish）：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-116">Run [dotnet publish](/dotnet/core/tools/dotnet-publish) from the development environment to package an app into a directory (for example, *bin/Release/&lt;target_framework_moniker&gt;/publish*) that can run on the server:</span></span>

```console
dotnet publish --configuration Release
```

<span data-ttu-id="c1b0b-117">如果不希望维护服务器上的 .NET Core 运行时，还可将应用发布为[独立部署](/dotnet/core/deploying/#self-contained-deployments-scd)。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-117">The app can also be published as a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd) if you prefer not to maintain the .NET Core runtime on the server.</span></span>

<span data-ttu-id="c1b0b-118">使用集成到组织工作流的工具（例如 SCP、SFTP）将 ASP.NET Core 应用复制到服务器。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-118">Copy the ASP.NET Core app to the server using a tool that integrates into the organization's workflow (for example, SCP, SFTP).</span></span> <span data-ttu-id="c1b0b-119">通常可在 var 目录（例如 var/www/helloapp）下找到 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-119">It's common to locate web apps under the *var* directory (for example, *var/www/helloapp*).</span></span>

> [!NOTE]
> <span data-ttu-id="c1b0b-120">在生产部署方案中，持续集成工作流会执行发布应用并将资产复制到服务器的工作。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-120">Under a production deployment scenario, a continuous integration workflow does the work of publishing the app and copying the assets to the server.</span></span>

## <a name="configure-a-proxy-server"></a><span data-ttu-id="c1b0b-121">配置代理服务器</span><span class="sxs-lookup"><span data-stu-id="c1b0b-121">Configure a proxy server</span></span>

<span data-ttu-id="c1b0b-122">反向代理是为动态 Web 应用提供服务的常见设置。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-122">A reverse proxy is a common setup for serving dynamic web apps.</span></span> <span data-ttu-id="c1b0b-123">反向代理终止 HTTP 请求，并将其转发到 ASP.NET 应用。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-123">The reverse proxy terminates the HTTP request and forwards it to the ASP.NET app.</span></span>

<span data-ttu-id="c1b0b-124">代理服务器将客户端请求转发到另一个服务器，而不是自身实现这些请求。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-124">A proxy server is one which forwards client requests to another server instead of fulfilling requests itself.</span></span> <span data-ttu-id="c1b0b-125">反向代理转发到固定的目标，通常代表任意客户端。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-125">A reverse proxy forwards to a fixed destination, typically on behalf of arbitrary clients.</span></span> <span data-ttu-id="c1b0b-126">在本指南中，Apache 被配置为反向代理，在 Kestrel 为 ASP.NET Core 应用提供服务的同一服务器上运行。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-126">In this guide, Apache is configured as the reverse proxy running on the same server that Kestrel is serving the ASP.NET Core app.</span></span>

<span data-ttu-id="c1b0b-127">由于请求是通过反向代理转接的，因此使用 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 包中的[转接头中间件](xref:host-and-deploy/proxy-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-127">Because requests are forwarded by reverse proxy, use the [Forwarded Headers Middleware](xref:host-and-deploy/proxy-load-balancer) from the [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) package.</span></span> <span data-ttu-id="c1b0b-128">此中间件使用 `X-Forwarded-Proto` 标头来更新 `Request.Scheme`，使重定向 URI 和其他安全策略能够正常工作。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-128">The middleware updates the `Request.Scheme`, using the `X-Forwarded-Proto` header, so that redirect URIs and other security policies work correctly.</span></span>

<span data-ttu-id="c1b0b-129">调用转接头中间件后，必须放置依赖于该架构的组件，例如身份验证、链接生成、重定向和地理位置。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-129">Any component that depends on the scheme, such as authentication, link generation, redirects, and geolocation, must be placed after invoking the Forwarded Headers Middleware.</span></span> <span data-ttu-id="c1b0b-130">作为一般规则，转接头中间件应在诊断和错误处理中间件以外的其他中间件之前运行。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-130">As a general rule, Forwarded Headers Middleware should run before other middleware except diagnostics and error handling middleware.</span></span> <span data-ttu-id="c1b0b-131">此顺序可确保依赖于转接头信息的中间件可以使用标头值进行处理。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-131">This ordering ensures that the middleware relying on forwarded headers information can consume the header values for processing.</span></span>

::: moniker range=">= aspnetcore-2.0"

> [!NOTE]
> <span data-ttu-id="c1b0b-132">使用或不使用反向代理服务器进行配置对 ASP.NET Core 2.0 或更高版本的应用来说都是有效且受支持的托管配置。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-132">Either configuration&mdash;with or without a reverse proxy server&mdash;is a valid and supported hosting configuration for ASP.NET Core 2.0 or later apps.</span></span> <span data-ttu-id="c1b0b-133">有关详细信息，请参阅[何时结合使用 Kestrel 和反向代理](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-133">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

::: moniker-end

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="c1b0b-134">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="c1b0b-134">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="c1b0b-135">在调用 [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) 或类似的身份验证方案中间件之前，调用 `Startup.Configure` 中的 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 方法。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-135">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) or similar authentication scheme middleware.</span></span> <span data-ttu-id="c1b0b-136">配置中间件以转接 `X-Forwarded-For` 和 `X-Forwarded-Proto` 标头：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-136">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="c1b0b-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="c1b0b-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="c1b0b-138">在调用 [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) 和 [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) 或类似的身份验证方案中间件之前，调用 `Startup.Configure` 中的 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 方法。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-138">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) and [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) or similar authentication scheme middleware.</span></span> <span data-ttu-id="c1b0b-139">配置中间件以转接 `X-Forwarded-For` 和 `X-Forwarded-Proto` 标头：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-139">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseIdentity();
app.UseFacebookAuthentication(new FacebookOptions()
{
    AppId = Configuration["Authentication:Facebook:AppId"],
    AppSecret = Configuration["Authentication:Facebook:AppSecret"]
});
```

---

<span data-ttu-id="c1b0b-140">如果没有为中间件指定 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)，则要转接的默认标头为 `None`。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-140">If no [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) are specified to the middleware, the default headers to forward are `None`.</span></span>

<span data-ttu-id="c1b0b-141">默认情况下仅信任 localhost (127.0.0.1, [::1]) 上运行的代理。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-141">Only proxies running on localhost (127.0.0.1, [::1]) are trusted by default.</span></span> <span data-ttu-id="c1b0b-142">如果组织内的其他受信任代理或网络处理 Internet 与 Web 服务器之间的请求，请使用 <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions> 将其添加到 <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownProxies*> 或 <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownNetworks*> 的列表。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-142">If other trusted proxies or networks within the organization handle requests between the Internet and the web server, add them to the list of <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownProxies*> or <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownNetworks*> with <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions>.</span></span> <span data-ttu-id="c1b0b-143">以下示例会将 IP 地址为 10.0.0.100 的受信任代理服务器添加到 `Startup.ConfigureServices` 中的转接头中间件 `KnownProxies`：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-143">The following example adds a trusted proxy server at IP address 10.0.0.100 to the Forwarded Headers Middleware `KnownProxies` in `Startup.ConfigureServices`:</span></span>

```csharp
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.KnownProxies.Add(IPAddress.Parse("10.0.0.100"));
});
```

<span data-ttu-id="c1b0b-144">有关更多信息，请参见<xref:host-and-deploy/proxy-load-balancer>。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-144">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>

### <a name="install-apache"></a><span data-ttu-id="c1b0b-145">安装 Apache</span><span class="sxs-lookup"><span data-stu-id="c1b0b-145">Install Apache</span></span>

<span data-ttu-id="c1b0b-146">将 CentOS 包更新为其最新稳定版本：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-146">Update CentOS packages to their latest stable versions:</span></span>

```bash
sudo yum update -y
```

<span data-ttu-id="c1b0b-147">使用单个 `yum` 命令在 CentOS 上安装 Apache Web 服务器：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-147">Install the Apache web server on CentOS with a single `yum` command:</span></span>

```bash
sudo yum -y install httpd mod_ssl
```

<span data-ttu-id="c1b0b-148">运行该命令后的示例输出：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-148">Sample output after running the command:</span></span>

```bash
Downloading packages:
httpd-2.4.6-40.el7.centos.4.x86_64.rpm               | 2.7 MB  00:00:01
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Installing : httpd-2.4.6-40.el7.centos.4.x86_64      1/1 
Verifying  : httpd-2.4.6-40.el7.centos.4.x86_64      1/1 

Installed:
httpd.x86_64 0:2.4.6-40.el7.centos.4

Complete!
```

> [!NOTE]
> <span data-ttu-id="c1b0b-149">在此示例中，输出反映了 httpd.86_64，因为 CentOS 7 版本是 64 位的。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-149">In this example, the output reflects httpd.86_64 since the CentOS 7 version is 64 bit.</span></span> <span data-ttu-id="c1b0b-150">若要验证 Apache 的安装位置，请从命令提示符运行 `whereis httpd`。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-150">To verify where Apache is installed, run `whereis httpd` from a command prompt.</span></span>

### <a name="configure-apache"></a><span data-ttu-id="c1b0b-151">配置 Apache</span><span class="sxs-lookup"><span data-stu-id="c1b0b-151">Configure Apache</span></span>

<span data-ttu-id="c1b0b-152">Apache 的配置文件位于 `/etc/httpd/conf.d/` 目录内。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-152">Configuration files for Apache are located within the `/etc/httpd/conf.d/` directory.</span></span> <span data-ttu-id="c1b0b-153">除了 `/etc/httpd/conf.modules.d/` 中的模块配置文件外（其中包含加载模块所需的任何配置文件），将对任何带 .conf 扩展名的文件按字母顺序进行处理。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-153">Any file with the *.conf* extension is processed in alphabetical order in addition to the module configuration files in `/etc/httpd/conf.modules.d/`, which contains any configuration files necessary to load modules.</span></span>

<span data-ttu-id="c1b0b-154">为应用创建名为 helloapp.conf 的配置文件：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-154">Create a configuration file, named *helloapp.conf*, for the app:</span></span>

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ServerName www.example.com
    ServerAlias *.example.com
    ErrorLog ${APACHE_LOG_DIR}helloapp-error.log
    CustomLog ${APACHE_LOG_DIR}helloapp-access.log common
</VirtualHost>
```

<span data-ttu-id="c1b0b-155">`VirtualHost` 块可以在服务器上的一个或多个文件中多次出现。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-155">The `VirtualHost` block can appear multiple times, in one or more files on a server.</span></span> <span data-ttu-id="c1b0b-156">在前面的配置文件中，Apache 接受端口 80 上的公共流量。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-156">In the preceding configuration file, Apache accepts public traffic on port 80.</span></span> <span data-ttu-id="c1b0b-157">正在向域 `www.example.com` 提供服务，`*.example.com` 别名解析为同一网站。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-157">The domain `www.example.com` is being served, and the `*.example.com` alias resolves to the same website.</span></span> <span data-ttu-id="c1b0b-158">有关详细信息，请参阅[基于名称的虚拟主机支持](https://httpd.apache.org/docs/current/vhosts/name-based.html)。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-158">See [Name-based virtual host support](https://httpd.apache.org/docs/current/vhosts/name-based.html) for more information.</span></span> <span data-ttu-id="c1b0b-159">请求会通过代理从根位置转到 127.0.0.1 处的服务器的端口 5000。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-159">Requests are proxied at the root to port 5000 of the server at 127.0.0.1.</span></span> <span data-ttu-id="c1b0b-160">对于双向通信，需要 `ProxyPass` 和 `ProxyPassReverse`。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-160">For bi-directional communication, `ProxyPass` and `ProxyPassReverse` are required.</span></span> <span data-ttu-id="c1b0b-161">要更改 Kestrel 的 IP/端口，请参阅 [Kestrel：终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-161">To change Kestrel's IP/port, see [Kestrel: Endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration).</span></span>

> [!WARNING]
> <span data-ttu-id="c1b0b-162">未能指定 VirtualHost 块中的正确 [ServerName 指令](https://httpd.apache.org/docs/current/mod/core.html#servername)会公开应用的安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-162">Failure to specify a proper [ServerName directive](https://httpd.apache.org/docs/current/mod/core.html#servername) in the **VirtualHost** block exposes your app to security vulnerabilities.</span></span> <span data-ttu-id="c1b0b-163">如果可控制整个父域（区别于易受攻击的 `*.com`），则子域通配符绑定（例如，`*.example.com`）不具有此安全风险。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-163">Subdomain wildcard binding (for example, `*.example.com`) doesn't pose this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="c1b0b-164">有关详细信息，请参阅 [rfc7230 第 5.4 条](https://tools.ietf.org/html/rfc7230#section-5.4)。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-164">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

<span data-ttu-id="c1b0b-165">可以使用 `ErrorLog` 和 `CustomLog` 指令配置每个 `VirtualHost` 的日志记录。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-165">Logging can be configured per `VirtualHost` using `ErrorLog` and `CustomLog` directives.</span></span> <span data-ttu-id="c1b0b-166">`ErrorLog` 是服务器记录错误的位置，`CustomLog` 则设置文件名和日志文件的格式。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-166">`ErrorLog` is the location where the server logs errors, and `CustomLog` sets the filename and format of log file.</span></span> <span data-ttu-id="c1b0b-167">在这种情况下，这是记录请求信息的位置。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-167">In this case, this is where request information is logged.</span></span> <span data-ttu-id="c1b0b-168">每个请求将各占一行。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-168">There's one line for each request.</span></span>

<span data-ttu-id="c1b0b-169">保存文件，并测试配置。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-169">Save the file and test the configuration.</span></span> <span data-ttu-id="c1b0b-170">如果一切正常，响应应为 `Syntax [OK]`。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-170">If everything passes, the response should be `Syntax [OK]`.</span></span>

```bash
sudo service httpd configtest
```

<span data-ttu-id="c1b0b-171">重新启动 Apache：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-171">Restart Apache:</span></span>

```bash
sudo systemctl restart httpd
sudo systemctl enable httpd
```

## <a name="monitoring-the-app"></a><span data-ttu-id="c1b0b-172">监视应用</span><span class="sxs-lookup"><span data-stu-id="c1b0b-172">Monitoring the app</span></span>

<span data-ttu-id="c1b0b-173">Apache 现在已设置为将对 `http://localhost:80` 发起的请求转发到运行在 `http://127.0.0.1:5000` 处的 Kestrel 上的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-173">Apache is now setup to forward requests made to `http://localhost:80` to the ASP.NET Core app running on Kestrel at `http://127.0.0.1:5000`.</span></span>  <span data-ttu-id="c1b0b-174">但是，未将 Apache 设置为管理 Kestrel 进程。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-174">However, Apache isn't set up to manage the Kestrel process.</span></span> <span data-ttu-id="c1b0b-175">使用 systemd，并创建服务文件以启动和监视基础 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-175">Use *systemd* and create a service file to start and monitor the underlying web app.</span></span> <span data-ttu-id="c1b0b-176">systemd 是一个 init 系统，可以提供用于启动、停止和管理进程的许多强大的功能。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-176">*systemd* is an init system that provides many powerful features for starting, stopping, and managing processes.</span></span> 

### <a name="create-the-service-file"></a><span data-ttu-id="c1b0b-177">创建服务文件</span><span class="sxs-lookup"><span data-stu-id="c1b0b-177">Create the service file</span></span>

<span data-ttu-id="c1b0b-178">创建服务定义文件：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-178">Create the service definition file:</span></span>

```bash
sudo nano /etc/systemd/system/kestrel-helloapp.service
```

<span data-ttu-id="c1b0b-179">应用的一个示例服务文件：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-179">An example service file for the app:</span></span>

```
[Unit]
Description=Example .NET Web API App running on CentOS 7

[Service]
WorkingDirectory=/var/www/helloapp
ExecStart=/usr/local/bin/dotnet /var/www/helloapp/helloapp.dll
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=dotnet-example
User=apache
Environment=ASPNETCORE_ENVIRONMENT=Production 

[Install]
WantedBy=multi-user.target
```

<span data-ttu-id="c1b0b-180">如果配置未使用用户 *apache*，则必须先创建用户，并为该用户提供适当的文件所有权。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-180">If the user *apache* isn't used by the configuration, the user must be created first and given proper ownership of files.</span></span>

<span data-ttu-id="c1b0b-181">使用 `TimeoutStopSec` 配置在收到初始中断信号后等待应用程序关闭的持续时间。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-181">Use `TimeoutStopSec` to configure the duration of time to wait for the app to shut down after it receives the initial interrupt signal.</span></span> <span data-ttu-id="c1b0b-182">如果应用程序在此时间段内未关闭，则将发出 SIGKILL 以终止该应用程序。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-182">If the app doesn't shut down in this period, SIGKILL is issued to terminate the app.</span></span> <span data-ttu-id="c1b0b-183">提供作为无单位秒数的值（例如，`150`）、时间跨度值（例如，`2min 30s`）或 `infinity` 以禁用超时。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-183">Provide the value as unitless seconds (for example, `150`), a time span value (for example, `2min 30s`), or `infinity` to disable the timeout.</span></span> <span data-ttu-id="c1b0b-184">`TimeoutStopSec` 默认为管理器配置文件（*systemd-system.conf*、*system.conf.d*、*systemd-user.conf*、*user.conf.d*）中 `DefaultTimeoutStopSec` 的值。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-184">`TimeoutStopSec` defaults to the value of `DefaultTimeoutStopSec` in the manager configuration file (*systemd-system.conf*, *system.conf.d*, *systemd-user.conf*, *user.conf.d*).</span></span> <span data-ttu-id="c1b0b-185">大多数分发版的默认超时时间为 90 秒。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-185">The default timeout for most distributions is 90 seconds.</span></span>

```
# The default value is 90 seconds for most distributions.
TimeoutStopSec=90
```

<span data-ttu-id="c1b0b-186">必须转义某些值（例如，SQL 连接字符串）以供配置提供程序读取环境变量。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-186">Some values (for example, SQL connection strings) must be escaped for the configuration providers to read the environment variables.</span></span> <span data-ttu-id="c1b0b-187">使用以下命令生成适当的转义值以供在配置文件中使用：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-187">Use the following command to generate a properly escaped value for use in the configuration file:</span></span>

```console
systemd-escape "<value-to-escape>"
```

<span data-ttu-id="c1b0b-188">保存该文件并启用该服务：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-188">Save the file and enable the service:</span></span>

```bash
sudo systemctl enable kestrel-helloapp.service
```

<span data-ttu-id="c1b0b-189">启动该服务，并确认它正在运行：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-189">Start the service and verify that it's running:</span></span>

```bash
sudo systemctl start kestrel-helloapp.service
sudo systemctl status kestrel-helloapp.service

● kestrel-helloapp.service - Example .NET Web API App running on CentOS 7
    Loaded: loaded (/etc/systemd/system/kestrel-helloapp.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-helloapp.service
            └─9021 /usr/local/bin/dotnet /var/www/helloapp/helloapp.dll
```

<span data-ttu-id="c1b0b-190">在配置了反向代理并通过 systemd 管理 Kestrel 后，Web 应用现已完全配置，并能在本地计算机上的浏览器中从 `http://localhost` 进行访问。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-190">With the reverse proxy configured and Kestrel managed through *systemd*, the web app is fully configured and can be accessed from a browser on the local machine at `http://localhost`.</span></span> <span data-ttu-id="c1b0b-191">检查响应标头，服务器标头表示 ASP.NET Core 应用由 Kestrel 提供服务：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-191">Inspecting the response headers, the **Server** header indicates that the ASP.NET Core app is served by Kestrel:</span></span>

```
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a><span data-ttu-id="c1b0b-192">查看日志</span><span class="sxs-lookup"><span data-stu-id="c1b0b-192">Viewing logs</span></span>

<span data-ttu-id="c1b0b-193">由于使用 Kestrel 的 Web 应用是通过 systemd 进行管理的，因此事件和进程将记录到集中日志。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-193">Since the web app using Kestrel is managed using *systemd*, events and processes are logged to a centralized journal.</span></span> <span data-ttu-id="c1b0b-194">但是，此日志包含由 systemd 管理的所有服务和进程的条目。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-194">However, this journal includes entries for all of the services and processes managed by *systemd*.</span></span> <span data-ttu-id="c1b0b-195">若要查看特定于 `kestrel-helloapp.service` 的项，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-195">To view the `kestrel-helloapp.service`-specific items, use the following command:</span></span>

```bash
sudo journalctl -fu kestrel-helloapp.service
```

<span data-ttu-id="c1b0b-196">若要进行时间筛选，请使用命令指定时间选项。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-196">For time filtering, specify time options with the command.</span></span> <span data-ttu-id="c1b0b-197">例如，使用 `--since today` 筛选出当天或 `--until 1 hour ago` 来查看前一小时的条目。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-197">For example, use `--since today` to filter for the current day or `--until 1 hour ago` to see the previous hour's entries.</span></span> <span data-ttu-id="c1b0b-198">有关详细信息，请参阅 [journalctl 手册页](https://www.unix.com/man-page/centos/1/journalctl/)。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-198">For more information, see the [man page for journalctl](https://www.unix.com/man-page/centos/1/journalctl/).</span></span>

```bash
sudo journalctl -fu kestrel-helloapp.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="data-protection"></a><span data-ttu-id="c1b0b-199">数据保护</span><span class="sxs-lookup"><span data-stu-id="c1b0b-199">Data protection</span></span>

<span data-ttu-id="c1b0b-200">[ASP.NET Core 数据保护堆栈](xref:security/data-protection/index)由多个 ASP.NET Core [中间件](xref:fundamentals/middleware/index)（包括 cookie 中间件等身份验证中间件）和跨站点请求伪造 (CSRF) 保护使用。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-200">The [ASP.NET Core Data Protection stack](xref:security/data-protection/index) is used by several ASP.NET Core [middlewares](xref:fundamentals/middleware/index), including authentication middleware (for example, cookie middleware) and cross-site request forgery (CSRF) protections.</span></span> <span data-ttu-id="c1b0b-201">即使用户代码不调用数据保护 API，也应该配置数据保护，以创建持久的加密[密钥存储](xref:security/data-protection/implementation/key-management)。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-201">Even if Data Protection APIs aren't called by user code, data protection should be configured to create a persistent cryptographic [key store](xref:security/data-protection/implementation/key-management).</span></span> <span data-ttu-id="c1b0b-202">如果不配置数据保护，则密钥存储在内存中。重启应用时，密钥会被丢弃。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-202">If data protection isn't configured, the keys are held in memory and discarded when the app restarts.</span></span>

<span data-ttu-id="c1b0b-203">如果密钥环存储于内存中，则在应用重启时：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-203">If the key ring is stored in memory when the app restarts:</span></span>

* <span data-ttu-id="c1b0b-204">所有基于 cookie 的身份验证令牌都无效。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-204">All cookie-based authentication tokens are invalidated.</span></span>
* <span data-ttu-id="c1b0b-205">用户需要在下一次请求时再次登录。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-205">Users are required to sign in again on their next request.</span></span>
* <span data-ttu-id="c1b0b-206">无法再解密使用密钥环保护的任何数据。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-206">Any data protected with the key ring can no longer be decrypted.</span></span> <span data-ttu-id="c1b0b-207">这可能包括 [CSRF 令牌](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration)和 [ASP.NET Core MVC TempData cookie](xref:fundamentals/app-state#tempdata)。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-207">This may include [CSRF tokens](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) and [ASP.NET Core MVC TempData cookies](xref:fundamentals/app-state#tempdata).</span></span>

<span data-ttu-id="c1b0b-208">若要配置数据保护以持久保存并加密密钥环，请参阅：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-208">To configure data protection to persist and encrypt the key ring, see:</span></span>

* <xref:security/data-protection/implementation/key-storage-providers>
* <xref:security/data-protection/implementation/key-encryption-at-rest>

## <a name="securing-the-app"></a><span data-ttu-id="c1b0b-209">保护应用</span><span class="sxs-lookup"><span data-stu-id="c1b0b-209">Securing the app</span></span>

### <a name="configure-firewall"></a><span data-ttu-id="c1b0b-210">配置防火墙</span><span class="sxs-lookup"><span data-stu-id="c1b0b-210">Configure firewall</span></span>

<span data-ttu-id="c1b0b-211">*Firewalld* 是管理防火墙的动态守护程序，支持网络区域。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-211">*Firewalld* is a dynamic daemon to manage the firewall with support for network zones.</span></span> <span data-ttu-id="c1b0b-212">仍可以使用 iptable 管理端口和数据包筛选。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-212">Ports and packet filtering can still be managed by iptables.</span></span> <span data-ttu-id="c1b0b-213">默认情况下应安装 *Firewalld*。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-213">*Firewalld* should be installed by default.</span></span> <span data-ttu-id="c1b0b-214">`yum` 可用于安装包或验证是否已安装。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-214">`yum` can be used to install the package or verify it's installed.</span></span>

```bash
sudo yum install firewalld -y
```

<span data-ttu-id="c1b0b-215">使用 `firewalld` 仅打开应用所需的端口。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-215">Use `firewalld` to open only the ports needed for the app.</span></span> <span data-ttu-id="c1b0b-216">在此示例中，使用的是端口 80 和 443。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-216">In this case, port 80 and 443 are used.</span></span> <span data-ttu-id="c1b0b-217">以下命令将端口 80 和 443 永久设置为打开：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-217">The following commands permanently set ports 80 and 443 to open:</span></span>

```bash
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --add-port=443/tcp --permanent
```

<span data-ttu-id="c1b0b-218">重新加载防火墙设置。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-218">Reload the firewall settings.</span></span> <span data-ttu-id="c1b0b-219">检查默认区域中可用的服务和端口。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-219">Check the available services and ports in the default zone.</span></span> <span data-ttu-id="c1b0b-220">通过检查 `firewall-cmd -h` 获取可用选项。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-220">Options are available by inspecting `firewall-cmd -h`.</span></span>

```bash
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```

```bash
public (default, active)
interfaces: eth0
sources: 
services: dhcpv6-client
ports: 443/tcp 80/tcp
masquerade: no
forward-ports: 
icmp-blocks: 
rich rules: 
```

### <a name="ssl-configuration"></a><span data-ttu-id="c1b0b-221">SSL 配置</span><span class="sxs-lookup"><span data-stu-id="c1b0b-221">SSL configuration</span></span>

<span data-ttu-id="c1b0b-222">若要配置 Apache 用于 SSL，需使用 mod_ssl 模块。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-222">To configure Apache for SSL, the *mod_ssl* module is used.</span></span> <span data-ttu-id="c1b0b-223">安装了 httpd 模块时，也会安装了 mod_ssl 模块。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-223">When the *httpd* module was installed, the *mod_ssl* module was also installed.</span></span> <span data-ttu-id="c1b0b-224">如果未安装，请使用 `yum` 将其添加到配置。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-224">If it wasn't installed, use `yum` to add it to the configuration.</span></span>

```bash
sudo yum install mod_ssl
```

<span data-ttu-id="c1b0b-225">若要强制使用 SSL，请安装 `mod_rewrite` 模块以启用 URL 重写：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-225">To enforce SSL, install the `mod_rewrite` module to enable URL rewriting:</span></span>

```bash
sudo yum install mod_rewrite
```

<span data-ttu-id="c1b0b-226">修改 helloapp.conf 文件以启用 URL 重写和端口 443 上的安全通信：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-226">Modify the *helloapp.conf* file to enable URL rewriting and secure communication on port 443:</span></span>

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>

<VirtualHost *:443>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ErrorLog /var/log/httpd/helloapp-error.log
    CustomLog /var/log/httpd/helloapp-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

> [!NOTE]
> <span data-ttu-id="c1b0b-227">此示例中使用了本地生成的证书。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-227">This example is using a locally-generated certificate.</span></span> <span data-ttu-id="c1b0b-228">SSLCertificateFile 应为域名的主证书文件。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-228">**SSLCertificateFile** should be the primary certificate file for the domain name.</span></span> <span data-ttu-id="c1b0b-229">SSLCertificateKeyFile 应为创建 CSR 时生成的密钥文件。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-229">**SSLCertificateKeyFile** should be the key file generated when CSR is created.</span></span> <span data-ttu-id="c1b0b-230">SSLCertificateChainFile 应为证书颁发机构提供的中间证书文件（如有）。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-230">**SSLCertificateChainFile** should be the intermediate certificate file (if any) that was supplied by the certificate authority.</span></span>

<span data-ttu-id="c1b0b-231">保存文件，并测试配置：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-231">Save the file and test the configuration:</span></span>

```bash
sudo service httpd configtest
```

<span data-ttu-id="c1b0b-232">重新启动 Apache：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-232">Restart Apache:</span></span>

```bash
sudo systemctl restart httpd
```

## <a name="additional-apache-suggestions"></a><span data-ttu-id="c1b0b-233">其他 Apache 建议</span><span class="sxs-lookup"><span data-stu-id="c1b0b-233">Additional Apache suggestions</span></span>

### <a name="additional-headers"></a><span data-ttu-id="c1b0b-234">其他标头</span><span class="sxs-lookup"><span data-stu-id="c1b0b-234">Additional headers</span></span>

<span data-ttu-id="c1b0b-235">为了防止恶意攻击，应对一些标头进行修改或添加一些标头。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-235">In order to secure against malicious attacks, there are a few headers that should either be modified or added.</span></span> <span data-ttu-id="c1b0b-236">确保已安装 `mod_headers` 模块：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-236">Ensure that the `mod_headers` module is installed:</span></span>

```bash
sudo yum install mod_headers
```

#### <a name="secure-apache-from-clickjacking-attacks"></a><span data-ttu-id="c1b0b-237">保护 Apache 免受点击劫持攻击</span><span class="sxs-lookup"><span data-stu-id="c1b0b-237">Secure Apache from clickjacking attacks</span></span>

<span data-ttu-id="c1b0b-238">[点击劫持](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger)（也称为 *UI 伪装攻击*）是一种恶意攻击，其中网站访问者会上当受骗，从而导致在与当前要访问的页面不同的页面上单击链接或按钮。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-238">[Clickjacking](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger), also known as a *UI redress attack*, is a malicious attack where a website visitor is tricked into clicking a link or button on a different page than they're currently visiting.</span></span> <span data-ttu-id="c1b0b-239">使用 `X-FRAME-OPTIONS` 可保护网站。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-239">Use `X-FRAME-OPTIONS` to secure the site.</span></span>

<span data-ttu-id="c1b0b-240">编辑 *httpd.conf* 文件：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-240">Edit the *httpd.conf* file:</span></span>

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

<span data-ttu-id="c1b0b-241">添加行 `Header append X-FRAME-OPTIONS "SAMEORIGIN"`。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-241">Add the line `Header append X-FRAME-OPTIONS "SAMEORIGIN"`.</span></span> <span data-ttu-id="c1b0b-242">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-242">Save the file.</span></span> <span data-ttu-id="c1b0b-243">重启 Apache。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-243">Restart Apache.</span></span>

#### <a name="mime-type-sniffing"></a><span data-ttu-id="c1b0b-244">MIME 类型探查</span><span class="sxs-lookup"><span data-stu-id="c1b0b-244">MIME-type sniffing</span></span>

<span data-ttu-id="c1b0b-245">`X-Content-Type-Options` 标头阻止 Internet Explorer 进行 *MIME 探查*（从文件内容中确定文件的 `Content-Type`）。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-245">The `X-Content-Type-Options` header prevents Internet Explorer from *MIME-sniffing* (determining a file's `Content-Type` from the file's content).</span></span> <span data-ttu-id="c1b0b-246">如果服务器通过设置 `nosniff` 选项将 `Content-Type` 标头设置为 `text/html`，则不管文件内容为何，Internet Explorer 都会将内容呈现为 `text/html`。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-246">If the server sets the `Content-Type` header to `text/html` with the `nosniff` option set, Internet Explorer renders the content as `text/html` regardless of the file's content.</span></span>

<span data-ttu-id="c1b0b-247">编辑 *httpd.conf* 文件：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-247">Edit the *httpd.conf* file:</span></span>

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

<span data-ttu-id="c1b0b-248">添加行 `Header set X-Content-Type-Options "nosniff"`。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-248">Add the line `Header set X-Content-Type-Options "nosniff"`.</span></span> <span data-ttu-id="c1b0b-249">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-249">Save the file.</span></span> <span data-ttu-id="c1b0b-250">重启 Apache。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-250">Restart Apache.</span></span>

### <a name="load-balancing"></a><span data-ttu-id="c1b0b-251">负载平衡</span><span class="sxs-lookup"><span data-stu-id="c1b0b-251">Load Balancing</span></span>

<span data-ttu-id="c1b0b-252">此示例演示如何在同一实例计算机上的 CentOS 7 和 Kestrel 上设置和配置 Apache。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-252">This example shows how to setup and configure Apache on CentOS 7 and Kestrel on the same instance machine.</span></span> <span data-ttu-id="c1b0b-253">为了不出现单一故障点；使用 mod_proxy_balancer 并修改 VirtualHost 可实现在 Apache 代理服务器后方管理 Web 应用的多个实例。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-253">In order to not have a single point of failure; using *mod_proxy_balancer* and modifying the **VirtualHost** would allow for managing multiple instances of the web apps behind the Apache proxy server.</span></span>

```bash
sudo yum install mod_proxy_balancer
```

<span data-ttu-id="c1b0b-254">在下面所示的配置文件中，`helloapp` 的其他实例设置为在端口 5001 上运行。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-254">In the configuration file shown below, an additional instance of the `helloapp` is set up to run on port 5001.</span></span> <span data-ttu-id="c1b0b-255">“代理”部分设置了具有两个成员的均衡器配置，以便对 byrequests 进行负载均衡。</span><span class="sxs-lookup"><span data-stu-id="c1b0b-255">The *Proxy* section is set with a balancer configuration with two members to load balance *byrequests*.</span></span>

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>

<VirtualHost *:443>
    ProxyPass / balancer://mycluster/ 

    ProxyPassReverse / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5001/

    <Proxy balancer://mycluster>
        BalancerMember http://127.0.0.1:5000
        BalancerMember http://127.0.0.1:5001 
        ProxySet lbmethod=byrequests
    </Proxy>

    <Location />
        SetHandler balancer
    </Location>
    ErrorLog /var/log/httpd/helloapp-error.log
    CustomLog /var/log/httpd/helloapp-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

### <a name="rate-limits"></a><span data-ttu-id="c1b0b-256">速率限制</span><span class="sxs-lookup"><span data-stu-id="c1b0b-256">Rate Limits</span></span>

<span data-ttu-id="c1b0b-257">使用 httpd 模块中包含的 mod_ratelimit，客户端的带宽可以限制为：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-257">Using *mod_ratelimit*, which is included in the *httpd* module, the bandwidth of clients can be limited:</span></span>

```bash
sudo nano /etc/httpd/conf.d/ratelimit.conf
```
<span data-ttu-id="c1b0b-258">示例文件将根位置下的带宽限制为 600 KB/秒：</span><span class="sxs-lookup"><span data-stu-id="c1b0b-258">The example file limits bandwidth as 600 KB/sec under the root location:</span></span>

```
<IfModule mod_ratelimit.c>
    <Location />
        SetOutputFilter RATE_LIMIT
        SetEnv rate-limit 600
    </Location>
</IfModule>
```

## <a name="additional-resources"></a><span data-ttu-id="c1b0b-259">其他资源</span><span class="sxs-lookup"><span data-stu-id="c1b0b-259">Additional resources</span></span>

* [<span data-ttu-id="c1b0b-260">配置 ASP.NET Core 以使用代理服务器和负载均衡器</span><span class="sxs-lookup"><span data-stu-id="c1b0b-260">Configure ASP.NET Core to work with proxy servers and load balancers</span></span>](xref:host-and-deploy/proxy-load-balancer)
