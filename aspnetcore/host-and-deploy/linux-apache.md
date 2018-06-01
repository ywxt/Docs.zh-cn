---
title: 使用 Apache 在 Linux 上托管 ASP.NET Core
description: 了解如何在 CentOS 上将 Apache 设置为反向代理服务器，以将 HTTP 流量重定向到在 Kestrel 上运行的 ASP.NET Core Web 应用。
author: spboyer
manager: wpickett
ms.author: spboyer
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/linux-apache
ms.openlocfilehash: 473585f1be180645395c14a154c9c017ca50edab
ms.sourcegitcommit: 74be78285ea88772e7dad112f80146b6ed00e53e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "33962812"
---
# <a name="host-aspnet-core-on-linux-with-apache"></a>使用 Apache 在 Linux 上托管 ASP.NET Core

作者：[Shayne Boyer](https://github.com/spboyer)

使用本指南，了解如何在 [CentOS 7](https://www.centos.org/) 上将 [Apache](https://httpd.apache.org/) 设置为反向代理服务器，以将 HTTP 流量重定向到在 [Kestrel](xref:fundamentals/servers/kestrel) 上运行的 ASP.NET Core Web 应用。 [mod_proxy extension](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) 和相关模块可创建服务器的反向代理。

## <a name="prerequisites"></a>系统必备

1. 运行 CentOS 7 的服务器，使用具有 sudo 特权的标准用户帐户
2. ASP.NET Core 应用

## <a name="publish-the-app"></a>发布应用

在 CentOS 7 运行时 (`centos.7-x64`) 的发布配置中将应用作为[独立部署](/dotnet/core/deploying/#self-contained-deployments-scd)发布。 使用 SCP、FTP 或其他文件传输方法将 *bin/Release/netcoreapp2.0/centos.7-x64/publish* 文件夹的内容复制到服务器。

> [!NOTE]
> 在生产部署方案中，持续集成工作流会执行发布应用并将资产复制到服务器的工作。 

## <a name="configure-a-proxy-server"></a>配置代理服务器

反向代理是为动态 Web 应用提供服务的常见设置。 反向代理终止 HTTP 请求，并将其转发到 ASP.NET 应用。

代理服务器将客户端请求转发到另一个服务器，而不是自身实现这些请求。 反向代理转发到固定的目标，通常代表任意客户端。 在本指南中，Apache 被配置为反向代理，在 Kestrel 为 ASP.NET Core 应用提供服务的同一服务器上运行。

由于请求是通过反向代理转接的，因此使用 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 程序包中的转接头中间件。 此中间件使用 `X-Forwarded-Proto` 标头来更新 `Request.Scheme`，使重定向 URI 和其他安全策略能够正常工作。

当使用任何类型的身份验证中间件时，必须先运行转接头中间件。 此顺序可确保身份验证中间件可以使用标头值，并生成正确的重定向 URI。

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

### <a name="install-apache"></a>安装 Apache

将 CentOS 包更新为其最新稳定版本：

```bash
sudo yum update -y
```

使用单个 `yum` 命令在 CentOS 上安装 Apache Web 服务器：

```bash
sudo yum -y install httpd mod_ssl
```

运行该命令后的示例输出：

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
> 在此示例中，输出反映了 httpd.86_64，因为 CentOS 7 版本是 64 位的。 若要验证 Apache 的安装位置，请从命令提示符运行 `whereis httpd`。

### <a name="configure-apache-for-reverse-proxy"></a>配置 Apache 用于反向代理

Apache 的配置文件位于 `/etc/httpd/conf.d/` 目录内。 除了 `/etc/httpd/conf.modules.d/` 中的模块配置文件外（其中包含加载模块所需的任何配置文件），将对任何带 .conf 扩展名的文件按字母顺序进行处理。

为应用创建名为 hellomvc.conf 的配置文件：

```
<VirtualHost *:80>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ServerName www.example.com
    ServerAlias *.example.com
    ErrorLog ${APACHE_LOG_DIR}hellomvc-error.log
    CustomLog ${APACHE_LOG_DIR}hellomvc-access.log common
</VirtualHost>
```

`VirtualHost` 块可以在服务器上的一个或多个文件中多次出现。 在前面的配置文件中，Apache 接受端口 80 上的公共流量。 正在向域 `www.example.com` 提供服务，`*.example.com` 别名解析为同一网站。 有关详细信息，请参阅[基于名称的虚拟主机支持](https://httpd.apache.org/docs/current/vhosts/name-based.html)。 请求会通过代理从根位置转到 127.0.0.1 处的服务器的端口 5000。 对于双向通信，需要 `ProxyPass` 和 `ProxyPassReverse`。

> [!WARNING]
> 未能指定 VirtualHost 块中的正确 [ServerName 指令](https://httpd.apache.org/docs/current/mod/core.html#servername)会公开应用的安全漏洞。 如果可控制整个父域（区别于易受攻击的 `*.com`），则子域通配符绑定（例如，`*.example.com`）不具有此安全风险。 有关详细信息，请参阅 [rfc7230 第 5.4 条](https://tools.ietf.org/html/rfc7230#section-5.4)。

可以使用 `ErrorLog` 和 `CustomLog` 指令配置每个 `VirtualHost` 的日志记录。 `ErrorLog` 是服务器记录错误的位置，`CustomLog` 则设置文件名和日志文件的格式。 在这种情况下，这是记录请求信息的位置。 每个请求将各占一行。

保存文件，并测试配置。 如果一切正常，响应应为 `Syntax [OK]`。

```bash
sudo service httpd configtest
```

重新启动 Apache：

```bash
sudo systemctl restart httpd
sudo systemctl enable httpd
```

## <a name="monitoring-the-app"></a>监视应用

Apache 现在已设置为将对 `http://localhost:80` 发起的请求转发到运行在 `http://127.0.0.1:5000` 处的 Kestrel 上的 ASP.NET Core 应用。  但是，未将 Apache 设置为管理 Kestrel 进程。 使用 systemd，并创建服务文件以启动和监视基础 Web 应用。 systemd 是一个 init 系统，可以提供用于启动、停止和管理进程的许多强大的功能。 


### <a name="create-the-service-file"></a>创建服务文件

创建服务定义文件：

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

应用的一个示例服务文件：

```
[Unit]
Description=Example .NET Web API App running on CentOS 7

[Service]
WorkingDirectory=/var/aspnetcore/hellomvc
ExecStart=/usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
Restart=always
# Restart service after 10 seconds if dotnet service crashes
RestartSec=10
SyslogIdentifier=dotnet-example
User=apache
Environment=ASPNETCORE_ENVIRONMENT=Production 

[Install]
WantedBy=multi-user.target
```

> [!NOTE]
> **用户** &mdash; 如果配置未使用用户 apache，则必须先创建用户，并为该用户提供适当的文件所有权。

> [!NOTE]
> 必须转义某些值（例如，SQL 连接字符串）以供配置提供程序读取环境变量。 使用以下命令生成适当的转义值以供在配置文件中使用：
>
> ```console
> systemd-escape "<value-to-escape>"
> ```

保存该文件并启用该服务：

```bash
systemctl enable kestrel-hellomvc.service
```

启动该服务，并确认它正在运行：

```bash
systemctl start kestrel-hellomvc.service
systemctl status kestrel-hellomvc.service

● kestrel-hellomvc.service - Example .NET Web API App running on CentOS 7
    Loaded: loaded (/etc/systemd/system/kestrel-hellomvc.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-hellomvc.service
            └─9021 /usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
```

在配置了反向代理并通过 systemd 管理 Kestrel 后，Web 应用现已完全配置，并能在本地计算机上的浏览器中从 `http://localhost` 进行访问。 检查响应标头，服务器标头表示 ASP.NET Core 应用由 Kestrel 提供服务：

```
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a>查看日志

由于使用 Kestrel 的 Web 应用是通过 systemd 进行管理的，因此事件和进程将记录到集中日志。 但是，此日志包含由 systemd 管理的所有服务和进程的条目。 若要查看特定于 `kestrel-hellomvc.service` 的项，请使用以下命令：

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

若要进行时间筛选，请使用命令指定时间选项。 例如，使用 `--since today` 筛选出当天或 `--until 1 hour ago` 来查看前一小时的条目。 有关详细信息，请参阅 [journalctl 手册页](https://www.unix.com/man-page/centos/1/journalctl/)。

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="securing-the-app"></a>保护应用

### <a name="configure-firewall"></a>配置防火墙

*Firewalld* 是管理防火墙的动态守护程序，支持网络区域。 仍可以使用 iptable 管理端口和数据包筛选。 默认情况下应安装 *Firewalld*。 `yum` 可用于安装包或验证是否已安装。

```bash
sudo yum install firewalld -y
```

使用 `firewalld` 仅打开应用所需的端口。 在此示例中，使用的是端口 80 和 443。 以下命令将端口 80 和 443 永久设置为打开：

```bash
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --add-port=443/tcp --permanent
```

重新加载防火墙设置。 检查默认区域中可用的服务和端口。 通过检查 `firewall-cmd -h` 获取可用选项。

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

### <a name="ssl-configuration"></a>SSL 配置

若要配置 Apache 用于 SSL，需使用 mod_ssl 模块。 安装了 httpd 模块时，也会安装了 mod_ssl 模块。 如果未安装，请使用 `yum` 将其添加到配置。

```bash
sudo yum install mod_ssl
```
若要强制使用 SSL，请安装 `mod_rewrite` 模块以启用 URL 重写：

```bash
sudo yum install mod_rewrite
```

修改 hellomvc.conf 文件以启用 URL 重写和端口 443 上的安全通信：

```
<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/ [R,L]
</VirtualHost>

<VirtualHost *:443>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ErrorLog /var/log/httpd/hellomvc-error.log
    CustomLog /var/log/httpd/hellomvc-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

> [!NOTE]
> 此示例中使用了本地生成的证书。 SSLCertificateFile 应为域名的主证书文件。 SSLCertificateKeyFile 应为创建 CSR 时生成的密钥文件。 SSLCertificateChainFile 应为证书颁发机构提供的中间证书文件（如有）。

保存文件，并测试配置：

```bash
sudo service httpd configtest
```

重新启动 Apache：

```bash
sudo systemctl restart httpd
```

## <a name="additional-apache-suggestions"></a>其他 Apache 建议

### <a name="additional-headers"></a>其他标头

为了防止恶意攻击，应对一些标头进行修改或添加一些标头。 确保已安装 `mod_headers` 模块：

```bash
sudo yum install mod_headers
```

#### <a name="secure-apache-from-clickjacking-attacks"></a>保护 Apache 免受点击劫持攻击

[点击劫持](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger)（也称为 *UI 伪装攻击*）是一种恶意攻击，其中网站访问者会上当受骗，从而导致在与当前要访问的页面不同的页面上单击链接或按钮。 使用 `X-FRAME-OPTIONS` 可保护网站。

编辑 *httpd.conf* 文件：

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

添加行 `Header append X-FRAME-OPTIONS "SAMEORIGIN"`。 保存该文件。 重启 Apache。

#### <a name="mime-type-sniffing"></a>MIME 类型探查

`X-Content-Type-Options` 标头阻止 Internet Explorer 进行 *MIME 探查*（从文件内容中确定文件的 `Content-Type`）。 如果服务器通过设置 `nosniff` 选项将 `Content-Type` 标头设置为 `text/html`，则不管文件内容为何，Internet Explorer 都会将内容呈现为 `text/html`。

编辑 *httpd.conf* 文件：

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

添加行 `Header set X-Content-Type-Options "nosniff"`。 保存该文件。 重启 Apache。

### <a name="load-balancing"></a>负载平衡 

此示例演示如何在同一实例计算机上的 CentOS 7 和 Kestrel 上设置和配置 Apache。 为了不出现单一故障点；使用 mod_proxy_balancer 并修改 VirtualHost 可实现在 Apache 代理服务器后方管理 Web 应用的多个实例。

```bash
sudo yum install mod_proxy_balancer
```

在下面所示的配置文件中，`hellomvc` 应用的其他实例设置为在端口 5001 上运行。 “代理”部分设置了具有两个成员的均衡器配置，以便对 byrequests 进行负载均衡。

```
<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/ [R,L]
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
    ErrorLog /var/log/httpd/hellomvc-error.log
    CustomLog /var/log/httpd/hellomvc-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

### <a name="rate-limits"></a>速率限制
使用 httpd 模块中包含的 mod_ratelimit，客户端的带宽可以限制为：

```bash
sudo nano /etc/httpd/conf.d/ratelimit.conf
```
示例文件将根位置下的带宽限制为 600 KB/秒：

```
<IfModule mod_ratelimit.c>
    <Location />
        SetOutputFilter RATE_LIMIT
        SetEnv rate-limit 600
    </Location>
</IfModule>
```
