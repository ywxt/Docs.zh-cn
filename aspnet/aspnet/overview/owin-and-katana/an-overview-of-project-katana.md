---
uid: aspnet/overview/owin-and-katana/an-overview-of-project-katana
title: 项目 Katana 概述 |Microsoft Docs
author: howarddierking
description: ASP.NET Framework 已超过十年，并且该平台已启用的无数网站和服务开发。 为 Web 应用程序...
ms.author: riande
ms.date: 08/30/2013
ms.assetid: 0ee21741-c1bf-4025-a9b0-24580cae24bc
msc.legacyurl: /aspnet/overview/owin-and-katana/an-overview-of-project-katana
msc.type: authoredcontent
ms.openlocfilehash: 52007eba109de28c6d178505b82b1d5ff2883b47
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830039"
---
<a name="an-overview-of-project-katana"></a>项目 Katana 概述
====================
通过[Howard Dierking](https://github.com/howarddierking)

> ASP.NET Framework 已超过十年，并且该平台已启用的无数网站和服务开发。 Web 应用程序开发策略不断演进，如框架已经能够改进与 ASP.NET MVC 和 ASP.NET Web API 之类的技术步骤中。 Web 应用程序开发到云计算领域时其进化的下一步，项目[Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET)提供基础组件到 ASP.NET 应用程序，使他们能够灵活、 可移植，集轻量的并提供更好的性能 – 将另一种方法，项目[Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET)云优化您的 ASP.NET 应用程序。


## <a name="why-katana--why-now"></a>为什么 Katana-为什么要现在实施？

 是否其中一个讨论开发人员框架或最终用户产品，而不考虑，务必要了解有关创建基础的动机产品 – 和过程的一部分包括了解该产品已创建的。 ASP.NET 最初是通过记住两个客户创建的。   
  
**客户的第一个组是经典的 ASP 开发人员。** 在时，ASP 将已创建动态、 数据驱动网站和应用程序的交错执行标记和服务器端脚本的主要技术之一。 ASP 运行时提供服务器端脚本的一系列的对象抽象化基础 HTTP 协议和 Web 服务器的核心内容，并使用其他服务的此类会话和应用程序状态管理，提供缓存，等等。虽然功能强大，经典 ASP 应用程序变得难以管理，因为它们的大小和复杂性的不断发展。 这是代码的很大程度上是代码的由于缺乏中脚本编写环境结合生成的代码和标记交错的重复结构。 若要同时解决其问题的一些利用经典 ASP 的优势，ASP.NET 利用了代码组织与语言提供的面向对象的.NET Framework 的同时还保留的服务器端编程模型哪些经典 ASP 到开发人员有增长习惯。

**ASP.NET 的目标客户的第二个组是 Windows 业务应用程序开发人员。** 与经典 ASP 开发人员习惯于编写 HTML 标记和代码以生成更多的 HTML 标记，不同 （如之前的 VB6 开发人员） 的 WinForms 开发人员习惯于包含一个画布和一组丰富的用户设计时体验界面控件。 第一个版本的 ASP.NET-也称为"Web Forms"提供类似的设计时体验以及用户界面组件的服务器端事件模型和基础结构功能 （如视图状态） 的一组可在创建了无缝开发人员体验之间客户端和服务器端编程。 Web 窗体有效地 hid WinForms 开发人员所熟悉的有状态的事件模型下的站点的无状态性质。

### <a name="challenges-raised-by-the-historical-model"></a>引发的历史模型的挑战

**最终结果是成熟且功能丰富的运行时和开发人员的编程模型。** 但是，随着的丰富功能带来几个值得注意的挑战。 首先，该框架已**整体式**，与以逻辑方式完全不同的功能单元的紧密耦合在同一 System.Web.dll 程序集 （例如，使用的 Web 窗体框架的核心 HTTP 对象）。 其次，ASP.NET 已包括在内，作为更大的.NET Framework，这意味着，一部分**各版本之间的时间为大约年。** 这使得用户难以 asp.net 将与所有快速发展的 Web 开发中发生的更改保持同步。 最后，System.Web.dll 本身耦合到特定的 Web 托管选项的多种不同的方式在： Internet 信息服务 (IIS)。

### <a name="evolutionary-steps-aspnet-mvc-and-aspnet-web-api"></a>进化的步骤： ASP.NET MVC 和 ASP.NET Web API

和更改的很多 Web 开发中发生的事情 ！ 因为一系列小，聚焦组件而不是大框架已越来越多地开发 web 应用程序。 组件，以及与这些发布的发布的频率数过快的速度增加。 很明显，而不是更大、 功能更丰富，因此获取较小，易于分离，且更有针对性的框架需要保持同步的 web **ASP.NET 小组采用了几个进化的步骤来启用 ASP.NET 作为一系列可插入 Web 组件而不是单一框架**。

早期更改之一是在 Rails 上归功于 Ruby 等的 Web 开发框架的已知模型-视图-控制器 (MVC) 设计模式的受欢迎程度的增加。 这种样式的构建 Web 应用程序为开发人员提供了更好地控制其应用程序的标记，同时仍然保留标记和业务逻辑，这是一个 ASP.NET 初始卖点的分离。 为了满足这种样式的 Web 应用程序开发的需求，Microsoft，借此机会我们来为自身定位更好的未来**带外开发 ASP.NET MVC** （和不包含在.NET Framework 中）。 ASP.NET MVC 发布，作为独立下载。 这为工程团队提供的灵活性以将更新提供比以前可能已被频繁得多。

Web 应用程序开发中另一个重大的转变是静态初始标记使用的通信，客户端脚本生成的页的动态部分，向从动态的、 由服务器生成 Web pages 转变**与后端 Web Api 通过AJAX 请求**。 此体系结构改变帮助推动 Web Api 的兴起和 ASP.NET Web API 框架的开发。 对于 ASP.NET MVC 中，如 ASP.NET Web API 的版本提供另一个作为更加模块化框架进一步发展 ASP.NET 的机会。 工程小组采用了充分利用这个机会并 **，以便它有没有依赖关系，任何在 System.Web.dll 中找到的核心框架类型上生成 ASP.NET Web API**。 启用此两项操作： 首先，它意味着完全独立的方式可改进 ASP.NET Web API （和它无法继续进行快速迭代，因为它通过 NuGet 提供）。 其次，由于没有为 System.Web.dll，没有外部依赖关系，因此，没有依赖关系到 IIS，ASP.NET Web API 包含在自定义主机 （例如，控制台应用程序、 Windows 服务等） 中运行的功能

### <a name="the-future-a-nimble-framework"></a>一个灵活框架的未来：

通过分离从另一个 framework 组件，然后 NuGet 上发布，框架可以现在**循环访问更独立地以及更快地**。 此外的功能和灵活性的 Web API 的自承载功能被证明很有吸引力的开发人员希望**小巧、 轻便主机**用于其服务。 的确如此大的吸引力，实际上，其他框架还希望这项功能，和这显示了新的挑战在于每个框架上其自身的基址在其自己的主机进程中运行，并且需要进行管理 （启动、 停止等） 独立。 现代 Web 应用程序通常都支持静态文件服务、 动态页生成、 Web API 和更多最近实时的一次性/推送通知。 应为每个服务应将运行和分开管理的是只是不现实。

我们需要的是，将开发人员可以编写应用程序从各种不同的组件和框架，然后在支持的主机上运行该应用程序的单一托管抽象。

## <a name="the-open-web-interface-for-net-owin"></a>.NET (OWIN) 开放 Web 接口

 灵感源自通过来实现的好处[机架](http://rack.github.io/)Ruby 社区中的.NET 社区的多个成员着手创建 Web 服务器和框架组件之间的抽象。 两个用于 OWIN 抽象的设计目标是，它是简单和，所需的时间最少可能依赖项其他框架类型。 这两个目标有助于确保：

- 新的组件可以更轻松地开发和使用。
- 应用程序可以更轻松地移植主机和可能整个平台/操作系统之间。

生成抽象包含两个核心元素。 第一种是环境字典。 此数据结构是状态的负责存储所有用于处理 HTTP 请求和响应，以及任何相关服务器状态所需。 环境字典定义，如下所示：

[!code-console[Main](an-overview-of-project-katana/samples/sample1.cmd)]

兼容 OWIN 的 Web 服务器负责填充数据，如正文流和 HTTP 请求和响应的标头集合的环境字典。 然后是要填充或用其他值更新字典并写入到响应正文流的应用程序或框架组件的责任。

除了指定的环境字典类型，该 OWIN 规范定义核心字典键/值对的列表。 例如下, 表显示了 HTTP 请求的所需的字典键：

| 键名 | 值说明 |
| --- | --- |
| `"owin.RequestBody"` | 使用请求正文，如果任何 Stream。 如果没有请求正文，Stream.Null 可以用作占位符。 请参阅[请求正文](http://owin.org/html/owin.html#34-request-body-100-continue-and-completed-semantics)。 |
| `"owin.RequestHeaders"` | `IDictionary<string, string[]>`的请求标头。 请参阅[标头](http://owin.org/html/owin.html#3-3-headers)。 |
| `"owin.RequestMethod"` | 一个`string`包含请求的 HTTP 请求方法 (例如， `"GET"`， `"POST"`)。 |
| `"owin.RequestPath"` | 一个`string`包含请求路径。 该路径必须相对于应用程序委托; 的"根"请参阅[路径](http://owin.org/html/owin.html#5-3-paths)。 |
| `"owin.RequestPathBase"` | 一个`string`包含对应于"根"的应用程序委托; 的请求路径部分看到[路径](http://owin.org/html/owin.html#5-3-paths)。 |
| `"owin.RequestProtocol"` | 一个`string`包含的协议名称和版本 (例如`"HTTP/1.0"`或`"HTTP/1.1"`)。 |
| `"owin.RequestQueryString"` | 一个`string`包含查询字符串部分的 HTTP 请求 URI、 没有前导"？"(例如， `"foo=bar&baz=quux"`)。 值可能为空字符串。 |
| `"owin.RequestScheme"` | 一个`string`包含用于请求的 URI 方案 (例如， `"http"`， `"https"`); 请参阅[URI 方案](http://owin.org/html/owin.html#5-1-uri-scheme)。 |

OWIN 的第二个关键元素是应用程序委托。 这是一个函数签名，它可用作 OWIN 应用程序中的所有组件之间的主要接口。 应用程序委托的定义如下所示：

`Func<IDictionary<string, object>, Task>;`

然后，应用程序委托是只需 Func 委托类型，该函数接受环境字典作为输入并返回一个任务的实现。 此设计具有面向开发人员的几个含义：

- 有极少数才能写入 OWIN 组件所需的类型依赖项。 这极大地提高开发人员的 OWIN 的可访问性。
- 异步设计使抽象来高效地使用其处理的计算资源，尤其是在更多的 I/O 密集型操作。
- 因为应用程序委托是执行的原子单元，并且环境字典作为委托参数执行，因为 OWIN 组件可以轻松地链接在一起，以创建复杂的 HTTP 处理管道。

从实现的角度看，OWIN 是一种规范 ([http://owin.org/html/owin.html](http://owin.org/html/owin.html))。 其目标是不会在下一步的 Web 框架，但而不是一个用于 Web 框架和 Web 服务器的交互方式的规范。

如果您研究[OWIN](http://owin.org/)或[Katana](https://github.com/aspnet/AspNetKatana/wiki)，您可能还会发现[Owin NuGet 包](http://nuget.org/packages/Owin)和 Owin.dll。 此库包含一个界面[IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs)，其中可规范和编码中所述的启动顺序[节的第 4](http://owin.org/html/owin.html#4-application-startup)的 OWIN 规范。 尽管并不要求为了生成 OWIN 服务器[IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs)接口提供具体的参考点，并由 Katana 项目组件。

## <a name="project-katana"></a>Katana 项目

而同时[OWIN](http://owin.org/html/owin.html)规范和*Owin.dll*是拥有的社区，社区运行开源工作[Katana](https://github.com/aspnet/AspNetKatana/wiki)项目表示 OWIN 的组尽管仍开放源代码，生成并由 Microsoft 发布的组件。 这些组件包括基础结构组件，如主机和服务器，以及功能组件，例如身份验证组件和框架绑定如[SignalR](../../../signalr/index.md)和[ASP.NET WebAPI](../../../web-api/overview/getting-started-with-aspnet-web-api/index.md)。 项目具有以下三个高级别目标： 

- **可移植**– 组件应该能够轻松地替换为新的组件可用。 这包括所有类型的组件，从服务器和主机的 framework。 实现此目标的含义是，第三方框架可以无缝 Microsoft 在服务器上运行时 Microsoft 框架可以在第三方服务器和主机上运行。
- **灵活采用模块化结构/**– 与许多框架，其中包括大量的默认情况下启用的功能，不同，小且集中，将控件向应用程序开发人员在确定哪些组件应为 Katana 项目组件在其应用程序中使用。
- **轻型、 高性能/可缩放**– 通过传统的一个框架概念拆分为较小，一组专注于添加明确的应用程序开发人员，生成的 Katana 应用程序可以使用更少的计算的组件资源，并因此，比更多加载、 处理与其他类型的服务器和框架。 从底层基础结构的多个功能的应用程序的要求，如那些可以添加到 OWIN 管道中，但这应该是应用程序开发人员来说一个显式决策。 此外，较低级别的组件的可代替性意味着包含可用时，新的高性能服务器可以无缝地会引入 OWIN 应用程序的性能改进而不会破坏这些应用程序。

## <a name="getting-started-with-katana-components"></a>Katana 组件入门

当首次引入的一个方面[Node.js](http://nodejs.org/)立即吸引了人们的关注的框架已与一个无法制作和运行 Web 服务器的简单性。 如果 Katana 目标已设计框架的 light [Node.js](http://nodejs.org/)，其中一个可能通过说 Katana 带来了很多的优势进行汇总[Node.js](http://nodejs.org/) （和类似框架） 而不会迫使开发人员可以丢弃她了解的有关开发 ASP.NET Web 应用程序的全部内容。 对于此语句为真，Katana 项目入门应在本质上为同样简单[Node.js](http://nodejs.org/)。

## <a name="creating-hello-world"></a>创建"Hello World ！"

JavaScript 和.NET 开发之间的一个显著区别是编译器的存在 （或不存在）。 在这种情况下，简单的 Katana 服务器的起始点是一个 Visual Studio 项目。 但是，我们可以开始使用最小的项目类型： 空的 ASP.NET Web 应用程序。

[![](an-overview-of-project-katana/_static/image1.png)](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)

接下来，我们将安装[Microsoft.Owin.Host.SystemWeb](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)到项目的 NuGet 包。 此包提供在 ASP.NET 请求管道中运行一个 OWIN 服务器。 可以在上找到它[NuGet 库](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)，可以使用以下命令中使用 Visual Studio 包管理器对话框或包管理器控制台安装：

[!code-console[Main](an-overview-of-project-katana/samples/sample2.cmd)]

安装`Microsoft.Owin.Host.SystemWeb`包将安装几个其他包作为依赖项。 这些依赖项之一是`Microsoft.Owin`，提供了几个帮助程序类型和用于开发 OWIN 应用程序的方法的库。 我们可以使用这些类型可以快速编写以下"你好 world"服务器。

[!code-csharp[Main](an-overview-of-project-katana/samples/sample3.cs)]

现在可以使用 Visual Studio 运行此非常简单的 Web 服务器**F5**命令，并包含用于调试的完全支持。

## <a name="switching-hosts"></a>切换主机

默认情况下，前面的"你好 world"示例运行在 ASP.NET 请求管道中，在 IIS 的上下文中使用 System.Web。 这可以独自添加了巨大的价值因为它使我们能够受益于大的灵活性和可组合性的 OWIN 管道的管理功能和 IIS 的整体成熟度。 但是，可能有不需要由 IIS 提供的好处和愿望是更小、 更轻量的宿主。 所需，然后，运行 IIS 和 System.Web 之外我们简单的 Web 服务器？

为了说明的可移植性目标，将从命令行承载的 Web 服务器主机需要只需将新的服务器和主机依赖项添加到项目的输出文件夹，然后启动主机。 在此示例中，我们将托管我们的 Web 服务器中名为的 Katana 主机`OwinHost.exe`，将使用基于 Katana HttpListener 的服务器。 同样的其他 Katana 组件，这些将获取从 NuGet 使用以下命令：

[!code-console[Main](an-overview-of-project-katana/samples/sample4.cmd)]

我们可以从命令行，然后导航到项目根文件夹并只需运行`OwinHost.exe`（这在其各自的 NuGet 包的工具文件夹中安装的）。 默认情况下，`OwinHost.exe`配置为查找基于 HttpListener 的服务器，因此不需要任何其他配置。 在 Web 浏览器中导航`http://localhost:5000/`显示通过控制台现在正在运行的应用程序。

![](an-overview-of-project-katana/_static/image2.png)

## <a name="katana-architecture"></a>Katana 体系结构

 Katana 组件体系结构将应用程序分成四个逻辑层，如下所示：*主机、 服务器、 中间件*并*应用程序*。 组件体系结构被分解，这些层的实现可以轻松地替换，在许多情况下，而无需重新编译的应用程序的方式。   

![](an-overview-of-project-katana/_static/image3.png)

## <a name="host"></a>Host

 主机负责：

- 管理基础的过程。
- 将处理安排在服务器的选择和哪些请求通过 OWIN 管道的构造的工作流。

  目前，有 3 个主要的宿主选项基于 Katana 的应用程序：  
  
**Iis/ASP.NET**： 使用标准的 HttpModule 和 HttpHandler 类型，OWIN 管道可以在 IIS 上运行的 ASP.NET 请求流的一部分。 通过 Microsoft.AspNet.Host.SystemWeb NuGet 包安装到 Web 应用程序项目已启用 ASP.NET 托管支持。 此外，因为 IIS 充当主机和服务器，OWIN 服务器/主机区别交织在一起在此 NuGet 包中，这意味着如果使用的 SystemWeb 主机，开发人员不能将备用服务器实现替换。  
  
**自定义主机**: Katana 组件套件，开发人员可以在自己自定义过程中，托管应用程序无论是控制台应用程序、 Windows 服务，等等。此功能类似于 Web API 提供的自托管功能。 下面的示例显示了 Web API 代码的自定义主机：  

[!code-csharp[Main](an-overview-of-project-katana/samples/sample5.cs)]

Katana 应用程序的自托管安装程序是类似：

[!code-csharp[Main](an-overview-of-project-katana/samples/sample6.cs)]

Web API 和 Katana 自承载示例之间的一个显著区别是缺少 Katana 自承载示例 Web API 配置代码。 为了使可移植性和可组合性，Katana 将在服务器启动与配置请求处理管道的代码的代码分隔开来。 然后，配置 Web API 的代码被包含在启动时，此外还作为 WebApplication.Start 中的类型参数指定的类。

[!code-csharp[Main](an-overview-of-project-katana/samples/sample7.cs)]

将在本文后面的更详细地讨论 startup 类。 但是，代码需要启动的 Katana 自托管过程看起来极其类似于可能会在自托管 ASP.NET Web API 的应用程序中立即使用你的代码。

**OwinHost.exe**： 尽管一些客户想要编写一个自定义进程用于运行应用程序的 Katana Web，许多希望只需启动预建的可执行文件，可以启动服务器并运行其应用程序。 对于此方案中，Katana 组件套件包括`OwinHost.exe`。 从运行时在项目的根目录中，此可执行文件将启动的服务器 （它使用 HttpListener 服务器默认情况下），并使用约定来查找并运行用户的 startup 类。 对于更精细的控制，可执行文件提供了许多其他命令行参数。

![](an-overview-of-project-katana/_static/image4.png)

## <a name="server"></a>服务器

 而主机负责启动和维护的过程在其中应用程序运行，服务器的责任来打开网络套接字，侦听请求，并将其发送通过 OWIN 组件的管道由指定用户 （如你可能具有已注意到，此管道指定应用程序开发人员的 Startup 类中）。 目前，Katana 项目包括两个服务器实现： 

- **Microsoft.Owin.Host.SystemWeb**： 正如前面提到，IIS 与 ASP.NET 管道用作主机和服务器。 因此，当选择此宿主选项，IIS 同时管理主机级事宜，如进程激活并侦听的 HTTP 请求。 对于 ASP.NET Web 应用程序，它然后将请求发送到 ASP.NET 管道。 Katana SystemWeb 主机注册以截获请求流通过 HTTP 管道并将其发送通过用户指定的 OWIN 管道的 ASP.NET HttpModule 和 HttpHandler。
- **Microsoft.Owin.Host.HttpListener**： 此 Katana 服务器正如其名称，使用.NET Framework 的 HttpListener 类来打开套接字并将请求发送到开发人员指定 OWIN 管道。 这是当前的 Katana 自托管 API 和 OwinHost.exe 的默认服务器选择。

## <a name="middlewareframework"></a>中间件/框架

 如前文所述，当服务器接受来自客户端的请求时它负责通过 OWIN 组件，开发人员的启动代码由指定的管道。 这些管道组件被称为中间件。  
 在非常基本的级别，OWIN 中间件组件只是需要实现的 OWIN 应用程序委托，这样就可调用。

[!code-console[Main](an-overview-of-project-katana/samples/sample8.cmd)]

但是，为了简化开发和中间件组件的组合，Katana 对于中间件组件支持少量的约定和帮助程序类型。 其中最常见的是`OwinMiddleware`类。 使用此类生成的自定义中间件组件如下所示： 

[!code-csharp[Main](an-overview-of-project-katana/samples/sample9.cs)]

 此类派生`OwinMiddleware`，实现一个构造函数接受管道中的下一个中间件的实例作为其参数之一，然后将其传递到基构造函数。 使用用于配置中间件的其他参数后的下一个中间件参数也声明为构造函数参数。   
  
在运行时，中间件将执行通过重写`Invoke`方法。 此方法采用单个参数的类型`OwinContext`。 此上下文对象提供的`Microsoft.Owin`NuGet 包前面所述，并提供对请求、 响应和环境字典，以及少量其他帮助器类型的强类型化访问。   
  
中间件类可以轻松地添加到 OWIN 管道中应用程序启动代码，如下所示：   

[!code-csharp[Main](an-overview-of-project-katana/samples/sample10.cs)]

由于 Katana 基础结构只需构建了管道的 OWIN 中间件组件，并且组件只是需要支持要加入到管道中的应用程序委托，中间件组件的复杂程度从简单为整个框架，如 ASP.NET，Web API 记录器或[SignalR](../../../signalr/index.md)。 例如，将 ASP.NET Web API 添加到以前的 OWIN 管道需要添加以下启动代码：

[!code-csharp[Main](an-overview-of-project-katana/samples/sample11.cs)]

Katana 基础结构将生成基于添加到中的配置方法的 IAppBuilder 对象的顺序的中间件组件的管道。 然后，在本例中为 LoggerMiddleware 可以处理流通过管道，而不考虑最终如何处理这些请求的所有请求。 这使其中一个中间件组件 （例如身份验证组件） 可以处理请求的管道，包括多个组件和框架 （例如 ASP.NET Web API、 SignalR 和静态文件服务器） 的强大方案。
 
## <a name="applications"></a>应用程序

如前面的示例所示，OWIN 和 Katana 项目应不被认为是作为新的应用程序编程模型中，而是而不是作为抽象来分离应用程序的编程模型和从服务器和托管基础结构的框架。 例如，在生成 Web API 应用程序时，开发人员框架将继续使用 ASP.NET Web API 框架，而不考虑在使用 Katana 项目中的组件的 OWIN 管道中运行应用程序。 OWIN 相关的代码将对应用程序开发人员可见的一个位置将为应用程序启动代码，其中开发人员撰写 OWIN 管道。 在启动代码中，开发人员将注册一的系列 UseXx 语句，通常是一个用于每个中间件组件，将处理传入的请求。 这种体验将具有与当前的 System.Web 世界中注册的 HTTP 模块相同的效果。 通常情况下，更大框架中间件，如 ASP.NET Web API 或[SignalR](../../../signalr/index.md)将在管道末尾注册。 横切中间件组件，例如，用于身份验证或缓存，通常会管道的开始注册，以便它们将处理所有的框架和更高版本在管道中注册的组件的请求。 这种分离的中间件组件从每个其他和底层基础结构组件使组件可以确保整个系统保持不变的同时在不同的速度发展。

## <a name="components--nuget-packages"></a>组件-NuGet 包

许多最新的库和框架，如一组 NuGet 包形式交付 Katana 项目组件。 有关即将发布的版本 2.0 中，Katana 包依赖项关系图如下所示。 （单击图像可查看大图中）。

[![](an-overview-of-project-katana/_static/image6.png)](an-overview-of-project-katana/_static/image5.png)

Katana 项目中的几乎每个包取决于，直接或间接 Owin 包。 您可能还记得，这是包含 IAppBuilder 接口，它提供了 OWIN 规范的第 4 节中所述的应用程序启动顺序的具体实现的包。 此外，许多包依赖于 Microsoft.Owin，用于处理 HTTP 请求和响应提供一组帮助程序类型。 包的其余部分可以分类为托管基础结构包 （服务器或主机） 或中间件。 包和依赖项外部的 Katana 项目显示为橙色。

Katana 2.0 的托管基础结构包括 SystemWeb 和基于 HttpListener 的服务器，用于运行 OWIN 应用程序使用 OwinHost.exe，OwinHost 包和 Microsoft.Owin.Hosting 打包成自托管 OWIN 应用程序中的自定义主机 （例如控制台应用程序、 Windows 服务等）

对于 Katana 2.0，中间件组件主要侧重于提供的身份验证的不同方法。 提供用于诊断的一个其他中间件组件，这样对开始和错误页的支持。 OWIN 发展成实际承载抽象，如将还在数量增长中间件组件，这两个那些由 Microsoft 和第三方开发的生态系统。

## <a name="conclusion"></a>结束语

 从其开始 Katana 项目的目标不是创建并从而强制开发人员若要了解另一种 Web 框架。 相反，目标已创建一个抽象层，若要为.NET Web 应用程序开发人员提供比以前曾出现可能的更多选择。 分解成一组可更换的元件的典型 Web 应用程序堆栈的逻辑层，通过 Katana 项目能够在整个堆栈以提高在任何速率适合这些组件的组件。 通过构建简单的 OWIN 抽象周围的所有组件，Katana 支持框架和基于这些构建的应用程序能够在各种不同的服务器和主机之间移植。 通过开发人员置于堆栈的控件，Katana 可以确保开发人员进行有关如何轻量的最终选择，或者她 Web 堆栈是如何功能丰富。  
  

## <a name="for-more-information-about-katana"></a>有关 Katana 的详细信息

- GitHub 上的 Katana 项目： [ https://github.com/aspnet/AspNetKatana/ ](https://github.com/aspnet/AspNetKatana/)。
- 视频： [Katana 项目-ASP.NET 的 OWIN](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET)，Howard Dierking 通过。

## <a name="acknowledgements"></a>致谢

- [Rick Anderson](https://blogs.msdn.com/b/rickandy/): (twitter [ @RickAndMSFT ](http://twitter.com/RickAndMSFT) ) Rick 是 Microsoft 将重点放在 Azure 和 MVC 的资深编程作家。
- [Scott Hanselman](http://www.hanselman.com/blog/): (twitter [ @shanselman ](https://twitter.com/shanselman) )
- [Jon Galloway](https://weblogs.asp.net/jgalloway/default.aspx): (twitter [ @jongalloway ](https://twitter.com/jongalloway) )
