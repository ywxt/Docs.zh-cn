---
uid: web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
title: ASP.NET Web 窗体连接复原和命令截获 |Microsoft Docs
author: Erikre
description: 本教程介绍如何修改示例应用程序以支持连接复原和命令截获。
ms.author: riande
ms.date: 03/31/2014
ms.assetid: 6d497001-fa80-4765-b4cc-181fe90b894e
msc.legacyurl: /web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
msc.type: authoredcontent
ms.openlocfilehash: 039923a91d957765fa8b2c0cfe11abc8790c1e88
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832048"
---
<a name="aspnet-web-forms-connection-resiliency-and-command-interception"></a>ASP.NET Web 窗体连接复原和命令截获
====================
通过[Erik Reitan](https://github.com/Erikre)

在本教程中，您将修改 Wingtip Toys 示例应用程序以支持连接复原和命令截获。 通过启用连接复原，Wingtip Toys 示例应用程序将自动重试数据调用发生暂时性错误典型的云环境时。 此外，通过实施命令拦截，Wingtip Toys 示例应用程序将捕获所有发送到数据库才能登录或更改它们的 SQL 查询。

> [!NOTE] 
> 
> 此 Web 窗体教程基于 Tom Dykstra 以下 MVC 教程：  
> [连接复原和命令截获与 ASP.NET MVC 应用程序中的实体框架](../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)


## <a name="what-youll-learn"></a>你将学习：

- 如何提供连接复原能力。
- 如何实现命令拦截。

## <a name="prerequisites"></a>系统必备

在开始之前，请确保您已在计算机上安装以下软件：

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。 会自动安装.NET Framework。
- Wingtip Toys 示例项目中，以便可以实现在本教程中 Wingtip Toys 项目中所述的功能。 以下链接提供了下载详细信息：

    - [Getting Started with ASP.NET 4.5.1 Web 窗体的 Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) (C#)
- 本教程之前，请考虑查看相关的教程系列[Getting Started with ASP.NET 4.5 Web 窗体和 Visual Studio 2013](../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 此教程系列将帮助你熟悉**WingtipToys**项目和代码。

## <a name="connection-resiliency"></a>连接复原

考虑到 Windows Azure 应用程序部署时，要考虑的一个选项部署到的数据库**Windows** **Azure SQL 数据库**，云数据库服务。 连接到比你的 web 服务器和数据库服务器直接连接时一起位于同一数据中心的云数据库服务时，暂时性连接错误是通常更频繁。 即使在同一数据中心托管的云 web 服务器和云数据库服务，有更多的网络连接，它们可以出现问题，例如负载均衡器之间。

此外云服务是通常由其他用户共享，这意味着其响应能力可能受到它们。 并且您对数据库访问权限可能会受到限制。 限制意味着数据库服务会引发异常，当您尝试超出允许的更频繁地访问您*服务级别协议*(SLA)。

许多或大部分发生时正在访问云服务的连接问题是暂时的也就是说，他们自身解决在短时间的时间。 因此在重试数据库操作并获得一种类型的通常是暂时的错误，稍等片刻，该操作可能会成功后无法重试该操作。 如果通过自动尝试再次，处理暂时性错误，可以为用户提供更好的体验使其中的大多数客户不可见。 连接复原功能在 Entity Framework 6 中的自动执行的重试过程失败的 SQL 查询。

针对特定数据库服务，必须适当地配置连接复原功能：

1. 它必须知道哪些异常可能是暂时的。 你想要重试错误引起暂时失去网络连接中不由程序 bug，例如引起的错误。
2. 它必须等待适当的重试的失败的操作之间的时间。 你可以等待更长时间进行批处理的重试之间不是可以在线网页用户正在等待响应。
3. 它具有重试的次数之前放弃适当数量。 您可能想要重试更多次，就像在一个在线应用程序中的批处理中。

你可以配置这些设置手动为实体框架提供程序支持的任何数据库环境。

您只需启用连接复原的就是您的程序集派生中创建一个类`DbConfiguration`类，并在该类中设置 SQL 数据库执行策略，它在实体框架为另一种说法重试策略。

### <a name="implementing-connection-resiliency"></a>实现连接复原

1. 下载并打开[WingtipToys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409)示例在 Visual Studio 中的 Web 窗体应用程序。
2. 在中*逻辑*的文件夹**WingtipToys**应用程序中，添加名为的类文件*WingtipToysConfiguration.cs*。
3. 用下面的代码替换现有代码：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample1.cs)]

实体框架将自动运行的代码在派生类中找到`DbConfiguration`。 可以使用`DbConfiguration`类，以执行在中否则所执行的操作的代码中的配置任务*Web.config*文件。 有关详细信息，请参阅[EntityFramework 基于代码的配置](https://msdn.microsoft.com/data/jj680699)。

1. 在中*逻辑*文件夹中，打开*AddProducts.cs*文件。
2. 添加`using`语句`System.Data.Entity.Infrastructure`以黄色突出显示所示：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample2.cs?highlight=6)]
3. 添加`catch`阻止`AddProduct`方法，以便`RetryLimitExceededException`记录以黄色突出显示为：   

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample3.cs?highlight=14-15,17-22)]

