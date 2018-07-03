---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-cs
title: ELMAH (C#) 的日志记录错误详细信息 |Microsoft Docs
author: rick-anderson
description: 错误日志记录模块和处理程序 (ELMAH) 提供了另一种方法在生产环境中记录运行时错误。 ELMAH 是免费的开放源代码错误...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: 11f6fe44-64ef-4a38-a3b4-35c7bb992352
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-cs
msc.type: authoredcontent
ms.openlocfilehash: 0b9b91b54f50ddd86e102fea3b0dfd5505e3f594
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388472"
---
<a name="logging-error-details-with-elmah-c"></a>ELMAH (C#) 的日志记录错误详细信息
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_14_CS.zip)或[下载 PDF](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial14_ELMAH_cs.pdf)

> 错误日志记录模块和处理程序 (ELMAH) 提供了另一种方法在生产环境中记录运行时错误。 ELMAH 是一个免费的开放源代码错误日志记录库，包括错误筛选和查看错误日志在网页上，为 RSS 源，或下载作为以逗号分隔的文件的功能等功能。 本教程将指导完成下载和配置 ELMAH。


## <a name="introduction"></a>介绍

[前面的教程](logging-error-details-with-asp-net-health-monitoring-cs.md)检查 ASP。NET 的运行状况监控系统，它提供用于记录了很多 Web 事件框库的扩展。 许多开发人员使用的运行状况监视日志并通过电子邮件的未经处理的异常详细信息。 但是，有与此系统的一些痛点。 首先是缺少任何类型的用户界面，用于查看有关已记录事件的信息。 如果你想要看到的 10 个的最后一个错误，摘要或查看过去一周发生了错误的详细信息，则必须通过数据库任一挤出、 浏览你的电子邮件收件箱，或生成显示的信息的网页`aspnet_WebEvent_Events`表。

另一个难题是围绕运行状况监视的复杂性。 由于运行状况监视可用于记录大量不同的事件，并且有多种选项来指导如何以及何时记录事件，正确配置运行状况监控系统可能相当繁琐的任务。 最后，还有一些兼容性问题。 因为运行状况监视第一次添加到.NET Framework 2.0 版中，不可用较旧 web 构建的应用程序使用的 ASP.NET 版本 1.x。 此外，`SqlWebEventProvider`类，我们使用在前面的教程到数据库的日志错误详细信息，仅适用于 Microsoft SQL Server 数据库。 您需要创建自定义日志提供程序类应需要到备用数据存储，如 XML 文件或 Oracle 数据库中记录错误。

运行状况监控系统的替代方法是错误日志记录模块和处理程序 (ELMAH)，通过创建一个免费、 开源的错误日志记录系统[Atif Aziz](http://www.raboof.com/)。 两个系统之间最明显的区别是 ELAMH 的功能，以显示 RSS 源的形式的错误和从网页和一个特定错误的详细信息的列表。 ELMAH 是更轻松地配置比运行状况监视，因为它仅记录错误。 此外，elmah 却包含支持 ASP.NET 1.x、 ASP.NET 2.0 中，和 ASP.NET 3.5 应用程序，以及与各种日志源提供程序一起提供。

本教程将指导完成将 ELMAH 添加到 ASP.NET 应用程序所涉及的步骤。 让我们进入正题！

> [!NOTE]
> 运行状况监控系统和 ELMAH 都有其自己的优点和缺点。 我鼓励您尝试这两个系统并决定哪一个最适合你的需求。


## <a name="adding-elmah-to-an-aspnet-web-application"></a>将 ELMAH 添加到 ASP.NET Web 应用程序

将 ELMAH 集成到一个新的或现有的 ASP.NET 应用程序是一个简单、 直接的过程，将在五分钟。 简单地说，它涉及四个简单步骤：

1. 下载 ELMAH 并添加`Elmah.dll`到 web 应用程序，程序集
2. ELMAH 的 HTTP 模块和处理程序中的注册`Web.config`，
3. 指定 ELMAH 的配置选项和
4. 如果需要，创建错误日志中的源基础结构。

让我们演练一下每个四个步骤，一次一个。

### <a name="step-1-downloading-the-elmah-project-files-and-addingelmahdllto-your-web-application"></a>步骤 1： 下载 ELMAH 项目文件并将添加`Elmah.dll`对 Web 应用程序

ELMAH 1.0 BETA 3 (生成 10617)，在本文撰写之际，最新版本包含在适用于本教程中下载。 或者，也可以访问[ELMAH 网站](https://code.google.com/p/elmah/)以获取最新版本，或要下载的源代码。 提取 ELMAH 下载到您的桌面上的文件夹并找到 ELMAH 程序集文件 (`Elmah.dll`)。

> [!NOTE]
> `Elmah.dll`文件位于下载的`Bin`文件夹，其中具有不同的.NET Framework 版本和版本和调试版本中的子文件夹。 使用合适的框架版本的发布版本。 例如，如果您正在构建的 ASP.NET 3.5 web 应用程序，复制`Elmah.dll`文件从`Bin\net-3.5\Release`文件夹。


接下来，打开 Visual Studio 并右键单击网站名称，在解决方案资源管理器并从上下文菜单中选择添加引用添加到你的项目的程序集。 此时会打开添加引用对话框。 导航到浏览选项卡，然后选择`Elmah.dll`文件。 此操作将添加`Elmah.dll`web 应用程序的文件`Bin`文件夹。

> [!NOTE]
> Web 应用程序项目 (WAP) 类型不会显示`Bin`在解决方案资源管理器中的文件夹。 相反，它列出了引用文件夹下的这些项。


`Elmah.dll`程序集包括 ELMAH 系统使用的类。 这些类分为三个类别之一：

- **HTTP 模块**的 HTTP 模块是一个定义的事件处理程序类`HttpApplication`事件，如`Error`事件。 Elmah 却包含多个 HTTP 模块，三个最无关的要： 

    - `ErrorLogModule` -将未经处理的异常记录到日志源。
    - `ErrorMailModule` -电子邮件中发送未经处理的异常的详细信息。
    - `ErrorFilterModule` -应用开发人员指定筛选器，以确定哪些异常记录以及与将被忽略。
- **HTTP 处理程序**-HTTP 处理程序是一个类，负责生成特定类型的请求的标记。 Elmah 却包含为网页、 RSS 源，或以逗号分隔的文件 (CSV) 呈现错误详细信息的 HTTP 处理程序。
- **错误日志源**-现成 ELMAH 可以记录到 Microsoft SQL Server 数据库，到 Microsoft Access 数据库，到 Oracle 数据库的内存，错误到 XML 文件，到 SQLite 数据库，或 Vista DB 数据库。 运行状况监控系统，如 ELMAH 的体系结构是使用提供程序模型，这意味着你可以创建并无缝集成自己的自定义日志的源提供程序，如果需要生成的。

### <a name="step-2-registering-elmahs-http-module-and-handler"></a>步骤 2： 注册 ELMAH 的 HTTP 模块和处理程序

虽然`Elmah.dll`文件包含的 HTTP 模块和处理程序需要自动记录未处理的异常并显示在网页上的错误详细信息，这些必须显式注册 web 应用程序的配置中。 `ErrorLogModule` HTTP 模块，注册后，订阅`HttpApplication`的`Error`事件。 每当引发此事件`ErrorLogModule`将异常的详细信息记录到指定的日志源。 我们将了解如何在下一节中定义的日志源提供程序"的配置 ELMAH。" `ErrorLogPageFactory` HTTP 处理程序工厂负责生成标记，查看错误日志在网页上的时。

注册 HTTP 模块和处理程序的具体语法取决于为该站点提供强大支持的 web 服务器。 为 ASP.NET Development Server 和 Microsoft 的 IIS 6.0 及更早版本，HTTP 模块和处理程序中注册`<httpModules>`并`<httpHandlers>`部分，会出现`<system.web>`元素。 如果使用 IIS 7.0，则他们需要在中注册`<system.webServer>`元素的`<modules>`和`<handlers>`部分。 幸运的是，可以定义 HTTP 模块和处理程序中的*同时*放置而不考虑所使用的 web 服务器。 此选项是最可移植的一个，因为它允许同一配置，以在而不考虑所使用的 web 服务器在开发和生产环境中使用。

首先，注册`ErrorLogModule`HTTP 模块和`ErrorLogPageFactory`中的 HTTP 处理程序`<httpModules>`并`<httpHandlers>`主题中`<system.web>`。 如果你的配置已定义这两个元素然后只需包括`<add>`ELMAH 的 HTTP 模块和处理程序的元素。

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample1.xml)]

接下来，注册 ELMAH 的 HTTP 模块和处理程序中的`<system.webServer>`元素。 与前面一样，如果此元素不存在在配置中然后将其添加。

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample2.xml)]

