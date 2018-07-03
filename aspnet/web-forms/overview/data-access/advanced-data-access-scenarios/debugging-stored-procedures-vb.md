---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-vb
title: 调试存储的过程 (VB) |Microsoft Docs
author: rick-anderson
description: Visual Studio Professional 和 Team System 版本允许您设置断点并参与到 SQL Server 中的存储过程使调试存储...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/03/2007
ms.topic: article
ms.assetid: 9ed8ccb5-5f31-4eb4-976d-cabf4b45ca09
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-vb
msc.type: authoredcontent
ms.openlocfilehash: 67714284c44c7bc9b06dc599601e116b83017e3e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37401992"
---
<a name="debugging-stored-procedures-vb"></a>调试存储的过程 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_74_VB.zip)或[下载 PDF](debugging-stored-procedures-vb/_static/datatutorial74vb1.pdf)

> Visual Studio Professional 和 Team System 版本允许您设置断点并参与到 SQL Server 中的存储过程进行调试存储的过程与调试应用程序代码一样容易。 本教程演示了直接数据库调试和应用程序调试存储过程。


## <a name="introduction"></a>介绍

Visual Studio 提供了丰富的调试体验。 使用几个击键或鼠标，单击它可以使用断点停止执行程序，并检查其状态和控制流。 调试应用程序代码，以及 Visual Studio 提供了对调试存储的过程从 SQL Server 中的支持。 就像在 ASP.NET 代码隐藏类或业务逻辑层类的代码中设置断点以便也可以将它们放在存储过程。

在本教程中我们将查看单步执行存储过程从 Visual Studio 中的服务器资源管理器以及如何设置，则会命中断点时调用该存储的过程是从正在运行的 ASP.NET 应用程序。

> [!NOTE]
> 遗憾的是，只能将单步执行和调试通过 Visual Studio Professional 和 Team 系统版本的存储的过程。 如果使用 Visual Web Developer 或标准版本的 Visual Studio，你也可以阅读此过程，因为我们逐步调试存储的过程所需的步骤，但您将不能复制你的计算机上的这些步骤。


## <a name="sql-server-debugging-concepts"></a>SQL Server 调试概念

