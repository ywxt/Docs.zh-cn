---
uid: mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
title: 在 ASP.NET MVC 4 中使用异步方法 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建异步 ASP.NET MVC Web 应用程序使用 Visual Studio Express 2012 for Web，这是免费 ve 的基础知识...
ms.author: riande
ms.date: 06/06/2012
ms.assetid: a56572ba-81c3-47af-826d-941e9c4775ec
msc.legacyurl: /mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 757b15c34f6fa0078d0bca0dfb38d553bb73809d
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577699"
---
<a name="using-asynchronous-methods-in-aspnet-mvc-4"></a>在 ASP.NET MVC 4 中使用异步方法
====================
通过[Rick Anderson]((https://twitter.com/RickAndMSFT))

> 本教程将教您构建异步 ASP.NET MVC Web 应用程序中使用的基础知识[Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11)，这是 Microsoft Visual Studio 的免费版本。 此外可以使用[Visual Studio 2012](https://www.microsoft.com/visualstudio/11)。
> 
> 本教程中在 github 上提供的完整示例  [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/)


ASP.NET MVC 4[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller(VS.108).aspx)结合使用的类[.NET 4.5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx)使你能够编写的异步操作方法的返回类型的对象[任务&lt;ActionResult&gt;](https://msdn.microsoft.com/library/dd321424(VS.110).aspx). .NET Framework 4 引入了异步编程概念，称为[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)和 ASP.NET MVC 4 支持[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)。 任务由**任务**类型和中的相关的类型[System.Threading.Tasks](https://msdn.microsoft.com/library/system.threading.tasks.aspx)命名空间。 与此异步支持生成.NET Framework 4.5 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)和[异步](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)使用的关键字[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)比以前少得多复杂的对象异步方法。 [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)关键字是速记语法用于指示在某些其他代码段以异步方式等待一段代码。 [异步](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字都表示一个提示，可用于将方法标记为基于任务的异步方法。 组合**await**，**异步**，并**任务**对象可大大简化了.NET 4.5 中编写异步代码。 调用异步方法的新模型*基于任务的异步模式*(**点击**)。 本教程假定你已具备一定的使用异步编程[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)并[异步](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字并[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)命名空间。

有关使用的详细信息[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)并[异步](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字和[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)命名空间，请参阅以下参考资料。

- [在.NET 中的白皮书： 实现异步](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Async/Await FAQ](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio 异步编程](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>  线程池处理请求的方式

在 web 服务器上，.NET Framework 维护一个用于服务 ASP.NET 请求的线程池。 当请求到达时，将调度池中的线程以处理该请求。 如果以同步方式处理该请求，处理请求的线程是繁忙时请求正在处理，，线程不能另一个请求服务。   
  
这可能不是问题，因为线程池可以设置得足够大，以容纳多个忙碌线程数。 但是，在线程池中的线程数会受到限制 （默认为.NET 4.5 最大值为 5,000）。 在大型应用程序使用高并发的长时间运行的请求，所有可用线程可能正忙。 这种情况称为线程资源不足。 当达到这种情况时，web 服务器请求进行排队。 如果在请求队列已满，web 服务器会拒绝请求并处于 HTTP 503 状态 （服务器太忙）。 CLR 线程池将限制对新线程注入。 如果并发性突发 （也就是说，您的网站突然可以获取大量的请求） 和所有可用请求线程处于忙碌状态后端调用由于具有高延迟、 有限的线程注入速率可以使应用程序响应效果非常差。 此外，添加到线程池中每个新线程开销 （例如 1 MB 的堆栈内存)。 使用到服务高延迟调用同步方法的线程池增长到.NET 4.5 默认最多 5 个 web 应用程序，000 线程将占用大约为 5 GB 较多内存的应用程序可以比服务相同请求使用异步方法，并仅有 50 个线程。 当执行异步工作时，你不始终使用线程。 例如，当你进行的异步 web 服务请求，ASP.NET 将不使用任何线程之间**异步**方法调用和**await**。 使用为请求提供服务的线程池具有高延迟可能会导致内存占用量大和的服务器硬件的利用率不佳。

## <a name="processing-asynchronous-requests"></a>处理异步请求

在 web 应用中，会看到大量的并发请求数在启动时或具有突发负载 （其中会增加并发情况突然），使 web 服务调用异步会增加应用的响应能力。 异步请求采用相同量的时间来处理与同步请求。 如果某个请求生成 web 服务调用，需要两秒钟来完成，请求需要两个秒是否执行同步或异步。 但是在异步调用，线程不是从响应其他请求等待第一个请求完成时阻塞。 因此，异步请求可以防止出现请求排队和线程池增长时有许多并发请求调用长时间运行的操作。

## <a id="ChoosingSyncVasync"></a>  选择同步或异步操作方法

本部分列出了有关何时使用同步或异步操作方法的指导原则。 这些是只是一些准则;检查每个应用程序分别以确定是否异步方法能帮助提高性能。

一般情况下，使用同步方法满足以下条件：

- 操作很简单或短时间运行。
- 简单性比效率更重要。
- 操作是主要是 CPU 操作而不是涉及大量的磁盘或网络开销的操作。 对 CPU 密集型操作使用异步操作方法未提供任何好处，并导致更多的开销。

  一般情况下，使用异步方法在以下条件：

- 您要调用服务，可通过异步方法，并使用.NET 4.5 或更高版本。
- 操作是网络绑定的或绑定 I/O 而不是受 CPU 限制。
- 并行度不比代码的简单性更重要。
- 你想要提供一种机制，允许用户取消长时间运行的请求。
- 当切换线程的好处远远超过上下文切换的成本。 一般情况下，您应使方法异步不执行任何工作时对 ASP.NET 请求线程等待同步方法。 可以执行异步调用，ASP.NET 请求线程不被停止等待完成的 web 服务请求时任何工作。
- 测试显示阻塞操作是在站点的性能瓶颈和 IIS 可以通过使用异步方法对这些阻塞调用服务更多的请求。

  可下载的示例演示如何有效地使用异步操作方法。 提供的示例旨在提供在 ASP.NET MVC 4 中使用.NET 4.5 的异步编程的简单演示。 该示例不是要在 ASP.NET MVC 中异步编程的参考体系结构。 在示例程序调用[ASP.NET Web API](../../../web-api/index.md)方法，用于反过来调用[Task.Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx)以模拟长时间运行 web 服务调用。 大多数生产应用程序不会显示这种明显的优势，到使用异步操作方法。   
  
几个应用程序需要是异步的所有操作方法。 通常情况下，将几个同步操作方法转换为异步方法提供了显著增加所需的工作量。

## <a id="SampleApp"></a>  示例应用程序

您可以下载的示例应用程序[ https://github.com/RickAndMSFT/Async-ASP.NET/ ](https://github.com/RickAndMSFT/Async-ASP.NET)上[GitHub](https://github.com/)站点。 存储库包含三个项目：

- *Mvc4Async*: ASP.NET MVC 4 项目包含本教程中使用的代码。 Web API 调用**WebAPIpgw**服务。
- *WebAPIpgw*： 用于实现 ASP.NET MVC 4 Web API 项目`Products, Gizmos and Widgets`控制器。 它提供的数据*WebAppAsync*项目并*Mvc4Async*项目。
- *WebAppAsync*： 另一个教程中使用的 ASP.NET Web 窗体项目。

## <a id="GizmosSynch"></a>  Gizmos，请同步操作方法

 下面的代码演示`Gizmos`同步操作方法，用于显示 gizmos，请的列表。 （对于本文，零件是虚构的机械设备。） 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample1.cs)]

下面的代码演示`GetGizmos`零件服务的方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample2.cs)]

`GizmoService GetGizmos`方法将 URI 传递到 ASP.NET Web API HTTP 服务返回的 gizmos，请数据列表。 *WebAPIpgw*项目中包含的 Web API 实现`gizmos, widget`和`product`控制器。  
下图显示了示例项目中的 gizmos，请视图。

![Gizmos，请](using-asynchronous-methods-in-aspnet-mvc-4/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>  创建异步 gizmos，请操作方法

该示例使用新[异步](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)并[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)关键字 （在.NET 4.5 和 Visual Studio 2012 中提供） 让编译器负责维护复杂的转换的必要条件异步编程。 编译器可用于编写代码使用 C# 的同步的控制流构造，编译器会自动应用需使用回调，以避免阻塞线程的转换。

下面的代码演示`Gizmos`同步方法和`GizmosAsync`异步方法。 如果你的浏览器支持[HTML 5`<mark>`元素](http://www.w3.org/wiki/HTML/Elements/mark)，您会看到在更改`GizmosAsync`黄色突出显示框中。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample3.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample4.cs?highlight=1,3,5)]

 应用了以下更改，以允许`GizmosAsync`为异步。

- 方法将标有[异步](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字，它会告知编译器将生成的正文部分的回调并自动创建`Task<ActionResult>`返回。
- &quot;异步&quot;追加到方法名称。 追加"Async"不是必需的但编写异步方法时，是的约定。
- 返回类型已从`ActionResult`到`Task<ActionResult>`。 返回类型`Task<ActionResult>`表示正在进行的工作，并提供方法的调用方与用来等待异步操作完成的句柄。 在这种情况下，调用方是 web 服务。 `Task<ActionResult>` 表示正在进行处理的结果 `ActionResult.`
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)关键字已应用于 web 服务调用。
- 调用了异步 web 服务 API (`GetGizmosAsync`)。

内部`GetGizmosAsync`方法正文另一种异步方法，`GetGizmosAsync`调用。 `GetGizmosAsync` 立即返回`Task<List<Gizmo>>`，最终会完成时有可用的数据。 因为您不想要将零件数据之前执行任何其他操作，该代码等待任务 (使用**await**关键字)。 可以使用**await**关键字仅在方法中使用批注**异步**关键字。

**Await**关键字不会阻止线程，直到任务完成。 它以在任务中，回调注册方法的剩余部分，并立即返回。 等待的任务最终完成时，它将调用该回调，并因此恢复中断的位置的方法权限执行。 有关使用的详细信息[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)并[异步](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字并[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)命名空间，请参阅[异步引用](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async)。

下面的代码演示`GetGizmos`和`GetGizmosAsync`方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample5.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample6.cs?highlight=1,4-8)]

 异步更改是对所做的内容相似**GizmosAsync**上面。 

- 方法签名使用批注[异步](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字，返回类型已更改为`Task<List<Gizmo>>`，和*异步*追加到方法名称。
- 异步[HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)而不是使用类[WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx)类。
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)关键字已应用于[HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)异步方法。

下图显示了异步零件视图。

![async](using-asynchronous-methods-in-aspnet-mvc-4/_static/image2.png)

浏览器表示法的 gizmos，请数据是相同的同步调用创建的视图。 唯一的区别是异步版本可能是在重负载下的性能更高。

## <a id="Parallel"></a>  并行执行多个操作

异步操作方法后操作必须执行几个独立的操作，将通过同步方法的一个明显的优势。 在示例中提供，同步方法`PWG`（适用于产品、 小组件和 gizmos，请） 会显示三个 web 服务调用，以获取的产品、 小组件和 gizmos，请列表的结果。 [ASP.NET Web API](../../../web-api/index.md)项目提供了这些服务使用[Task.Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx)模拟延迟或慢速网络调用。 当延迟设置为 500 毫秒，异步`PWGasync`方法采用稍有超过 500 毫秒完成时同步`PWG`版本高于 1500 毫秒。 同步`PWG`方法显示在下面的代码。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample7.cs)]

异步`PWGasync`方法显示在下面的代码。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample8.cs?highlight=1,3,12)]