通过添加`RetryLimitExceededException`异常，你可以提供更好地日志记录或到他们可以选择要再次尝试该过程的用户显示一条错误消息。 通过捕获`RetryLimitExceededException`异常，可能是暂时性的唯一错误将已尝试并失败几次。 返回的实际异常将包装在`RetryLimitExceededException`异常。 此外，您还添加了常规 catch 块。 有关详细信息`RetryLimitExceededException`异常，请参阅[实体框架连接复原 / 重试逻辑](https://msdn.microsoft.com/data/dn456835)。

## <a name="command-interception"></a>命令截获

现在，你已启用了重试策略，如何你测试以验证它是否按预期工作？ 不可以十分轻松地强制暂时性错误发生，尤其是当您在本地，运行和会特别难以将实际的暂时性错误集成到自动化的单元测试。 若要测试连接复原功能，您需要一种方法截获 Entity Framework 将发送到 SQL Server 的查询和 SQL Server 响应替换通常是暂时异常类型。

此外可以使用查询拦截，为了实现云应用程序的最佳做法： 日志的延迟和成功或失败的所有调用对外部服务 （如数据库服务）。

在本教程的本部分中，您将使用实体框架[*拦截功能*](https://msdn.microsoft.com/data/dn469464)进行日志记录和用于模拟暂时性错误。

### <a name="create-a-logging-interface-and-class"></a>创建日志记录接口和类

日志记录的最佳做法是使用可完成的[ `interface` ](https://msdn.microsoft.com/library/ms173156.aspx)而不是硬编码调用`System.Diagnostics.Trace`或日志记录类。 这样，更轻松地更改更高版本的日志记录机制，如果您需要执行此操作。 因此在此部分中，您将创建日志记录接口和类来实现它。

根据上述过程，您必须下载并打开**WingtipToys**示例在 Visual Studio 中的应用程序。

1. 创建一个文件夹中的**WingtipToys**项目，并命名*日志记录*。
2. 在中*日志记录*文件夹中，创建名为的类文件*ILogger.cs*和默认代码替换为以下代码：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample4.cs)]

   该接口提供三种跟踪级别，以指示日志的相对重要性，另一个设计为提供对等数据库查询的外部服务调用的延迟信息。 日志记录方法具有重载，可传入异常。 这是这样实现的接口，而不是依赖于整个应用程序每个日志记录方法调用中完成这些操作后的类可靠地记录异常信息包括堆栈跟踪和内部异常信息。  
  
   `TraceApi`方法使您能够跟踪 SQL 数据库等外部服务每次调用的延迟。
3. 在中*日志记录*文件夹中，创建名为的类文件*Logger.cs*和默认代码替换为以下代码：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample5.cs)]

