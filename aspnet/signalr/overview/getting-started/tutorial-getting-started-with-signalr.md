---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 教程： SignalR 2 入门 |Microsoft Docs
author: pfletcher
description: 本教程介绍如何使用 SignalR 创建实时聊天应用程序。 将 SignalR 添加到空的 ASP.NET web 应用程序，并创建 HTML pa...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
ms.technology: dotnet-signalr
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: fcd00419de77a380e004cbe306eb46910655a355
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398179"
---
<a name="tutorial-getting-started-with-signalr-2"></a>教程： SignalR 2 入门
====================
通过[Patrick Fletcher](https://github.com/pfletcher)

[下载已完成的项目](http://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

> 本教程介绍如何使用 SignalR 创建实时聊天应用程序。 将 SignalR 添加到空的 ASP.NET web 应用程序，并创建 HTML 页以发送和显示的消息。 
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 版本 2
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a>本教程使用 Visual Studio 2012
> 
> 
> 若要学习本教程使用 Visual Studio 2012，请执行以下操作：
> 
> - 更新你[程序包管理器](http://docs.nuget.org/docs/start-here/installing-nuget)到最新版本。
> - 安装[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)。
> - 在 Web 平台安装程序中，搜索并安装**ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012**。 这将安装 Visual Studio 模板的 SignalR 类，如**中心**。
> - 某些模板 (如**OWIN 启动类**) 将不可用; 对于这些数据，改为使用的类文件。
> 
> 
> ## <a name="tutorial-versions"></a>教程版本
> 
> 有关 SignalR 的早期版本的信息，请参阅[SignalR 较早版本](../older-versions/index.md)。
> 
> ## <a name="questions-and-comments"></a>问题和提出的意见
> 
> 请在你喜欢本教程的内容以及我们可以改进的页的底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。


## <a name="overview"></a>概述

本教程介绍了通过演示如何生成简单的基于浏览器的聊天应用程序的 SignalR 开发。 将 SignalR 库添加到空的 ASP.NET web 应用程序，创建一个中心类，用于将消息发送到客户端，并创建使用户能够发送和接收聊天消息的 HTML 页。 有关演示如何在 MVC 5 中创建的聊天应用程序使用 MVC 视图的类似教程，请参阅[SignalR 2 和 MVC 5 入门](tutorial-getting-started-with-signalr-and-mvc.md)。

> [!NOTE]
> 本教程演示如何创建版本 2 中的 SignalR 应用程序。 有关 SignalR 之间的更改的详细信息 1.x 和 2，请参阅[升级 SignalR 1.x 项目](../releases/upgrading-signalr-1x-projects-to-20.md)并[Visual Studio 2013 发行说明](../../../visual-studio/overview/2013/release-notes.md#TOC13)。

SignalR 是构建 web 应用程序的需要实时用户交互或实时数据更新的开放源.NET 库。 示例包括社交应用程序、 多用户游戏、 业务协作和新闻、 天气或财务更新应用程序。 这些测试通常称为实时应用程序。

SignalR 简化了构建实时应用程序的过程。 它包括 ASP.NET 服务器库和 JavaScript 客户端库来轻松地管理客户端-服务器连接，并将内容更新推送到客户端。 您可以将 SignalR 库添加到现有 ASP.NET 应用程序以获取实时功能。

本教程演示以下的 SignalR 开发任务：

- SignalR 库添加到 ASP.NET web 应用程序。
- 创建用于将内容推送到客户端的中心类。
- 创建配置应用程序的 OWIN 启动类。
- 使用 SignalR jQuery 库在网页上发送消息并显示从中心的更新。

以下屏幕截图显示在浏览器中运行的聊天应用程序。 每个新用户可以发表评论，并查看用户加入聊天后已添加注释。

![聊天实例](tutorial-getting-started-with-signalr/_static/image1.png)

部分：

- [设置项目](#setup)
- [运行示例](#run)
- [检查代码](#code)
- [后续步骤](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>设置项目

本部分演示如何使用 Visual Studio 2013 和 SignalR 版本 2 创建空的 ASP.NET web 应用程序，将 SignalR 中，并创建聊天应用程序。

先决条件：

- Visual Studio 2013。 如果未安装 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)若要获取免费 Visual Studio 2013 Express 开发工具。

以下步骤使用 Visual Studio 2013 创建 ASP.NET 空 Web 应用程序并添加 SignalR 库：

1. 在 Visual Studio 中创建 ASP.NET Web 应用程序。

    ![创建 web](tutorial-getting-started-with-signalr/_static/image2.png)
2. 在中**新建 ASP.NET 项目**窗口中，保留**空**选中然后单击**创建项目**。

    ![创建空的 web](tutorial-getting-started-with-signalr/_static/image3.png)
3. 在中**解决方案资源管理器**，右键单击项目，选择**添加 |SignalR Hub 类 (v2)**。 将类命名**ChatHub.cs**并将其添加到项目。 此步骤将创建**ChatHub**类，并将一组脚本文件和支持 SignalR 的程序集引用添加到项目。

    > [!NOTE]
    > 您还可以将 SignalR 通过打开添加到项目**工具 |库包管理器 |包管理器控制台**并运行命令：

    `install-package Microsoft.AspNet.SignalR`

    如果使用控制台来添加 SignalR，SignalR hub 类作为单独的步骤后创建将 SignalR 添加。

    > [!NOTE]
    > 如果使用 Visual Studio 2012 中， **SignalR Hub 类 (v2)** 模板将不可用。 您可以添加纯**类**调用`ChatHub`相反。
4. 在中**解决方案资源管理器**，展开脚本节点。 适用于 jQuery 和 SignalR 的脚本库将显示在该项目。
5. 在新的代码替换为**ChatHub**用下面的代码的类。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. 在中**解决方案资源管理器**，右键单击项目，然后单击**添加 |OWIN 启动类**。 新类命名为`Startup`并单击确定。

    > [!NOTE]
    > 如果使用 Visual Studio 2012 中， **OWIN 启动类**模板将不可用。 您可以添加纯**类**调用`Startup`相反。
7. 将新的启动类的内容更改为以下。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. 在中**解决方案资源管理器**，右键单击项目，然后单击**添加 |HTML 页**。 命名新页面`index.html`。
    >[!NOTE]
    >可能需要更改对 JQuery 和 SignalR 库的引用的版本号
9. 在中**解决方案资源管理器**，右键单击刚创建的 HTML 页，然后单击**设为起始页**。
10. HTML 页中的默认代码替换为以下代码。

    > [!NOTE]
    > 可能通过程序包管理器安装 SignalR 脚本的更高版本。 验证以下脚本参考对应于版本的脚本文件在项目中 （它们将与此不同如果添加了使用 NuGet，而不是添加 hub 的 SignalR。）

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]
11. **保存所有**项目。

<a id="run"></a>

## <a name="run-the-sample"></a>运行示例

1. 按 F5 以在调试模式下运行该项目。 中的浏览器实例并提示输入用户名称的 HTML 页面加载。

    ![输入用户名](tutorial-getting-started-with-signalr/_static/image4.png)
2. 输入用户名称。
3. 从地址行中的浏览器复制 URL 并将其用于打开两个更多的浏览器实例。 在每个浏览器实例中，输入唯一的用户名称。
4. 在每个浏览器实例中，添加注释并单击**发送**。 注释应显示在浏览器的所有实例。

    > [!NOTE]
    > 此简单的聊天应用程序不维护服务器上的讨论上下文。 在中心广播到所有当前用户的注释。 加入聊天更高版本的用户将看到消息从时添加它们加入。

    下面的屏幕截图显示了在三个浏览器情况下，所有这些更新一个实例发送消息时运行的聊天应用程序：

    ![聊天浏览器](tutorial-getting-started-with-signalr/_static/image5.png)
5. 在中**解决方案资源管理器**，检查**脚本文档**节点运行的应用程序。 没有名为的脚本文件**中心**在运行时动态生成 SignalR 库。 此文件管理的 jQuery 脚本和服务器端代码之间的通信。

    ![](tutorial-getting-started-with-signalr/_static/image6.png)

<a id="code"></a>

## <a name="examine-the-code"></a>检查代码

SignalR 聊天应用程序演示了两个基本的 SignalR 开发任务： 在服务器上的主要协调对象为创建中心和使用 SignalR jQuery 库来发送和接收消息。

### <a name="signalr-hubs"></a>SignalR 集线器

中的代码示例**ChatHub**类派生自**Microsoft.AspNet.SignalR.Hub**类。 派生自**中心**类是一种有用的方式来构建 SignalR 应用程序。 可以在中心类上创建的公共方法，然后通过调用从网页中的脚本中访问这些方法。

在聊天代码中，客户端调用**ChatHub.Send**方法发送一封新邮件。 在中心反过来将消息发送给所有客户端，通过调用**Clients.All.broadcastMessage**。

**发送**方法演示了多个中心概念：

- 集线器上声明的公共方法，以便客户端可以调用它们。
- 使用**Microsoft.AspNet.SignalR.Hub.Clients**动态属性来访问所有客户端连接到此中心。
- 在客户端上调用的函数 (如`broadcastMessage`函数) 来更新客户端。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery"></a>SignalR 和 jQuery

HTML 页中的代码示例演示如何使用 SignalR jQuery 库与 SignalR 中心进行通信。 在代码中的基本任务声明的代理服务器能够引用中心，声明服务器可以将内容推送到客户端，调用的函数和启动的连接将消息发送到中心。

下面的代码声明对集线器代理的引用。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> 在 JavaScript 中于服务器类及其成员的引用位于混合大小写。 代码示例将引用 C# **ChatHub**中作为 JavaScript 类**chatHub**。


下面的代码是如何在脚本中创建一个回调函数。 在服务器上的中心类会调用此函数可将内容更新推送到每个客户端。 HTML 显示前先编码内容的两行都是可选的并显示简单的方法来阻止脚本注入。

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

下面的代码演示如何在中心打开的连接。 代码启动连接，然后将其传递函数来处理单击事件上**发送**HTML 页中的按钮。

> [!NOTE]
> 此方法可确保事件处理程序在执行之前建立的连接。


[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

<a id="next"></a>

## <a name="next-steps"></a>后续步骤

您学习了 SignalR 是一个框架，用于构建实时 web 应用程序。 您还学习了几个 SignalR 开发任务： 如何将 SignalR 添加到 ASP.NET 应用程序、 如何创建 hub 类以及如何发送和接收来自中心的消息。

有关如何部署到 Azure 的示例 SignalR 应用程序的演练，请参阅[Azure 应用服务中的 Web 应用使用 SignalR](../deployment/using-signalr-with-azure-web-sites.md)。 有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的详细信息，请参阅[在 Azure 应用服务中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。

若要了解更高级的 SignalR 开发概念，请访问以下站点 SignalR 源代码和资源：

- [SignalR 项目](http://signalr.net)
- [SignalR Github 和示例](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