下图显示了返回的视图**PWGasync**方法。

![pwgAsync](using-asynchronous-methods-in-aspnet-mvc-4/_static/image3.png)

## <a id="CancelToken"></a>  使用取消标记

异步操作方法返回`Task<ActionResult>`是否可取消，即它们采用[CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx)参数在与提供[AsyncTimeout](https://msdn.microsoft.com/library/system.web.mvc.asynctimeoutattribute(VS.108).aspx)属性。 下面的代码演示`GizmosCancelAsync`具有的 150 毫秒的超时值的方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample9.cs?highlight=1-3,5,10)]

下面的代码演示 GetGizmosAsync 重载，它采用[CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx)参数。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample10.cs)]

中提供的示例应用程序，选择*取消令牌演示*链接调用`GizmosCancelAsync`方法，并演示异步调用的取消。

## <a id="ServerConfig"></a>  针对高并发/高延迟 Web 服务调用的服务器配置

若要实现异步 web 应用程序的好处，可能需要对默认服务器配置进行一些更改。 请记住以下配置时的考虑和压力测试异步 web 应用程序中。

- Windows 7、 Windows Vista 和所有 Windows 客户端操作系统具有最多 10 个并发请求。 你将需要 Windows 服务器操作系统，若要查看在高负载下的异步方法的优势。
- 从提升的命令提示符向 IIS 注册.NET 4.5:  
  %windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet\_regiis-i  
  请参阅[ASP.NET IIS 注册工具 (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h.aspx)
- 你可能需要增加[HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture)队列限制从 1,000 到 5,000 个的默认值。 如果设置得太低，可能会看到[HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture)拒绝请求的 HTTP 503 状态。 若要更改 HTTP.sys 队列限制：

    - 打开 IIS 管理器并导航到应用程序池窗格中。
    - 在目标应用程序池上右键单击并选择**高级设置**。  
        ![advanced](using-asynchronous-methods-in-aspnet-mvc-4/_static/image4.png)
    - 在中**高级设置**对话框中，更改*队列长度*从 1,000 到 5,000。  
        ![队列长度](using-asynchronous-methods-in-aspnet-mvc-4/_static/image5.png)  
  
  请注意，在更高版本，映像的.NET framework 被列为 v4.0，即使应用程序池使用的.NET 4.5 也是如此。 若要了解这种差异，请参阅以下：

    - [.NET 版本控制和多重目标 —.NET 4.5 是.NET 4.0 的就地升级](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
    - [如何设置要使用 ASP.NET 3.5 而不是 2.0 的 IIS 应用程序或应用程序池](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
    - [.NET Framework 版本和依赖关系](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)
- 如果你的应用程序使用 web 服务或 System.NET 使用后端通过 HTTP 进行通信，可能需要增加[connectionManagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx)元素。 对于 ASP.NET 应用程序，这被受 12 倍的 Cpu 数的自动配置功能。 这意味着，在四处理器，您可以最多 12 \* 4 = 48 到 IP 终结点的并发连接。 因为这与[autoConfig](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx)，增加的最简单办法`maxconnection`应用程序是 ASP.NET 中设置[System.Net.ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx)以编程方式在从`Application_Start`中的方法*global.asax*文件。 请参阅下载有关示例的示例。
- 在.NET 4.5 中，默认值为 5000 [maxconcurrentrequestspercpu 配置](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)可以正常工作。