该实现使用`System.Diagnostics`以执行跟踪。 这是.NET 可以轻松生成和使用跟踪信息的内置功能。 有许多&quot;侦听器&quot;可用于`System.Diagnostics`将日志写入文件，例如，或将它们写入 Windows Azure 中的 blob 存储的跟踪。 了解的一些选项，以及指向其他资源的详细信息，在[网站进行故障排除 Windows Azure 在 Visual Studio 中](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)。 对于本教程，您将只能查看 Visual Studio 中的日志**输出**窗口。

在生产应用程序可能需要考虑使用跟踪框架不`System.Diagnostics`，和`ILogger`interface 可以相对轻松，若要切换到不同的跟踪机制，如果你决定要执行此操作。

### <a name="create-interceptor-classes"></a>创建侦听器类

接下来，将创建每次它会将查询发送到数据库，另一个来模拟暂时性错误进行日志记录时，实体框架会调用到的类。 这些侦听器类必须派生自`DbCommandInterceptor`类。 在其中，您编写查询时要在执行时自动调用的方法重写。 在这些方法可以检查或记录查询正被发送到数据库，并可以更改查询发送到数据库之前，也可以返回某些内容到实体框架自己而无需甚至将查询传递到数据库。

1. 若要创建的侦听器类将记录每个 SQL 查询发送到数据库之前，创建名为的类文件*InterceptorLogging.cs*中*逻辑*文件夹并将替换为默认值的代码使用以下代码：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample6.cs)]

   对于成功的查询或命令，此代码将写入延迟信息的信息的日志。 有关例外情况，它创建错误日志。
2. 若要创建在输入时，将生成虚拟的暂时性错误的侦听器类&quot;引发&quot;中**名称**名为页面上的文本框*AdminPage.aspx*，创建一个类名为的文件*InterceptorTransientErrors.cs*中*逻辑*文件夹并将替换为默认值的代码使用以下代码：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample7.cs)]

    此代码仅重写`ReaderExecuting`的查询，可以返回多行数据调用的方法。 如果你想要检查连接复原对于其他类型的查询，还可以重写`NonQueryExecuting`和`ScalarExecuting`方法，作为日志记录侦听器执行。  
  
   更高版本，您将以"管理员"身份登录，并选择**管理员**顶部导航栏上的链接。 然后，在*AdminPage.aspx*页将添加名为产品&quot;引发&quot;。 该代码创建虚拟 SQL 数据库异常的错误号 20，确定是通常暂时性的类型。 其他当前被识别为暂时性的错误编号均为 64、 233、 10053、 10054、 10060、 10928、 10929、 40197、 40501 和 40613，但它们是将在新版本的 SQL 数据库中进行。 该产品将重命名为"TransientErrorExample"，可以按照中的代码*InterceptorTransientErrors.cs*文件。  
  
   该代码对实体框架，而不是运行查询并传递返回的结果返回的异常。 返回暂时性异常*四个*次，然后代码将恢复到正常过程将查询传递到数据库。

    记录所有内容，因为您可以查看实体框架会尝试执行查询四次之后才最后成功，并在应用程序中唯一的区别是，花费更长时间才能呈现的页面包含查询结果。  
  
   实体框架将重试次数是可配置;该代码指定四次，因为这是 SQL 数据库执行策略的默认值。 如果更改执行策略，则必须也更改的代码，指定生成暂时性错误的次数。 您也可以更改代码以生成更多的异常，因此，实体框架将引发`RetryLimitExceededException`异常。
3. 在中*Global.asax*，添加以下 using 语句：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample8.cs)]
4. 然后，将添加到突出显示的行`Application_Start`方法：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample9.cs?highlight=17-20)]

以下几行代码是哪些因素会导致在 Entity Framework 将查询发送到数据库时要运行的侦听器代码。 请注意，因为创建单独的侦听器类进行模拟暂时性错误和日志记录，你可以单独启用和禁用它们。   
  
 您可以添加使用侦听器`DbInterception.Add`你的代码; 中的任意位置的方法其实不一定要在`Application_Start`方法。 另一个选项，如果您没有添加中的侦听器`Application_Start`方法，就是要更新或添加名为的类*WingtipToysConfiguration.cs*并将以上代码的构造函数的末尾添加`WingtipToysbConfiguration`类。