默认情况下，IIS 7 会指出如果 HTTP 模块和处理程序注册中`<system.web>`部分。 `validateIntegratedModeConfiguration`属性中`<validation>`元素指示 IIS 7 以取消显示此类错误消息。

请注意，注册的语法`ErrorLogPageFactory`HTTP 处理程序包括`path`属性设置为`elmah.axd`。 此特性告知 web 应用程序，如果为一个名为页的请求到达`elmah.axd`则应由处理该请求`ErrorLogPageFactory`HTTP 处理程序。 我们将看到`ErrorLogPageFactory`中稍后在本教程中的操作的 HTTP 处理程序。

### <a name="step-3-configuring-elmah"></a>步骤 3： 配置 ELMAH

有关其配置选项的网站中查找 ELMAH`Web.config`文件中一个名为的自定义配置部分`<elmah>`。 若要使用中的自定义节`Web.config`必须先将定义在`<configSections>`元素。 打开`Web.config`文件，并添加以下标记到`<configSections>`:

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample3.xml)]

> [!NOTE]
> 如果要配置 ELMAH ASP.NET 1.x 应用程序然后删除`requirePermission="false"`属性从`<section>`上面的元素。


上述语法注册自定义`<elmah>`部分和其子章节： `<security>`， `<errorLog>`， `<errorMail>`，和`<errorFilter>`。

