---
title: Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持
author: shirhatti
description: 发现对调试 ASP.NET Core 应用的支持（在 Windows Server 上的 IIS 后方运行时）。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/14/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: 0bf4585d44e61c5e7e5b89ce9d8dfdfa10d5460e
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
ms.locfileid: "34233074"
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a>Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持

作者：[Sourabh Shirhatti](https://twitter.com/sshirhatti)、[Luke Latham](https://github.com/guardrex)

本文介绍了对调试（在 Windows Server 上的 IIS 后方运行的）ASP.NET Core 应用的 [Visual Studio](https://www.visualstudio.com/vs/) 支持。 本主题逐步介绍如何启用此功能并设置项目。

## <a name="prerequisites"></a>系统必备

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="enable-iis"></a>启用 IIS

1. 导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。
1. 选中“Internet Information Services”复选框。

![Windows 功能将选中的“Internet Information Services”复选框显示为实心方形（而不是复选标记），指示已启用某些 IIS 功能](development-time-iis-support/_static/enable_iis.png)

IIS 安装可能需要重启系统。

## <a name="configure-iis"></a>配置 IIS

IIS 必须具有具备以下配置的网站：

* 与应用启动配置文件 URL 主机名匹配的主机名。
* 使用分配的证书绑定端口 443。

例如，所添加网站的主机名设置为“localhost”（在本主题之后部分启动配置文件也将使用“localhost”）。 端口设置为“443”(HTTPS)。 “IIS Express 开发证书”已分配给该网站，但可使用任何有效的证书：

![在 IIS 中添加网站窗口，显示已分配证书的端口 443 上 localhost 的绑定集。](development-time-iis-support/_static/add-website-window.png)

如果 IIS 安装已经有一个默认网站，且其主机名与应用的启动配置文件 URL 主机名相匹配：

* 为端口 443 (HTTPS) 添加端口绑定。
* 向网站分配一个有效证书。

## <a name="enable-development-time-iis-support-in-visual-studio"></a>在 Visual Studio 中启用开发时 IIS 支持

1. 启动 Visual Studio 安装程序。
1. 选择“开发时 IIS 支持”组件。 该组件在“ASP.NET 和 Web 开发”工作负荷的“摘要”面板中列为可选。 此组件将安装 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)，该模块是在反向代理配置中的 IIS 的后方运行 ASP.NET Core 应用所需的本机 IIS 模块。

![修改 Visual Studio 功能：选择“工作负荷”选项卡。 在“Web 和云”部分，选择“ASP.NET 和 Web 开发”面板。 在“摘要”面板的“可选”区域右侧，有一“开发时 IIS 支持”复选框。](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a>配置项目

### <a name="https-redirection"></a>HTTPS 重定向

对于新项目，请选中“新建 ASP.NET Core Web 应用程序”窗口中的“配置 HTTPS”复选框：

![选中“新建 ASP.NET Core Web 应用程序”窗口中的“配置 HTTPS”复选框。](development-time-iis-support/_static/new-app.png)

在现有项目中，通过调用 [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) 扩展方法在 `Startup.Configure` 中使用 HTTPS 重定向中间件：

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    app.UseHttpsRedirection();
    app.UseStaticFiles();
    app.UseCookiePolicy();

    app.UseMvc();
}
```

### <a name="iis-launch-profile"></a>IIS 启动配置文件

创建新的启动配置文件以添加开发时 IIS 支持：

1. 对于配置文件，请选择“新建”按钮。 在弹出窗口中将该配置文件命名为“IIS”。 选择“确定”创建配置文件。
1. 对于“启动”设置，请从列表中选择“IIS”。
1. 选中“启动浏览器”复选框并提供终结点 URL。 使用 HTTPS 协议。 本示例使用 `https://localhost/WebApplication1`。
1. 在“环境变量”部分中，选择“添加”按钮。 提供一个密钥为 `ASPNETCORE_ENVIRONMENT` 和值为 `Development` 的环境变量。
1. 在“Web 服务器设置”区域中，设置“应用 URL”。 本示例使用 `https://localhost/WebApplication1`。
1. 保存配置文件。

![选择了“调试”选项卡的“项目属性”窗口。 将“配置文件”和“启动”设置设为 IIS。 为“启动浏览器”功能配置了 https://localhost/WebApplication1 地址。 Web Server 设置区域的“应用 URL”字段中也提供相同的地址。](development-time-iis-support/_static/project_properties.png)

或者，可以将启动配置文件手动添加到应用中的 [launchSettings.json](http://json.schemastore.org/launchsettings) 文件：

```json
{
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iis": {
      "applicationUrl": "https://localhost/WebApplication1",
      "sslPort": 0
    }
  },
  "profiles": {
    "IIS": {
      "commandName": "IIS",
      "launchBrowser": true,
      "launchUrl": "https://localhost/WebApplication1",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

## <a name="run-the-project"></a>运行该项目

在 VS 用户界面中，将“运行”按钮设置为 IIS 配置文件，然后选择此按钮以启动该应用：

![运行 VS 工具栏中设置为“IIS”配置文件的按钮。](development-time-iis-support/_static/toolbar.png)

如果不以管理员身份运行，Visual Studio 可能会提示重启。 如果出现提示，请重启 Visual Studio。

如果使用不受信任的开发证书，则浏览器可能会要求你为不受信任的证书创建异常。

## <a name="additional-resources"></a>其他资源

* [使用 IIS 在 Windows 上托管 ASP.NET Core](xref:host-and-deploy/iis/index)
* [ASP.NET Core 模块简介](xref:fundamentals/servers/aspnet-core-module)
* [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)
* [Enforce HTTPS](xref:security/enforcing-ssl)
