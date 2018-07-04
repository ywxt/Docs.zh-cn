---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: 教程： 使用 signalr 2 实现高频率实时 |Microsoft Docs
author: pfletcher
description: 本教程演示如何创建使用 ASP.NET SignalR 来提供高频率消息传送功能的 web 应用程序。 高频率内消息传送...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
ms.technology: dotnet-signalr
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8bcc80492804aff2e5a7d3c63004a84447600530
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393243"
---
<a name="tutorial-high-frequency-realtime-with-signalr-2"></a>教程： 使用 signalr 2 实现高频率实时
====================
通过[Patrick Fletcher](https://github.com/pfletcher)

[下载已完成的项目](http://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

> 本教程演示如何创建使用 ASP.NET SignalR 2 提供高频率的消息传送功能的 web 应用程序。 在这种情况下消息传送高频率意味着费率是固定的; 在发送的更新对于此应用程序，最多 10 个消息的第二个。
> 
> 将在本教程中创建的应用程序显示用户可以将一个形状。 在所有其他连接的浏览器中的形状位置然后将更新以匹配使用定时的更新拖动形状的位置。
> 
> 本教程中介绍的概念有实时游戏中的应用程序和其他模拟应用程序。
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

本教程演示如何创建应用程序与其他浏览器实时共享对象的状态。 我们将创建应用程序被称为 MoveShape。 MoveShape 页将显示的 HTML Div 元素，用户可拖动;当用户拖动该 Div，其新位置将发送到服务器，然后告知所有其他连接的客户端以更新要匹配的形状的位置。

![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

在本教程中创建的应用程序基于 Damian edwards 提供演示。 可以看到其中包含此演示视频[此处](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)。

本教程将首先演示如何将 SignalR 消息发送时所触发该形状拖动每个事件。 每个连接的客户端然后将更新该形状的本地版本的位置每次收到一条消息。

虽然应用程序将正常使用此方法，这并不建议的编程模型，因为会有获取发送，因此客户端和服务器无法获取过重消息并将会降低性能的消息数没有上限. 在客户端上显示的动画也是不相互连接，每个方法会立即移动形状，而不是移动顺利地为每个新的位置。 本教程的后面部分将演示如何创建将由客户端或服务器，发送消息的最大速率限制的计时器函数以及如何位置之间顺利移动形状。 在本教程中创建的应用程序的最终版本可以从下载[代码库](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)。

本教程包含以下各节：

- [先决条件](#prerequisites)
- [创建项目并添加 SignalR 和 JQuery.UI NuGet 包](#createtheproject2013)
- [创建基本应用程序](#baseapp)
- [在应用程序启动时启动中心](#startup2013)
- [添加客户端循环](#clientloop)
- [添加服务器循环](#serverloop)
- [添加客户端上流畅的动画](#animation)
- [执行进一步的步骤](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a>系统必备

本教程需要 Visual Studio 2013。

<a id="createtheproject2013"></a>

## <a name="create-the-project-and-add-the-signalr-and-jqueryui-nuget-package"></a>创建项目并添加 SignalR 和 JQuery.UI NuGet 包

在本部分中，我们将创建 Visual Studio 2013 中的项目。

以下步骤使用 Visual Studio 2013 创建 ASP.NET 空 Web 应用程序并将添加的 SignalR 和 jQuery.UI 库：

1. 在 Visual Studio 创建 ASP.NET Web 应用程序。

    ![创建 web](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)
2. 在中**新建 ASP.NET 项目**窗口中，保留**空**选中然后单击**创建项目**。

    ![创建空的 web](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
3. 在中**解决方案资源管理器**，右键单击项目，选择**添加 |SignalR Hub 类 (v2)**。 将类命名**MoveShapeHub.cs**并将其添加到项目。 此步骤将创建**MoveShapeHub**类，并将一组脚本文件和支持 SignalR 的程序集引用添加到项目。

    > [!NOTE]
    > 您还可以将 SignalR 通过单击添加到项目**工具 |库包管理器 |包管理器控制台**并运行命令：

    `install-package Microsoft.AspNet.SignalR`。 

    如果使用控制台来添加 SignalR，SignalR hub 类作为单独的步骤后创建将 SignalR 添加。
4. 单击**工具 |库包管理器 |包管理器控制台**。 在包管理器窗口中，运行以下命令：

    `Install-Package jQuery.UI.Combined`

    这将安装 jQuery UI 库，这将用于对形状进行动画处理。
5. 在中**解决方案资源管理器**展开脚本节点。 JQuery、 jQueryUI，和 SignalR 的脚本库将显示在该项目。

    ![脚本库引用](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="baseapp"></a>

## <a name="create-the-base-application"></a>创建基本应用程序

在本部分中，我们将创建在每个鼠标移动事件向服务器发送形状的位置的浏览器应用程序。 服务器然后会接收广播到所有其他连接的客户端此信息。 我们将在稍后的部分此应用程序上进行扩展。

1. 如果尚未创建 MoveShapeHub.cs 类中**解决方案资源管理器**，右键单击该项目并选择**添加**，**类...**.将类命名**MoveShapeHub**然后单击**添加**。
2. 在新的代码替换为**MoveShapeHub**用下面的代码的类。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

    `MoveShapeHub`上面类是 SignalR 集线器的实现。 在中作为[SignalR 入门](tutorial-getting-started-with-signalr.md)教程中，中心都有客户端将直接调用的方法。 在这种情况下，客户端将发送一个对象，包含新的服务器，然后获取将广播到所有其他连接的客户端到形状的 X 和 Y 坐标。 SignalR 将自动序列化此对象使用 JSON。

    将发送到客户端的对象 (`ShapeModel`) 包含成员来存储该形状的位置。 在服务器上对象的版本还包含成员来跟踪哪些客户端的数据存储，以便指定客户端将不会发送自己的数据。 此成员使用`JsonIgnore`属性以防止进行序列化并发送到客户端。

<a id="startup2013"></a>
## <a name="starting-the-hub-when-the-application-starts"></a>在应用程序启动时启动中心

1. 接下来，我们将设置到中心的映射，应用程序启动时。 在 SignalR 2 中，这是通过添加 OWIN 启动类，后者会调用`MapSignalR`时启动类的`Configuration`OWIN 启动时执行方法。 将类添加到 OWIN 的启动处理使用`OwinStartup`程序集属性。

    在中**解决方案资源管理器**，右键单击项目，然后单击**添加 |OWIN 启动类**。 将类命名*启动*然后单击**确定**。
2. 将 Startup.cs 的内容更改为以下：

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<a id="client"></a>
## <a name="adding-the-client"></a>添加客户端

1. 接下来，我们将添加客户端。 在中**解决方案资源管理器**，右键单击项目，然后单击**添加 |新项**。 在中**添加新项**对话框中，选择**Html 页**。 将该页命名为**Default.html**然后单击**添加**。
2. 在中**解决方案资源管理器**，右键单击刚创建的页，然后单击**设为起始页**。
3. HTML 页中的默认代码替换为以下代码片段。

    > [!NOTE]
    > 验证该脚本引用以下匹配项添加到你的项目的 Scripts 文件夹中的包。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html)]

    上面的 HTML 和 JavaScript 代码创建名为形状的红色 Div、 启用形状的拖放行为使用 jQuery 库，并使用形状的`drag`事件以向服务器发送形状的位置。
4. 按 F5 启动应用程序。 复制页面的 URL，并将其粘贴到第二个浏览器窗口。 在一个浏览器窗口中; 将形状在其他浏览器窗口中的形状应移动。

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a>添加客户端循环

由于发送的每个鼠标移动事件中的形状的位置将创建不必要数量的网络流量，从客户端的消息需要受到限制。 我们将使用 javascript`setInterval`函数来设置一个循环，将新的位置信息发送到服务器以固定费率。 此循环是"游戏循环"，驱动器的所有功能的游戏或其他模拟重复调用函数的非常基本表示形式。

1. 更新要匹配下面的代码段的 HTML 页面中的客户端代码。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html)]

    更高版本的更新添加了`updateServerModel`函数，它获取名为按固定的频率。 此函数将位置数据发送到服务器时`moved`标志指示是要发送的新位置数据。
2. 按 F5 启动应用程序。 复制页面的 URL，并将其粘贴到第二个浏览器窗口。 在一个浏览器窗口中; 将形状在其他浏览器窗口中的形状应移动。 获取发送到服务器的消息数会受到限制，因为动画不会顺利地如前一部分中所示。

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a>添加服务器循环

在当前应用程序，从服务器发送到客户端的消息转通常它们被接收。 这会产生类似的问题，因为客户端; 上出现过通常需要它们，然后连接可能会变得来路因此可以将消息发送。 本部分介绍如何更新服务器以实现一个计时器，用于限制的传出消息的速率。

1. 内容替换为`MoveShapeHub.cs`使用以下代码片段。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    上面的代码中扩展客户端添加`Broadcaster`类，该类将限制传出消息使用`Timer`从.NET framework 类。

    由于中心本身是暂时性 （创建每次在需要时），`Broadcaster`将创建为单一实例。 （在.NET 4 中引入） 的迟缓初始化用于将其创建推迟，直到有必要，确保计时器启动之前完全创建第一个集线器实例。

    对客户端的调用`UpdateShape`函数然后移出该中心的`UpdateModel`方法，因此它不再接收传入消息时，立即调用。 而是发送到客户端的消息将发送的每秒 25 调用速率受`_broadcastLoop`中的计时器`Broadcaster`类。

    最后，而不是调用客户端方法从中心直接`Broadcaster`类需要获取对当前正在运行的中心的引用 (`_hubContext`) 使用`GlobalHost`。
2. 按 F5 启动应用程序。 复制页面的 URL，并将其粘贴到第二个浏览器窗口。 在一个浏览器窗口中; 将形状在其他浏览器窗口中的形状应移动。 不会在浏览器中从上一节中看到的差异，但将被发送到客户端的消息数。

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a>添加客户端上流畅的动画

应用程序几乎已完成，但我们可以进行一更多项改进，在客户端上形状的动态移动以响应服务器消息。 而不是将该形状的位置设置为给定服务器的新位置，我们将使用 JQuery UI 库`animate`函数以其当前和新位置之间顺利移动形状。

1. 更新客户端的`updateShape`方法看起来像下面突出显示的代码：

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

    上面的代码将从旧位置形状移到新服务器 （在本例中为 100 毫秒） 的动画时间间隔内提供。 新动画开始之前清除该形状上运行任何前一个动画。
2. 按 F5 启动应用程序。 复制页面的 URL，并将其粘贴到第二个浏览器窗口。 在一个浏览器窗口中; 将形状在其他浏览器窗口中的形状应移动。 在其他窗口中的形状的移动应显示较低即使如及其移动内插时间，而无需一次设置每个传入消息。

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image8.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a>执行进一步的步骤

在本教程中，已学习了如何发送客户端和服务器之间的高频率消息 SignalR 应用程序进行编程。 这种通信模式可用于开发联机游戏和其他模拟，如[ShootR 游戏使用 SignalR 创建](http://shootr.signalr.net)。

在本教程中创建的完整应用程序可以从下载[代码库](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)。

若要了解有关 SignalR 开发概念的详细信息，请访问以下站点 SignalR 源代码和资源：

- [SignalR 项目](http://signalr.net)
- [SignalR Github 和示例](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

有关如何部署到 Azure 的 SignalR 应用程序的演练，请参阅[Azure 应用服务中的 Web 应用使用 SignalR](../deployment/using-signalr-with-azure-web-sites.md)。 有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的详细信息，请参阅[在 Azure 应用服务中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。
