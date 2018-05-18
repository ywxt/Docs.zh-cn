---
title: Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持
author: shirhatti
description: 发现的用于调试 ASP.NET Core 应用时在 Windows Server 上运行之后 IIS 的支持。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a>Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持

通过[Sourabh Shirhatti](https://twitter.com/sshirhatti)和[Luke Latham](https://github.com/guardrex)

本指南介绍了[Visual Studio](https://www.visualstudio.com/vs/)支持的用于调试在 IIS 后面运行 Windows Server 上的 ASP.NET Core 应用。 本主题将指导完成启用此功能，并设置项目。

## <a name="prerequisites"></a>系统必备

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="enable-iis"></a>启用 IIS

1. 导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。
1. 选择**Internet Information Services**复选框。

![检查为黑色方块 （不复选标记） 后，该值指示启用了 IIS 功能的某些 Windows 功能显示 Internet Information Services 复选框](development-time-iis-support/_static/enable_iis.png)

IIS 安装可能需要重新启动系统。

## <a name="configure-iis"></a>配置 IIS

IIS 必须拥有的网站进行以下配置：

* 应用程序的发布配置文件 URL 主机名称相匹配的主机名称。
* 端口 443 与分配的证书的绑定。

例如，**主机名**添加的网站设置为"localhost"（启动配置文件将还使用"localhost"本主题中的更高版本）。 端口设置为"443"(HTTPS)。 **IIS Express 开发证书**分配给网站，但任何有效的证书工作原理：

![显示分配的证书为 localhost 设置的绑定在端口 443 上的 IIS 中添加网站窗口。](development-time-iis-support/_static/add-website-window.png)

如果 IIS 安装已具有**Default Web Site**使用与应用程序的发布配置文件 URL 主机名匹配的主机名：

* 添加为端口 443 (HTTPS) 的端口绑定。
* 向网站分配一个有效的证书。

## <a name="enable-development-time-iis-support-in-visual-studio"></a>启用 Visual Studio 中的开发时间 IIS 支持

1. 启动 Visual Studio 安装程序。
1. 选择**IIS 支持的开发时间**组件。 列出为可选中了该组件**摘要**面板**ASP.NET 和 web 开发**工作负荷。 组件安装[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)，即反向代理配置中运行 ASP.NET Core 后面 IIS 的应用所需的本机 IIS 模块。

![修改 Visual Studio 功能：选择“工作负荷”选项卡。 在“Web 和云”部分，选择“ASP.NET 和 Web 开发”面板。 在摘要面板中的可选区域右侧有 IIS 支持的开发时间是复选框。](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a>配置项目

### <a name="https-redirection"></a>HTTPS 重定向

对于新项目中，选中复选框以**针对 HTTPS 配置**中**新 ASP.NET 核心 Web 应用程序**窗口：

![新的 ASP.NET 核心 Web 应用程序窗口，并针对 HTTPS 复选框处于选中状态配置。](development-time-iis-support/_static/new-app.png)

在现有项目中，使用 HTTPS 重定向中的中间件`Startup.Configure`通过调用[UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)扩展方法：

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

创建新的发布配置文件添加开发时间 IIS 支持：

1. 有关**配置文件**，选择**新建**按钮。 在弹出窗口中将该配置文件"IIS"。 选择**确定**创建配置文件。
1. 有关**启动**设置中选择**IIS**从列表中。
1. 选中的复选框**启动浏览器**和提供的终结点 URL。 使用 HTTPS 协议。 本示例使用 `https://localhost/WebApplication1`。
1. 在**环境变量**部分中，选择**添加**按钮。 环境变量提供的密钥`ASPNETCORE_ENVIRONMENT`和的值`Development`。
1. 在**Web 服务器设置**区域中，设置**应用程序 URL**。 本示例使用 `https://localhost/WebApplication1`。
1. 保存配置文件。

![选择了“调试”选项卡的“项目属性”窗口。 将“配置文件”和“启动”设置设为 IIS。 启动浏览器功能启用地址为https://localhost/WebApplication1。 在 Web 服务器设置区域的应用程序 URL 字段中还提供相同的地址。](development-time-iis-support/_static/project_properties.png)

或者，手动添加到的启动配置文件[launchSettings.json](http://json.schemastore.org/launchsettings)应用程序中的文件：

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

## <a name="run-the-project"></a>运行项目

在 VS UI 中，设置为运行按钮**IIS**分析，并选择按钮以启动应用程序：

![在 VS 工具栏中设置为"IIS"配置文件运行按钮。](development-time-iis-support/_static/toolbar.png)

如果未以管理员身份运行 visual Studio 可能会提示重新启动。 如果出现提示，请重启 Visual Studio。

如果将使用的不受信任的开发证书，浏览器可能需要你针对不受信任的证书创建例外。

## <a name="additional-resources"></a>其他资源

* [使用 IIS 在 Windows 上托管 ASP.NET Core](xref:host-and-deploy/iis/index)
* [ASP.NET Core 模块简介](xref:fundamentals/servers/aspnet-core-module)
* [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)
* [Enforce HTTPS](xref:security/enforcing-ssl)