接下来，添加`<elmah>`部分`Web.config`。 本部分中应出现在相同的级别`<system.web>`元素。 内部`<elmah>`部分中添加`<security>`和`<errorLog>`部分如下所示：

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample4.xml)]

`<security>`节的`allowRemoteAccess`属性指示是否允许远程访问。 如果此值设置为 0，然后在错误日志 web 页只能查看本地。 如果此属性设置为 1 在错误日志 web 页可用于远程和本地访问者。 现在，让我们为远程访客禁用错误日志 web 页。 我们有机会讨论这样做的安全问题后，我们将更高版本允许远程访问。

`<errorLog>`节定义错误日志源，其中记录错误详细信息; 它是类似于哪些决定`<providers>`运行状况监控系统中的部分。 上述语法指定`SqlErrorLog`类作为错误记录到 Microsoft SQL Server 数据库指定的错误日志源`connectionStringName`属性值。

> [!NOTE]
> ELMAH 附带有其他错误的日志提供程序可用于 XML 文件、 Microsoft Access 数据库、 Oracle 数据库和其他数据存储中记录错误。 请参阅示例`Web.config`是包含有关如何使用这些备用错误日志提供程序的信息在 ELMAH 下载的文件。


### <a name="step-4-creating-the-error-log-source-infrastructure"></a>步骤 4： 创建错误日志源基础结构

ELMAH 的`SqlErrorLog`提供程序错误详细信息记录到指定的 Microsoft SQL Server 数据库。 `SqlErrorLog`提供程序需要此数据库有一个名为表`ELMAH_Error`和三个存储过程： `ELMAH_GetErrorsXml`， `ELMAH_GetErrorXml`，和`ELMAH_LogError`。 ELMAH 下载内容还包括名为的文件`SQLServer.sql`在`db`文件夹包含用于创建此表并将这些 T-SQL 存储过程。 将需要使用在数据库上运行这些语句`SqlErrorLog`提供程序。

**图 1**并**2**后所需的数据库对象显示在 Visual Studio 中的数据库资源管理器`SqlErrorLog`已添加提供程序。

[![](logging-error-details-with-elmah-cs/_static/image2.png)](logging-error-details-with-elmah-cs/_static/image1.png)

**图 1**:`SqlErrorLog`提供程序记录到错误`ELMAH_Error`表

[![](logging-error-details-with-elmah-cs/_static/image4.png)](logging-error-details-with-elmah-cs/_static/image3.png)

**图 2**:`SqlErrorLog`提供程序使用三个存储的过程