只要您将此代码中，请注意不要执行`DbInterception.Add`相同的侦听器的时间超过一次，或者你将获得其他侦听器实例。 例如，如果两次添加日志记录的侦听器，将看到两个日志对于每个 SQL 查询。

侦听器执行以注册顺序 (依据的顺序`DbInterception.Add`调用方法)。 顺序可能重要具体取决于你在侦听器中所执行的操作。 例如，侦听器可能会更改 SQL 命令可获取中`CommandText`属性。 如果它确实发生更改的 SQL 命令下, 一步侦听器将获取已更改的 SQL 命令，而不是原始的 SQL 命令。

您已编写的暂时性错误模拟代码可以通过在 UI 中输入一个不同的值导致暂时性错误的方式。 或者，可以编写以始终生成暂时性异常的序列，而检查特定的参数值的侦听器代码。 然后，仅当你想要生成暂时性错误时，可以添加侦听器。 如果这样做，但是，数据库初始化完成后不添加到侦听器。 换而言之，执行如查询一个实体集上的至少一个数据库操作，然后开始生成暂时性错误。 实体框架在数据库初始化期间执行多个查询和它们在事务中，因此在初始化期间的错误可能会导致上下文才能进入不一致的状态不会执行。

## <a name="test-logging-and-connection-resiliency"></a>测试日志记录和连接弹性

1. 在 Visual Studio 中，按**F5**在调试模式下，和登录名为"Admin"作为密码使用"Pa$ $word"中运行应用程序。
2. 选择**管理员**顶部导航栏中。
3. 输入一个新的产品名为"引发"与相应的说明、 价格和图像文件。
4. 按**添加产品**按钮。  
   您会注意到浏览器看起来时实体框架重试查询多次挂起数秒钟的时间。 首次重试发生速度非常快，然后在每个额外的重试之前等待会增加。 此过程的调用每次重试之前再等待*指数退避算法*。
5. 等待，直到页面已不再 atttempting 加载。
6. 停止项目，看看 Visual Studio**输出**窗口以查看跟踪输出。 您可以找到**输出**通过选择窗口**调试** - &gt; **Windows**  - &gt; **输出**。 您可能需要滚动浏览多个由记录器写入其他日志。  
  
   请注意，您可以看到实际的 SQL 查询发送到数据库。 您看到一些初始查询和命令的实体框架执行的操作以开始，请检查数据库版本和迁移历史记录表。   
    ![输出窗口](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image1.png)   
   请注意，不能重复此测试，除非停止应用程序并重新启动它。 如果你想要能够测试应用程序的单次运行中的连接复原多次，您可以编写代码来重置中的错误计数器`InterceptorTransientErrors`。
7. 若要查看不同之处执行策略 （重试策略） 发出，注释`SetExecutionStrategy`行中*WingtipToysConfiguration.cs*中的文件*逻辑*文件夹中，运行**管理员**同样，在调试模式下页上，添加名为产品&quot;引发&quot;试。  
  
   这一次调试器停止上第一个生成的异常后尝试执行第一次的查询，将立即。  
    ![调试-查看详细信息](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image2.png)
8. 取消注释`SetExecutionStrategy`行中*WingtipToysConfiguration.cs*文件。

## <a name="summary"></a>总结

在本教程中已了解如何修改 Web 窗体示例应用程序，以支持连接复原和命令截获。

## <a name="next-steps"></a>后续步骤

查看连接复原和命令截获在 ASP.NET Web 窗体后，查看 ASP.NET Web 窗体主题[ASP.NET 4.5 中的异步方法](../performance-and-caching/using-asynchronous-methods-in-aspnet-45.md)。 本主题将介绍生成使用 Visual Studio 的异步 ASP.NET Web 窗体应用程序的基础知识。
