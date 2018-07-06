---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: OWIN 和 Katana 入门 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 58a3d234867821d5e23cce2f01e105dfab88ac33
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826650"
---
<a name="getting-started-with-owin-and-katana"></a>OWIN 和 Katana 入门
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[打开 Web Interface for.NET (OWIN)](http://owin.org/)定义.NET web 服务器和 web 应用程序之间的抽象。 通过分离应用程序从 web 服务器，OWIN 使得更轻松地创建.NET web 开发的中间件。 此外，OWIN 简化了到其他主机的端口 web 应用程序&#8212;例如，自托管 Windows 服务或其他进程中。

OWIN 是一个社区拥有规范，不实现。 Katana 项目是一组由 Microsoft 开发的开源 OWIN 组件。 OWIN 和 Katana 的常规概述，请参阅[项目 Katana 概述](an-overview-of-project-katana.md)。 在本文中，我将直接跳转到代码，以开始。

本教程使用[Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566)，但也可以使用 Visual Studio 2012。 几个步骤是在 Visual Studio 2012，我注意到以下不同的。

## <a name="host-owin-in-iis"></a>承载在 IIS 中的 OWIN

在本部分中，我们将托管在 IIS 中的 OWIN。 此选项可提供灵活性和可组合性的 OWIN 管道以及 IIS 的成熟功能集。 使用此选项，在 ASP.NET 请求管道中运行 OWIN 应用程序。

首先，创建一个新的 ASP.NET Web 应用程序项目。 （在 Visual Studio 2012 中，使用 ASP.NET 空 Web 应用程序项目类型）。

![](getting-started-with-owin-and-katana/_static/image1.png)

在中**新建 ASP.NET 项目**对话框中，选择**空**模板。

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a>添加 NuGet 包

接下来，添加所需的 NuGet 包。 从**工具**菜单中，选择**库程序包管理器**，然后选择**程序包管理器控制台**。 在包管理器控制台窗口中，键入以下命令：

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a>添加一个 Startup 类

接下来，添加 OWIN 启动类。 在解决方案资源管理器，右键单击该项目并选择**外**，然后选择**新项**。 在中**添加新项**对话框中，选择**Owin 启动类**。 配置启动类的详细信息，请参阅[OWIN 启动类检测](owin-startup-class-detection.md)。

![](getting-started-with-owin-and-katana/_static/image4.png)

将以下代码添加到 `Startup1.Configuration` 方法：

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

此代码将一段简单的中间件添加到 OWIN 管道中，作为接收函数实现**Microsoft.Owin.IOwinContext**实例。 当服务器收到 HTTP 请求时，OWIN 管道调用中间件。 中间件设置响应的内容类型，并写入响应正文。

> [!NOTE]
> OWIN Startup 类模板是 Visual Studio 2013 中可用。 如果正在使用 Visual Studio 2012，只需添加新的空类命名为`Startup1`，并粘贴以下代码：


[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a>运行应用程序

按 F5 开始调试。 Visual Studio 将打开一个浏览器窗口以`http://localhost:*port*/`。 页面应如以下所示：

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a>在控制台应用程序中自托管 OWIN

很容易地从 IIS 承载到自承载自定义过程中转换此应用程序。 使用 IIS 承载，IIS 充当 HTTP 服务器和承载服务的进程。 与自托管，你的应用程序创建过程，并使用**HttpListener**类作为 HTTP 服务器。

在 Visual Studio 中，创建一个新的控制台应用程序。 在包管理器控制台窗口中，键入以下命令：

`Install-Package Microsoft.Owin.SelfHost -Pre`

添加`Startup1`本教程的第 1 部分中对项目的类。 无需修改此类。

实现应用程序的`Main`方法，如下所示。

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

服务器在运行控制台应用程序时，开始侦听`http://localhost:9000`。 如果你导航到此地址在 web 浏览器中，您将看到"Hello world"页面。

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a>添加 OWIN 诊断

Microsoft.Owin.Diagnostics 包中包含的捕获未经处理的异常并显示错误详细信息的 HTML 页中间件。 此页函数非常像有时被称为 ASP.NET 错误页"[黄色死机紫屏](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)"(YSOD)。 如 YSOD，Katana 错误页可在开发期间，但最好在生产模式下禁用它。

若要在项目中安装诊断程序包，请在包管理器控制台窗口中键入以下命令：

`install-package Microsoft.Owin.Diagnostics –Pre`

中的代码更改在`Startup1.Configuration`方法，如下所示：

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

现在使用 CTRL + F5 运行应用程序而不进行调试，以便 Visual Studio 将不在异常上中断。 应用程序的行为相同与之前一样，直到您导航到`http://localhost/fail`，此时应用程序将引发异常。 错误页中间件将捕获该异常并显示有关错误的信息的 HTML 页。 您可以单击选项卡以查看堆栈、 查询字符串、 cookie、 请求标头和 OWIN 环境变量。

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a>后续步骤

- [OWIN 启动类检测](owin-startup-class-detection.md)
- [使用 OWIN 自托管 ASP.NET Web API](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [使用 OWIN 自承载 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