## <a name="elmah-in-action"></a>在操作中的 ELMAH

现在我们已添加到注册的 web 应用程序的 ELMAH `ErrorLogModule` HTTP 模块和`ErrorLogPageFactory`HTTP 处理程序中，指定中的 ELMAH 的配置选项`Web.config`，并添加所需的数据库对象的`SqlErrorLog`错误日志提供程序。 我们现已准备好在操作中看到 ELMAH ！ 访问书评网站，请访问生成运行时错误，例如页面`Genre.aspx?ID=foo`，或不存在页，如`NoSuchPage.aspx`。 访问这些页面时看到的内容取决于`<customErrors>`配置和是否正在访问本地或远程。 (回头[*显示自定义错误页*教程](displaying-a-custom-error-page-cs.md)上本主题复习。)

ELMAH 不会影响发生未经处理的异常; 时，向用户显示哪些内容它只需记录其详细信息。 此错误日志是可访问的网页`elmah.axd`根目录中的你的网站，如`http://localhost/BookReviews/elmah.axd`。 (此文件不以物理方式存在于项目中，但为传入的请求时`elmah.axd`运行时将调度到`ErrorLogPageFactory`HTTP 处理程序，它将生成发送回浏览器的标记。)

> [!NOTE]
> 此外可以使用`elmah.axd`页后，可以指示 ELMAH 生成一个测试错误。 访问`elmah.axd/test`(作为 in `http://localhost/BookReviews/elmah.axd/test`) 会导致引发异常的类型的 ELMAH `Elmah.TestException`，其中包含错误消息:"这是可以安全地忽略测试异常"。


**图 3**访问时显示的错误日志`elmah.axd`从开发环境。

[![](logging-error-details-with-elmah-cs/_static/image6.png)](logging-error-details-with-elmah-cs/_static/image5.png)

**图 3**:`Elmah.axd`显示在网页上的错误日志  
([单击此项可查看原尺寸图像](logging-error-details-with-elmah-cs/_static/image7.png))

错误日志**图 3**包含六个错误条目。 每个条目包括 HTTP 状态代码 （404 或 500，对于这些错误）、 类型、 说明、 出现错误，已登录用户的名称以及日期和时间。 单击详细信息链接将显示包括错误详细信息黄色屏幕死机中所示相同的错误消息的页面 (请参阅**图 4**) 以及在出现此错误时服务器变量的值 (请参阅**图 5**)。 此外可以查看在其中保存错误详细信息，其中包括 HTTP POST 标头中的其他信息，例如值的原始 XML。

[![](logging-error-details-with-elmah-cs/_static/image9.png)](logging-error-details-with-elmah-cs/_static/image8.png)

**图 4**： 查看错误详细信息 YSOD  
([单击此项可查看原尺寸图像](logging-error-details-with-elmah-cs/_static/image10.png))

[![](logging-error-details-with-elmah-cs/_static/image12.png)](logging-error-details-with-elmah-cs/_static/image11.png)

**图 5**： 浏览服务器变量集合中错误的时间处的值  
([单击此项可查看原尺寸图像](logging-error-details-with-elmah-cs/_static/image13.png))

部署到生产网站的 ELMAH 需要：

- 复制`Elmah.dll`文件为`Bin`上生产中，文件夹
- 复制到的特定于 ELMAH 的配置设置`Web.config`在生产环境中，使用文件和
- 将错误日志源基础结构添加到生产数据库。

我们已经探讨了技术，可将复制从开发到生产环境在前面的教程。 生产数据库上获取错误日志源基础结构的最简单方法是使用 SQL Server Management Studio 连接到生产数据库并执行可能`SqlServer.sql`脚本文件，这将创建所需的表和存储过程。

### <a name="viewing-the-error-details-page-on-production"></a>在生产环境中查看错误详细信息页

之后您的网站部署到生产环境，请访问生产网站并生成未经处理的异常。 开发环境中，如 ELMAH 产生任何影响上发生未经处理的异常; 时显示的错误页面相反，它只是记录的错误。 如果你尝试访问错误日志页 (`elmah.axd`) 从生产环境中，你将看到与禁止访问页中所示**图 6**。