Microsoft SQL Server 2005 旨在提供与集成[公共语言运行时 (CLR)](https://msdn.microsoft.com/netframework/aa497266.aspx)，这是所有.NET 程序集都使用的运行时。 因此，SQL Server 2005 支持托管的数据库对象。 也就是说，可以作为 Visual Basic 类中的方法来创建数据库对象，如存储的过程和用户定义函数 (Udf)。 这样，这些存储的过程和 Udf 以利用.NET Framework 中并从您自己的自定义类的功能。 当然，SQL Server 2005 还提供支持的 T-SQL 的数据库对象。

SQL Server 2005 提供 T-SQL 和托管的数据库对象调试支持。 但是，这些对象，仅通过 Visual Studio 2005 专业版和团队系统版本进行调试。 在本教程中我们将检查调试 T-SQL 的数据库对象。 后续教程讨论调试托管的数据库对象。

[概述的 T-SQL 和 CLR 调试在 SQL Server 2005](https://blogs.msdn.com/sqlclr/archive/2006/06/29/651644.aspx)中的博客条目[SQL Server 2005 CLR 集成团队](https://blogs.msdn.com/sqlclr/default.aspx)突出显示要调试 Visual Studio 中的 SQL Server 2005 对象的三种方法：

- **直接数据库调试 (DDD)** -从服务器资源管理器中我们可以单步执行任何 T-SQL 的数据库对象，如存储的过程和 Udf。 我们将检查在步骤 1 中的 DDD。
- **应用程序调试**-我们可以设置的数据库对象中的断点，然后运行我们的 ASP.NET 应用程序。 执行数据库对象时，将会命中断点和控制移交到调试器。 请注意，与应用程序调试我们无法单步执行数据库对象从应用程序代码。 我们必须显式设置断点在这些存储的过程或 Udf 中想要停止调试器。 在步骤 2 中启动检查应用程序调试。
- **从 SQL Server 项目调试**-Visual Studio Professional 和 Team 系统版本包括一个 SQL Server 项目类型，通常用于创建托管的数据库对象。 我们将探究如何使用 SQL Server 项目并在下一教程中进行调试其内容。

Visual Studio 可以调试在本地和远程 SQL Server 实例上的存储的过程。 本地 SQL Server 实例是安装在 Visual Studio 的同一台计算机上。 如果你使用的 SQL Server 数据库不在你的开发计算机上，它被视为远程实例。 这些教程中我们一直在使用本地 SQL Server 实例。 调试远程的 SQL server 实例上的存储的过程需要比时调试的本地实例上的存储的过程的详细配置步骤。

如果使用本地 SQL Server 实例，可以从步骤 1 开始，并在学习本教程末尾。 如果使用远程 SQL Server 实例，但是，您将首先需要确保您在调试时将记录到开发计算机与远程实例具有 SQL Server 登录名的 Windows 用户帐户。 Moveover，此数据库登录名和用于从正在运行的 ASP.NET 应用程序连接到数据库的数据库登录名必须是成员的`sysadmin`角色。 配置 Visual Studio 和 SQL Server，若要调试的远程实例的详细信息本教程结束时，在远程实例部分看到调试 T-SQL 的数据库对象。

最后，了解调试支持 T-SQL 的数据库对象都不为调试.NET 应用程序的支持丰富的功能。 例如，断点条件和筛选器不支持，只能使用调试窗口中的一个子集，不能使用编辑并继续、 即时窗口呈现毫无意义，等等。 请参阅[调试器命令和功能的限制](https://msdn.microsoft.com/library/ms165035(VS.80).aspx)有关详细信息。

## <a name="step-1-directly-stepping-into-a-stored-procedure"></a>步骤 1： 直接单步执行存储过程

Visual Studio 就可轻松进行直接调试数据库对象。 让我们来看看如何使用直接数据库调试 (DDD) 功能来单步执行`Products_SelectByCategoryID`Northwind 数据库中存储过程。 正如其名，`Products_SelectByCategoryID`返回特定类别; 的产品信息在其中创建它[使用现有存储过程的类型化数据集 s Tableadapter](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)教程。 首先，转到服务器资源管理器并展开 Northwind 数据库节点。 接下来，向下钻取到存储过程文件夹，右键单击`Products_SelectByCategoryID`存储过程，然后从上下文菜单中选择到存储过程的步骤选项。 这将启动调试器。

由于`Products_SelectByCategoryID`存储的过程需要`@CategoryID`输入的参数，我们会要求提供此值。 输入 1，这将返回有关饮料的信息。


![使用值 1 为@CategoryID参数](debugging-stored-procedures-vb/_static/image1.png)

**图 1**： 使用值 1 为`@CategoryID`参数


提供的值后`@CategoryID`参数，该存储过程执行。 不过，而不是运行完成，调试器暂停执行第一个语句。 请注意，该值指示当前存储过程中的位置边距的黄色箭头。 您可以查看和编辑参数值通过监视窗口或悬停在该存储过程中的参数名称。


[![调试器已停止的存储过程的第一个语句](debugging-stored-procedures-vb/_static/image3.png)](debugging-stored-procedures-vb/_static/image2.png)

**图 2**： 存储过程的第一个语句上暂停调试器已 ([单击以查看实际尺寸的图像](debugging-stored-procedures-vb/_static/image4.png))


若要单步执行存储的过程一次的一个语句，请单击工具栏中的单步跳过按钮或按 F10 键。 `Products_SelectByCategoryID`存储的过程包含单个`SELECT`语句，以便按 F10 将逐过程执行单个语句，并完成存储过程的执行。 存储的过程完成后，其输出将显示在输出窗口中，调试器将终止。

> [!NOTE]
> T-SQL 调试发生在语句级别;不能单步执行`SELECT`语句。


## <a name="step-2-configuring-the-website-for-application-debugging"></a>步骤 2： 配置应用程序调试的网站

调试存储的过程直接从服务器资源管理器非常方便，而在许多情况下的多类调用从我们的 ASP.NET 应用程序时调试存储的过程。 我们可以将断点添加到 Visual Studio 中的存储过程的然后开始调试 ASP.NET 应用程序。 从应用程序调用具有断点的存储的过程时，执行将在断点处暂停和我们可以查看和更改存储的过程的参数值，就像我们在步骤 1 中单步执行其语句。

我们可以开始调试应用程序中调用存储的过程之前，我们需要指示 ASP.NET web 应用程序将与 SQL Server 调试器进行集成。 通过右键单击解决方案资源管理器中的网站名称启动 (`ASPNET_Data_Tutorial_74_VB`)。 从上下文菜单中选择属性页选项，选择在左侧的启动选项项并检查调试器部分中的 SQL Server 复选框 （请参见图 3）。


[![检查应用程序的属性页中的 SQL Server 复选框](debugging-stored-procedures-vb/_static/image6.png)](debugging-stored-procedures-vb/_static/image5.png)

**图 3**： 检查应用程序的属性页中的 SQL Server 复选框 ([单击以查看实际尺寸的图像](debugging-stored-procedures-vb/_static/image7.png))


此外，我们需要更新应用程序，以便禁用连接池时使用的数据库连接字符串。 关闭与数据库的连接时，相应`SqlConnection`对象放在池中的可用连接。 建立连接到数据库时，可用的连接对象可以检索从这个池而不会创建并建立新连接。 此池的连接对象是一种性能增强和默认情况下启用。 但是，在调试时我们想要关闭连接池，因为调试基础结构不正确地重新建立使用从相应池中获取的连接时。

为已禁用的连接池，更新`NORTHWNDConnectionString`中`Web.config`以使其包括设置`Pooling=false`。


[!code-xml[Main](debugging-stored-procedures-vb/samples/sample1.xml)]

> [!NOTE]
> 完成后通过 ASP.NET 应用程序调试 SQL Server 会确保恢复连接池通过删除`Pooling`从连接字符串设置 (或将其设置为`Pooling=true`)。


此时配置 ASP.NET 应用程序以允许 Visual Studio 以调试 SQL Server 数据库对象时通过 web 应用程序调用。 现在剩下的工作是对存储过程来添加断点并开始调试 ！

## <a name="step-3-adding-a-breakpoint-and-debugging"></a>步骤 3： 添加断点并调试

打开`Products_SelectByCategoryID`存储过程，并在开头设置断点`SELECT`语句通过在适当的位置的边距中单击或将光标放在开头`SELECT`语句并按 F9。 如图 4 所示，该断点显示为距中的红色圆圈。


[![Products_SelectByCategoryID 中设置断点存储过程](debugging-stored-procedures-vb/_static/image9.png)](debugging-stored-procedures-vb/_static/image8.png)

**图 4**： 中设置断点`Products_SelectByCategoryID`存储过程 ([单击以查看实际尺寸的图像](debugging-stored-procedures-vb/_static/image10.png))


为了使 SQL 数据库对象调试通过客户端应用程序，则必须将数据库配置为支持应用程序进行调试。 当首次设置断点时，此设置应会自动切换，但谨慎仔细检查。 右键单击`NORTHWND.MDF`服务器资源管理器中的节点。 上下文菜单应包括选中的菜单项名为应用程序调试。


![请确保启用了应用程序调试选项](debugging-stored-procedures-vb/_static/image11.png)

**图 5**： 确保已启用应用程序调试选项


设置断点和支持的应用程序调试选项，我们已准备好调试存储的过程时从 ASP.NET 应用程序调用。 通过转到调试菜单启动调试器并在工具栏中选择开始调试，通过按 F5，或通过单击绿色播放图标。 这将启动调试器并启动该网站。

`Products_SelectByCategoryID`中创建存储的过程[使用现有存储过程的类型化数据集 s Tableadapter](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)教程。 其相应的 web 页面 (`~/AdvancedDAL/ExistingSprocs.aspx`) 包含一个 GridView，显示此存储过程返回的结果。 访问本页可通过浏览器。 一旦达到页上，在断点`Products_SelectByCategoryID`将达到存储的过程，并且控制返回到 Visual Studio。 就像在步骤 1 中，您可以单步执行该存储的过程的语句并查看和修改参数值。


[![ExistingSprocs.aspx 页最初显示饮料](debugging-stored-procedures-vb/_static/image13.png)](debugging-stored-procedures-vb/_static/image12.png)

**图 6**:`ExistingSprocs.aspx`页上最初显示饮料 ([单击以查看实际尺寸的图像](debugging-stored-procedures-vb/_static/image14.png))


[![存储过程 s 已到达断点](debugging-stored-procedures-vb/_static/image16.png)](debugging-stored-procedures-vb/_static/image15.png)

**图 7**: 存储过程 s 到达断点 ([单击以查看实际尺寸的图像](debugging-stored-procedures-vb/_static/image17.png))


图 7 所示的值中的监视窗口为`@CategoryID`参数为 1。 这是因为`ExistingSprocs.aspx`页上最初显示产品的饮料类别中，具有`CategoryID`值为 1。 从下拉列表中选择一个不同的类别。 执行此操作导致回发和重新执行`Products_SelectByCategoryID`存储过程。 同样，但这次命中断点`@CategoryID`参数的值反映了所选的下拉列表项的`CategoryID`。


[![从下拉列表中选择一个不同的类别](debugging-stored-procedures-vb/_static/image19.png)](debugging-stored-procedures-vb/_static/image18.png)

**图 8**： 从下拉列表中选择一个不同的类别 ([单击以查看实际尺寸的图像](debugging-stored-procedures-vb/_static/image20.png))


[![@CategoryID参数反映了在 Web 页上选择的类别](debugging-stored-procedures-vb/_static/image22.png)](debugging-stored-procedures-vb/_static/image21.png)

**图 9**:`@CategoryID`参数反映了在 Web 页中选择类别 ([单击以查看实际尺寸的图像](debugging-stored-procedures-vb/_static/image23.png))


> [!NOTE]
> 如果中的断点`Products_SelectByCategoryID`存储的过程时不会发生时访问`ExistingSprocs.aspx`页上，请确保已在 ASP.NET 应用程序的属性页的调试器部分中选中的 SQL Server 复选框，确保连接池已禁用和启用数据库 s 应用程序调试选项。 如果重新仍遇到问题，重新启动 Visual Studio，然后重试。


## <a name="debugging-t-sql-database-objects-on-remote-instances"></a>调试远程实例上的 T-SQL 的数据库对象

在 Visual Studio 的同一台计算机上的 SQL Server 数据库实例时，调试数据库对象，通过 Visual Studio 其实非常简单。 但是，如果 SQL Server 和 Visual Studio 位于不同的计算机然后一些经过慎重的配置是所需一切都正常工作。 有两个我们面对的核心任务：

- 确保用于连接到通过 ADO.NET 的数据库的登录名属于`sysadmin`角色。
- 确保在开发计算机上使用的 Visual Studio 的 Windows 用户帐户是有效的 SQL Server 登录帐户属于`sysadmin`角色。

第一步是相对来说比较简单。 首先，标识用于从 ASP.NET 应用程序连接到数据库，然后，从 SQL Server Management Studio 中，添加到该登录帐户的用户帐户`sysadmin`角色。

第二个任务需要用于调试应用程序的 Windows 用户帐户是远程数据库上的有效登录名。 但是，很可能您登录到你工作站的 Windows 帐户不是有效的 SQL Server 上的登录名。 而不是将您的特定登录帐户添加到 SQL Server，更好的选择是将某个 Windows 用户帐户指定为 SQL Server 调试帐户。 然后，若要调试的远程 SQL Server 实例的数据库对象，将运行 Visual Studio 中使用的 Windows 登录帐户的凭据。

示例可以帮助阐明事项。 假设有一个名为的 Windows 帐户`SQLDebug`Windows 域中。 此帐户需要添加到远程 SQL Server 实例作为有效的登录名的成员以及`sysadmin`角色。 然后，若要调试 Visual Studio 中的远程 SQL Server 实例，我们将需要运行 Visual Studio 作为`SQLDebug`用户。 这可以通过返回以登录我们的工作站，超出的日志记录`SQLDebug`，然后启动 Visual Studio 中，但更简单的方法会登录到我们的工作站使用我们自己的凭据，然后使用`runas.exe`以启动 Visual Studio`SQLDebug`用户。 `runas.exe` 允许特定的应用程序执行假借不同的用户帐户。 若要启动 Visual Studio 作为`SQLDebug`，可以输入以下语句在命令行：


[!code-console[Main](debugging-stored-procedures-vb/samples/sample2.cmd)]

有关此过程的更多详细说明，请参阅[William R.Vaughn](http://betav.com/BLOG/billva/) s *Hitchhiker 到 Visual Studio 和 SQL Server，第七版指南*，以及[How To： 设置 SQL Server 权限用于调试](https://msdn.microsoft.com/library/w1bhybwz(VS.80).aspx)。

> [!NOTE]
> 如果你的开发计算机正在运行 Windows XP Service Pack 2 将需要 Internet 连接防火墙配置为允许远程调试。 [如何为： 启用 SQL Server 2005 调试](https://msdn.microsoft.com/library/s0fk6z6e(VS.80).aspx)一文说明这涉及到两个步骤: （a） 在 Visual Studio 主机计算机，则必须添加`Devenv.exe`到例外列表并打开 TCP 135 端口; 以及 （b） 的远程的 (SQL) 计算机上，则必须打开TCP 135 端口，并添加`sqlservr.exe`到例外列表。 如果您的域策略要求通过 IPSec 进行网络通信，则必须打开 UDP 4500 和 UDP 500 端口。


## <a name="summary"></a>总结

除了为.NET 应用程序代码提供调试支持，Visual Studio 还提供各种 SQL Server 2005 的调试选项。 在本教程中我们介绍了这些选项的两个： 直接数据库调试和应用程序调试。 若要直接调试 T-SQL 的数据库对象，找到通过服务器资源管理器对象然后右键单击它，并选择单步执行。 这将启动调试器并在数据库对象，此时可以单步执行该对象的语句并查看和修改参数值中的第一个语句上暂停。 在步骤 1 中我们使用这种方法来单步执行`Products_SelectByCategoryID`存储过程。

应用程序调试，直接在数据库对象中设置的断点。 从客户端应用程序 （如 ASP.NET web 应用程序） 调用具有断点的数据库对象时，程序将停止调试器时。 应用程序调试很有用，因为它更清楚地显示应用程序的操作会导致要调用的特定数据库对象。 但是，它需要更多的配置和设置比直接数据库调试。

此外可以通过 SQL Server 项目调试数据库对象。 我们将介绍如何使用 SQL Server 项目，并在下一教程中，如何使用它们来创建和调试托管数据库对象。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一页](protecting-connection-strings-and-other-configuration-information-vb.md)
> [下一页](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb.md)
