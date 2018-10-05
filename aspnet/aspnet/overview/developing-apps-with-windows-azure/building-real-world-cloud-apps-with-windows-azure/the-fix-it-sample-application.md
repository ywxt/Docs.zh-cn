---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 附录： 修复它示例应用程序 （构建实际云应用与 Azure） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 435ee61a9c28ad0035457990cd3a889f5b240517
ms.sourcegitcommit: 7890dfb5a8f8c07d813f166d3ab0c263f893d0c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48795533"
---
<a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>附录： 修复它示例应用程序 （构建使用 Azure 的真实世界云应用程序）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)

[下载该项目的修补程序](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。

本附录的构建真实世界云应用与 Azure 的电子书包含以下各节提供有关 Fix It 示例应用程序，您可以下载的其他信息：

- [已知的问题](#knownissues)
- [最佳做法](#bestpractices)
- [如何从 Visual Studio 在本地计算机上运行该应用程序](#run-in-vs)
- [如何将基本应用程序部署到 Azure 应用服务 Web 应用，通过使用 Windows PowerShell 脚本](#deploybase)
- [Windows PowerShell 脚本故障排除](#troubleshooting)
- [如何使用队列处理到 Azure 应用服务 Web 应用和 Azure 云服务部署应用程序](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>已知问题

Fix It 应用最初是为了说明尽可能简单地的一些模式显示此电子书中开发的。 但是，由于电子书是有关构建实际的应用程序，我们受到 Fix It 代码评审和测试过程类似于我们对于发布的软件将执行操作。 我们发现许多问题，并且与任何实际的应用程序中，我们修复了其中一些，并且其中一些我们推迟到以后的版本。

以下列表包含应解决的问题，在生产应用程序，但其中一个原因或另一个我们决定不修复它示例应用程序的初始版本中的地址。

### <a name="security"></a>安全性

- 请确保不能将任务分配给不存在的所有者。
- 确保你仅可以查看和修改的创建或分配给你的任务。
- 针对登录页和身份验证 cookie 使用 HTTPS。
- 指定身份验证 cookie 的时间限制。

### <a name="input-validation"></a>输入的验证

一般情况下，像生产应用的详细信息输入验证比 Fix It 应用程序。 例如，图像大小 / image 允许应限制上传的文件大小。

### <a name="administrator-functionality"></a>管理员功能

管理员应能够在现有任务上更改所有权。 例如，一项任务的创建者可能会使公司，没有人留下颁发机构来维护任务，除非已启用的管理访问权限。

### <a name="queue-message-processing"></a>处理队列消息

修复其应用中处理的队列消息被可简单，以便将阐释最少量的代码使用以队列为中心的工作模式。 此简单的代码并不是足够的实际的生产应用程序。

- 该代码不保证将最多一次处理每个队列消息。 如果从队列中获取一条消息，则超时期限，在此期间的消息是看不到其他队列侦听器。 如果在超时到期之前删除该消息，消息将再次可见。 因此，如果辅助角色实例花费很长时间处理消息，它是相同的消息得到处理两次，从理论上讲可能导致数据库中的重复任务。 有关此问题的详细信息，请参阅[使用 Azure 存储队列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。
- 队列轮询逻辑可能是更具成本效益，批处理的消息检索。 每次调用[CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)，没有事务费用。 相反，您可以调用[CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (请注意复数形式的)，它将在单个事务中获取多个消息。 Azure 存储队列事务成本是非常低，因此对成本的影响不是大量在大多数情况下。
- 队列消息处理代码中的紧密循环会导致不有效地利用多核虚拟机的 CPU 关联。 更好的设计将使用任务并行度以并行方式运行多个异步任务。
- 处理队列消息具有仅基本异常处理。 例如，代码不会处理[有害消息](https://msdn.microsoft.com/library/ms789028.aspx)。 （当消息处理导致异常时，必须记录错误并删除该消息或辅助角色将尝试再次对其进行处理和则循环将无限期地继续。）

### <a name="sql-queries-are-unbounded"></a>SQL 查询是不受限制

当前修复该代码对索引页的查询可能返回的行数没有限制。 如果大量的任务输入到数据库时，收到的生成列表的大小可能会导致性能问题。 解决方案是实现分页。 有关示例，请参阅[排序、 筛选和分页与 ASP.NET MVC 应用程序中的实体框架](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)。

### <a name="view-models-recommended"></a>建议的视图模型

Fix It 应用使用 FixItTask 实体类在控制器和视图之间传递信息。 一种最佳做法是使用视图模型。 域模型 （例如，FixItTask 实体类） 被专为所需的数据暂留，尽管视图模型可供数据演示文稿。 有关详细信息，请参阅[12 ASP.NET MVC 最佳实践](http://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)。

### <a name="secure-image-blob-recommended"></a>建议的安全映像 blob

修复其应用商店上传图像为公共的这意味着找到 URL 的任何人可以访问图像。 而不是公用的方式保护映像。

### <a name="no-powershell-automation-scripts-for-queues"></a>队列没有 PowerShell 自动化脚本

Automation 示例 PowerShell 脚本是仅为修复它完全在 Azure 应用服务 Web 应用中运行的基础版本编写的。 我们尚未提供用于设置和部署到 web 应用和云服务环境所需的队列处理的脚本。

### <a name="special-handling-for-html-codes-in-user-input"></a>对用户输入中的 HTML 代码的特殊处理

ASP.NET 自动防止恶意用户可能会通过在用户输入的文本框中输入脚本跨站点脚本攻击尝试在其中的许多方面。 和 MVC`DisplayFor`用来显示任务的帮助器标题和说明会自动进行 HTML 编码的值发送到浏览器。 但在生产应用中，可能想要采取其他措施。 有关详细信息，请参阅[在 ASP.NET 请求验证](https://msdn.microsoft.com/library/hh882339.aspx)。

<a id="bestpractices"></a>
## <a name="best-practices"></a>最佳实践

以下是一些代码评审中发现和修复其应用程序的原始版本的测试已修复后的问题。 一些而引起原始代码编写者不是特定的最佳做法，了解一些只因为代码快速写入，并且不适用于发布的软件。 我们正在列出此处的问题，以防还有一些我们得出此评审和测试，可能有帮助的其他人也在开发 web 应用。

### <a name="dispose-the-database-repository"></a>释放数据库存储库

`FixItTaskRepository`类必须释放 Entity Framework`DbContext`实例。 我们是通过实现`IDisposable`在`FixItTaskRepository`类：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

请注意，将自动释放 AutoFac`FixItTaskRepository`实例，因此我们无需显式释放。

另一种方法是删除`DbContext`成员变量，从`FixItTaskRepository`，并改为创建一个本地`DbContext`变量在每个存储库方法中，内部`using`语句。 例如：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>这种情况下注册 DI 的单一实例

由于只有一个实例`PhotoService`类和`Logger`需要类时，这些类就[注册为单一实例的依赖项注入](https://code.google.com/p/autofac/wiki/InstanceScope)中*DependenciesConfig.cs*:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>安全性： 不向用户显示错误详细信息

Fix It 应用原始未包含常规错误页面，并只是让所有异常气泡至 UI，因此一些例外情况，例如数据库连接错误可能会导致显示在浏览器的完整堆栈跟踪。 详细的错误消息有时可以方便地被恶意用户攻击。 解决方案是记录异常详细信息并显示一个错误页面不包含错误详细信息的用户。 已记录 Fix It 应用，并为了显示一个错误页面，我们添加`<customErrors mode=On>`Web.config 文件中。

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

默认情况下这会导致*Views\Shared\Error.cshtml*若要显示的错误。 你可以自定义*Error.cshtml*或创建你自己的错误页面视图，并添加`defaultRedirect`属性。 此外可以指定不同的错误页面的特定错误。

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>安全性： 仅允许由其创建者要编辑的任务

仪表板索引页仅显示任务创建的登录的用户，但恶意用户可以使用到另一个用户的任务的 ID 创建一个 URL。 我们添加了中的代码*DashboardController.cs*以这种情况下返回 404 错误：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>不抑制异常

Fix It 应用原始只返回了 null 在日志中记录的 SQL 查询产生异常：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

这将使其呈现给用户，因为如果查询成功，但只是未返回任何行。 解决方案是重新引发异常后捕获和日志记录：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>在辅助角色中捕捉所有异常

在辅助角色中的任何未处理的异常会导致 VM 才能将回收，因此想要将所有内容包装在 try catch 块中执行操作和处理所有异常。

### <a name="specify-length-for-string-properties-in-entity-classes"></a>在实体类中指定的字符串属性的长度

若要显示简单的代码，请修复其应用程序的原始版本未指定 FixItTask 实体的字段长度并因此它们被定义为 varchar （max） 在数据库中。 因此，UI 将接受几乎任何数量的输入。 将同时应用于用户的指定长度集限制输入中的网页和在数据库中的列大小：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>将私有成员标记为 readonly，当它们不预期的更改时

例如，在`DashboardController`类的实例`FixItTaskRepository`创建，并且不更改，因此我们把它作为定义[readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>使用列表。Any （)，而不是列表。Count （) &gt; 0

如果您所有你关注的信息列表中的一个或多个项是否适合指定的条件，请使用[任何](https://msdn.microsoft.com/library/bb534972.aspx)方法，因为它返回立即找到适合条件的项，而`Count`方法始终必须循环访问通过每个项。 在仪表板*Index.cshtml*文件最初具有此代码：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

我们将它更改为：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>在使用 MVC 帮助程序的 MVC 视图中生成的 Url

有关**创建 Fix It**按钮在主页上，修复其应用程序硬编码的定位点元素：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

有关此类的视图/操作链接最好使用[Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 帮助器，例如：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>在辅助角色中使用而不是 Thread.Sleep 的 Task.Delay

新项目模板将`Thread.Sleep`在示例代码辅助角色，而导致线程进入休眠状态可能会导致要生成其他不必要的线程的线程池。 可以通过使用避免这[Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx)相反。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>避免 async void

如果异步方法不需要返回一个值，则返回`Task`类型而非`void`。

此示例摘自`FixItQueueManager`类：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

应使用`async void`仅为顶级事件处理程序。 如果定义一个方法作为`async void`，调用方不能**await**方法或捕获该方法将引发任何异常。 有关详细信息，请参阅[中的异步编程的最佳做法](https://msdn.microsoft.com/magazine/jj991977.aspx)。

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>使用取消标记来中断工作线程角色循环

通常情况下，**运行**辅助角色上的方法包含无限循环。 辅助角色停止时， [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)调用方法。 应使用此方法来取消内部完成工作**运行**方法并退出正常。 否则，进程可能正在操作终止。

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>选择禁用自动 MIME 探查过程

在某些情况下，Internet Explorer 报告不同于由 web 服务器指定的类型的 MIME 类型。 例如，如果 Internet Explorer 找到 HTML 内容传递使用 HTTP 响应标头的内容类型的文件中： text/plain Internet 资源管理器确定内容应呈现为 HTML。 遗憾的是，此"MIME 探查"可能也会导致服务器承载不受信任的内容的安全问题。 若要克服此问题，Internet Explorer 8 对 MIME 类型确定代码中进行了大量更改，并允许应用程序开发人员[选择退出 MIME 探查](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。 以下代码添加到*Web.config*文件。

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>启用捆绑和缩小

当 Visual Studio 创建新的 web 项目时，默认情况下是未启用 JavaScript 文件的捆绑和缩小。 我们在 BundleConfig.cs 中添加一行代码：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>设置身份验证 cookie 的到期超时

默认情况下，身份验证 cookie 在两周后过期。 较短的时间会更加安全。 可以更改此设置在*StartupAuth.cs*:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>如何从 Visual Studio 在本地计算机上运行该应用程序

有两种方法来运行修复其应用：

- 运行新任务将直接写入到 SQL 数据库的基本应用程序。
- 运行应用程序使用队列以及后端服务创建的任务。 队列模式一章中所述[以队列为中心的工作模式](queue-centric-work-pattern.md)。

<a id="runbase"></a>
### <a name="run-the-base-application"></a>运行基本的应用程序

1. 安装[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。
2. 安装[针对 Visual Studio 用于.NET 的 Azure SDK](https://azure.microsoft.com/downloads/)。
3. 下载.zip 文件[MSDN 代码库](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)。
4. 在文件资源管理器，右键单击.zip 文件并单击属性，然后在属性窗口中单击取消阻止。
5. 将文件解压缩。
6. 双击.sln 文件以启动 Visual Studio。
7. 从工具菜单中，单击库程序包管理器，然后包管理器控制台。
8. 在包管理器控制台 (PMC) 中，单击还原。
9. 退出 Visual Studio。
10. 启动[Azure 存储模拟器](/azure/storage/common/storage-use-emulator)。
11. 重新启动 Visual Studio 中，打开上一步中要关闭的解决方案文件。
12. 请确保 fix It 项目设置为启动项目，然后按 CTRL + F5 以运行该项目。

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>与队列处理运行应用程序

1. 遵循的指导[运行基本的应用程序](#runbase)，然后关闭浏览器并关闭 Visual Studio。
2. 使用管理员权限启动 Visual Studio。 （您将使用 Azure 计算仿真程序，并且需要管理员权限。）
3. 在应用程序中*Web.config*中的文件*MyFixIt*项目 （web 项目） 中，更改的值`appSettings/UseQueues`为"true":

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. 如果[Azure 存储模拟器](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)不是仍在运行，重新启动它。
5. 同时运行 FixIt web 项目和 MyFixItCloudService 项目。

    使用 Visual Studio:

   1. 按**F5**运行 fix It 项目。
   2. 在中**解决方案资源管理器**，右键单击 MyFixItCloudService 项目，然后单击**调试** > **启动新实例**。

    使用 Visual Studio 2013 Express for Web:

   3. 在解决方案资源管理器，右键单击 fix It 解决方案，然后选择**属性**。
   4. 选择**多个启动项目**。
   5. 在中**操作**下 MyFixIt 和 MyFixItCloudService，下拉列表中的选择**启动**。
   6. 单击 **“确定”**。
   7. 按**F5**运行这两个项目。

      运行 MyFixItCloudService 项目时，Visual Studio 将启动 Azure 计算仿真程序。 根据您的防火墙配置，可能需要允许通过防火墙的仿真程序。

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>如何将基本应用程序部署到 Azure 应用服务 Web 应用，通过使用 Windows PowerShell 脚本

为了说明[使一切自动化](automate-everything.md)模式，修复其应用程序提供的设置在 Azure 中的环境并将项目部署到新环境的脚本。 下面的说明解释如何使用脚本。

如果你想要在 Azure 中运行而无需使用队列，并且进行了更改后，若要使用队列在本地运行，请确保将 UseQueues appSetting 值设置回 false 之前继续执行下面的说明。

这些说明假定您已经下载并本地运行时 Fix It 解决方案，并获得了 Azure 帐户，或具有 Azure 订阅有权管理。

1. 安装**Azure PowerShell**控制台。 有关说明，请参阅[如何安装和配置 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。

    此自定义的控制台配置为使用你的 Azure 订阅。 在安装 Azure 模块*Program Files*目录并在每次使用 Azure PowerShell 控制台中自动导入。

    如果想要使用不同的主机程序，如 Windows PowerShell ISE 中，请务必使用[导入模块](https://go.microsoft.com/fwlink/?LinkID=141553)cmdlet 导入 Azure 模块或使用 Azure 模块中的命令来触发自动导入的模块。
2. 启动 Azure PowerShell**以管理员身份运行**选项。
3. 运行[Set-executionpolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet 来将 Azure PowerShell 执行策略设为`RemoteSigned`。 输入**Y** （为否) 以完成策略更改。

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    此设置，可运行本地未进行数字签名的脚本。 (还可以设置执行策略为`Unrestricted`，这会消除对取消阻止步骤的需要更高版本，但不是建议这样做出于安全原因。)
4. 运行`Add-AzureAccount`cmdlet 与你的帐户的凭据设置 PowerShell。

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    这些凭据在一段时间后过期，您必须重新运行`Add-AzureAccount`cmdlet。 是在编写这本电子书，在凭据过期之前的时间限制为 12 小时。
5. 如果你有多个订阅，请使用 Select-azuresubscription cmdlet 来指定想要创建测试环境中的订阅。
6. 使用导入同一个 Azure 订阅的管理证书`Get-AzurePublishSettingsFile`和`Import-AzurePublishSettingsFile`cmdlet。 这些 cmdlet 的第一个下载的证书文件，并为了将其导入在第二个指定该文件的位置。 > [!IMPORTANT]
   > 将下载的文件保存在安全位置，或删除它完成后使用它，因为它包含可用于管理 Azure 服务的证书。

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    使用该证书才能设置 SQL 数据库服务器上的防火墙规则检测到开发计算机的 IP 地址的 REST API 调用。
7. 运行[Set-location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (别名`cd`， `chdir`，和`sl`) 若要导航到包含的脚本的目录。 (它们位于*自动化*Fix It 解决方案文件夹中的文件夹。)如果任何目录名称包含空格，请将路径用引号引起来。 例如，若要导航到`c:\Sample Apps\FixIt\Automation`目录可以输入以下命令：

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. 若要允许 Windows PowerShell 以运行这些脚本，请使用[Unblock-file](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet。 （脚本被阻止，因为它们从 Internet 下载。）

    > [!WARNING]
    > 安全性-然后再运行`Unblock-File`上任何脚本或可执行文件，在记事本中打开该文件、 检查命令，并验证它们是否包含任何恶意代码。

    例如，以下命令将运行`Unblock-File`cmdlet 在当前目录中的所有脚本。

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. 若要创建适用于基 （未处理的队列） 的 web 应用修复其应用程序，请运行环境创建脚本。

    所需`Name`参数指定的数据库的名称，还用于该脚本创建的存储帐户。 名称必须全局唯一在 azurewebsites.net 域中。 如果指定的名称不是唯一的如 fix It 或测试 （或甚至是如下所示的示例中，fixitdemo） `New-AzureWebsite` cmdlet 失败并报告冲突发生内部错误。 该脚本将名称转换为全部小写，以符合的 web 应用、 存储帐户和数据库名称要求。

    所需`SqlDatabasePassword`参数指定将为 SQL 数据库创建的管理员帐户的密码。 不要在密码中包含特殊 XML 字符 (&amp; &lt; &gt; ;)。 这是方法的 azure 的脚本编写的不属于限制的限制。

    例如，如果你想要创建名为"fixitdemo"的 web 应用和使用 SQL Server 管理员密码"Passw0rd1"，您可以输入以下命令：

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    名称在 azurewebsites.net 域中，必须是唯一，并且密码必须满足密码复杂性的 SQL 数据库要求。 （示例 Passw0rd1 符合要求。）

    请注意，该命令将开始使用".\"。 为了帮助防止恶意脚本的执行，Windows PowerShell 要求你运行脚本时提供的脚本文件的完全限定的路径。 可以使用句点来指示当前目录 ("。\")或提供的完全限定的路径，例如：

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    有关脚本的详细信息，请使用`Get-Help`cmdlet。

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    可以使用`Detailed`， `Full`， `Parameters`，和`Examples`来筛选返回的帮助的 Get-help cmdlet 的参数。

    如果脚本失败或生成错误，例如"New-azurewebsite:: 调用 Set-azuresubscription 和 Select-azuresubscription 第一，"可能未完成 Azure PowerShell 的配置。

    在脚本完成后，可以使用 Azure 管理门户，查看已创建的资源，如中所示[使一切自动化](automate-everything.md)一章。
10. 若要将 fix It 项目部署到新的 Azure 环境中，使用*AzureWebsite.ps1*脚本。 例如：

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    完成部署后，浏览器打开与修复它在 Azure 中运行。

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Windows PowerShell 脚本故障排除

运行这些脚本时遇到的最常见错误是与权限相关的。 请确保`Add-AzureAccount`和`Import-AzurePublishSettingsFile`已成功完成，并用于在同一 Azure 订阅。 即使`Add-AzureAccount`已成功您可能需要重新运行。 通过添加权限`Add-AzureAccount`在 12 小时后过期。

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>对象引用未设置为某个对象的实例。

如果该脚本返回错误，例如"对象引用未设置为对象的实例"这意味着 Windows PowerShell 找不到的对象 （这是 null 引用异常） 的过程，运行`Add-AzureAccount`cmdlet，然后重试该脚本。

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError： 服务器遇到内部错误。

`New-AzureWebsite`名称在 azurewebsites.net 域中不唯一时，cmdlet 将返回内部错误。 若要解决此错误，使用不同的值的名称，即 Name 参数中*新建 AzureWebsiteEnv.ps1*。

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>重新启动脚本

如果你需要重启*新建 AzureWebsiteEnv.ps1*脚本因为它不能打印的"脚本已完成"消息之前，你可能想要删除资源之前创建的脚本停止。 例如，如果该脚本创建 ContosoFixItDemo web 应用，并且具有相同名称重新运行该脚本，脚本将失败，因为名称正在使用中。

若要确定哪些资源停止之前创建的脚本，请使用以下 cmdlet:

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`： 若要运行此 cmdlet，通过管道传递到的数据库服务器名称`Get-AzureSqlDatabase`:   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

若要删除这些资源，请使用以下命令。 请注意，是否删除数据库服务器，则你会自动删除与服务器关联的数据库。

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>如何使用队列处理到 Azure 应用服务 Web 应用和 Azure 云服务部署应用程序

若要启用队列，请在 MyFixIt\Web.config 文件进行以下更改。 下`appSettings`，更改的值`UseQueues`为"true":

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

然后部署到 Azure 应用服务中的 web 应用的 MVC 应用程序，如所述[早期](#deploybase)。

接下来，创建新的 Azure 云服务。 修复其应用中包含的脚本不要创建或部署云服务，以便为此，必须使用 Azure 门户。 在门户中，单击**新建** -- **计算**–**云服务** -- **快速创建**，然后输入一个 URL和数据中心位置。 使用同一数据中心部署 web 应用的位置。

![](the-fix-it-sample-application/_static/image1.png)

部署云服务之前，你需要更新一些配置文件。

在 MyFixIt.WorkerRoler\app.config 下, `connectionStrings`，将的值为`appdb`使用 SQL 数据库的实际连接字符串的连接字符串。 可以从门户获取连接字符串。 在门户中，单击**SQL 数据库** - **appdb** - **查看 SQL 数据库的 ADO.Net、 ODBC、 PHP 和 JDBC 连接字符串**。 复制 ADO.NET 连接字符串并将值粘贴到 app.config 文件。 替换为"{你\_密码\_此处}"使用自己的数据库密码。 (假设您使用脚本来部署 MVC 应用程序，指定中的数据库密码`SqlDatabasePassword`脚本参数。)

结果应如以下所示：

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

在同一个 MyFixIt.WorkerRoler\app.config 文件中，在`appSettings`，两个占位符值替换为 Azure 存储帐户。

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

可以从门户获取的访问密钥。 请参阅[如何管理存储帐户](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)。

在 MyFixItCloudService\ServiceConfiguration.Cloud.cscfg，将为 Azure 存储帐户中相同的两个占位符值。

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

现在已准备好部署云服务。 在解决方案资源管理器，右键单击 MyFixItCloudService 项目并选择**发布**。 有关详细信息，请参阅"[部署到 Azure 应用程序](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)"，这是中的第 2 部分[本教程](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)。

> [!div class="step-by-step"]
> [上一篇](more-patterns-and-guidance.md)