[![](logging-error-details-with-elmah-cs/_static/image15.png)](logging-error-details-with-elmah-cs/_static/image14.png)

**图 6**： 默认情况下，远程访问者不能查看错误日志 Web 页  
([单击此项可查看原尺寸图像](logging-error-details-with-elmah-cs/_static/image16.png))

请记住，ELMAH 配置中`<security>`部分中我们将设置`allowRemoteAccess`属性为 0，这将禁止远程用户查看错误日志。 请务必禁止匿名访问者查看错误日志，如安全漏洞或其他敏感信息可能会显示错误详细信息。 如果您决定将此属性设置为 1 并启用远程访问错误日志，则务必锁定`elmah.axd`路径，因此，只有经过授权的访问者可以访问它。 这可以通过添加`<location>`元素`Web.config`文件。

下面的配置允许管理员角色才能访问错误日志 web 页只有用户：

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample5.xml)]

> [!NOTE]
> 在添加了管理员角色和-Scott、 Jisun 和 Alice-在系统中的三个用户[*配置网站，使用应用程序服务*教程](configuring-a-website-that-uses-application-services-cs.md)。 用户 Scott 和 Jisun 是管理员角色的成员。 有关身份验证和授权的详细信息，请参阅我[网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。


远程用户; 可以立即查看错误日志在生产环境回头**图 3**， **4**，并**5**错误日志 web 页的屏幕截图。 但是，如果匿名或非管理员用户尝试查看错误日志页则自动重定向到登录页 (`Login.aspx`)，作为**图 7**显示。

[![](logging-error-details-with-elmah-cs/_static/image18.png)](logging-error-details-with-elmah-cs/_static/image17.png)

**图 7**： 未经授权的用户会自动重定向到登录页  
([单击此项可查看原尺寸图像](logging-error-details-with-elmah-cs/_static/image19.png))

### <a name="programmatically-logging-errors"></a>以编程方式记录错误

ELMAH 的`ErrorLogModule`HTTP 模块将自动记录到指定的日志源的未经处理的异常。 此外，还可以记录错误而无需使用引发未经处理的异常`ErrorSignal`类并将其`Raise`方法。 `Raise`方法传递`Exception`对象并将其记录该异常被引发了异常且已达到 ASP.NET 运行时无需处理。 这种区别，但该请求将继续正常后执行`Raise`已调用了方法，而引发的未经处理异常中断请求的正常执行，并会导致 ASP.NET 运行时，若要显示已配置错误页。

`ErrorSignal`类是在其中某项操作，可能会失败，但其失败并不是灾难性的整体操作正在执行的情况下很有用。 例如，网站可能包含一个窗体，接受用户的输入、 将其存储在数据库中，然后将用户发送一封电子邮件，告知他们他们已处理的信息。 如果信息保存到数据库已成功，但存在错误时发送电子邮件消息，则应发生什么情况？ 一种方法是引发异常，并向用户发送到错误页。 但是，这可能会让用户迷惑误以为不保存这些输入的信息。 另一种方法是记录与电子邮件相关的错误，但不是会更改以任何方式的用户的体验。 这就是`ErrorSignal`类很有用。

[!code-csharp[Main](logging-error-details-with-elmah-cs/samples/sample6.cs)]

## <a name="error-notification-via-email"></a>通过电子邮件的错误通知

到数据库的日志记录错误，以及 ELMAH 还可以配置为通过电子邮件发送给指定收件人的错误详细信息。 提供此功能`ErrorMailModule`HTTP 模块中; 因此，必须注册此 HTTP 模块中`Web.config`才能发送错误详细信息通过电子邮件。

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample7.xml)]

接下来，指定有关中的错误电子邮件的信息`<elmah>`元素的`<errorMail>`部分中，电子邮件的发件人和收件人，其使用者，该值指示是否以异步方式发送电子邮件。

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample8.xml)]

在准备好上述设置，每当出现运行时错误，则 ELMAH 将发送一封电子邮件到support@example.com附带错误详细信息。 ELMAH 的错误电子邮件包含错误详细信息 web 页，即错误消息、 堆栈跟踪和服务器变量中显示的相同信息 (回头**图 4**并**5**)。 错误电子邮件还包括异常详细信息黄色屏幕死机内容作为附件 (`YSOD.html`)。

