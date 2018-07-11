---
title: 使用 Nginx 在 Linux 上托管 ASP.NET Core
author: rick-anderson
description: 了解如何在 Ubuntu 16.04 上将 Nginx 设置为反向代理，从而将 HTTP 流量转发到在 Kestrel 上运行的 ASP.NET Core Web 应用。
ms.author: riande
ms.custom: mvc
ms.date: 05/22/2018
uid: host-and-deploy/linux-nginx
ms.openlocfilehash: 840a9f98b3409f74b9a41ee24ff7bcb33a875470
ms.sourcegitcommit: 18339e3cb5a891a3ca36d8146fa83cf91c32e707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37433930"
---
# <a name="host-aspnet-core-on-linux-with-nginx"></a>使用 Nginx 在 Linux 上托管 ASP.NET Core

作者：[Sourabh Shirhatti](https://twitter.com/sshirhatti)

本指南介绍如何在 Ubuntu 16.04 服务器上设置生产就绪 ASP.NET Core 环境。 这些说明可能适用于较新版本的 Ubuntu，但尚未使用较新版本进行测试。

> [!NOTE]
> 对于 Ubuntu 14.04，建议进行监控，以此作为监视 Kestrel 进程的解决方案。 在 Ubuntu 14.04 上不提供 systemd。 有关 Ubuntu 14.04 的说明，请参阅[本主题的以前版本](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md)。

本指南：

* 将现有 ASP.NET Core 应用置于反向代理服务器后方。
* 设置反向代理服务器，以便将请求转发到 Kestrel Web 服务器。
* 确保 Web 应用在启动时作为守护程序运行。
* 配置进程管理工具以帮助重新启动 Web 应用。

## <a name="prerequisites"></a>系统必备

1. 使用具有 sudo 特权的标准用户帐户访问 Ubuntu 16.04 服务器。
1. 在服务器上安装 .NET Core 运行时。
   1. 访问 [.NET Core“所有下载”页](https://www.microsoft.com/net/download/all)。
   1. 从“运行时”下的列表中选择最新的非预览运行时。
   1. 选择并执行适用于 Ubuntu 且匹配服务器的 Ubuntu 版本的说明。
1. 一个现有 ASP.NET Core 应用。

## <a name="publish-and-copy-over-the-app"></a>通过应用发布和复制

配置应用以进行[依赖框架的部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)。

在开发环境中运行 [dotnet publish](/dotnet/core/tools/dotnet-publish)，将应用打包到可在服务器上运行的目录中（例如 bin/Release/&lt;target_framework_moniker&gt;/publish）：

```console
dotnet publish --configuration Release
```

如果不希望维护服务器上的 .NET Core 运行时，还可将应用发布为[独立部署](/dotnet/core/deploying/#self-contained-deployments-scd)。

使用集成到组织工作流的工具（例如 SCP、SFTP）将 ASP.NET Core 应用复制到服务器。 通常可在 var 目录（例如 var/aspnetcore/hellomvc）下找到 Web 应用。

> [!NOTE]
> 在生产部署方案中，持续集成工作流会执行发布应用并将资产复制到服务器的工作。

测试应用：

1. 在命令行中运行应用：`dotnet <app_assembly>.dll`。
1. 在浏览器中，导航到 `http://<serveraddress>:<port>` 以确认应用在 Linux 本地正常运行。

## <a name="configure-a-reverse-proxy-server"></a>配置反向代理服务器

反向代理是为动态 Web 应用提供服务的常见设置。 反向代理终止 HTTP 请求，并将其转发到 ASP.NET Core 应用。

::: moniker range=">= aspnetcore-2.0"

> [!NOTE]
> 使用或不使用反向代理服务器进行配置对 ASP.NET Core 2.0 或更高版本的应用来说都是有效且受支持的托管配置。 有关详细信息，请参阅[何时结合使用 Kestrel 和反向代理](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)。

::: moniker-end

### <a name="use-a-reverse-proxy-server"></a>使用反向代理服务器

Kestrel 非常适合从 ASP.NET Core 提供动态内容。 但是，Web 服务功能不像服务器（如 IIS、Apache 或 Nginx）那样功能丰富。 反向代理服务器可以从 HTTP 服务器卸载服务静态内容、缓存请求、压缩请求和 SSL 终端等工作。 反向代理服务器可能驻留在专用计算机上，也可能与 HTTP 服务器一起部署。

鉴于此指南的目的，使用 Nginx 的单个实例。 它与 HTTP 服务器一起运行在同一服务器上。 根据要求，可以选择不同的设置。

由于请求是通过反向代理转接的，因此使用 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 包中的[转接头中间件](xref:host-and-deploy/proxy-load-balancer)。 此中间件使用 `X-Forwarded-Proto` 标头来更新 `Request.Scheme`，使重定向 URI 和其他安全策略能够正常工作。

调用转接头中间件后，必须放置依赖于该架构的组件，例如身份验证、链接生成、重定向和地理位置。 作为一般规则，转接头中间件应在诊断和错误处理中间件以外的其他中间件之前运行。 此顺序可确保依赖于转接头信息的中间件可以使用标头值进行处理。

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

在调用 [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) 或类似的身份验证方案中间件之前，调用 `Startup.Configure` 中的 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 方法。 配置中间件以转接 `X-Forwarded-For` 和 `X-Forwarded-Proto` 标头：

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

在调用 [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) 和 [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) 或类似的身份验证方案中间件之前，调用 `Startup.Configure` 中的 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 方法。 配置中间件以转接 `X-Forwarded-For` 和 `X-Forwarded-Proto` 标头：

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

如果没有为中间件指定 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)，则要转接的默认标头为 `None`。

对于托管在代理服务器和负载均衡器后方的应用，可能需要附加配置。 有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。

### <a name="install-nginx"></a>安装 Nginx

使用 `apt-get` 安装 Nginx。 安装程序将创建一个 systemd init 脚本，该脚本运行 Nginx，作为系统启动时的守护程序。 

```bash
sudo -s
nginx=stable # use nginx=development for latest development version
add-apt-repository ppa:nginx/$nginx
apt-get update
apt-get install nginx
```

Ubuntu 个人包存档 (PPA) 由志愿者维护，并且不由 [nginx.org](https://nginx.org/) 分发。有关详细信息，请参阅 [Nginx：二进制版本：官方 Debian/Ubuntu 包](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#official-debian-ubuntu-packages)。

> [!NOTE]
> 如果需要可选 Nginx 模块，则可能需要从源代码生成 Nginx。

因为是首次安装 Nginx，通过运行以下命令显式启动：

```bash
sudo service nginx start
```

确认浏览器显示 Nginx 的默认登陆页。 可在 `http://<server_IP_address>/index.nginx-debian.html` 访问登陆页面。

### <a name="configure-nginx"></a>配置 Nginx

若要将 Nginx 配置为反向代理以将请求转接到 ASP.NET Core 应用，请修改 /etc/nginx/sites-available/default。 在文本编辑器中打开它，并将内容替换为以下内容：

```nginx
server {
    listen        80;
    server_name   example.com *.example.com;
    location / {
        proxy_pass         http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection keep-alive;
        proxy_set_header   Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    }
}
```

当没有匹配的 `server_name` 时，Nginx 使用默认服务器。 如果没有定义默认服务器，则配置文件中的第一台服务器是默认服务器。 作为最佳做法，添加指定默认服务器，它会在配置文件中返回状态代码 444。 默认的服务器配置示例是：

```nginx
server {
    listen   80 default_server;
    # listen [::]:80 default_server deferred;
    return   444;
}
```

使用上述配置文件和默认服务器，Nginx 接受主机标头 `example.com` 或 `*.example.com` 端口 80 上的公共流量。 与这些主机不匹配的请求不会转接到 Kestrel。 Nginx 将匹配的请求转接到 `http://localhost:5000` 中的 Kestrel。 有关详细信息，请参阅 [nginx 如何处理请求](https://nginx.org/docs/http/request_processing.html)。 要更改 Kestrel 的 IP/端口，请参阅 [Kestrel：终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)。

> [!WARNING]
> 未能指定正确的 [server_name 指令](https://nginx.org/docs/http/server_names.html)会公开应用的安全漏洞。 如果可控制整个父域（区别于易受攻击的 `*.com`），则子域通配符绑定（例如，`*.example.com`）不具有此安全风险。 有关详细信息，请参阅 [rfc7230 第 5.4 条](https://tools.ietf.org/html/rfc7230#section-5.4)。

完成配置 Nginx 后，运行 `sudo nginx -t` 来验证配置文件的语法。 如果配置文件测试成功，可以通过运行 `sudo nginx -s reload` 强制 Nginx 选取更改。

要直接在服务器上运行应用：

1. 请导航到应用目录。
1. 运行应用的可执行文件：`./<app_executable>`。

如果出现权限错误，请更改权限：

```console
chmod u+x <app_executable>
```

如果应用在服务器上运行，但无法通过 Internet 响应，请检查服务器的防火墙，并确认端口 80 已打开。 如果使用 Azure Ubuntu VM，请添加启用入站端口 80 流量的网络安全组 (NSG) 规则。 不需要启用出站端口 80 规则，因为启用入站规则后会自动许可出站流量。

测试应用完成后，请在命令提示符处按 `Ctrl+C` 关闭应用。

## <a name="monitoring-the-app"></a>监视应用

服务器设置为将对 `http://<serveraddress>:80` 发起的请求转接到在 `http://127.0.0.1:5000` 中的 Kestrel 上运行的 ASP.NET Core 应用。 但是，未将 Nginx 设置为管理 Kestrel 进程。 systemd 可用于创建服务文件以启动和监视基础 Web 应用。 systemd 是一个 init 系统，可以提供用于启动、停止和管理进程的许多强大的功能。 

### <a name="create-the-service-file"></a>创建服务文件

创建服务定义文件：

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

以下是应用的一个示例服务文件：

```ini
[Unit]
Description=Example .NET Web API App running on Ubuntu

[Service]
WorkingDirectory=/var/aspnetcore/hellomvc
ExecStart=/usr/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
SyslogIdentifier=dotnet-example
User=www-data
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target
```

如果配置未使用用户 www-data，则必须先创建此处定义的用户，并为该用户提供适当的文件所有权。

Linux 具有区分大小写的文件系统。 将 ASPNETCORE_ENVIRONMENT 设置为“生产”会导致搜索配置文件 appsettings.Production.json，而不是 appsettings.production.json。

> [!NOTE]
> 必须转义某些值（例如，SQL 连接字符串）以供配置提供程序读取环境变量。 使用以下命令生成适当的转义值以供在配置文件中使用：
>
> ```console
> systemd-escape "<value-to-escape>"
> ```

保存该文件并启用该服务。

```bash
systemctl enable kestrel-hellomvc.service
```

启用该服务，并确认它正在运行。

```
systemctl start kestrel-hellomvc.service
systemctl status kestrel-hellomvc.service

● kestrel-hellomvc.service - Example .NET Web API App running on Ubuntu
    Loaded: loaded (/etc/systemd/system/kestrel-hellomvc.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-hellomvc.service
            └─9021 /usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
```

在配置了反向代理并通过 systemd 管理 Kestrel 后，Web 应用现已完全配置，并能在本地计算机上的浏览器中从 `http://localhost` 进行访问。 也可以从远程计算机进行访问，同时限制可能进行阻止的任何防火墙。 检查响应标头，`Server` 标头显示由 Kestrel 所提供的 ASP.NET Core 应用。

```text
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a>查看日志

使用 Kestrel 的 Web 应用是通过 `systemd` 进行管理的，因此所有事件和进程都被记录到集中日志。 但是，此日志包含由 `systemd` 管理的所有服务和进程的全部条目。 若要查看特定于 `kestrel-hellomvc.service` 的项，请使用以下命令：

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

有关进一步筛选，使用时间选项（如 `--since today`、`--until 1 hour ago`）或这些选项的组合可以减少返回的条目数。

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="securing-the-app"></a>保护应用

### <a name="enable-apparmor"></a>启用 AppArmor

Linux 安全模块 (LSM) 是一个框架，它是自 Linux 2.6 后的 Linux kernel 的一部分。 LSM 支持安全模块的不同实现。 [AppArmor](https://wiki.ubuntu.com/AppArmor) 是实现强制访问控制系统的 LSM，它允许将程序限制在一组有限的资源内。 确保已启用并成功配置 AppArmor。

### <a name="configuring-the-firewall"></a>配置防火墙

关闭所有未使用的外部端口。 通过为配置防火墙提供命令行接口，不复杂的防火墙 (ufw) 为 `iptables` 提供了前端。 确认已配置 `ufw` 以允许所需的任何端口上的流量。

```bash
sudo apt-get install ufw
sudo ufw enable

sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

### <a name="securing-nginx"></a>保护 Nginx

#### <a name="change-the-nginx-response-name"></a>更改 Nginx 响应名称

编辑 src/http/ngx_http_header_filter_module.c：

```c
static char ngx_http_server_string[] = "Server: Web Server" CRLF;
static char ngx_http_server_full_string[] = "Server: Web Server" CRLF;
```

#### <a name="configure-options"></a>配置选项

用其他必需模块配置服务器。 请考虑使用 [ModSecurity](https://www.modsecurity.org/) 等 Web 应用防火墙来加强对应用的保护。

#### <a name="configure-ssl"></a>配置 SSL

* 通过指定由受信任的证书颁发机构 (CA) 颁发的有效证书来配置服务器，以侦听端口 `443` 上的 HTTPS 流量。

* 通过采用以下“/etc/nginx/nginx.conf”文件中所示的某些做法来增强安全保护。 示例包括选择更强的密码并将通过 HTTP 的所有流量重定向到 HTTPS。

* 添加 `HTTP Strict-Transport-Security` (HSTS) 标头可确保由客户端发起的所有后续请求都仅通过 HTTPS。

* 如果以后会禁用 SSL，则不要添加 Strict-Transport-Security 标头或选择相应的 `max-age`。

添加 /etc/nginx/proxy.conf 配置文件：

[!code-nginx[](linux-nginx/proxy.conf)]

编辑 /etc/nginx/nginx.conf 配置文件。 示例包含一个配置文件中的 `http` 和 `server` 部分。

[!code-nginx[](linux-nginx/nginx.conf?highlight=2)]

#### <a name="secure-nginx-from-clickjacking"></a>保护 Nginx 免受点击劫持的侵害
点击劫持是收集受感染用户的点击数的恶意技术。 点击劫持诱使受害者（访问者）点击受感染的网站。 使用 X-FRAME-OPTIONS 保护站点。

编辑 nginx.conf 文件：

```bash
sudo nano /etc/nginx/nginx.conf
```

添加行 `add_header X-Frame-Options "SAMEORIGIN";` 并保存文件，然后重新启动 Nginx。

#### <a name="mime-type-sniffing"></a>MIME 类型探查

此标头可阻止大部分浏览器通过 MIME 方式探查来自已声明内容类型的响应，因为标头会指示浏览器不要替代响应内容类型。 使用 `nosniff` 选项后，如果服务器认为内容是“文本/html”，则浏览器将其显示为“文本/html”。

编辑 nginx.conf 文件：

```bash
sudo nano /etc/nginx/nginx.conf
```

添加行 `add_header X-Content-Type-Options "nosniff";` 并保存文件，然后重新启动 Nginx。

## <a name="additional-resources"></a>其他资源

* [Nginx：二进制版本：官方 Debian/Ubuntu 包](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#official-debian-ubuntu-packages)
* [配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)
* [NGINX：使用转接头](https://www.nginx.com/resources/wiki/start/topics/examples/forwarded/)
