---
uid: aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
title: 在 IIS 中的 OWIN 中间件集成管道 |Microsoft Docs
author: Praburaj
description: 本文介绍如何运行 OWIN 中间件组件 (OMCs) 在 IIS 集成管道中，以及如何设置管道事件 OMC 上运行。 应...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/07/2013
ms.topic: article
ms.assetid: d031c021-33c2-45a5-bf9f-98f8fa78c2ab
ms.technology: ''
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
msc.type: authoredcontent
ms.openlocfilehash: 1c2f7a9b948331eae2f5b44f25219adb76a0c745
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37379055"
---
<a name="owin-middleware-in-the-iis-integrated-pipeline"></a>IIS 集成管道中的 OWIN 中间件
====================
通过[Praburaj Thiagarajan](https://github.com/Praburaj)， [Rick Anderson](https://github.com/Rick-Anderson)

> 本文介绍如何运行 OWIN 中间件组件 (OMCs) 在 IIS 集成管道中，以及如何设置管道事件 OMC 上运行。 你应该查看[项目 Katana 概述](an-overview-of-project-katana.md)并[OWIN 启动类检测](owin-startup-class-detection.md)阅读本教程之前，先。 本教程由 Rick Anderson 编写 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )，Chris Ross、 Praburaj Thiagarajan 和 Howard Dierking ( [ @howard \_dierking](https://twitter.com/howard_dierking) )。


尽管[OWIN](an-overview-of-project-katana.md)中间件组件 (OMCs) 主要用于在服务器不可知管道中运行，可以将 IIS 集成管道中还运行 OMC (**经典模式是*不*支持**)。 OMC 可以进行工作 IIS 集成管道中，通过安装以下包从包管理器控制台 (PMC):

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample1.cmd)]

这意味着所有应用程序框架，甚至包括那些尚不能运行 IIS 和 System.Web，之外可以受益于现有的 OWIN 中间件组件。 

> [!NOTE]
> 所有`Microsoft.Owin.Security.*`包随附在 Visual Studio 2013 中新的标识系统 (例如： Cookie、 Microsoft 帐户、 Google、 Facebook、 Twitter[持有者令牌](http://self-issued.info/docs/draft-ietf-oauth-v2-bearer.html)，OAuth 授权服务器，JWT，Azure Active目录和 Active directory 联合身份验证服务） 编写为 OMCs，并可以在自承载和 IIS 托管方案中使用。

## <a name="how-owin-middleware-executes-in-the-iis-integrated-pipeline"></a>如何在 IIS 集成管道中执行的 OWIN 中间件

对于 OWIN 控制台应用程序，应用程序管道使用构建[启动配置](owin-startup-class-detection.md)通过使用添加组件的顺序设置`IAppBuilder.Use`方法。 在 OWIN 管道，即[Katana](an-overview-of-project-katana.md)运行时将使用注册的顺序处理 OMCs `IAppBuilder.Use`。 IIS 集成管道中请求管道组成[HttpModules](https://msdn.microsoft.com/library/ms178468(v=vs.85).aspx)如订阅一组预定义的管道事件[BeginRequest](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx)， [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)， [AuthorizeRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)，等等。

如果我们进行比较的 OMC [HttpModule](https://msdn.microsoft.com/library/zec9k340(v=vs.85).aspx)在 ASP.NET 领域中，OMC 必须注册到正确的预定义的管道事件。 例如，HttpModule`MyModule`传入请求时将调用[AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)管道中的阶段：

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample2.cs?highlight=10)]

为了使 OMC 参与此相同的、 基于事件的执行顺序[Katana](an-overview-of-project-katana.md)通过扫描运行时代码[启动配置](owin-startup-class-detection.md)和订阅的每个到中间件组件集成的管道事件。 例如，以下 OMC 和注册代码，可看到中间件组件的默认事件注册。 (有关更多详细创建 OWIN 启动类的说明，请参阅[OWIN 启动类检测](owin-startup-class-detection.md)。)

1. 创建一个空的 web 应用程序项目并将其命名**owin2**。
2. 从包管理器控制台 (PMC) 中，运行以下命令： 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample3.cmd)]
3. 添加`OWIN Startup Class`并将其命名`Startup`。 生成的代码替换为的以下 （突出显示所做的更改）：  

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample4.cs?highlight=5-7,15-36)]
4. 按 F5 运行该应用程序。

启动配置设置了管道，其中包含三个中间件组件，前两个显示诊断信息和对事件作出响应的最后一个 （以及还显示诊断信息）。 `PrintCurrentIntegratedPipelineStage`方法显示此中间件调用的集成的管道事件和消息。 输出窗口显示以下信息：

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample5.cmd)]

Katana 运行时映射到的 OWIN 中间件组件的每个[PreExecuteRequestHandler](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)默认情况下，这对应于 IIS 管道事件[PreRequestHandlerExecute](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)。

## <a name="stage-markers"></a>阶段标记

您可以将标记 OMCs 使用执行特定阶段的管道`IAppBuilder UseStageMarker()`扩展方法。 若要在某个特定阶段期间运行的一组中间件组件，请插入阶段标记后的最后一个组件是在注册过程组。 可以在管道的哪个阶段执行中间件的规则和顺序组件必须运行 （这些规则在本教程后面介绍）。 添加`UseStageMarker`方法`Configuration`代码如下所示：

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample6.cs?highlight=13,19)]

`app.UseStageMarker(PipelineStage.Authenticate)`调用配置 （在此情况下，我们两个诊断组件） 的所有以前注册的中间件组件上的身份验证阶段的管道运行。 最后一个中间件组件 （它将显示诊断和响应的请求） 将在上运行`ResolveCache`阶段 ( [ResolveRequestCache](https://msdn.microsoft.com/library/system.web.httpapplication.resolverequestcache.aspx)事件)。

按 F5 运行该应用程序。输出窗口显示以下信息：

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample7.cmd)]

## <a name="stage-marker-rules"></a>阶段标记规则

Owin 中间件组件 (OMC) 可以配置为运行在 OWIN 管道阶段的以下事件：

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample8.cs)]

1. 默认情况下，在最后一个事件运行 OMCs (`PreHandlerExecute`)。 这就是为什么我们的第一个示例代码显示"PreExecuteRequestHandler"。
2. 可以使用`app.UseStageMarker`中列出的方法来注册 OMC 运行更早版本，在 OWIN 管道的任何阶段`PipelineStage`枚举。
3. OWIN 管道和 IIS 管道的排序，因此调用`app.UseStageMarker`必须按顺序。 不能位于与已注册到的最后一个事件的事件设置事件处理程序`app.UseStageMarker`。 例如，*后*调用：

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample9.cmd)]

   调用`app.UseStageMarker`传递`Authenticate`或`PostAuthenticate`不会遵循，并且会引发任何异常。 在最新的阶段，即默认情况下运行的 OMCs `PreHandlerExecute`。 使用阶段标记以使它们之前运行。 如果指定无序的阶段标记，我们将舍入到的早期标记。 换而言之，添加阶段标记显示"最晚阶段 X 运行"。 OMC 的运行时间最早的阶段标记后添加 OWIN 管道中。
4. 对调用的最早阶段`app.UseStageMarker`wins。 例如，如果切换顺序`app.UseStageMarker`我们上一示例中的调用：

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample10.cs?highlight=13,19)]

   输出窗口将显示： 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample11.cmd)]

   均在中运行的 OMCs`AuthenticateRequest`阶段，因为使用注册的最后一个 OMC`Authenticate`事件，和`Authenticate`事件之前的所有其他事件。