**图 8**显示了 ELMAH 的错误电子邮件，请访问生成`Genre.aspx?ID=foo`。 虽然**图 8**显示仅错误消息和堆栈跟踪，则服务器变量是包含进一步向下电子邮件的正文中。

[![](logging-error-details-with-elmah-cs/_static/image21.png)](logging-error-details-with-elmah-cs/_static/image20.png)

**图 8**： 你可以配置 ELMAH 发送错误详细信息通过电子邮件  
([单击此项可查看原尺寸图像](logging-error-details-with-elmah-cs/_static/image22.png))

## <a name="only-logging-errors-of-interest"></a>仅记录感兴趣的错误

默认情况下，ELMAH 记录每个未处理的异常，包括 404 和其他 HTTP 错误的详细信息。 您可以指示 ELMAH 忽略这些文件路径或其他类型的使用错误筛选的错误。 ELMAH 的执行筛选逻辑`ErrorFilterModule`HTTP 模块，将需要在注册`Web.config`若要使用筛选逻辑。 中指定的筛选规则`<errorFilter>`部分。

以下标记指示 ELMAH，记录 404 错误。

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample9.xml)]

> [!NOTE]
> 请不要忘记，若要使用错误筛选，必须注册`ErrorFilterModule`HTTP 模块。


`<equal>`元素内的`<test>`部分被称为断言。 如果计算结果为 true 的断言错误则将筛选从 ELMAH 的日志。 有可用的其他断言，包括： `<greater>`， `<greater-or-equal>`， `<not-equal>`， `<lesser>`， `<lesser-or-equal>`，依次类推。 您也可以组合使用断言`<and>`和`<or>`布尔运算符。 更重要的是，甚至可以包括一个简单的 JavaScript 表达式用作断言，或在 C# 或 Visual Basic 中编写您自己断言。

有关筛选功能的 ELMAH 的错误的详细信息，请参阅[错误筛选部分](https://code.google.com/p/elmah/wiki/ErrorFiltering)中[ELMAH wiki](https://code.google.com/p/elmah/w/list)。

## <a name="summary"></a>总结

ELMAH 提供了一种简单但功能强大的机制，用于将 ASP.NET web 应用程序中的日志记录错误。 Microsoft 的运行状况监视系统，如 ELMAH 可以将错误记录到数据库，并可以向开发人员通过电子邮件发送错误详细信息。 与不同的运行状况监控系统，elmah 却包含现成支持的更广泛的错误日志数据存储，包括： Microsoft SQL Server、 Microsoft Access、 Oracle、 XML 文件，以及其他几个人。 此外，ELMAH 提供了用于查看错误日志和 web 页上，从特定错误的详细信息的内置机制`elmah.axd`。 `elmah.axd`页还可以呈现为 RSS 源或为逗号分隔值文件 (CSV)，它可以使用 Microsoft Excel 读取的错误信息。 您可以从使用声明性或以编程方式断言日志筛选器的错误指示 ELMAH。 和 ELMAH 可与 ASP.NET 1.x 版应用程序。

每个已部署的应用程序应具有一些机制来自动记录未处理的异常并将通知发送给开发团队。 是否使用运行状况监视或 ELMAH 完成这是辅助。 换而言之，并不真正重要得多使用运行状况监视还是 ELMAH;计算两个系统，然后选择最适合你的需求。 从根本上说重要的是某种机制将采取的措施，在生产环境中记录未处理的异常。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ELMAH 的错误日志记录模块和处理程序](http://dotnetslackers.com/articles/aspnet/ErrorLoggingModulesAndHandlers.aspx)
- [ELMAH 项目页](https://code.google.com/p/elmah/)（来源为代码、 示例、 wiki）
- [插入 ELMAH 到 Web 应用程序一捕获未经处理的异常](http://screencastaday.com/ScreenCasts/43_Plugging_Elmah_into_Web_Application_to_Catch_Unhandled_Exceptions.aspx)（视频）
- [安全错误日志页](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)
- [使用 HTTP 模块和处理程序来创建可插入的 ASP.NET 组件](https://msdn.microsoft.com/library/aa479332.aspx)
- [网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [上一页](logging-error-details-with-asp-net-health-monitoring-cs.md)
> [下一页](precompiling-your-website-cs.md)
