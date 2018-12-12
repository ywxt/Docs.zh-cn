---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: 教程：使用 SignalR 2 和 MVC 5 入门 |Microsoft Docs
author: pfletcher
description: 本教程演示如何使用 ASP.NET SignalR 2 来创建实时聊天应用程序。 将 SignalR 添加到 MVC 5 应用程序并创建一个聊天视图...
ms.author: riande
ms.date: 06/10/2014
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.openlocfilehash: 568f82daa67f33736c2bf7a45a3e1339f265c487
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287504"
---
<a name="tutorial-getting-started-with-signalr-2-and-mvc-5"></a>教程：使用 SignalR 2 和 MVC 5 入门
====================
通过[Patrick Fletcher](https://github.com/pfletcher)， [Tim Teebken](https://github.com/timlt)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[下载已完成的项目](http://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

> 本教程演示如何使用 ASP.NET SignalR 2 来创建实时聊天应用程序。 将将 SignalR 添加到 MVC 5 应用程序，并创建要发送，并显示消息的聊天视图。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - MVC 5
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

本教程向您介绍使用 ASP.NET SignalR 2 和 ASP.NET MVC 5 开发的实时 web 应用程序。 本教程使用相同的聊天应用程序代码作为[SignalR 入门教程](tutorial-getting-started-with-signalr.md)，但显示了如何将其添加到 MVC 5 应用程序。

在本主题中，您将学习以下的 SignalR 开发任务：

- SignalR 库添加到 MVC 5 应用程序。
- 创建中心和 OWIN 启动类，可将内容推送到客户端。
- 使用 SignalR jQuery 库在网页上发送消息并显示从中心的更新。

以下屏幕截图显示在浏览器中运行的已完成的聊天应用程序。

![聊天实例](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

部分：

- [设置项目](#setup)
- [运行示例](#run)
- [检查代码](#code)
- [后续步骤](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>设置项目

先决条件：

- Visual Studio 2013。 如果未安装 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)若要获取免费 Visual Studio 2013 Express 开发工具。

本部分演示如何创建一个 ASP.NET MVC 5 应用程序、 添加 SignalR 库，并创建聊天应用程序。

1. 在 Visual Studio 中，创建面向.NET Framework 4.5 的 C# ASP.NET 应用程序、 其命名为 SignalRChat，并单击确定。

    ![创建 web](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)
2. 在中`New ASP.NET Project`对话框中，然后选择**MVC**，然后单击**更改身份验证**。

    ![创建 web](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)
3. 选择**无身份验证**中**更改身份验证**对话框中，然后单击**确定**。

    ![选择无身份验证](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

    > [!NOTE]
    > 如果为应用程序中，选择不同的身份验证提供程序`Startup.cs`将为您创建类; 不需要创建您自己`Startup.cs`下面的步骤 10 中的类。
4. 单击**确定**中**新建 ASP.NET 项目**对话框。
5. 打开**工具 > NuGet 包管理器 > 程序包管理器控制台**并运行以下命令。 此步骤将一组脚本文件和启用 SignalR 功能的程序集引用添加到项目。

    `install-package Microsoft.AspNet.SignalR`
6. 在中**解决方案资源管理器**，展开脚本文件夹。 请注意有关 SignalR 的脚本库已添加到项目。

    ![脚本文件夹](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)
7. 在中**解决方案资源管理器**，右键单击项目，选择**添加 |新的文件夹**，并添加名为的新文件夹**中心**。
8. 右键单击**中心**文件夹中，单击**添加 |新项**，选择**Visual C# |Web |SignalR**中的节点**已安装**窗格中，选择**SignalR Hub 类 (v2)** 在中心窗格中，并创建一个名为的新中心**ChatHub.cs**。 将此类用作 SignalR 服务器集线器将消息发送到所有客户端。

    ![创建新的中心](tutorial-getting-started-with-signalr-and-mvc/_static/image6.png)
9. 中的代码替换**ChatHub**用下面的代码的类。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]
10. 创建一个名为 Startup.cs 的新类。 更改为以下文件的内容。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]
11. 编辑`HomeController`类中找到**controllers/Homecontroller.cs**并将以下方法添加到类。 此方法返回**聊天**将在稍后的步骤中创建的视图。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]
12. 右键单击**Views/Home**文件夹，然后选择**添加...|视图**。
13. 在中**添加视图**对话框中，命名新视图**聊天**。

    ![添加视图](tutorial-getting-started-with-signalr-and-mvc/_static/image7.png)
14. 内容替换为**Chat.cshtml**用下面的代码。

    > [!IMPORTANT]
    > 当您将 SignalR 和其他脚本库添加到你的 Visual Studio 项目中时，包管理器可能会安装比本主题中所示的版本更新的 SignalR 脚本文件的版本。 请确保在代码中的脚本引用与脚本库在项目中安装的版本匹配。

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]
15. **保存所有**项目。

<a id="run"></a>

## <a name="run-the-sample"></a>运行示例

1. 按 F5 以在调试模式下运行该项目。
2. 在浏览器地址行中，追加 **/home/聊天**到项目的默认页的 URL。 聊天页面加载中的浏览器实例并提示输入用户名称。

    ![输入用户名](tutorial-getting-started-with-signalr-and-mvc/_static/image8.png)
3. 输入用户名称。
4. 从地址行中的浏览器复制 URL 并将其用于打开两个更多的浏览器实例。 在每个浏览器实例中，输入唯一的用户名称。
5. 在每个浏览器实例中，添加注释并单击**发送**。 注释应显示在浏览器的所有实例。

    > [!NOTE]
    > 此简单的聊天应用程序不维护服务器上的讨论上下文。 在中心广播到所有当前用户的注释。 加入聊天更高版本的用户将看到消息从时添加它们加入。
6. 以下屏幕截图显示在浏览器中运行的聊天应用程序。

    ![聊天浏览器](tutorial-getting-started-with-signalr-and-mvc/_static/image9.png)
7. 在中**解决方案资源管理器**，检查**脚本文档**节点运行的应用程序。 如果使用 Internet Explorer 作为你的浏览器，此节点会显示在调试模式下。 没有名为的脚本文件**中心**在运行时动态生成 SignalR 库。 此文件管理的 jQuery 脚本和服务器端代码之间的通信。 如果使用 Internet Explorer 以外的浏览器，您还可以访问动态**中心**通过浏览到它直接，例如文件 http://mywebsite/signalr/hubs 。

<a id="code"></a>

## <a name="examine-the-code"></a>检查代码

SignalR 聊天应用程序演示了两个基本的 SignalR 开发任务： 在服务器上的主要协调对象为创建中心和使用 SignalR jQuery 库来发送和接收消息。

### <a name="signalr-hubs"></a>SignalR 集线器

中的代码示例**ChatHub**类派生自**Microsoft.AspNet.SignalR.Hub**类。 派生自**中心**类是一种有用的方式来构建 SignalR 应用程序。 可以在中心类上创建的公共方法，然后通过调用从网页中的脚本中访问这些方法。

在聊天代码中，客户端调用**ChatHub.Send**方法发送一封新邮件。 在中心反过来将消息发送给所有客户端，通过调用**Clients.All.addNewMessageToPage**。

**发送**方法演示了多个中心概念：

- 集线器上声明的公共方法，以便客户端可以调用它们。
- 使用**Microsoft.AspNet.SignalR.Hub.Clients**属性来访问所有客户端连接到此中心。
- 在客户端上调用的函数 (如`addNewMessageToPage`函数) 来更新客户端。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR 和 jQuery

**Chat.cshtml**视图文件中的代码示例演示如何使用 SignalR jQuery 库与 SignalR 中心进行通信。 在代码中的基本任务创建对自动生成的代理为中心，声明函数的服务器可以调用内容推送到客户端，并启动连接来将消息发送到中心的引用。

下面的代码声明对集线器代理的引用。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> 在 JavaScript 中于服务器类及其成员的引用位于混合大小写。 代码示例将引用 C# **ChatHub**中作为 JavaScript 类**chatHub**。 如果你想要引用`ChatHub`类在 jQuery 中使用传统的 Pascal 大小写，就像在 C# 中，编辑 ChatHub.cs 类文件。 添加`using`语句来引用`Microsoft.AspNet.SignalR.Hubs`命名空间。 然后添加`HubName`归于`ChatHub`类，例如`[HubName("ChatHub")]`。 最后，更新到你的 jQuery 引用`ChatHub`类。


下面的代码演示如何在脚本中创建一个回调函数。 在服务器上的中心类会调用此函数可将内容更新推送到每个客户端。 可选调用`htmlEncode`函数将显示一种方式，以 html 格式显示在页中，作为一种方法，以防止脚本注入之前编码消息内容。

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

下面的代码演示如何在中心打开的连接。 代码启动连接，然后将其传递函数来处理单击事件上**发送**聊天页中的按钮。

> [!NOTE]
> 此方法可确保事件处理程序在执行之前建立的连接。


[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>后续步骤

您学习了 SignalR 是一个框架，用于构建实时 web 应用程序。 您还学习了几个 SignalR 开发任务： 如何将 SignalR 添加到 ASP.NET 应用程序、 如何创建 hub 类以及如何发送和接收来自中心的消息。

有关如何部署到 Azure 的示例 SignalR 应用程序的演练，请参阅[Azure 应用服务中的 Web 应用使用 SignalR](../deployment/using-signalr-with-azure-web-sites.md)。 有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的详细信息，请参阅[在 Azure 应用服务中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。

若要了解更高级的 SignalR 开发概念，请访问以下站点 SignalR 源代码和资源：

- [SignalR 项目](http://signalr.net)
- [SignalR Github 和示例](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
