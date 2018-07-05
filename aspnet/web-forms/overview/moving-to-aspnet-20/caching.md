---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: 缓存 |Microsoft Docs
author: microsoft
description: 了解缓存对于良好的 ASP.NET 应用程序至关重要。 ASP.NET 1.x 提供三个不同选项进行缓存;输出缓存...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: 4f52a88680db54de6271b17bd52cbdace66425e9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37387694"
---
<a name="caching"></a>缓存
====================
by [Microsoft](https://github.com/microsoft)

> 了解缓存对于良好的 ASP.NET 应用程序至关重要。 ASP.NET 1.x 提供三个不同选项进行缓存;输出缓存、 片段缓存和缓存 API。


了解缓存对于良好的 ASP.NET 应用程序至关重要。 ASP.NET 1.x 提供三个不同选项进行缓存;输出缓存、 片段缓存和缓存 API。 ASP.NET 2.0 提供了所有这三种方法，但它添加了一些重要的其他功能。 有几个新的缓存依赖项和开发人员现在可以创建自定义缓存依赖项的选项。 也已在 ASP.NET 2.0 中显著改进的缓存配置。

## <a name="new-features"></a>新增功能

## <a name="cache-profiles"></a>缓存配置文件

缓存配置文件允许开发人员定义然后可应用于各个页面的特定缓存设置。 例如，如果必须在 12 小时后应从缓存过期某些页，可以轻松地创建可应用于这些页面的缓存配置文件。 若要添加新的缓存配置文件，请使用&lt;outputCacheSettings&gt;配置文件中的部分。 例如，下面是名为缓存配置文件的配置*twoday*用于配置缓存持续时间为 12 个小时。

[!code-xml[Main](caching/samples/sample1.xml)]

若要将此缓存配置文件应用于特定页面上，使用 @ OutputCache 指令的 CacheProfile 属性，如下所示：

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>自定义缓存依赖项

ASP.NET 1.x 开发人员执行了自定义缓存依赖项。 在 ASP.NET 1.x 中，CacheDependency 类密封的哪些阻止的开发人员从其派生其自己的类。 在 ASP.NET 2.0 中，取消该限制和开发人员可以随意开发他们自己的自定义缓存依赖项。 CacheDependency 类可以创建基于文件、 目录或缓存密钥的自定义缓存依赖项。

例如，下面的代码将创建基于名为 stuff.xml 位于 Web 应用程序的根目录中的文件新的自定义缓存依赖项：

[!code-csharp[Main](caching/samples/sample3.cs)]

在此方案中，当 stuff.xml 文件发生更改，缓存的项会失效。

还有可能创建自定义缓存依赖项使用缓存键。 使用此方法，则将使缓存键中的删除失效的缓存的数据。 下面的示例阐释了这一点：

[!code-csharp[Main](caching/samples/sample4.cs)]

要使之无效的项的上方插入了，只需删除已插入缓存，以用作缓存的键的项。

[!code-csharp[Main](caching/samples/sample5.cs)]

请注意，充当缓存键的项的键必须与添加到缓存密钥的数组的值相同。

## <a name="polling-based-sql-cache-dependenciesemalso-called-table-based-dependenciesem"></a>基于轮询的 SQL 缓存依赖项<em>（也称为基于表的依赖项）</em>

SQL Server 7 和 2000年使用 SQL 缓存依赖项基于轮询的模型。 基于轮询的模型上的数据库表，表中的数据更改时，会触发使用触发器。 触发更新**changeId** ASP.NET 会定期检查通知表中的字段。 如果**changeId**已更新字段，ASP.NET 就会知道数据已更改，并且不使缓存的数据失效。

> [!NOTE]
> SQL Server 2005 还可以使用基于轮询的模型中，但由于基于轮询的模型不是最有效的模式，则最好使用 SQL Server 2005 使用基于查询的模型 （稍后讨论）。


为了使 SQL 缓存依赖项使用基于轮询的模型才能正常工作，这些表必须具有启用通知。 这可以实现使用 SqlCacheDependencyAdmin 类以编程方式或通过使用 aspnet\_regsql.exe 实用程序。

下面的命令行位于名为的 SQL Server 实例上的 Northwind 数据库中注册的 Products 表*dbase*的 SQL 缓存依赖项。

[!code-console[Main](caching/samples/sample6.cmd)]

下面是上述命令中使用的命令行开关的说明：

| **命令行开关** | **目的** |
| --- | --- |
| -S *server* | 指定服务器名称。 |
| -ed | 指定数据库，应启用 SQL 缓存依赖项。 |
| -d*数据库\_名称* | 指定应启用 SQL 缓存依赖项的数据库名称。 |
| -E | 指定该 aspnet\_regsql 应使用 Windows 身份验证连接到数据库时。 |
| -et | 指定我们要启用 SQL 缓存依赖项的数据库表。 |
| -t*表\_名称* | 指定要启用 SQL 缓存依赖项的数据库表的名称。 |

> [!NOTE]
> 有其他开关可用于 aspnet\_regsql.exe。 有关完整列表，运行 aspnet\_regsql.exe-？ 从命令行。


此命令运行时对 SQL Server 数据库进行以下更改：

- **AspNet\_SqlCacheTablesForChangeNotification**添加表。 此表包含每个表为其启用 SQL 缓存依赖项在数据库中的一行。
- 在数据库内创建以下存储的过程：


| AspNet\_SqlCachePollingStoredProcedure | 查询 AspNet\_SqlCacheTablesForChangeNotification 表，并返回已启用 SQL 缓存依赖项和每个表的 changeId 的值的所有表。 此存储的过程用于轮询用于确定数据是否已更改。 |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | 返回的所有表启用 SQL 缓存依赖项通过查询 AspNet\_SqlCacheTablesForChangeNotification 表和返回所有表都启用 sql 缓存依赖项。 |
| AspNet\_SqlCacheRegisterTableStoredProcedure | 通过通知表中添加必要的入口注册 SQL 缓存依赖项的表，并将触发器添加。 |
| AspNet\_SqlCacheUnRegisterTableStoredProcedure | 通过通知表中删除该条目注销 SQL 缓存依赖项的表和删除触发器。 |
| AspNet\_SqlCacheUpdateChangeIdStoredProcedure | 通过递增所更改表 changeId 更新通知表。 ASP.NET 使用此值来确定数据是否已更改。 如下所述，启用表时，创建触发器被执行此存储的过程。 |


- SQL Server 触发器调用 ***表\_名称 *\_AspNet\_SqlCacheNotification\_触发器**为该表创建。 此触发器执行 AspNet\_SqlCacheUpdateChangeIdStoredProcedure 时对表执行 INSERT、 UPDATE 或 DELETE。
- SQL Server 角色称为**aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess**添加到数据库。

**Aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** SQL Server 角色具有 EXEC 权限到 AspNet\_SqlCachePollingStoredProcedure。 为了使轮询模型才能正常工作，必须将进程帐户添加到 aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess 角色。 Aspnet\_regsql.exe 工具将执行此操作为您。

### <a name="configuring-polling-based-sql-cache-dependencies"></a>配置基于轮询的 SQL 缓存依赖项

有几个步骤所需的配置基于轮询的 SQL 缓存依赖项。 第一步是启用的数据库和表如上文所述。 该步骤完成后，配置的其余部分如下所示：

- 配置 ASP.NET 配置文件。
- 配置 SqlCacheDependency

### <a name="configuring-the-aspnet-configuration-file"></a>配置 ASP.NET 配置文件

除了添加的连接字符串，如前一模块中所述，还必须配置&lt;缓存&gt;具有元素&lt;sqlCacheDependency&gt;元素如下所示：

[!code-xml[Main](caching/samples/sample7.xml)]

此配置上启用 SQL 缓存依赖项*pubs*数据库。 请注意，在 pollTime 特性&lt;sqlCacheDependency&gt;元素默认值为 60000 毫秒或 1 分钟。 （此值不能为不超过 500 毫秒）。在此示例中，&lt;添加&gt;元素将添加一个新的数据库，并重写 pollTime，将其设置为 9000000 毫秒为单位。

#### <a name="configuring-the-sqlcachedependency"></a>配置 SqlCacheDependency

下一步是配置 SqlCacheDependency。 要完成此操作的最简单方法是按如下所示在 @ Outcache 指令中指定 SqlDependency 属性的值为：

[!code-aspx[Main](caching/samples/sample8.aspx)]

在上面的 @ OutputCache 指令，为配置 SQL 缓存依赖项*作者*表中*pubs*数据库。 可以通过以分号分隔配置多个依赖项如下所示：

[!code-aspx[Main](caching/samples/sample9.aspx)]

配置 SqlCacheDependency 的另一种方法是以编程方式执行操作。 下面的代码上创建新的 SQL 缓存依赖项*作者*表中*pubs*数据库。

[!code-csharp[Main](caching/samples/sample10.cs)]

以编程方式定义 SQL 缓存依赖项的优势之一是，您可以处理可能发生的任何异常。 例如，如果您试图定义尚未启用通知，请为数据库的 SQL 缓存依赖项**DatabaseNotEnabledForNotificationException**将引发异常。 在这种情况下，您可以尝试通过调用启用通知的数据库**SqlCacheDependencyAdmin.EnableNotifications**方法并将其传递数据库名称。

同样，如果您试图定义尚未启用通知，一个表的 SQL 缓存依赖项**TableNotEnabledForNotificationException**将引发。 然后，可以调用**SqlCacheDependencyAdmin.EnableTableForNotifications**方法并传递它的数据库名称和表名称。

下面的代码示例说明了如何配置 SQL 缓存依赖项时正确配置异常处理。

[!code-csharp[Main](caching/samples/sample11.cs)]

详细信息： [https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>基于查询的 SQL 缓存依赖项 (仅 SQL Server 2005)

当使用 SQL Server 2005 为 SQL 缓存依赖项时，不需要基于轮询的模型。 SQL 缓存依赖项时与 SQL Server 2005 一起使用，通过 SQL 连接到 SQL Server 实例 （不需要任何进一步的配置） 直接通信使用 SQL Server 2005 查询通知。

若要启用基于查询的通知的最简单方法是以声明方式设置进行**SqlCacheDependency**到数据源对象的属性**CommandNotification**并设置**EnableCaching**归于 **，则返回 true**。 使用此方法，则不不需要的任何代码。 如果针对数据源更改执行命令的结果，它将使失效的缓存数据。

下面的示例配置 SQL 缓存依赖项的数据源控件：

[!code-aspx[Main](caching/samples/sample12.aspx)]

在此情况下，如果查询中指定**SelectCommand**返回不同的结果比它按照最初，缓存的结果是无效。

此外可以指定所有数据源通过设置启用 SQL 缓存依赖项**SqlDependency**的属性 **@ OutputCache**指令**CommandNotification**. 下面的示例阐释了这一点。

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> 有关 SQL Server 2005 中的查询通知的详细信息，请参阅 SQL Server 联机丛书。


配置基于查询的 SQL 缓存依赖关系的另一种方法是执行此操作使用 SqlCacheDependency 类以编程方式。 下面的代码示例说明了如何实现这一点。

[!code-csharp[Main](caching/samples/sample14.cs)]

详细信息： [https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>缓存后替换

对页面进行缓存，可以大幅提高 Web 应用程序的性能。 但是，在某些情况下需要要缓存的页的大多数和某些片段中页后，可以是动态的。 例如，如果创建完全是静态的设定时间段内的新闻故事页时，可以设置整个页后，可以缓存。 如果你想要包括的每个页请求更改旋转 ad 标题，包含播发的页的一部分需要是动态的。 若要允许您缓存页面，但动态替换一些内容，可以使用 ASP.NET 缓存后替换。 使用缓存后替换整个页面是输出缓存，并将标记为从缓存中免除的特定部分。 在示例中的广告横幅，AdRotator 控件，可充分利用缓存后替换，以便为每个用户和每个页面刷新时动态创建广告。

有三种方法来实现缓存后替换：

- 以声明方式，使用 Substitution 控件。
- 以编程方式，使用 Substitution 控件 API。
- 隐式地使用 AdRotator 控件。

### <a name="substitution-control"></a>Substitution 控件

ASP.NET Substitution 控件指定是动态创建而不进行缓存的缓存页的部分。 在想要显示的动态内容页上的位置放置了一个替代控件。 在运行时，Substitution 控件调用的 MethodName 属性与指定的方法。 该方法必须返回一个字符串，然后将替换替换控件的内容。 该方法必须包含的页或用户控件的静态方法。 使用 substitution 控件将导致客户端的可缓存性更改为服务器可缓存性，以便不会在客户端上缓存页。 这可确保将来的页面请求调用的方法再次生成动态内容。

### <a name="substitution-api"></a>替换 API

若要以编程方式创建的缓存的页面的动态内容，可以调用[WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx)在页代码中，将其作为参数传递的方法名称的方法。 处理动态内容的创建方法采用单个[HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)参数并返回一个字符串。 返回字符串是在给定位置将替换的内容。 调用 WriteSubstitution 方法而不是以声明方式使用 Substitution 控件的一个优点是，可以调用任意对象，而不是调用的页面或用户控件对象的静态方法的方法。

调用 WriteSubstitution 方法会导致客户端的可缓存性更改为服务器可缓存性，以便不会在客户端上缓存页。 这可确保将来的页面请求调用的方法再次生成动态内容。

### <a name="adrotator-control"></a>AdRotator 控件

服务器控件实现的 AdRotator 在内部支持缓存后替换。 如果将您的页面上的 AdRotator 控件，它会呈现在每个请求，而不考虑是否缓存父页上的唯一播发。 因此，包括 AdRotator 控件的页是仅缓存的服务器端。

## <a name="controlcachepolicy-class"></a>ControlCachePolicy 类

ControlCachePolicy 类允许以编程方式控制的缓存使用用户控件的片段。 ASP.NET 将嵌入的用户控件[BasePartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx)实例。 BasePartialCachingControl 类表示启用了输出缓存的用户控件。

当访问[BasePartialCachingControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx)的属性[PartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx)控件，将始终接收有效的 ControlCachePolicy 对象。 但是，如果您访问[UserControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx)的属性[UserControl](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx)控件，你可以收到有效的 ControlCachePolicy 对象，仅当已包装用户控件BasePartialCachingControl 控件。 如果不换行，该属性返回的 ControlCachePolicy 对象将尝试对其进行操作，因为它不具有关联的 BasePartialCachingControl 时引发异常。 若要确定用户控件实例是否支持缓存不会生成异常，请检查[SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx)属性。

使用 ControlCachePolicy 类是可启用输出缓存的几种方式之一。 以下列表介绍了可用于启用输出缓存的方法：

- 使用[@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)指令，使输出缓存在声明性方案中。
- 使用[PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx)特性，使用户控件代码隐藏文件中的缓存。
- ControlCachePolicy 类用于指定在其中使用 BasePartialCachingControl 实例已启用缓存的使用上述方法之一并使用动态加载的编程方案中的缓存设置[System.Web.UI.TemplateControl.LoadControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx)方法。

可以仅在控件生命周期的 Init 和 PreRender 阶段之间成功操作 ControlCachePolicy 实例。 如果 PreRender 阶段完成之后修改 ControlCachePolicy 对象，ASP.NET 将引发异常，因为后呈现该控件所做的任何更改不能实际影响 （在呈现阶段期间缓存控件） 的缓存设置。 最后，用户控件实例 （和其 ControlCachePolicy 对象） 可用于以编程方式操作时才实际呈现。

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>将更改为缓存配置-&lt;缓存&gt;元素

没有为缓存配置 ASP.NET 2.0 中的多个更改。 &lt;缓存&gt;元素是 ASP.NET 2.0 中的新增功能，允许您在配置文件中进行缓存的配置更改。 以下属性将可用。

| **元素** | **说明** |
| --- | --- |
| **cache** | 可选元素。 定义全局应用程序缓存设置。 |
| **outputCache** | 可选元素。 指定应用程序范围的输出缓存设置。 |
| **outputCacheSettings** | 可选元素。 指定可以应用于应用程序中的页的输出缓存设置。 |
| **sqlCacheDependency** | 可选元素。 为 ASP.NET 应用程序配置 SQL 缓存依赖项。 |

### <a name="the-ltcachegt-element"></a>&lt;缓存&gt;元素

以下属性位于&lt;缓存&gt;元素：

| **特性** | **说明** |
| --- | --- |
| **disableMemoryCollection** | 可选**布尔**属性。 获取或设置一个值，该值指示是否禁用缓存内存收集的计算机处于内存压力下时，会发生。 |
| **disableExpiration** | 可选**布尔**属性。 获取或设置一个值，该值指示是否禁用缓存过期时间。 禁用时，缓存的项不会过期并后台清理过期的缓存项不会发生。 |
| **privateBytesLimit** | 可选**Int64**属性。 获取或设置一个值，该值指示之前在缓存开始刷新应用程序的专用字节的最大大小已过期的项目并尝试回收内存。 此限制包括使用缓存的内存以及正常的内存开销从运行的应用程序。 如果设置为零指示 ASP.NET 将用于确定何时开始回收内存使用自己的试探法。 |
| **percentagePhysicalMemoryUsedLimit** | 可选**Int32**属性。 获取或设置一个值，该值指示在缓存开始刷新之前，应用程序可以使用的计算机的物理内存的最大百分比过期项和尝试回收此内存使用量包括这两个内存缓存也使用的内存为运行的应用程序的正常内存使用情况。 如果设置为零指示 ASP.NET 将用于确定何时开始回收内存使用自己的试探法。 |
| **privateBytesPollTime** | 可选**TimeSpan**属性。 获取或设置一个值，该值的时间间隔轮询应用程序的专用字节内存使用情况。 |

### <a name="the-ltoutputcachegt-element"></a>&lt;OutputCache&gt;元素

以下属性是可用于&lt;outputCache&gt;元素。


|       <strong>特性</strong>        |                                                                                                                                                                                                                                                       <strong>说明</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>enableOutputCache</strong>    |                                                                                                                                                          可选<strong>布尔</strong>属性。 启用/禁用页面输出缓存。 如果禁用，不会缓存页而不考虑以编程方式或声明性设置。 默认值是<strong>，则返回 true</strong>。                                                                                                                                                           |
|  <strong>enableFragmentCache</strong>   |                                                可选<strong>布尔</strong>属性。 启用/禁用应用程序片段缓存。 如果禁用，不会缓存页而不考虑[@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)指令或缓存使用配置文件。 包含指示，上游代理服务器，以及浏览器客户端不应尝试向缓存页面输出缓存控制标头。 默认值是<strong>false</strong>。                                                 |
| <strong>sendCacheControlHeader</strong> |                                                                                                                                                      可选<strong>布尔</strong>属性。 获取或设置一个值，该值指示是否<strong>缓存的控件： private</strong>标头由输出缓存模块发送默认情况下。 默认值是<strong>false</strong>。                                                                                                                                                      |
|      <strong>omitVaryStar</strong>      | 可选<strong>布尔</strong>属性。 启用/禁用发送 Http"<strong>Vary: \</strong ><em>"在响应中的标头。如果使用默认设置为 false，"</em>* Vary: \* <strong>"标头发送为输出缓存页。Vary 标头发送时，它允许不同版本要缓存基于 Vary 标头中指定的内容。例如，<em>变化： 用户的代理</em>将存储不同版本的基于发出请求的用户代理的页面。默认值为 * * false</strong>。 |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;OutputCacheSettings&gt;元素

&lt;OutputCacheSettings&gt;元素允许按前面所述的缓存配置文件的创建。 唯一子级元素&lt;outputCacheSettings&gt;元素是&lt;outputCacheProfiles&gt;元素来配置缓存配置文件。

### <a name="the-ltsqlcachedependencygt-element"></a>&lt;SqlCacheDependency&gt;元素

以下属性是可用于&lt;sqlCacheDependency&gt;元素。

| **特性** | **说明** |
| --- | --- |
| **enabled** | 所需**布尔**属性。 指示轮询更改。 |
| **pollTime** | 可选**Int32**属性。 设置与 SqlCacheDependency 轮询数据库表更改的频率。 此值对应于连续两次轮询之间的毫秒数。 它不能设置为小于 500 毫秒。 默认值为 1 分钟。 |

### <a name="more-information"></a>详细信息

没有应注意的有关缓存配置一些其他信息。

- 如果未设置辅助进程专用字节限制，将使用缓存的下列限制之一： 

    - x86 2 GB: 800 MB 或 60%的物理 RAM 小者为准
    - x86 3 GB: 1800 MB 或 60%的物理 RAM 小者为准
    - 64: 1 terabyte 或 60%的物理 RAM 小者为准
- 如果这两个工作进程专用字节限制以及&lt;缓存 privateBytesLimit /&gt;进行设置，缓存将使用的两个最小值。
- 就像在 1.x 中，我们删除缓存项，并调用 GC。收集以下两个原因： 

    - 我们非常接近专用字节限制
    - 可用内存较接近或低于 10%
- 您可以有效地禁用剪裁，通过设置缓存的可用内存不足的情况&lt;缓存 percentagePhysicalMemoryUseLimit /&gt;到 100 之间。
- 与 1.x 不同，2.0 将挂起的剪裁和收集调用最后一个 GC。收集未减少专用字节或超过 1%（缓存） 内存限制的托管堆的大小。

## <a name="lab1-custom-cache-dependencies"></a>Lab1： 自定义缓存依赖项

1. 创建新的 Web 站点。
2. 添加名为 cache.xml 的新 XML 文件并将其保存到 Web 应用程序的根目录。
3. 将以下代码添加到页\_加载 default.aspx 代码隐藏中的方法： 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. 以下代码添加到 default.aspx 源视图中的顶部： 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. 浏览 Default.aspx。 时间的说是什么？
6. 刷新浏览器。 时间的说是什么？
7. 打开 cache.xml 并添加以下代码： 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. 保存 cache.xml。
9. 刷新浏览器。 时间的说是什么？
10. 说明为什么而不是显示以前缓存的值更新时间：

## <a name="lab-2-using-polling-based-cache-dependencies"></a>实验室 2： 使用基于轮询的缓存依赖项

此实验室中使用可对通过 GridView 和 DetailsView 控件 Northwind 数据库中的数据进行编辑前一模块中创建的项目。

1. 在 Visual Studio 2005 中打开该项目。
2. 运行 aspnet\_regsql 实用工具对 Northwind 数据库，若要启用的数据库和产品表。 使用以下命令从 Visual Studio 命令提示符： 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. 以下代码添加到 web.config 文件： 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. 添加名为 showdata.aspx 的新 web 窗体。
5. @ Outputcache 指令以下内容添加到 showdata.aspx 页： 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. 将以下代码添加到页\_showdata.aspx 负载： 

    [!code-html[Main](caching/samples/sample21.html)]
7. 将新的 SqlDataSource 控件添加到 showdata.aspx 并将其配置为使用 Northwind 数据库连接。 单击下一步。
8. 选择产品名称和产品 id 复选框，然后单击下一步。
9. 单击完成。
10. 将新 GridView 添加到 showdata.aspx 页。
11. 从下拉列表中选择 sqldatasource1。
12. 保存并浏览 showdata.aspx。 记下显示的时间。
