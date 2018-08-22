---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: 配置和检测 |Microsoft Docs
author: microsoft
description: 有配置中的重大更改和 ASP.NET 2.0 中的检测。 新的 ASP.NET 配置 API 允许进行拉取请求的配置更改...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: ba116140faa0667d504e0ff101c274db9f46079e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824438"
---
<a name="configuration-and-instrumentation"></a>配置和检测
====================
by [Microsoft](https://github.com/microsoft)

> 有配置中的重大更改和 ASP.NET 2.0 中的检测。 新的 ASP.NET 配置 API 允许以编程方式进行配置更改。 此外，许多新的配置设置存在允许对新的配置和检测。


有配置中的重大更改和 ASP.NET 2.0 中的检测。 新的 ASP.NET 配置 API 允许以编程方式进行配置更改。 此外，许多新的配置设置存在允许对新的配置和检测。

在此模块中，我们将讨论 ASP.NET 配置 API，它与读取和写入 ASP.NET 配置文件，以及我们还将介绍 ASP.NET 检测。 我们还将介绍 ASP.NET 跟踪中提供的新功能。

## <a name="aspnet-configuration-api"></a>ASP.NET 配置 API

ASP.NET 配置 API，可开发、 部署和使用单一的编程接口管理应用程序配置数据。 配置 API 可用于开发和以编程方式修改完成配置，ASP.NET，而无需直接编辑配置文件中的 XML。 此外，您可以使用配置 API 在控制台应用程序和脚本开发的、 基于 Web 的管理工具，以及 Microsoft 管理控制台 (MMC) 管理单元。

以下两个配置管理工具使用的配置 API，它们包含在.NET Framework 2.0 版：

- ASP.NET mmc 管理单元，它使用的配置 API 来简化管理任务，提供本地配置数据从配置层次结构的所有级别的集成的视图。
- 网站管理工具，可用于管理本地和远程应用程序配置设置，包括承载的站点。

ASP.NET 配置 API 包含一组可用于以编程方式配置网站和应用程序的 ASP.NET 管理对象。 管理对象将作为.NET Framework 类库。 配置 API 编程模型可帮助确保代码一致性和可靠性，通过在编译时强制数据类型。 若要使其更轻松地管理应用程序配置，配置 API，可查看作为单个集合，而不是将这些数据视为来自不同的单独集合合并从配置层次结构中的所有点的数据配置文件。 此外，配置 API 使您无需直接编辑配置文件中的 XML 处理整个应用程序配置。 最后，该 API 简化了通过支持管理工具，如网站管理工具的配置任务。 配置 API 简化了部署过程通过支持的配置文件的计算机上创建并跨多台计算机运行配置脚本。

> [!NOTE]
> 配置 API 不支持创建 IIS 应用程序。


## <a name="working-with-local-and-remote-configuration-settings"></a>使用本地和远程配置设置

配置对象表示应用于特定的物理实体，如一台计算机，或逻辑实体，例如应用程序或网站的配置设置的合并的视图。 在本地计算机或远程服务器上，可以存在指定的逻辑实体。 当配置文件不存在指定的实体时，配置对象表示由 Machine.config 文件定义的默认配置设置。

可以使用以下类的打开配置方法之一来获取配置对象：

1. ConfigurationManager 类中，如果你的实体是一个客户端应用程序。
2. WebConfigurationManager 类中，如果你的实体是一个 Web 应用程序。

这些方法将返回的所需的方法和属性，以处理基础的配置文件又提供了对配置对象。 你可以访问这些文件进行读取或写入。

### <a name="reading"></a>阅读

使用 GetSection 或 GetSectionGroup 方法来读取配置信息。 用户或读取的进程必须具有读取权限的所有配置文件层次结构中。

> [!NOTE]
> 如果你使用采用了路径参数的静态 GetSection 方法，该路径参数必须引用在其中运行代码的应用程序。 否则为将忽略此参数并返回当前正在运行的应用程序的配置信息。


### <a name="writing"></a>写入

您可以使用 Save 方法之一编写配置信息。 用户或进程的写入操作必须具有写权限的配置文件和当前配置层次结构级别，在目录中，以及读取权限的所有配置文件层次结构中。

若要生成表示指定实体的继承的配置设置的配置文件，请使用以下配置保存方法之一：

1. 要创建新的配置文件的保存方法。
2. 要生成新的配置文件在另一个位置的 SaveAs 方法。

## <a name="configuration-classes-and-namespaces"></a>配置类和命名空间

许多配置类和方法彼此相似。 下表介绍最常用的配置类和命名空间。

| **配置类或命名空间** | **说明** |
| --- | --- |
| [System.Configuration](https://msdn.microsoft.com/library/system.configuration.aspx)命名空间 | 包含所有.NET Framework 应用程序的主要配置类。 部分处理程序类用于从方法，例如 GetSection 和 GetSectionGroup 获取节的配置数据。 这两种方法是非静态。 |
| System.Configuration.Configuration 类 | 表示一组计算机、 应用程序、 Web 目录或其他资源的配置数据。 此类包含有用的方法，如 GetSection 和 GetSectionGroup，更新配置设置和获取对节和节组的引用。 此类用作获取设计时配置数据，如 WebConfigurationManager 和 ConfigurationManager 类的方法的方法的返回类型。 |
| System.Web.Configuration 命名空间 | 包含部分处理程序类，用于在 ASP.NET 配置节定义[ASP.NET 配置设置](https://msdn.microsoft.com/library/b5ysx397.aspx)。 部分处理程序类用于从方法，例如 GetSection 和 GetSectionGroup 获取节的配置数据。 |
| System.Web.Configuration.WebConfigurationManager 类 | 提供用于获取对运行时和设计时的配置设置的引用的有用方法。 这些方法使用 System.Configuration.Configuration 类作为返回类型。 可以互换使用此类的静态 GetSection 方法或 System.Configuration.ConfigurationManager 类的非静态 GetSection 方法。 对于 Web 应用程序配置，而不是 System.Configuration.ConfigurationManager 类建议 System.Web.Configuration.WebConfigurationManager 类。 |
| [System.Configuration.Provider](https://msdn.microsoft.com/library/system.configuration.provider.aspx)命名空间 | 使您能够自定义和扩展的配置提供程序。 这是在配置系统中的所有提供程序类的基类。 |
| [System.Web.Management](https://msdn.microsoft.com/library/system.web.management.aspx)命名空间 | 包含类和接口用于管理和监视 Web 应用程序的运行状况。 严格地说，此命名空间不考虑配置 API 的一部分。 例如，跟踪和事件触发通过此命名空间中的类。 |
| [System.Management.Instrumentation](https://msdn.microsoft.com/library/system.management.instrumentation.aspx)命名空间 | 提供所需的应用程序来公开其管理信息和向潜在使用者通过 Windows Management Instrumentation (WMI) 事件检测的类。 ASP.NET 运行状况监视使用 WMI 来将事件传送。 严格地说，此命名空间不考虑配置 API 的一部分。 |

## <a name="reading-from-aspnet-configuration-files"></a>从 ASP.NET 配置文件进行读取

WebConfigurationManager 类是从 ASP.NET 配置文件进行读取的核心类。 有三个步骤实质上是为读取 ASP.NET 配置文件：

1. 获取使用 OpenWebConfiguration 方法的配置对象。
2. 获取对所需的配置文件中的部分的引用。
3. 从配置文件读取所需的信息。

对象表示的配置不表示特定配置文件。 相反，它表示的计算机、 应用程序或网站配置的合并的视图。 下面的代码示例实例化配置对象，表示配置的 Web 应用程序调用*ProductInfo*。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> 请注意，是否 /ProductInfo 路径不存在，上面的代码将在 machine.config 文件中返回指定的默认配置。


配置对象后，可以使用 GetSection 或 GetSectionGroup 方法深入了解配置设置。 下面的示例获取上述 ProductInfo 应用程序的模拟设置的引用：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>编写对 ASP.NET 配置文件

如下所示从配置文件进行读取，WebConfigurationManager 类是用于将写入 Asp.NET 配置文件的核心。 也有三个步骤到编写对 ASP.NET 配置文件。

1. 获取使用 OpenWebConfiguration 方法的配置对象。
2. 获取对所需的配置文件中的部分的引用。
3. 编写所需的信息从配置文件使用 Save 或 SaveAs 方法。

下面的代码更改**调试**的属性&lt;编译&gt;为 false 的元素：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

此代码执行时，**调试**的属性&lt;编译&gt;元素将设置为 false *webApp*应用程序的 web.config 文件。

## <a name="systemwebmanagement-namespace"></a>System.Web.Management Namespace

System.Web.Management 命名空间提供的类和接口用于管理和监视 ASP.NET 应用程序的运行状况。

日志记录通过定义一个提供程序相关联的事件的规则。 该规则定义的事件发送到提供程序的类型。 以下基本事件是可用于您记录：

| **WebBaseEvent** | 用于所有事件的基本事件类。 包含所需的事件代码、 事件详细信息代码、 日期和时间引发事件，如所有事件的属性序列号、 事件消息和事件的详细信息。 |
| --- | --- |
| **WebManagementEvent** | 用于管理事件，如应用程序生命周期、 请求、 错误和审核事件的基本事件类。 |
| **WebHeartbeatEvent** | 生成固定的时间间隔中的应用程序以捕获有用的运行时状态信息的事件。 |
| **WebAuditEvent** | 安全审核事件，用于将标记条件授权失败，解密失败，如类的基类*等。* |
| **WebRequestEvent** | 所有信息性请求事件的基类。 |
| **WebBaseErrorEvent** | 指明错误条件的所有事件的基类。 |

可用提供程序的类型，可将事件输出发送到事件查看器、 SQL Server、 Windows Management Instrumentation (WMI) 和电子邮件。 预配置的提供程序和事件映射减少记录的事件输出所需的工作量。

ASP.NET 2.0 使用事件日志提供程序--现成的日志事件基于应用程序域启动和停止，以及日志记录任何未经处理的异常。 这有助于介绍一些基本方案。 例如，假设你的应用程序将引发异常，但用户不会保存错误，无法重新生成它。 使用默认事件日志规则时，你将能够收集异常和堆栈的信息，更好地了解哪种错误发生。 另一个示例适用于你的应用程序丢失会话状态。 在这种情况下，你可以查看事件日志以确定是否回收应用程序域，并在应用程序域在第一时间停止的原因。

此外，运行状况监控系统是可扩展的。 例如，可以定义自定义 Web 事件、 引发这些应用程序中，然后定义一个规则以将事件信息发送到你的电子邮件等提供程序。 这使您轻松地将绑定到运行状况监视提供程序的检测。 另一个示例中，无法激发事件每次处理订单并将其设置将每个事件发送到 SQL Server 数据库的规则。 也可以激发事件时用户无法多次登录某行中，并将事件设置为使用基于电子邮件提供程序。

全局的 Web.config 文件中存储的默认提供程序和事件的配置。 全局的 Web.config 文件将存储所有基于 Web 的设置已存储在 ASP.NET 1 中的 Machine.config 文件中的 x。 全局的 Web.config 文件位于以下目录中：

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

&lt;HealthMonitoring&gt;全局的 Web.config 文件的部分提供了默认配置设置。 可以重写这些设置，也可以通过实现来配置你自己的设置&lt;healthMonitoring&gt;你的应用程序的 Web.config 文件中的部分。

&lt;HealthMonitoring&gt;全局的 Web.config 文件部分包含以下各项：

| **提供程序** | 包含有关事件查看器、 WMI 和 SQL Server 设置的提供程序。 |
| --- | --- |
| **eventMappings** | 包含用于各种 WebBase 类映射。 如果生成您自己事件的类，您可以扩展此列表。 生成你自己的事件类为您提供更细的粒度对发送到的信息的提供程序。 例如，可以配置未经处理的异常时将自定义事件发送到电子邮件发送到 SQL Server。 |
| **规则** | 链接到提供程序 eventMappings。 |
| **缓冲** | 与 SQL Server 和电子邮件提供程序一起使用，以确定通常将事件刷新到该提供程序的方式。 |

下面是全局的 Web.config 文件中的一个代码示例。

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>如何存储到事件查看器事件

如前文所述，记录事件的提供程序在事件查看器会为您配置全局的 Web.config 文件中。 默认情况下，所有事件都基于**WebBaseErrorEvent**并**WebFailureAuditEvent**记录。 您可以添加其他规则来记录到事件日志中的其他信息。 例如，如果你想要记录所有事件 (*即*，每个事件基于**WebBaseEvent**)，可以向 Web.config 文件添加以下规则：

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

此规则会链接**的所有事件**事件映射到事件日志提供程序。 EventMapping 和提供程序包含在全局的 Web.config 文件中。

## <a name="how-to-store-events-to-sql-server"></a>如何存储到 SQL Server 事件

此方法使用**ASPNETDB**数据库，生成的 Aspnet\_regsql.exe 工具。 默认提供程序使用 LocalSqlServer 连接字符串，它在应用中使用这两个基于文件的数据库\_数据文件夹或 SQL Server 的本地 SQLExpress 实例。 LocalSqlServer 连接字符串和 SqlProvider 全局的 Web.config 文件中进行配置。

全局的 Web.config 文件中的 LocalSqlServer 连接字符串如下所示：

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

如果你想要使用另一个 SQL Server 实例，您将需要使用 Aspnet\_regsql.exe 工具，可在 %windir%\microsoft.net\framework\v2.0。\*文件夹。 使用 Aspnet\_regsql.exe 工具生成一个自定义**ASPNETDB**数据库的 SQL Server 实例上，然后将连接字符串添加到你的应用程序配置文件，然后使用新的添加提供程序连接字符串。 一旦您有**ASPNETDB**创建的数据库，您将需要设置一个规则，以链接到 sqlProvider eventMapping。

是否使用默认 SqlProvider 或配置自己的提供程序时，你将需要添加链接与事件映射提供程序的规则。 以下规则链接到前面创建的新提供程序**的所有事件**事件映射。 此规则将记录所有事件基于**WebBaseEvent**并将其发送到将使用 MYASPNETDB 连接字符串 MySqlWebEventProvider。 以下代码添加一个规则以将与事件映射提供程序链接：

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

如果您想要仅将错误发送到 SQL Server，则可以添加以下规则：

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>如何将事件转发到 WMI

此外可以将事件转发到 WMI。 WMI 提供程序为您在全局的 Web.config 文件中配置，默认情况下。

下面的代码示例添加一个规则以将事件转发到 WMI:

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

您将需要添加一个规则，以将该提供程序，而且还需要 WMI 侦听器应用程序以侦听事件 eventMapping 相关联。 下面的代码示例添加一个规则以链接到的 WMI 提供程序**的所有事件**事件映射：

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>如何将事件转发到电子邮件

此外可以转发到电子邮件的事件。 请谨慎您映射到电子邮件提供商，如可以无意中向自己发送大量信息的哪些事件规则可能是更好地适用于 SQL Server 或事件日志。 有两个电子邮件提供程序;SimpleMailWebEventProvider 和 TemplatedMailWebEventProvider。 每个具有相同的配置属性，但"模板"和"detailedTemplateErrors"属性，这两个仅位于 TemplatedMailWebEventProvider 除外。

> [!NOTE]
> 这些电子邮件提供程序都不会为您配置。 你将需要将它们添加到 Web.config 文件。


这些两个电子邮件提供程序之间的主要区别是 SimpleMailWebEventProvider 发送电子邮件中的通用模板，不能修改。 示例 Web.config 文件使用以下规则将此电子邮件提供程序添加到配置的提供程序的列表：

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

此外添加了以下规则将绑定到电子邮件提供商**的所有事件**事件映射：

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 跟踪

有三个主要的增强功能在 ASP.NET 2.0 中进行跟踪。

1. 集成的跟踪功能
2. 以编程方式访问跟踪消息
3. 改进了应用程序级别跟踪

## <a name="integrated-tracing-functionality"></a>集成跟踪功能

现在可以将由 asp.net 跟踪输出，System.Diagnostics.Trace 类发出的消息路由和路由发出的对 System.Diagnostics.Trace 的 ASP.NET 跟踪的消息。 此外可以对 System.Diagnostics.Trace 转发 ASP.NET 检测事件。 此功能提供的新**writeToDiagnosticsTrace**的属性&lt;跟踪&gt;元素。 如果此布尔值为 true，ASP.NET 跟踪消息将转发到使用 System.Diagnostics 跟踪基础结构由已注册，以显示跟踪消息的所有侦听器。

## <a name="programmatic-access-to-trace-messages"></a>以编程方式访问跟踪消息

ASP.NET 2.0 允许以编程方式访问通过的所有跟踪消息**TraceContextRecord**类和**TraceRecords**集合。 访问跟踪消息的最有效方式是注册**TraceContextEventHandler** （ASP.NET 2.0 中还新增） 的委托来处理新**TraceFinished**事件。 根据需要，然后可以循环访问的跟踪消息。

下面的代码示例阐释了这一点：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

在上述示例中，我循环访问 TraceRecords 集合，然后将每条消息写入到响应流。

## <a name="improved-application-level-tracing"></a>改进了应用程序级别跟踪

通过引入的新改进的应用程序级别跟踪**mostRecent**的属性&lt;跟踪&gt;元素。 此属性指定是否显示最新的应用程序级别的跟踪输出，并丢弃较旧的跟踪数据超出了所指示的 requestLimit 的限制。 如果为 false，直至达到 requestLimit 属性的请求显示跟踪数据。

## <a name="aspnet-command-line-tools"></a>ASP.NET 命令行工具

有几种命令行工具来帮助中的 ASP.NET 配置。 ASP.NET 开发人员应熟悉 aspnet\_regiis.exe 工具。 ASP.NET 2.0 提供了三个其他命令行工具，可帮助配置中。

以下命令行工具有：

| **工具** | **使用** |
| --- | --- |
| **aspnet\_regiis.exe** | 允许使用 ASP.NET 和 IIS 注册。 有两个版本的此工具附带 ASP.NET 2.0，（在框架文件夹中） 的 32 位系统和 64 位系统 （在 Framework64 文件夹中。）未将 32 位操作系统上安装 64 位版本。 |
| **aspnet\_regsql.exe** | ASP.NET SQL Server 注册工具用于在 ASP.NET 中，创建由 SQL Server 提供程序使用 Microsoft SQL Server 数据库，或用于添加或从现有数据库中删除选项。 Aspnet\_regsql.exe 文件位于 [drive:]\WINDOWS\Microsoft.NET\Framework\versionNumber Web 服务器上的文件夹。 |
| **aspnet\_regbrowsers.exe** | ASP.NET 浏览器注册工具将分析和编译成一个程序集的所有系统级的浏览器定义并将程序集安装到全局程序集缓存。 该工具使用浏览器定义文件 (。浏览器文件） 从.NET Framework 的浏览器子目录。 该工具可以 %SystemRoot%\Microsoft.NET\Framework\version\ 目录中找到。 |
| **aspnet\_compiler.exe** | ASP.NET 编译工具，可编译的 ASP.NET Web 应用程序中的位置或以部署到目标位置，例如生产服务器。 就地编译有助于应用程序的性能，因为最终用户不会遇到延迟对应用程序的第一个请求上编译应用程序时。 |

因为 aspnet\_regiis.exe 工具不是 ASP.NET 2.0 中新增的这里我们将不讨论。

## <a name="aspnet-sql-server-registration-tool---aspnetregsqlexe"></a>ASP.NET SQL Server 注册工具 aspnet\_regsql.exe

可以设置多个类型的使用 ASP.NET SQL Server 注册工具的选项。 可以指定 SQL 连接、 指定的 ASP.NET 应用程序服务使用 SQL Server 管理的信息，指示哪些数据库或表用于 SQL 缓存依赖项，并添加或删除对使用 SQL Server 存储过程和会话状态的支持。

多个 ASP.NET 应用程序服务依赖于提供程序来管理存储和从数据源检索数据。 每个提供程序是特定于数据源。 ASP.NET 包括以下 ASP.NET 功能的 SQL Server 提供程序：

- 成员资格 ( [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)类)。
- 角色管理 ( [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)类)。
- 配置文件 ( [SqlProfileProvider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx)类)。
- Web 部件的个性化设置 ( [SqlPersonalizationProvider](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx)类)。
- Web 事件 ( [SqlWebEventProvider](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx)类)。

在安装 ASP.NET 时，你的服务器的 Machine.config 文件包括指定为每个依赖于提供程序的 ASP.NET 功能的 SQL Server 提供程序的配置元素。 默认情况下，若要连接到 SQL Server Express 2005 的本地用户实例配置这些提供程序。 如果更改由提供程序使用的默认连接字符串，则可以使用任何计算机配置中配置的 ASP.NET 功能之前必须安装 SQL Server 数据库和数据库元素为您所选的功能使用 Aspnet\_regsql.exe。 如果尚不存在指定的数据库，您使用 SQL 注册工具 （aspnetdb 将默认数据库如果未指定命令行上），则当前用户必须具有在 SQL Server 和创建架构中创建数据库的权限在数据库中的元素。

### <a name="sql-cache-dependency"></a>SQL 缓存依赖项

ASP.NET 输出缓存的一项高级的功能是 SQL 缓存依赖项。 SQL 缓存依赖项支持两个不同的操作模式： 一个使用 ASP.NET 实现表轮询和使用 SQL Server 2005 的查询通知功能的第二个模式。 SQL 注册工具可以用于配置的表轮询操作模式。

### <a name="session-state"></a>会话状态

默认情况下，在 ASP.NET 进程内的内存中存储会话状态的值和信息。 或者，可以将会话数据存储在 SQL Server 数据库中，其中可由多个 Web 服务器共享它。 如果不存在的数据库的指定的会话状态使用 SQL 注册工具，当前用户必须有权在 SQL Server 和创建数据库中的架构元素中创建数据库。 如果该数据库存在，当前用户必须有权在现有数据库中创建架构元素。

若要在 SQL Server 上安装会话状态数据库，运行 Aspnet\_regsql.exe 工具并提供与该命令的以下信息：

- SQL Server 的名称实例，请使用 **-S**选项。
- 具有运行 SQL Server 的计算机上创建数据库的权限的帐户登录凭据。 使用 **-E**选项以使用当前登录的用户，或使用 **-U**选项以指定用户 ID，并使用 **-P**选项指定一个密码。
- **-Ssadd**命令行选项来添加会话状态数据库。

默认情况下，不能使用 Aspnet\_regsql.exe 工具来运行 SQL Server 2005 Express Edition 的计算机上安装会话状态数据库。

### <a name="the-aspnet-browser-registration-tool---aspnetregbrowsersexe"></a>ASP.NET 浏览器注册工具-aspnet\_regbrowsers.exe

在 ASP.NET 1.1 版中，Machine.config 文件包含一个名为部分&lt;browserCaps&gt;。 本部分包含一的系列定义基于正则表达式的各种浏览器的配置的 XML 条目。 Asp.net 2.0 版中，一个新。浏览器文件定义的特定浏览器中使用 XML 项的参数。 您添加新的浏览器上添加一个新的信息。浏览器文件复制到位于 %SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers 在系统上的文件夹。

由于每次需要浏览器信息时，应用程序并没有读取.config 文件，您可以创建一个新。浏览器文件和运行的 Aspnet\_regbrowsers.exe 对程序集添加所需的更改。 这使得服务器能够立即访问新的浏览器信息，因此不需要关闭任何应用程序以提取信息。 应用程序可以通过浏览器属性的当前 HttpRequest 访问浏览器功能。

以下是可选项时运行 aspnet\_regbrowser.exe:

| **选项** | **说明** |
| --- | --- |
| **-?** | 显示 Aspnet\_regbbrowsers.exe 命令窗口中的帮助文本。 |
| **-i** | 创建运行时浏览器功能的程序集并将其安装在全局程序集缓存。 |
| **-u** | 从全局程序集缓存中卸载运行时浏览器功能的程序集。 |

## <a name="the-aspnet-compilation-tool---aspnetcompilerexe"></a>ASP.NET 编译工具-aspnet\_compiler.exe

ASP.NET 编译工具可在两种常规方法： 进行就地编译和部署，其中指定目标输出目录的编译。

### <a name="compiling-an-application-in-placehttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[编译中的位置的应用程序](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET 编译工具可以编译的应用程序中的位置，也就是说，它会模拟应用程序，从而导致正则编译对进行多个请求的行为。 预编译站点的用户不会通过编译的页上第一个请求而导致的延迟。

当你进行预编译中的位置的站点时，应该注意下列事项：

- 站点将保留其文件和目录结构。
- 您必须具有站点服务器上使用的所有编程语言的编译器。
- 如果任何文件的编译将失败，整个站点编译将失败。

此外可以重新编译后向其中添加新的源文件的应用程序中的位置。 此工具会仅将新的或更改文件，除非您包括 **-c**选项。

> [!NOTE]
> 包含嵌套的应用程序的应用程序的编译不编译嵌套的应用程序。 嵌套的应用程序必须单独编译。


### <a name="compiling-an-application-for-deploymenthttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[编译为部署的应用程序](https://msdn.microsoft.com/library/ms229863.aspx)

通过指定 targetDir 参数编译的应用程序部署 （编译到目标位置）。 TargetDir 可以是 Web 应用程序的最后一个位置，也可以进一步部署已编译的应用程序。 使用 **-u**选项编译的方式，你可以无需重新编译它，编译的应用程序中的某些文件进行更改的应用程序。 Aspnet\_compiler.exe 对进行了区分静态和动态的文件类型，并创建生成的应用程序时以不同方式处理它们。

- 静态文件类型是指那些没有关联的编译器或生成提供程序，例如它的文件命名已扩展，如.css、.gif、.htm、.html、.jpg、.js，依此类推。 这些文件只被复制到目标的位置，它们保留在目录结构中的相对位置。
- 动态文件类型是那些具有关联的编译器或生成提供程序，包括具有如.asax、.ascx、.ashx、.aspx、.browser、.master，等特定于 ASP.NET 的文件扩展名的文件。 从这些文件，ASP.NET 编译工具生成的程序集。 如果 **-u**省略选项，该工具还会创建扩展名的文件的名称。映射到其程序集的原始源文件的编译。 若要确保保留的应用程序源目录结构，该工具，请生成目标应用程序中的相应位置中的占位符文件。

必须使用 **-u**选项以指示可以修改已编译的应用程序的内容。 否则为后续修改将被忽略，或者会导致运行时错误。

下表描述了如何 ASP.NET 编译工具处理的不同文件类型 **-u**已包含选项。

| **文件类型** | **编译器操作** |
| --- | --- |
| .ascx、.aspx、.master | 这些文件被拆分为标记和源代码，其中包括代码隐藏文件和任何代码都括在&lt;脚本 runat ="server"&gt;元素。 源代码编译到程序集中，其派生自哈希算法的名称和程序集位于 Bin 目录中。 任何内联代码，这就是，代码括**&lt; %** 并**% &gt;** 方括号，包括在标记，不进行编译。 创建要包含的标记和放置在相应的输出目录中与源文件同名的新文件。 |
| .ashx、.asmx | 这些文件不进行编译，移动到输出目录，并且不进行编译。 如果你想要编译的处理程序代码，将代码放入应用程序中的源代码文件\_代码目录。 |
| .cs、.vb、.jsl、.cpp （不包括代码隐藏文件的前面列出的文件类型） | 这些文件编译，并包含为中对其进行引用的程序集的资源。 源文件不复制到输出目录中。 如果不引用代码文件，则不编译。 |
| 自定义文件类型 | 未编译这些文件。 这些文件复制到相应的输出目录。 |
| 源代码文件的应用中\_代码子目录 | 这些文件将编译到程序集并放置在 Bin 目录中。 |
| 在应用中的.resx 和.resource 文件\_GlobalResources 子目录 | 这些文件将编译到程序集并放置在 Bin 目录中。 无应用\_下主输出目录中，创建 GlobalResources 子目录和位于源目录中没有.resx 或.resources 文件复制到输出目录。 |
| 在应用中的.resx 和.resource 文件\_LocalResources 子目录 | 这些文件未编译，并复制到相应的输出目录。 |
| 在应用中的.skin 文件\_主题子目录 | .Skin 文件和静态主题文件不进行编译，复制到相应的输出目录。 |
| .browser Web.config 静态文件类型的 Bin 目录中已存在的程序集 | 这些文件原封不动地复制到输出目录。 |

下表描述了如何 ASP.NET 编译工具处理的不同文件类型 **-u**省略选项。

| **文件类型** | **编译器操作** |
| --- | --- |
| .aspx、.asmx、.ashx、.master | 这些文件被拆分为标记和源代码，其中包括代码隐藏文件和任何代码都括在&lt;脚本 runat ="server"&gt;元素。 源代码编译到程序集中，其派生自哈希算法的名称。 生成的程序集位于 Bin 目录中。 任何内联代码，这就是，代码括**&lt; %** 并**% &gt;** 方括号，包括在标记，不进行编译。 编译器会创建新文件包含与源文件同名的标记。 这些生成的文件位于 Bin 目录中。 编译器还创建文件与源文件同名但扩展名为。COMPILED 包含映射的信息。 。已编译的文件放置在与原始源文件的位置相对应的输出目录中。 |
| .ascx | 这些文件被拆分为标记和源代码。 源代码编译到程序集中，放在 Bin 目录中，使用派生自哈希算法的名称。 生成无标记文件。 |
| .cs、.vb、.jsl、.cpp （不包括代码隐藏文件的前面列出的文件类型） | 从.ascx、.ashx、 或.aspx 文件生成的程序集引用的源代码是编译为程序集和放在 Bin 目录中。 复制没有源代码文件。 |
| 自定义文件类型 | 像动态文件一样，这些文件进行编译。 具体取决于它们所基于的文件的类型，编译器可以将映射文件放在输出目录中。 |
| 在应用中的文件\_代码子目录 | 此子目录中的源代码文件都编译到程序集和放在 Bin 目录中。 |
| 在应用中的文件\_GlobalResources 子目录 | 这些文件将编译到程序集并放置在 Bin 目录中。 无应用\_主输出目录下创建 GlobalResources 子目录。 如果配置文件指定 appliesTo ="All".resx 和.resources 文件复制到输出目录。 如果引用的它们不会复制[BuildProvider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)。 |
| 在应用中的.resx 和.resource 文件\_LocalResources 子目录 | 这些文件将编译到程序集中具有唯一名称，并放置在 Bin 目录中。 没有文件.resx 或.resource 文件复制到输出目录。 |
| 在应用中的.skin 文件\_主题子目录 | 主题将编译到程序集并放置在 Bin 目录中。 存根 （stub） 文件将为.skin 文件创建并放置在相应的输出目录中。 静态文件 （例如.css) 复制到输出目录。 |
| .browser Web.config 静态文件类型的 Bin 目录中已存在的程序集 | 这些文件原封不动地复制到输出目录。 |

### <a name="fixed-assembly-nameshttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[固定的程序集名称](https://msdn.microsoft.com/library/ms229863.aspx##)

某些情况下，例如部署 Web 应用程序使用 MSI Windows 安装程序，需要使用一致的文件名称和内容，以及一致的目录结构，以标识程序集或更新的配置设置。 在这些情况下，你可以使用 **-fixednames**选项以指定 ASP.NET 编译工具应编译为程序集的每个源代码文件而不是使用 where 多个页面被编译到程序集。 这可能会导致大量的程序集，因此如果您担心与可伸缩性应谨慎使用此选项。

### <a name="strong-name-compilationhttpsmsdnmicrosoftcomlibraryms229863aspx"></a>[强名称编译](https://msdn.microsoft.com/library/ms229863.aspx##)

**Aptca**， **-delaysign**， **-keycontainer**并 **-keyfile**选项可用，以便可以使用 Aspnet\_compiler.exe 能够生成强名称程序集，而无需使用[强名称工具 (Sn.exe)](https://msdn.microsoft.com/library/k5b5tt23.aspx)单独。 这些选项，分别对应到**AllowPartiallyTrustedCallersAttribute**， **AssemblyDelaySignAttribute**， **AssemblyKeyNameAttribute**，并且**AssemblyKeyFileAttribute**。

这些属性的讨论不在本课程的作用域。

## <a name="labs"></a>实验室

每个以下的实验室基于上一个实验室。 你将需要按顺序执行。

## <a name="lab-1-using-the-configuration-api"></a>实验室 1： 使用配置 API

1. 创建一个名为的新网站*mod9lab*。
2. 向站点添加新的 Web 配置文件。
3. 以下代码添加到 web.config 文件：


[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

这将确保您有权将更改保存到 web.config 文件。

1. 将新的标签控件添加到 Default.aspx 并将更改为 ID **lblDebugStatus**。
2. 将新的按钮控件添加到 Default.aspx。
3. 更改到按钮控件的 ID **btnToggleDebug**和文本**切换调试状态**。
4. 打开 Default.aspx 代码隐藏文件的代码视图，并添加**使用**语句**System.Web.Configuration** ，如下所示：


[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. 将两个私有变量添加到类和一个页面\_Init 方法，如下所示：


[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. 将以下代码添加到页\_负载：


[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. 保存并浏览 default.aspx。 请注意标签控件显示当前的调试状态。
2. 双击设计器中的按钮控件并将以下代码添加到按钮控件的单击事件：


[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. 保存和浏览 default.aspx 并单击按钮。
2. 打开 web.config 文件之后每个按钮单击，然后观察,**调试**属性中&lt;编译&gt;部分。

## <a name="lab-2-logging-application-restarts"></a>实验室 2： 日志记录应用程序重新启动

在此实验中，将创建代码，您可以切换日志记录的应用程序关闭、 初创公司和事件查看器中的重新编译。

1. 将 DropDownList 添加到 default.aspx 并将 ID 更改为 ddlLogAppEvents。
2. 设置**AutoPostBack**属性为 DropDownList **true**。
3. 将三个项添加到 DropDownList 的项集合。 请**文本**的第一项*Select Value*和值为-1。 使**文本**和**值**的第二项**True**并**文本**和**值**的第三个项**False**。
4. 将新标签添加到 default.aspx。 更改到的 ID **lblLogAppEvents**。
5. 打开 default.aspx 代码隐藏视图并添加新的变量类型的声明 HealthMonitoringSection，如下所示：


[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. 将以下代码添加到页面中的现有代码\_Init:


[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. 双击 DropDownList 并将以下代码添加到的 SelectedIndexChanged 事件：


[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. 浏览 default.aspx。
2. 设置下拉列表中为**False**。
3. 清除事件查看器中的应用程序日志。
4. 单击按钮以更改应用程序的调试属性。
5. 刷新事件查看器中的应用程序日志。 

    1. 记录任何事件？
    2. 为什么或为什么不？
6. 设置下拉列表中为 **，则返回 True。**
7. 单击该按钮以切换应用程序的调试属性。
8. 刷新应用程序登录名在事件查看器。 

    1. 记录任何事件？
    2. 应用程序关闭的原因是什么？
9. 试验启用和禁用日志记录并查看对 web.config 文件所做的更改。

## <a name="more-information"></a>详细信息：

ASP.NET 2.0 的提供程序模型可以创建自己的提供程序不只是应用程序检测，但许多其他用途，以及如成员身份、 配置文件，等等。有关编写自定义提供程序可应用程序事件记录到文本文件的详细信息，请访问[此链接](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)。
