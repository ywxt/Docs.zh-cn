---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 和 Visual Studio 2010 Web 开发概述 |Microsoft Docs
author: rick-anderson
description: 本文档概述了有关 ASP.NET 中的.net Framework 4 和 Visual Studio 2010 中包含的许多新功能。
ms.author: aspnetcontent
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: 5c7aa95b18bc0a97f42cc981476c110830286fa5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829038"
---
<a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a>ASP.NET 4 和 Visual Studio 2010 Web 开发概述
====================
> 本文档概述了有关 ASP.NET 中的.net Framework 4 和 Visual Studio 2010 中包含的许多新功能。
> 
> [下载此白皮书](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)


**内容**

**[Core Services](#0.2__Toc253429238 "_Toc253429238")**  
[Web.config 文件重构](#0.2__Toc253429239 "_Toc253429239")  
[可扩展的输出缓存](#0.2__Toc253429240 "_Toc253429240")  
[自动启动 Web 应用程序](#0.2__Toc253429241 "_Toc253429241")  
[永久重定向页面](#0.2__Toc253429242 "_Toc253429242")  
[收缩会话状态](#0.2__Toc253429243 "_Toc253429243")  
[扩展该范围的允许的 Url](#0.2__Toc253429244 "_Toc253429244")  
[可扩展请求验证](#0.2__Toc253429245 "_Toc253429245")  
[对象缓存和对象缓存扩展性](#0.2__Toc253429246 "_Toc253429246")  
[可扩展的 HTML、 URL 和编码的 HTTP 标头](#0.2__Toc253429247 "_Toc253429247")  
[在单个辅助进程中的单个应用程序的性能监视](#0.2__Toc253429248 "_Toc253429248")  
[Multi-Targeting](#0.2__Toc253429249 "_Toc253429249")

**[Ajax](#0.2__Toc253429250 "_Toc253429250")**  
[使用 Web 窗体和 MVC 包含 jQuery](#0.2__Toc253429251 "_Toc253429251")  
[内容交付网络支持](#0.2__Toc253429252 "_Toc253429252")  
[ScriptManager 显式脚本](#0.2__Toc253429253 "_Toc253429253")

**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**  
[设置使用 Page.MetaKeywords 和 Page.MetaDescription 属性的 Meta 标记](#0.2__Toc253429257 "_Toc253429257")  
[对单个控件启用视图状态](#0.2__Toc253429258 "_Toc253429258")  
[浏览器功能将变为](#0.2__Toc253429259 "_Toc253429259")  
[ASP.NET 4 中的路由](#0.2__Toc253429260 "_Toc253429260")  
[设置客户端 Id](#0.2__Toc253429261 "_Toc253429261")  
[保持在数据控件中的行选择](#0.2__Toc253429262 "_Toc253429262")  
[ASP.NET 图表控件](#0.2__Toc253429263 "_Toc253429263")  
[用 QueryExtender 控件筛选数据](#0.2__Toc253429264 "_Toc253429264")  
[Html 编码的代码表达式](#0.2__Toc253429265 "_Toc253429265")  
[项目模板的更改](#0.2__Toc253429266 "_Toc253429266")  
[CSS 改进](#0.2__Toc253429267 "_Toc253429267")  
[隐藏 div 元素周围隐藏字段](#0.2__Toc253429268 "_Toc253429268")  
[模板化控件的呈现外部表](#0.2__Toc253429269 "_Toc253429269")  
[ListView 控件增强功能](#0.2__Toc253429270 "_Toc253429270")  
[CheckBoxList 和 RadioButtonList 控件增强功能](#0.2__Toc253429271 "_Toc253429271")  
[菜单控件改进](#0.2__Toc253429272 "_Toc253429272")  
[向导和 CreateUserWizard 控件 56](#0.2__Toc253429273 "_Toc253429273")

**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**  
[区域支持](#0.2__Toc253429275 "_Toc253429275")  
[数据注释属性验证支持](#0.2__Toc253429276 "_Toc253429276")  
[模板化帮助器](#0.2__Toc253429277 "_Toc253429277")

**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**  
[对于现有项目中启用动态数据](#0.2__Toc253429279 "_Toc253429279")  
[DynamicDataManager 控件声明性语法](#0.2__Toc253429280 "_Toc253429280")  
[实体模板](#0.2__Toc253429281 "_Toc253429281")  
[新的字段模板的 Url 和电子邮件地址](#0.2__Toc253429282 "_Toc253429282")  
[创建链接与 DynamicHyperLink 控件](#0.2__Toc253429283 "_Toc253429283")  
[对数据模型中继承的支持](#0.2__Toc253429284 "_Toc253429284")  
[对多对多关系 （仅适用于实体框架） 的支持](#0.2__Toc253429285 "_Toc253429285")  
[新属性来控制显示和支持枚举](#0.2__Toc253429286 "_Toc253429286")  
[对筛选器的增强支持](#0.2__Toc253429287 "_Toc253429287")

**[Visual Studio 2010 Web 开发改进](#0.2__Toc253429288 "_Toc253429288")**  
[CSS 兼容性得到改进](#0.2__Toc253429289 "_Toc253429289")  
[HTML 和 JavaScript 代码段](#0.2__Toc253429290 "_Toc253429290")  
[JavaScript IntelliSense 增强功能](#0.2__Toc253429291 "_Toc253429291")

**[Web 应用程序部署使用 Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**  
[Web 打包](#0.2__Toc253429293 "_Toc253429293")  
[Web.config Transformation](#0.2__Toc253429294 "_Toc253429294")  
[数据库部署](#0.2__Toc253429295 "_Toc253429295")  
[单击发布为 Web 应用程序](#0.2__Toc253429296 "_Toc253429296")  
[Resources](#0.2__Toc253429297 "_Toc253429297")

**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a>核心服务

ASP.NET 4 引入了许多的功能，可提高核心 ASP.NET 服务，如输出缓存和会话状态存储。

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a>重构的 Web.config 文件

`Web.config`文件，其中包含配置为 Web 应用程序已增长得多在过去的几个版本的.NET framework 已添加新功能，如 Ajax，如路由，以及与 IIS 7 的集成。 这具有就很难配置或启动新的 Web 应用程序而无需 Visual Studio 之类的工具。 只 NET Framework 4，主要的配置元素已被移动到`machine.config`文件和应用程序现在将继承这些设置。 这允许`Web.config`ASP.NET 4 应用程序可以为空，或者包含仅的以下行，其指定 Visual Studio 的哪个版本的应用程序所面向的框架中的文件：

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a>可扩展的输出缓存

自 ASP.NET 1.0 发布时，输出缓存已启用开发人员能够在内存中存储生成的页面、 控件和 HTTP 响应输出。 在后续的 Web 请求，ASP.NET 可以提供内容更快地通过检索生成的输出从内存而不是重新生成从零开始的输出。 但是，这种方法有一个限制，生成的内容始终具有要存储在内存中，并在遇到大量流量的服务器上，使用输出缓存的内存可以竞争与其它部分中的 Web 应用程序的内存要求。

ASP.NET 4 将添加一个扩展点为输出缓存，使你能够配置一个或多个自定义输出缓存提供程序。 输出缓存提供程序可以使用任何存储机制来保持 HTML 内容。 这就可以为不同的持久性机制，它可以包括本地或远程磁盘，云存储，创建自定义输出缓存提供程序和分布式缓存引擎。

作为派生新类创建自定义输出缓存提供程序*System.Web.Caching.OutputCacheProvider*类型。 然后，可以配置中的提供程序`Web.config`使用新的文件*提供程序*的子节*outputCache*元素，如下面的示例中所示：

[!code-xml[Main](overview/samples/sample2.xml)]

默认情况下，在 ASP.NET 4 中，所有 HTTP 响应，呈现的页面和控件使用内存中输出缓存中，如下所示在上一示例中，其中*defaultProvider*属性设置为 AspNetInternalProvider。 你可以通过指定不同的提供程序名称的 Web 应用程序使用的默认输出缓存提供程序*defaultProvider*。

此外，可以选择不同的输出缓存提供程序每个控件和每个请求。 若要选择不同的 Web 用户控件的不同输出缓存提供程序的最简单方法是以声明方式使用新进行*providerName*属性中的控件指令，如下面的示例中所示：

[!code-aspx[Main](overview/samples/sample3.aspx)]

指定的 HTTP 请求的不同的输出缓存提供程序需要更多工作。 而不是以声明方式指定提供程序，则重写的新*GetOuputCacheProviderName*中的方法`Global.asax`文件以编程方式指定要用于特定请求的提供程序。 下面的示例演示如何执行此操作。

[!code-csharp[Main](overview/samples/sample4.cs)]

通过添加到 ASP.NET 4 的输出缓存提供程序可扩展性，现在可以为您的网站追求更主动和更智能的输出缓存策略。 例如，现可以缓存页面在磁盘有较低流量时缓存在内存中，站点的"前 10 个"页。 或者，您可以缓存呈现页中，每个不同的组合，但使用分布式的缓存，以便从前端 Web 服务器卸载的内存占用情况。

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a>自动启动 Web 应用程序

某些 Web 应用程序需要加载大量数据或执行成本高昂的初始化处理就可为第一个请求提供服务。 在 ASP.NET 的早期版本中，对于这些情况下您必须设计自定义方法"唤醒"ASP.NET 应用程序，然后运行过程中的初始化代码*应用程序\_负载*中的方法`Global.asax`文件。

名为的新可伸缩性功能*自动启动*，直接地址提供了此方案的 ASP.NET 4 运行时在 Windows Server 2008 R2 上的 IIS 7.5 上。 自动启动功能提供了启动应用程序池、 初始化 ASP.NET 应用程序，以及然后接受 HTTP 请求的控制的方法。

> [!NOTE] 
> 
> 用于 IIS 7.5 的 IIS 应用程序预热模块
> 
> 用于 IIS 7.5，IIS 团队已发布应用程序预热模块的第一个 beta 版测试的版本。 这样，您甚至比前面所述的应用程序正在预热。 而不是编写自定义代码，您指定资源的 Url 以 Web 应用程序接受来自网络的请求之前执行。 在 IIS 服务的启动期间发生此预热 (如果配置的 IIS 应用程序池*AlwaysRunning*) 和 IIS 工作进程回收时。 在回收，过程将继续旧的 IIS 工作进程，以执行请求，直到完全预热新生成的工作进程，以便应用程序出现任何中断或 unprimed 缓存导致的其他问题。 请注意，此模块的工作原理与任何版本的 ASP.NET 2.0 版开始。
> 
> 有关详细信息，请参阅[应用程序预热](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net)IIS.net 网站上。 有关演示如何使用预热功能的演练，请参阅[开始使用 IIS 7.5 应用程序预热模块](https://www.iis.net/learn/manage)IIS.net 网站上。


若要使用自动启动功能，IIS 管理员设置了应用程序池在 IIS 7.5，通过使用中的以下配置为自动启动`applicationHost.config`文件：

[!code-xml[Main](overview/samples/sample5.xml)]

由于单个应用程序池可以包含多个应用程序，指定单个应用程序通过使用中的以下配置为自动启动`applicationHost.config`文件：

[!code-xml[Main](overview/samples/sample6.xml)]

IIS 7.5 的 IIS 7.5 服务器是冷启动或单个应用程序池被回收时，使用中的信息`applicationHost.config`文件以确定哪个 Web 应用程序都需要为自动启动。 对于每个应用程序标记为自动启动，IIS7.5 发送请求到 ASP.NET 4 中启动应用程序中的状态在此期间应用程序暂时不接受 HTTP 请求。 当它处于此状态时，ASP.NET 实例定义的类型化*serviceAutoStartProvider*属性 （如在前面的示例所示） 并调用到其公共入口点。

使用必要的入口点中实现创建托管的自动启动类型*IProcessHostPreloadClient*接口，如以下示例所示：

[!code-csharp[Main](overview/samples/sample7.cs)]

在运行代码在初始化后*预加载*方法和方法返回时，ASP.NET 应用程序已准备好处理请求。

添加了对 IIS.5 和 ASP.NET 4 自动启动，您就具有有明确定义的执行成本高昂的应用程序初始化之前处理的第一个 HTTP 请求方法。 例如，可以使用新的自动启动功能初始化应用程序及然后指示应用程序已初始化并准备好接受 HTTP 流量负载均衡器。

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a>永久重定向页面

它是在 Web 应用程序随着时间推移，这可能会导致搜索引擎中的过时链接会累积移动页面和其他内容周围的常见做法。 在 ASP.NET 中，开发人员具有传统上处理对旧 Url 的请求通过使用通过使用*Response.Redirect*方法以将请求转发到新 URL。 但是，*重定向*方法发出 HTTP 302 已找到 （临时重定向） 响应，这会导致额外的 HTTP 往返当用户尝试访问的旧 Url。

添加一个新的 ASP.NET 4 *RedirectPermanent*帮助器方法，可以方便地对问题 HTTP 301 已永久移动响应，如以下示例所示：

[!code-csharp[Main](overview/samples/sample8.cs)]

搜索引擎和其他识别永久重定向的用户代理将存储内容，它消除不必要的往返行程所做的临时重定向的浏览器与相关联的新 URL。

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a>收缩会话状态

ASP.NET 提供的 Web 场中存储会话状态的两个默认选项： 调用的进程外会话状态服务器的会话状态提供程序和 Microsoft SQL Server 数据库中存储数据的会话状态提供程序。 由于这两个选项涉及存储 Web 应用程序的工作进程之外的状态信息，会话状态必须进行序列化之前将其发送到远程存储。 具体取决于多少开发人员将保存在会话状态的信息，序列化数据的大小可以变得很大。

ASP.NET 4 引入了新的压缩选项，这两种不同的进程外会话状态提供程序。 当*compressionEnabled*下面的示例中所示的配置选项设置为*true*，ASP.NET 将压缩 （和解压缩） 使用.NET Framework序列化的会话状态*System.IO.Compression.GZipStream*类。

[!code-xml[Main](overview/samples/sample9.xml)]

通过将新属性的简单添加`Web.config`文件，具有 Web 服务器上的备用 CPU 周期的应用程序可以实现显著减小的大小的序列化会话状态数据。

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a>扩展该范围允许 Url

ASP.NET 4 引入了新选项来扩展应用程序 Url 的大小。 ASP.NET 的早期版本约束为 260 个字符，NTFS 文件路径限制基于 URL 路径长度。 在 ASP.NET 4 中，您可以选择增加 （或减少） 根据您的应用程序，此限制使用两个新*httpRuntime*配置特性。 下面的示例显示了这些新属性。

[!code-xml[Main](overview/samples/sample10.xml)]

若要允许较长或更短路径 （不包括协议、 服务器名称和查询字符串的 URL 的部分），请修改*[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 属性。 若要允许较长或更短的查询字符串，请修改的值*[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 属性。

ASP.NET 4 还可配置的 URL 字符检查使用的字符。 在 ASP.NET 中 URL 的路径部分找到无效的字符，它将拒绝该请求，并发出 HTTP 400 错误。 在以前版本的 ASP.NET 中，URL 字符检查的限制为一组固定的字符。 在 ASP.NET 4 中，你可以自定义使用新的有效字符集*requestPathInvalidChars*的属性*httpRuntime*配置元素，如下面的示例中所示：

[!code-xml[Main](overview/samples/sample11.xml)]

默认情况下<em>requestPathInvalidChars</em>属性定义为无效的八个字符。 (分配给在字符串中<em>requestPathInvalidChars</em>默认情况下<em>，</em>小于 (&lt;)、 大于 (&gt;)，和 and 符 (&amp;) 字符编码的因为`Web.config`文件是一个 XML 文件。)根据需要可以自定义无效字符的组。

> [!NOTE]
> 请注意，ASP.NET 4 始终拒绝包含 0x00 到 0x1F 的 ASCII 范围中的字符的 URL 路径，因为这些无效的 URL 字符中的 IETF RFC 2396 定义 ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt))。 在 Windows Server 版本上运行 IIS 6 或更高版本，http.sys 协议设备驱动程序自动拒绝 Url 有了这些字符。


<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a>可扩展请求验证

ASP.NET 请求验证搜索字符串的常用的传入 HTTP 请求的数据中跨站点脚本 (XSS) 攻击。 如果找到潜在的 XSS 字符串，请求验证标记可疑字符串并返回错误。 仅当它找到的 XSS 攻击中使用的最常见字符串时，内置请求验证将返回错误。 此前在尝试进行 XSS 验证更为严格导致误报过多。 但是，客户可能希望更加严格，或反之可能想要有意放宽 XSS 请求验证检查的特定页面，或者为特定类型的请求。

在 ASP.NET 4 中，请求验证功能进行扩展，以便您可以使用自定义请求验证逻辑。 若要扩展请求验证，您创建派生自新的类*System.Web.Util.RequestValidator*类型，，并配置应用程序 (在*httpRuntime* 部分`Web.config`文件) 以使用自定义的类型。 下面的示例演示如何配置自定义请求验证类：

[!code-xml[Main](overview/samples/sample12.xml)]

新*requestValidationType*特性需要指定提供自定义请求验证的类的一个标准的.NET Framework 类型标识符字符串。 对于每个请求，ASP.NET 调用以处理每条传入 HTTP 请求数据的自定义类型。 入站 URL、 所有的 HTTP 标头 （cookie 和自定义标头），和的实体正文都可用于检查由自定义请求验证类在下面的示例所示：

[!code-csharp[Main](overview/samples/sample13.cs)]

没有要检查传入的 HTTP 数据一段的情况下，请求验证类可以进行回退，让 ASP.NET 默认请求验证运行只需调用*基。IsValidRequestString。*

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a>对象缓存和对象缓存扩展性

自首次发布以来 ASP.NET 就提供了强大的内存中对象缓存 (*System.Web.Caching.Cache*)。 缓存实现已很常见，它具有非 Web 应用程序中已使用。 但是，很困难的 Windows 窗体或 WPF 应用程序，包括对引用`System.Web.dll`只是为了能够使用 ASP.NET 对象缓存。

若要使缓存可供所有应用程序，.NET Framework 4 引入了新的程序集、 新的命名空间、 某些基本类型和具体的缓存实现。 新`System.Runtime.Caching.dll`程序集包含在一个新的缓存 API *System.Runtime.Caching*命名空间。 该命名空间包含两个类的核心集：

- 为构建任何类型的自定义缓存实现提供了基础的抽象类型。
- 具体的内存中对象缓存实现 ( *system.runtime.caching.memorycache 有关的问题*类)。

新*MemoryCache*类在 ASP.NET 缓存中，紧密地建模并共享大量的内部缓存引擎逻辑与 ASP.NET。 尽管在公共的缓存 Api *System.Runtime.Caching*已更新，以支持开发的自定义缓存，如果您用过 ASP.NET*缓存*对象，您会发现在熟悉的概念新的 Api。

新的深入讨论*MemoryCache*类和支持性的基础 Api 需要整个文档。 但是，下面的示例揭示了新的缓存 API 的工作原理。 该示例针对没有任何依赖项的 Windows 窗体应用程序的编写上`System.Web.dll`。

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a>可扩展的 HTML、 URL 和编码的 HTTP 标头

在 ASP.NET 4 中，您可以创建以下常见文本编码任务的自定义编码例程：

- HTML 编码。
- URL 编码。
- HTML 特性编码。
- 编码出站 HTTP 标头。

可以通过从新派生来创建自定义编码器*System.Web.Util.HttpEncoder*类型，然后配置 ASP.NET 使用中的自定义类型*httpRuntime*一部分`Web.config`文件中，为以下示例中所示：

[!code-xml[Main](overview/samples/sample15.xml)]

配置自定义编码器后，ASP.NET 会自动调用自定义编码实现只要公共编码的方法*System.Web.HttpUtility*或*System.Web.HttpServerUtility*的类称为。 这允许创建自定义编码器实现主动字符编码，尽管 Web 开发团队的其余部分仍使用公共 ASP.NET 编码 Api 的 Web 开发团队的一个部分。 通过集中配置中的自定义编码器*httpRuntime*元素，可以保证从公共 ASP.NET 编码 Api 的所有文本编码呼叫都会都路由通过自定义编码器。

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a>在单个辅助进程中的单个应用程序的性能监视

为了提高的可以在一台服务器承载的网站的数量，很多宿主在单个辅助进程中运行多个 ASP.NET 应用程序。 但是，如果多个应用程序使用单个共享的辅助进程，很难服务器管理员可以确定单个应用程序出现了问题。

ASP.NET 4 利用由 CLR 引入的新资源监视功能。 若要启用此功能，可以添加到下面的 XML 配置片段`aspnet.config`配置文件。

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> 请注意`aspnet.config`文件是在安装.NET Framework 的目录中。 它不是`Web.config`文件。


当*appDomainResourceMonitoring*启用功能，两个新的性能计数器可用于中的"ASP.NET 应用程序"性能类别：*托管处理器时间百分比*并*托管内存使用*。 这两个这些性能计数器使用新的 CLR 应用程序域资源管理功能来跟踪估计的 CPU 时间和各个 ASP.NET 应用程序的托管的内存使用率。 因此，与 ASP.NET 4 中，管理员现在可以在单个辅助进程中运行的单个应用程序的资源消耗的更精细视图。

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a>多目标

可以创建面向特定版本的.NET framework 的应用程序。 在 ASP.NET 4 中，在新的属性*编译*元素的`Web.config`文件允许您面向.NET Framework 4 及更高版本。 如果你明确指定目标.NET Framework 4 中，并且包含中的可选元素`Web.config`如的项的文件*system.codedom*，这些元素必须是正确的.NET Framework 4。 (如果你不明确的目标.NET Framework 4，从中的条目缺乏推断的目标框架`Web.config`文件。)

下面的示例演示如何使用*targetFramework*属性中*编译*元素的`Web.config`文件。

[!code-xml[Main](overview/samples/sample17.xml)]

请注意有关的目标.NET Framework 的特定版本的以下信息：

- 在.NET Framework 4 应用程序池中，ASP.NET 生成系统假定在.NET Framework 4 为目标如果`Web.config`文件不包括*targetFramework*属性或如果`Web.config`找不到文件。 （您可能需要对应用程序，使其运行.NET Framework 4 下进行编码更改。）
- 如果包括*targetFramework*属性，并且如果*system.codeDom*中定义元素`Web.config`文件，此文件必须针对.NET Framework 4 包含正确的条目。
- 如果使用的*aspnet\_编译器*命令将其预编译应用程序 （例如在生成环境），则必须使用正确版本的*aspnet\_编译器*目标框架的命令。 使用与.NET Framework 2.0 （%windir%\microsoft.net\framework\v2.0.50727) 随附的编译器进行编译的.NET Framework 3.5 及更早版本。 使用与.NET Framework 4 附带的编译器来编译创建的应用程序使用该框架或更高版本。
- 在运行时，编译器将使用的计算机安装的最新 framework 程序集 (并因此在 GAC 中)。 如果对 framework 更高版本进行了更新 （例如，安装假设版本 4.1），你将能够即使在较新版本的 framework 中使用功能*targetFramework*属性以较低版本为目标（例如 4.0)。 (但是，在 Visual Studio 2010，或者在使用中的设计时*aspnet\_编译器*命令时，使用 framework 的较新功能将导致编译器错误)。

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a>Ajax

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a>jQuery 与 Web 窗体和 MVC 包含

Web 窗体和 MVC 的 Visual Studio 模板包括开放源代码 jQuery 库。 当您创建新网站或项目时，创建包含以下 3 个文件的脚本文件夹：

- jQuery 1.4.1.js – 用户可读，unminified 的 jQuery 库的版本。
- jQuery-14.1.min.js – 的缩小版 jQuery 库。
- jQuery-1.4.1-vsdoc.js – jQuery 库的 Intellisense 文档文件。

在开发的应用程序时包括 jQuery 的 unminified 的版本。 包括的缩小的版 jQuery 用于生产应用程序。

例如，以下 Web 窗体页说明了如何使用 jQuery，若要更改为黄色，当它们具有焦点时的 ASP.NET TextBox 控件的背景色。

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a>内容交付网络支持

Microsoft Ajax 内容交付网络 (CDN)，可轻松地将 ASP.NET Ajax 和 jQuery 脚本添加到 Web 应用程序。 例如，可以开始使用 jQuery 库，只需通过添加`<script>`页指向 Ajax.microsoft.com 如下标记：

[!code-html[Main](overview/samples/sample19.html)]

通过利用 Microsoft Ajax CDN，可以显著改进 Ajax 应用程序的性能。 Microsoft Ajax CDN 的内容缓存在位于世界各地的服务器上。 此外，Microsoft Ajax CDN 使浏览器可以位于不同域中的网站重用缓存的 JavaScript 文件。

Microsoft Ajax 内容交付网络支持 SSL (HTTPS)，以防您需要使用安全套接字层为网页提供服务。

当 CDN 不可用时，请实现回退。 测试回退。

若要了解有关 Microsoft Ajax CDN 的详细信息，请访问以下网站：

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

ASP.NET ScriptManager 支持 Microsoft Ajax CDN。 只需通过设置一个属性，EnableCdn 属性，可以从 CDN 检索所有 ASP.NET 框架 JavaScript 文件：

[!code-aspx[Main](overview/samples/sample20.aspx)]

将 EnableCdn 属性设置为值为 true 后，ASP.NET 框架将从 CDN 包括用于验证和 UpdatePanel 的所有 JavaScript 文件检索所有 ASP.NET 框架 JavaScript 文件。 设置此属性可以对 web 应用程序的性能具有重大影响。

可以通过使用 WebResource 属性对 JavaScript 文件中设置的 CDN 路径。 新的 CdnPath 属性指定当 EnableCdn 属性设置为值为 true 时，使用 CDN 的路径：

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a>ScriptManager 显式脚本

在过去，如果您使用过 ASP.NET ScriptManger 然后需要加载整个整体化 ASP.NET Ajax 库。 通过利用新的 ScriptManager.AjaxFrameworkMode 属性，可以控制完全加载 ASP.NET Ajax 库的组件，并加载 ASP.NET Ajax 库所需的组件。

ScriptManager.AjaxFrameworkMode 属性可以设置为以下值：

- 已启用-指定 ScriptManager 控件自动包括 MicrosoftAjax.js 脚本文件，它是所有核心框架脚本 （旧版行为） 的合并的脚本文件。
- 禁用-指定所有 Microsoft Ajax 脚本功能将被都禁用，ScriptManager 控件不自动引用任何脚本。
- 显式-指定将显式包含对页面所需的单独框架核心脚本文件的脚本引用，并确保将包含对每个脚本文件所需的依赖项的引用。

例如，如果 AjaxFrameworkMode 属性设置为显式的值，然后可以指定所需的特定 ASP.NET Ajax 组件脚本：

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a>Web Forms — Web 窗体

Web 窗体自 ASP.NET 1.0 发布以来已在 ASP.NET 中的核心功能。 在此区域中的 ASP.NET 4 中，其中包括了许多增强功能：

- 若要设置的功能*meta*标记。
- 更好地控制视图状态。
- 可使用浏览器功能的更简单方法。
- 支持使用 ASP.NET Web 窗体路由。
- 更好地控制生成的 Id。
- 可以保存在数据控件中选定的行。
- 更好地控制中呈现的 HTML *FormView*并*ListView*控件。
- 筛选数据源控件的支持。

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a>设置使用 Page.MetaKeywords 和 Page.MetaDescription 属性的 Meta 标记

ASP.NET 4 添加到两个属性*页上*类， *MetaKeywords*并*MetaDescription*。 这两个属性表示对应*meta*标记在网页中，如下面的示例中所示：

[!code-aspx[Main](overview/samples/sample23.aspx)]

这两个属性的工作方式相同的方式页*标题*属性。 它们遵循以下规则：

1. 如果有没有*元*标记中*head*与属性名称相匹配的元素 (即命名 ="关键字" *Page.MetaKeywords*和名称 = "说明"*Page.MetaDescription*，不设置这些属性的含义)，则*元*标记将在呈现时添加到页面。
2. 如果已有*meta*带这些名称的标记，这些属性的含义相同 get 和 set 方法的现有标记的内容。

可以在运行时，它可让你从数据库或其他源获取内容并允许您设置动态内容描述的标记中设置这些属性是特定页。

您还可以设置*关键字*并*说明*中的属性 *@ Page*指令顶部的 Web 窗体页标记中，如以下示例所示：

[!code-aspx[Main](overview/samples/sample24.aspx)]

这将重写*meta*标记已在页中声明的内容 （如果有）。

说明的内容*meta*标记用于改善搜索列出 Google 中的预览。 (有关详细信息，请参阅[提高与元说明功能改进的代码段](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html)Google 网站管理员中心博客上。)Google 和 Windows Live Search 不使用的关键字的内容的任何内容，但其他搜索引擎可能。 有关详细信息，请参阅[Meta 关键字建议](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php)搜索引擎指南网站上。

这些新属性是一个简单的功能，但它们将保存您的要求，以将它们手动添加或编写你自己的代码创建*meta*标记。

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a>对单个控件启用视图状态

默认情况下，页的页上的每个控件可能存储视图状态，即使它不是应用程序需要的结果与启用了视图状态。 视图状态数据包含在标记中，页面将生成并增大到客户端发送一个页面和回发所需的时间量。 存储不必要的更多视图状态可能会导致性能明显下降。 在 ASP.NET 的早期版本中，开发人员可以禁用单个控件的视图状态，以减少页面大小，但必须明确为单独的控件。 在 ASP.NET 4 中，包括 Web 服务器控件*ViewStateMode*允许您默认情况下禁用视图状态，然后启用它仅用于需要在页中的控件的属性。

*ViewStateMode*属性采用枚举具有三个值：*已启用*，*禁用*，以及*继承*。 *已启用*启用视图状态的该控件和设置为任何子控件*继承*或有任何设置。 *已禁用*禁用视图状态，并*继承*指定该控件使用*ViewStateMode*设置从父控件。

下面的示例演示如何*ViewStateMode*属性工作原理。 标记和代码中的以下页面的控件包括的值*ViewStateMode*属性：

[!code-aspx[Main](overview/samples/sample25.aspx)]

如您所见，代码将禁用 PlaceHolder1 控件的视图状态。 子 label1 控件继承此属性的值 (*Inherit*是默认值为*ViewStateMode*控件。)，从而节省没有视图状态。 PlaceHolder2 掌控*ViewStateMode*设置为*已启用*，因此 label2 继承此属性并保存视图状态。 在首次加载页面时*文本*属性均*标签*控件设置为字符串"[DynamicValue]"。

这些设置的效果是，如果页面可加载第一次，下面的输出将显示在浏览器中：

已禁用 `: [DynamicValue]`

已启用：`[DynamicValue]`

在回发后但是，将显示以下输出：

已禁用 `: [DeclaredValue]`

已启用：`[DynamicValue]`

Label1 控件 (其*ViewStateMode*值设置为*禁用*) 具有不会保留在代码中设置为它的值。 但是，label2 控制 (其*ViewStateMode*值设置为*已启用*) 已保留其状态。

您还可以设置*ViewStateMode*中 *@ Page*指令，如以下示例所示：

[!code-aspx[Main](overview/samples/sample26.aspx)]

*页*类是只是另一个控件，它是作为页面中的所有其他控件的父控件。 默认值*ViewStateMode*是*已启用*有关的实例*页*。 因为默认为控件*继承*，控件将继承*已启用*属性值，除非您设置*ViewStateMode*页或控制级别。

值*ViewStateMode*属性确定是否视图状态才*EnableViewState*属性设置为*true*。 如果*EnableViewState*属性设置为*false*，将不保留视图状态即使*ViewStateMode*设置为*已启用*。

此功能的良好用法是与*ContentPlaceHolder*主页面，可以在其中设置中的控件*ViewStateMode*到*禁用*主数据页上，然后启用它为单独*ContentPlaceHolder*又可以包含需要的控件的控件视图状态。

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a>对浏览器功能的更改

ASP.NET 确定用户用于浏览您的站点通过使用名为的功能的浏览器的功能*浏览器功能*。 浏览器功能由*HttpBrowserCapabilities*对象 (由公开*Request.Browser*属性)。 例如，可以使用*HttpBrowserCapabilities*对象，以确定的类型和版本的当前浏览器是否支持 JavaScript 的特定版本。 或者，可以使用*HttpBrowserCapabilities*对象，以确定请求是否来自移动设备。

*HttpBrowserCapabilities*对象由一组的浏览器定义文件驱动。 这些文件包含特定的浏览器的功能信息。 在 ASP.NET 4 中，这些浏览器定义文件已更新为包含有关最近引入的浏览器和设备如 Google Chrome、 研究运动 BlackBerry 智能手机和 Apple iPhone 中的信息。

以下列表显示新的浏览器定义文件：

- *blackberry.browser*
- *chrome.browser*
- *Default.browser*
- *firefox.browser*
- *gateway.browser*
- *generic.browser*
- *ie.browser*
- *iemobile.browser*
- *iphone.browser*
- *opera.browser*
- *safari.browser*

#### <a name="using-browser-capabilities-providers"></a>使用浏览器功能提供程序

在 ASP.NET 3.5 版 Service Pack 1，您可以定义浏览器具有以下方面的功能：

- 在计算机级别中，创建或更新`.browser`以下文件夹中的 XML 文件：

- [!code-console[Main](overview/samples/sample27.cmd)]

- 定义的浏览器功能后，运行以下命令通过 Visual Studio 命令提示以重新生成浏览器功能程序集并将其添加到 gac 中：

- [!code-console[Main](overview/samples/sample28.cmd)]

- 对于单个应用程序，您创建`.browser`应用程序的文件中`App_Browsers`文件夹。

这些方法需要您更改 XML 文件和计算机级别的更改，必须重新启动该应用程序后运行 aspnet\_regbrowsers.exe 过程。

ASP.NET 4 包含一项功能称为*浏览器功能提供程序*。 顾名思义，此，你可以生成一个提供程序，进而使你可以使用你自己的代码来确定浏览器功能。

在实践中，开发人员通常不定义自定义浏览器功能。 浏览器文件会进行硬若要更新，该过程相当复杂，对它们进行更新为和的 XML 语法的`.browser`文件可以是复杂，无法使用和定义。 什么会使此过程更加轻松是常见的浏览器定义语法，好像或一个包含最新的浏览器定义或甚至此类数据库的 Web 服务的数据库。 新的浏览器功能提供程序功能使整个这些方案可能和实用，为第三方开发人员。

有两种主要方法使用新的 ASP.NET 4 浏览器功能提供程序功能： 扩展 ASP.NET 浏览器功能定义功能，或完全替换它。 以下各节首先介绍如何替换功能，以及如何对其进行扩展。

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a>替换 ASP.NET 浏览器功能功能

若要完全替换 ASP.NET 浏览器功能定义功能，请按照下列步骤：

1. 创建提供程序类派生自*HttpCapabilitiesProvider*它将替代*GetBrowserCapabilities*方法，如以下示例所示： 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    此示例中的代码创建一个新*HttpBrowserCapabilities*对象，指定名为浏览器并将该功能设置为 MyCustomBrowser 功能。
2. 将提供程序注册应用程序。 

    若要与应用程序使用提供程序，必须添加*提供程序*归于*browserCaps*主题中`Web.config`或`Machine.config`文件。 (您还可以定义中的提供程序属性*位置*元素为应用程序，例如特定的移动设备的文件夹中的特定目录。)下面的示例演示如何设置*提供程序*配置文件中的属性：

    [!code-xml[Main](overview/samples/sample30.xml)]

    若要注册新的浏览器功能定义的另一种方法是使用代码，如下面的示例中所示：

    [!code-csharp[Main](overview/samples/sample31.cs)]

    此代码必须在运行*应用程序\_启动*事件的`Global.asax`文件。 将更改为任何*BrowserCapabilitiesProvider*之前执行该应用程序中的任何代码，以确保缓存保留在已解析的有效状态，必须执行类*HttpCapabilitiesBase*对象。

#### <a name="caching-the-httpbrowsercapabilities-object"></a>缓存 HttpBrowserCapabilities 对象

前面的示例中已有一个问题是这些代码将运行自定义提供程序调用以获取每次*HttpBrowserCapabilities*对象。 这可以在每个请求期间发生多次。 在示例中，提供程序的代码没有多大用处。 但是，如果自定义提供程序中的代码执行中的大量工作以便获得*HttpBrowserCapabilities*对象，这可能会影响性能。 若要避免这种情况发生，可以缓存*HttpBrowserCapabilities*对象。 请执行这些步骤：

1. 创建派生的类*HttpCapabilitiesProvider*，如下面的示例所示： 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    在示例中，代码通过调用自定义 BuildCacheKey 方法，生成的缓存键和此方法通过调用自定义 GetCacheTime 方法获取的缓存的时间长度。 然后代码将添加已解析*HttpBrowserCapabilities*到缓存的对象。 可以从缓存中检索和上重复使用该对象进行的后续请求使用的自定义提供程序。
2. 将提供程序注册应用程序，如前面的过程中所述。

#### <a name="extending-aspnet-browser-capabilities-functionality"></a>扩展 ASP.NET 浏览器功能的功能

上一节介绍了如何创建一个新*HttpBrowserCapabilities* ASP.NET 4 中的对象。 此外可以通过将新的浏览器功能定义添加到已在 ASP.NET 中的那些扩展 ASP.NET 浏览器功能的功能。 您可以执行此操作而无需使用 XML 的浏览器定义。 下面的过程演示如何。

1. 创建派生的类*HttpCapabilitiesEvaluator*它将替代*GetBrowserCapabilities*方法，如以下示例所示： 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    此代码首先使用 ASP.NET 浏览器功能功能来尝试找出在浏览器。 但是，如果浏览器不确定基于在请求中定义的信息 (即，如果*浏览器*的属性*HttpBrowserCapabilities*对象是字符串"Unknown")，该代码调用自定义提供程序 (MyBrowserCapabilitiesEvaluator) 来标识浏览器。
2. 将提供程序注册应用程序，如前面的示例中所述。

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a>通过将新功能添加到现有的功能定义扩展浏览器功能的功能

除了创建自定义浏览器定义提供程序和动态地创建新的浏览器定义，您可以扩展现有的浏览器定义具有其他功能。 这允许您使用接近所需但缺少仅几项功能的定义。 为此，请执行下列步骤。

1. 创建派生的类*HttpCapabilitiesEvaluator*它将替代*GetBrowserCapabilities*方法，如以下示例所示： 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    此代码示例扩展了现有的 ASP.NET *HttpCapabilitiesEvaluator*类，并获取*HttpBrowserCapabilities*与当前的请求定义通过使用以下代码相匹配的对象:

    [!code-csharp[Main](overview/samples/sample35.cs)]

    然后，代码可以添加或修改此浏览器的功能。 有两种方法来指定新的浏览器功能：

    - 添加到的键/值对*IDictionary*对象，它由公开*功能*属性*HttpCapabilitiesBase*对象。 在上一示例中，该代码将添加一项功能的值创建名为多点触控 *，则返回 true*。
    - 设置的现有属性*HttpCapabilitiesBase*对象。 在上述示例中，代码会设置*帧*属性设置为*true*。 此属性是只需访问器的*IDictionary*对象，它由公开*功能*属性。 

        > [!NOTE]
        > 请注意此模型适用于的任何属性*HttpBrowserCapabilities*，包括控件适配器。
2. 将提供程序注册应用程序，如前面的过程中所述。

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a>ASP.NET 4 中的路由

ASP.NET 4 添加了对使用 Web 窗体路由的内置支持。 路由可以配置为接受的应用程序请求不会映射到物理文件的 Url。 相反，您可以使用路由来定义，对用户有意义和，可帮助你的应用程序的搜索引擎搜索引擎优化 (SEO) 的 Url。 例如，用于显示产品类别中的现有应用程序的页面的 URL 可能如下面的示例所示：

[!code-console[Main](overview/samples/sample36.cmd)]

通过使用路由，可以配置应用程序接受以下 URL 来呈现相同的信息：

[!code-console[Main](overview/samples/sample37.cmd)]

路由已从 ASP.NET 3.5 SP1 开始提供。 (有关如何使用 ASP.NET 3.5 SP1 中的路由的示例，请参阅文章[路由使用与 WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "此项的标题。") Phil Haack 的博客。）但是，ASP.NET 4 包括一些功能，使其更轻松地使用路由，其中包括：

- *PageRouteHandler*类，该类是一个简单的 HTTP 处理程序定义的路由时所用的。 类将数据传递给请求路由到的页。
- 新属性*HttpRequest.RequestContext*并*Page.RouteData* (即为代理*HttpRequest.RequestContext.RouteData*对象)。 这些属性使其能够更轻松地从该路由传递的访问信息。
- 下面的新表达式构建器中定义*System.Web.Compilation.RouteUrlExpressionBuilder*并*System.Web.Compilation.RouteValueExpressionBuilder*:
- *RouteUrl*，简单的方式来创建对应于 ASP.NET 服务器控件中的路由 URL 的 URL。
- *RouteValue*，以简单的方式来提取从信息*RouteContext*对象。
- *RouteParameter*类，因此可以轻松地将数据包含在传递*RouteContext*针对数据源控件的查询的对象 (类似于[ *FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).

#### <a name="routing-for-web-forms-pages"></a>Web 窗体页的路由

下面的示例演示如何使用新的定义 Web 窗体路由*MapPageRoute*方法*路由*类：

[!code-csharp[Main](overview/samples/sample38.cs)]

ASP.NET 4 引入了*MapPageRoute*方法。 下面的示例等效于上一示例所示的 SearchRoute 定义，但使用*PageRouteHandler*类。

[!code-csharp[Main](overview/samples/sample39.cs)]

在示例中的代码映射到物理页的路由 (在第一个路由到`~/search.aspx`)。 第一个路由定义还指定应从 URL 中提取并传递到页名为 searchterm 的参数。

*MapPageRoute*方法支持以下方法重载：

- *MapPageRoute （字符串 routeName，字符串 routeUrl、 字符串 physicalFile，bool checkPhysicalUrlAccess）*
- *MapPageRoute （字符串 routeName、 字符串 routeUrl、 字符串 physicalFile、 bool checkPhysicalUrlAccess、 RouteValueDictionary 默认值）*
- *MapPageRoute （字符串 routeName、 字符串 routeUrl、 字符串 physicalFile、 bool checkPhysicalUrlAccess、 RouteValueDictionary 默认值、 RouteValueDictionary 约束）*

*CheckPhysicalUrlAccess*参数指定该路由是否应检查其路由到物理页的安全权限 (在本例中为 search.aspx) 以及对传入 URL 的权限 （在这种情况下，搜索/ {searchterm})。 如果的值*checkPhysicalUrlAccess*是*false*，将检查仅传入 URL 的权限。 这些权限定义中`Web.config`文件中使用如下所示的设置：

[!code-xml[Main](overview/samples/sample40.xml)]

在示例配置中，访问被拒绝到物理页`search.aspx`除了管理员角色中的所有用户。 当*checkPhysicalUrlAccess*参数设置为*true* （这是其默认值），只有管理员用户允许访问 URL /search/ {searchterm}，因为物理页 search.aspx 是限制为该角色中的用户。 如果*checkPhysicalUrlAccess*设置为*false*和站点配置为在前面的示例所示，将允许所有经过身份验证的用户访问 URL /search/ {searchterm}。

#### <a name="reading-routing-information-in-a-web-forms-page"></a>读取 Web 窗体页中的路由信息

在 Web 窗体物理页的代码中，您可以访问路由已从 URL 中提取的信息 (或另一个对象已添加到其他信息*RouteData*对象) 通过使用两个新属性： *HttpRequest.RequestContext*并*Page.RouteData*。 (*Page.RouteData*包装*HttpRequest.RequestContext.RouteData*。)下面的示例演示如何使用*Page.RouteData*。

[!code-csharp[Main](overview/samples/sample41.cs)]

代码将提取如前面的示例路由中定义为 searchterm 参数中，传递的值。 请考虑以下请求 URL:

[!code-console[Main](overview/samples/sample42.cmd)]

发出此请求时，会在呈现"scott"一词`search.aspx`页。

#### <a name="accessing-routing-information-in-markup"></a>访问标记中的路由信息

在上一部分中所述的方法演示如何在 Web 窗体页中的代码中获取路由数据。 此外可以使用相同的信息让你访问在标记中的表达式。 表达式生成器是一种功能强大、 巧妙的方法，以使用声明性代码。 (有关详细信息，请参阅文章[Express 自己的自定义表达式生成器](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx)Phil Haack 的博客上。)

ASP.NET 4 包括两个新的表达式生成器的 Web 窗体路由。 下面的示例演示如何使用它们。

[!code-aspx[Main](overview/samples/sample43.aspx)]

在示例中， *RouteUrl*表达式用于定义根据路由参数的 URL。 这使您不必将硬编码到标记中，完整的 URL，并允许您更改 URL 结构更高版本而无需对此链接的任何更改。

根据前面定义的路由，此标记将生成以下 URL:

[!code-console[Main](overview/samples/sample44.cmd)]

ASP.NET 会自动制定正确的路由 （即，它生成正确的 URL） 根据输入参数。 此外可以在表达式中，从中可以指定要使用的路由包含路由名称。

下面的示例演示如何使用*RouteValue*表达式。

[!code-aspx[Main](overview/samples/sample45.aspx)]

包含此控件的页的运行时，标签中显示"scott"的值。

*RouteValue*表达式可以轻松地在标记中，使用路由数据和它避免了必须使用更复杂的 Page.RouteData["x"] 在标记中的语法。

#### <a name="using-route-data-for-data-source-control-parameters"></a>使用路由数据的数据源控件参数

*RouteParameter*类，可以指定作为数据源控件中的查询参数值的路由数据。 它[工作方式非常类似于](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)类，如以下示例所示：

[!code-aspx[Main](overview/samples/sample46.aspx)]

在这种情况下，路由参数 searchterm 的值将用于@companyname中的参数<em>选择</em>语句。

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a>设置客户端 Id

新*ClientIDMode*属性，解决了长期存在的问题在 ASP.NET 中，即如何控件创建*id*所呈现元素的属性。 知道*id*呈现元素的属性是重要信息： 如果你的应用程序包括在引用这些元素的客户端脚本。

*Id*中为 Web 服务器控件呈现的 HTML 属性基于生成*ClientID*控件的属性。 ASP.NET 4 中，用于生成算法直到*id*属性从*ClientID*属性已连接的命名容器 （如果有） 的 id，并在重复 （作为中控件的情况下数据控件），添加一个前缀和一个顺序号。 尽管这始终有保证的页面中控件 Id 是唯一，该算法导致控件不是可预测，并且因此非常难以为客户端脚本中引用的 Id。

新*ClientIDMode*属性，可以指定更准确地说如何的客户端 ID 生成的控件。 可以设置*ClientIDMode*任何控件，包括页面的属性。 可能的设置如下所示：

- *AutoID* – 这是等效于用于生成算法*ClientID* ASP.NET 的早期版本中使用的属性值。
- *静态*– 此步骤指定*ClientID*值将为无需连接的父命名容器的 Id 的 ID 相同。 这可以是 Web 用户控件中很有用。 由于 Web 用户控件可能位于不同页上和在不同的容器控件中，可能难以使用的控件的客户端脚本编写*AutoID*算法因为无法预测的 ID 值将是什么.
- *可预测*– 此选项主要是为了在使用重复的模板的数据控件中使用。 它将连接在一起的控件的命名容器，但生成的 ID 属性*ClientID*值不包含类似"ctlxxx"字符串。 此设置结合工作*ClientIDRowSuffix*控件的属性。 您设置*ClientIDRowSuffix*属性设置为数据字段的名称和该字段的值生成的用后缀*ClientID*值。 通常使用作为数据记录的主键*ClientIDRowSuffix*值。
- *继承*– 此设置是控件的默认行为; 它指定生成控件的 ID 是其父项相同。

可以设置*ClientIDMode*页面级别的属性。 此定义的默认*ClientIDMode*当前页中的所有控件的值。

默认值*ClientIDMode*在页面级别的值是*AutoID*，并且默认值*ClientIDMode*控制级别的值是*继承*. 因此，如果未执行操作在代码中任意位置设置此属性，则所有控件将都默认为*AutoID*算法。

设置页面级别值 *@ Page*指令，如下面的示例中所示：

[!code-aspx[Main](overview/samples/sample47.aspx)]

您还可以设置*ClientIDMode*在配置文件中，在计算机 （计算机） 级别或应用程序级别的值。 此定义的默认*ClientIDMode*设置应用程序中的所有页中的所有控件。 如果在计算机级别设置的值，它定义的默认*ClientIDMode*在该计算机上设置的所有 Web 站点。 下面的示例演示*ClientIDMode*配置文件中的设置：

[!code-xml[Main](overview/samples/sample48.xml)]

如前文所述的值*ClientID*属性派生自命名容器的控件的父级。 在某些情况下，例如当使用主页面，控件可以得到 Id 类似于以下中呈现的 HTML:

[!code-html[Main](overview/samples/sample49.html)]

即使*输入*标记所示的元素 (从*文本框*控制) 是只有两个命名容器的页中的深度 (嵌套*ContentPlaceholder*控件)，由于主页面进行处理的方式，最终结果是如下所示的控件 ID:

[!code-console[Main](overview/samples/sample50.cmd)]

此 ID 保证是唯一在页中，但在大多数情况对于长是不必要地。 想象你想以减少呈现 ID 的长度并更好地控制如何生成 ID。 （例如，您希望清除"ctlxxx"前缀。）若要实现此目的的最简单方法是通过设置*ClientIDMode*属性，如以下示例所示：

[!code-aspx[Main](overview/samples/sample51.aspx)]

在此示例中， *ClientIDMode*属性设置为*静态*对于最外面*NamingPanel*元素，并设置为*可预测*为内部*NamingControl*元素。 这些设置会导致以下标记 （页和母版页的其余部分被假定为如前面示例中相同）：

[!code-html[Main](overview/samples/sample52.html)]

*静态*设置的效果的重置包含最外面的任何控件的命名层次结构*NamingPanel*元素，并消除*ContentPlaceHolder*并*MasterPage* Id 从生成的 id。 (*名称*呈现的元素的属性不受影响，以便正常的 ASP.NET 功能保留的事件中，视图状态，依次类推。)重置命名层次结构的一个副作用是，即使移动的标记*NamingPanel*元素为另一种*ContentPlaceholder*控件，呈现客户端 Id 保持不变。

> [!NOTE]
> 请注意它是由您来确保呈现的控件 Id 是唯一的。 如果它们不是，它会中断任何功能的单个 HTML 元素，如客户端所需的唯一 Id *document.getElementById*函数。


#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a>在数据绑定控件中创建可预测的客户端 Id

*ClientID*旧算法的数据绑定列表控件中的控件可以是生成的值长，不是真正的可预测。 *ClientIDMode*功能可以帮助你进行更大的控制权生成通过如何将这些 Id。

下面的示例中的标记包括*ListView*控件：

[!code-aspx[Main](overview/samples/sample53.aspx)]

在上一示例中， *ClientIDMode*并*RowClientIDRowSuffix*标记中设置属性。 *ClientIDRowSuffix*属性可用于仅在数据绑定控件中，并且其行为不同，具体取决于哪个控件使用。 不同之处在于这些：

- *GridView*控件 — 您可以在数据源中，它在运行时创建客户端 Id 结合指定一个或多个列的名称。 例如，如果您设置*RowClientIDRowSuffix*为"产品名称，产品 id"，控件 Id，用于呈现的元素所采用的格式如下所示：

- [!code-console[Main](overview/samples/sample54.cmd)]

- *ListView*控件 — 可以追加到客户端 id。 在数据源中指定的单个列 例如，如果您设置*ClientIDRowSuffix* "ProductName"到呈现的控件 Id 所采用的格式如下所示：

- [!code-console[Main](overview/samples/sample55.cmd)]

- 在这种情况下尾随 1 派生自当前数据项的产品 ID。

- *Repeater*控件，此控件不支持*ClientIDRowSuffix*属性。 在中*Repeater*控件中，当前行的索引使用。 当你使用 ClientIDMode ="可预测" *Repeater*控制，客户端 Id 生成具有以下格式：

- [!code-console[Main](overview/samples/sample56.cmd)]

- 尾随 0 是当前行的索引。

*FormView*并*DetailsView*控件不显示多个行，因此它们不支持*ClientIDRowSuffix*属性。

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a>保持在数据控件中的行选择

*GridView*并*ListView*控件可以让用户选择一行。 在以前版本的 ASP.NET，具有已选择基于页上的行索引。 例如，如果你选择第 1 页上的第三个项，然后将其移到第 2 页选择该页面上的第三个项。

仅在.NET Framework 3.5 SP1 中的动态数据项目中最初支持持久化的选择。 如果启用此功能，当前选定的项基于项的数据键。 这意味着，如果您选择第 1 页上的第三个行，并移动到第 2 页，则不选择在第 2 页。 时移到第 1 页，第三行仍处于选中状态。 现在支持持久化的选择*GridView*并*ListView*使用的所有项目中的控件*EnablePersistedSelection*属性，如中所示下面的示例：

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a>ASP.NET 图表控件

ASP.NET*图表*控件扩展.NET Framework 中的数据可视化产品/服务。 使用*图表*控件，可以创建具有复杂的统计或财务分析使用直观和极具视觉表现力的图表的 ASP.NET 页面。 ASP.NET*图表*控件作为外接程序引入到.NET Framework 版本 3.5 SP1 版本，.NET Framework 4 版本的一部分。

控件包括以下功能：

- 35 种不同的图表类型。
- 无限的数量的图表区、 标题、 图例和批注。
- 各种不同的所有图表元素的外观设置。
- 对于大多数图表类型的三维支持。
- 可以自动适应数据点周围的智能数据标签。
- 条带线、 刻度分隔线和对数缩放。
- 包含 50 多个用于数据分析和转换的财务和统计公式。
- 简单绑定和操作的图表数据。
- 对支持常见的数据格式，如日期、 时间和货币。
- 以实现交互性和事件驱动的自定义，包括客户端的支持，请单击使用 Ajax 的事件。
- 状态管理。
- 二进制流。

以下各图显示所生成的 ASP.NET 图表控件的财务图表的示例。

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

图 2: ASP.NET 图表控件示例

有关如何使用 ASP.NET 图表控件的更多示例上下载示例代码[Microsoft 图表控件的示例环境](https://go.microsoft.com/fwlink/?LinkId=128300)MSDN 网站上的页。 您可以找到更多示例社区内容在[图表控件论坛](https://go.microsoft.com/fwlink/?LinkId=128713)。

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a>将图表控件添加到 ASP.NET 页面

下面的示例演示如何添加*图表*到通过使用标记的 ASP.NET 页面的控件。 在示例中，*图表*控件生成静态数据点的柱形图。

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a>使用三维图表

*图表*控件包含*ChartAreas*集合，它可以包含*ChartArea*定义的图表区的特性的对象。 例如，若要使用三维图表区，使用*Area3DStyle*属性，如以下示例所示：

[!code-aspx[Main](overview/samples/sample59.aspx)]

下图显示了四个系列的三维图表*栏*图表类型。

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

图 3： 三维条形图

#### <a name="using-scale-breaks-and-logarithmic-scales"></a>使用刻度分隔线和对数刻度

刻度分隔线和对数刻度是两种方法可以向图表添加复杂。 这些功能是特定于每个轴在图表区中。 例如，若要在图表区的主 Y 轴上使用这些功能，使用*AxisY.IsLogarithmic*并*ScaleBreakStyle*中的属性*ChartArea*对象。 以下代码片段演示如何使用主 Y 轴上的刻度分隔线。

[!code-aspx[Main](overview/samples/sample60.aspx)]

下图显示了具有启用了刻度分隔线的 Y 轴。

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

图 4： 刻度分隔线

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a>用 QueryExtender 控件筛选数据

创建数据驱动的网页开发人员非常常见的任务是筛选数据。 这通常已由执行构建*其中*子句中的数据源控件。 此方法可能很复杂，在某些情况下*其中*语法不允许您充分利用基础数据库的完整功能。

若要简化筛选操作，一个新*QueryExtender*已在 ASP.NET 4 中添加控件。 此控件可以添加到*EntityDataSource*或*LinqDataSource*以便筛选这些控件返回的数据的控件。 因为*QueryExtender*控件依赖于 LINQ，则将数据发送到页上，这会导致非常高效地执行操作之前筛选器在数据库服务器上应用。

*QueryExtender*控件支持的各种筛选器选项。 以下部分介绍了这些选项，并提供有关如何使用它们的示例。

#### <a name="search"></a>搜索

搜索选项时， *QueryExtender*控件中指定的字段执行搜索。 在以下示例中，该控件使用 TextBoxSearch 控件和对其内容中的搜索中输入的文本`ProductName`并`Supplier.CompanyName`中返回的数据的列*LinqDataSource*控件。

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a>范围

范围选项类似于搜索选项，但指定的值来定义范围的对。 在以下示例中， *QueryExtender*控制搜索`UnitPrice`中返回的数据列*LinqDataSource*控件。 从页面上的 TextBoxFrom 和 TextBoxTo 控件中读取范围。

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a>PropertyExpression

属性表达式选项，可以定义为属性值的比较。 如果表达式的计算结果 *，则返回 true*，返回所检查的数据。 在以下示例中， *QueryExtender*控件通过比较中的数据筛选数据`Discontinued`CheckBoxDiscontinued 控件在页上的值列。

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a>CustomExpression

最后，可以指定要使用的自定义表达式*QueryExtender*控件。 此选项可以定义自定义筛选器逻辑的页面中调用函数。 下面的示例演示如何以声明方式指定的自定义表达式*QueryExtender*控件。

[!code-aspx[Main](overview/samples/sample64.aspx)]

下面的示例演示自定义函数，它通过调用*QueryExtender*控件。 在这种情况下，而不是使用包含的数据库查询*其中*子句中，代码使用 LINQ 查询来筛选的数据。

[!code-csharp[Main](overview/samples/sample65.cs)]

以下示例演示了正在使用中只有一个表达式*QueryExtender*控件一次。 但是，可以包含多个表达式内的*QueryExtender*控件。

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a>Html 编码的代码表达式

使用依赖于 （特别是使用 ASP.NET MVC) 的某些 ASP.NET 站点`<%` =  `expression %>` （通常称为"代码片段"） 的语法将一些文本写入响应。 当您使用的代码表达式时，它很容易忘记进行 HTML 编码的文本，如果文本来自用户输入，它可能会导致页打开到 XSS （跨站点脚本） 攻击。

ASP.NET 4 引入了以下新代码表达式的语法：

[!code-aspx[Main](overview/samples/sample66.aspx)]

此语法使用写入到响应时，HTML 编码，默认情况下。 此新表达式有效地转换为以下：

[!code-aspx[Main](overview/samples/sample67.aspx)]

例如， &lt;%: 请求"/userinput&gt"%&gt;执行 HTML 编码的值*请求"/userinput&gt"*。

此功能旨在使其可以替换为旧语法的所有实例的新语法，以便将无需再决定每个步骤要使用哪一个。 但是，一些情况下要输出的文本要作为 HTML 或已经进行了编码，在这种情况下这可能会导致双重解码。

对于这些情况下，ASP.NET 4 引入了一个新的接口*IHtmlString*，具体实现，以及*HtmlString*。 这些类型的实例，您可以指示，返回值是已正确编码 （或否则检查） 用于显示为 HTML，并，因此值不应为 HTML 编码试。 例如，以下不应为 （并不是） 编码的 HTML:

[!code-aspx[Main](overview/samples/sample68.aspx)]

ASP.NET 4 运行时，已更新为使用此新语法，以便它们不是双编码的但仅限于 ASP.NET MVC 2 帮助器方法。 运行使用 ASP.NET 3.5 SP1 的应用程序时，则此新语法无效。

请注意这并不保证 XSS 攻击防护。 例如，使用不在引号中的属性值的 HTML 可以包含仍然容易遇到用户输入。 请注意，ASP.NET 控件和 ASP.NET MVC 帮助程序的输出始终包含属性值在引号中，这是建议的方法。

同样，此语法不执行 JavaScript 编码，例如当您创建基于用户输入的 JavaScript 字符串。

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a>项目模板更改

在 ASP.NET 的早期版本中，使用 Visual Studio 来创建新网站项目或 Web 应用程序项目时生成的项目包含仅 Default.aspx 页上，默认值`Web.config`文件，和`App_Data`文件夹中，按如下所示图：

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

Visual Studio 还支持空网站项目类型，不包含任何文件根本下, 图中所示：

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

结果是，对于初学者，很少指导如何构建生产型 Web 应用程序。 因此，ASP.NET 4 引入了三个新模板，另一个为空的 Web 应用程序项目，每个 Web 应用程序和网站项目。

#### <a name="empty-web-application-template"></a>空 Web 应用程序模板

顾名思义，空 Web 应用程序模板是一个精简的 Web 应用程序项目。 下图中所示，可以从 Visual Studio 新项目对话框中，选择此项目模板：

[![](overview/_static/image7.png)](overview/_static/image6.png)

([单击此项可查看原尺寸图像](overview/_static/image8.png))

创建空的 ASP.NET Web 应用程序时，Visual Studio 将创建以下文件夹布局：

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

这是类似于空网站布局从早期版本的 ASP.NET 中，有一个例外。 在 Visual Studio 2010 中，空 Web 应用程序和空网站项目包含以下最小`Web.config`文件，其中包含 Visual Studio 用来标识该项目面向的框架的信息：

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

如果没有此*targetFramework*属性，Visual Studio 默认值为面向.NET Framework 2.0，以打开较旧的应用程序时保持兼容性。

#### <a name="web-application-and-web-site-project-templates"></a>Web 应用程序和网站项目模板

其他两个新项目模板随附 Visual Studio 2010 包含重大更改。 下图显示了在创建新的 Web 应用程序项目时创建的项目布局。 （对于网站项目布局是几乎完全相同）。

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

该项目包括一个未在早期版本中创建的文件数。 此外，新的 Web 应用程序项目配置了基本成员资格功能，可让您快速开始保护对新应用程序的访问。 由于此包含`Web.config`文件新的项目包含用于配置成员资格、 角色和配置文件的条目。 下面的示例演示`Web.config`新的 Web 应用程序项目文件。 (在这种情况下， *roleManager*被禁用。)

[![](overview/_static/image13.png)](overview/_static/image12.png)

([单击此项可查看原尺寸图像](overview/_static/image14.png))

项目还包含第二个`Web.config`文件中`Account`目录。 第二个配置文件提供了一种方法来确保安全访问的 ChangePassword.aspx 页不记录在用户。 下面的示例演示的第二个内容`Web.config`文件。

![](overview/_static/image15.png)

默认情况下，新的项目模板中创建的页面还包含比在早期版本的详细内容。 此项目包含默认母版页和 CSS 文件，并已配置的默认页面 (Default.aspx) 默认情况下用于主页面。 结果是，如果第一次运行的 Web 应用程序或网站，默认 （家庭） 页将已正常运行。 事实上，它是类似于启动一个新的 MVC 应用程序时，将显示默认页面。

[![](overview/_static/image17.png)](overview/_static/image16.png)

([单击此项可查看原尺寸图像](overview/_static/image18.png))

项目模板的这些更改的目的是提供有关如何开始构建新的 Web 应用程序的指导。 使用语义正确，严格 XHTML 1.0 符合标记和使用 CSS 指定的布局，在模板中的页表示用于构建 ASP.NET 4 Web 应用程序的最佳实践。 默认页还具有您可以轻松地自定义的两列布局。

例如，假设为新的 Web 应用程序想要更改的某些颜色并插入我的 ASP.NET 应用程序徽标代替你公司的徽标。 若要执行此操作，创建一个新目录下的`Content`来存储你的徽标图像：

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

若要将映像添加到页面，然后打开`Site.Master`文件中，找到其中我的 ASP.NET 应用程序文本定义，并将其替换为*映像*元素的*src*属性设置为新的徽标图像，如以下示例所示：

[![](overview/_static/image21.png)](overview/_static/image20.png)

([单击此项可查看原尺寸图像](overview/_static/image22.png))

然后，可以进入 Site.css 文件并修改 CSS 类定义，以更改页面的背景色以及的标头。

这些更改的结果是，可以显示不费吹灰之力自定义的主页上：

[![](overview/_static/image24.png)](overview/_static/image23.png)

([单击此项可查看原尺寸图像](overview/_static/image25.png))

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a>CSS 改进

在 ASP.NET 4 中主要领域之一是工作的帮助呈现 HTML 与最新的 HTML 标准兼容的。 这包括对 ASP.NET Web 服务器控件如何使用 CSS 样式的更改。

#### <a name="compatibility-setting-for-rendering"></a>呈现的兼容性设置

默认情况下，当 Web 应用程序或网站以.NET Framework 4 为目标*controlRenderingCompatibilityVersion*的属性*页面*元素设置为"4.0"。 此元素定义在计算机级别`Web.config`文件，默认情况下适用于所有 ASP.NET 4 应用程序：

[!code-xml[Main](overview/samples/sample69.xml)]

值*controlRenderingCompatibility*是一个字符串，它允许潜在的新版本定义在将来的版本。 在当前版本中，此属性支持以下值：

- "3.5". 此设置指示旧式呈现和标记。 呈现的控件的标记是 100%向后兼容，以及设置的*xhtmlConformance*遵循属性。
- "4.0". 如果该属性具有此设置，ASP.NET Web 服务器控件执行以下操作：
- *XhtmlConformance*属性始终被视为"Strict"。 因此，控件将呈现 XHTML 1.0 Strict 标记。
- 禁用非输入控件不再呈现无效样式。
- *div*现在样式围绕隐藏的字段的元素，以便它们不会干扰用户创建 CSS 规则。
- 菜单控件呈现在语义上正确并且符合辅助功能准则的标记。
- 验证控件不呈现内联样式。
- 控制以前呈现边框 ="0"(派生自 ASP.NET 控件*表*控制和 ASP.NET*映像*控件) 不再呈现此属性。

#### <a name="disabling-controls"></a>禁用控件

在 ASP.NET 3.5 SP1 和更早版本中，该框架呈现*禁用*特性的 HTML 标记中任何控制其*已启用*属性设置为*false*。 但是，根据 HTML 4.01 规范，仅*输入*元素应具有此属性。

在 ASP.NET 4 中，可以设置*controlRenderingCompatabilityVersion*属性设置为"3.5"，如以下示例所示：

[!code-xml[Main](overview/samples/sample70.xml)]

您可以创建标记*标签*如下所示，禁用了控件的控件：

[!code-aspx[Main](overview/samples/sample71.aspx)]

*标签*控件将呈现以下 HTML:

[!code-html[Main](overview/samples/sample72.html)]

在 ASP.NET 4 中，可以设置*controlRenderingCompatabilityVersion*为"4.0"。 在这种情况下，仅控制呈现的*输入*元素将呈现*禁用*属性时控件的*已启用*属性设置为*false*. 控件不呈现 HTML*输入*改为呈现元素*类*引用可用于定义一个已禁用的控件外观的 CSS 类的属性。 例如，*标签*中前面的示例所示的控件将生成以下标记：

[!code-html[Main](overview/samples/sample73.html)]

为此控件指定的类的默认值为"aspNetDisabled"。 但是，可以更改此默认值通过设置静态*DisabledCssClass*的静态属性*WebControl*类。 对控件开发人员要使用的特定控件的行为还可以定义使用*SupportsDisabledAttribute*属性。

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a>隐藏 div 元素周围隐藏字段

ASP.NET 2.0 和更高版本的呈现特定于系统的隐藏的字段 (如*隐藏*用于存储视图状态信息的元素) 内*div*元素中，以便符合 XHTML 标准。 但是，这会导致问题，在 CSS 规则影响*div*页面上的元素。 例如，这样可能会出现在页面中的一个像素行大约隐藏*div*元素。 在 ASP.NET 4 中， *div*将由 ASP.NET 生成的隐藏的字段的元素添加 CSS 类引用，如以下示例所示：

[!code-html[Main](overview/samples/sample74.html)]

然后可以定义仅适用于一个 CSS 类*隐藏*元素生成的 ASP.NET 中，如以下示例所示：

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a>模板化控件的呈现外部表

默认情况下，以下 ASP.NET Web 服务器控件支持的模板的自动包装在用于将应用内联样式的外部表中：

- *FormView*
- *登录名*
- *PasswordRecovery*
- *ChangePassword*
- *向导*
- *CreateUserWizard*

名为的新属性*RenderOuterTable*已添加到允许的外部表，根据标记要删除这些控件。 例如，考虑下面的示例对*FormView*控件：

[!code-aspx[Main](overview/samples/sample76.aspx)]

此标记呈现到页上，其中包括一个 HTML 表的以下输出：

[!code-html[Main](overview/samples/sample77.html)]

若要防止表呈现，可以设置*FormView*控件的*RenderOuterTable*属性，如以下示例所示：

[!code-aspx[Main](overview/samples/sample78.aspx)]

前面的示例将以下输出，而不呈现*表*， *tr*，并*td*元素：

> 内容


此增强功能可以轻松地使用 CSS 时，控件的内容的样式因为没有任何意外的标记呈现的控件。

> [!NOTE]
> 请注意此更改禁用对 Visual Studio 2010 设计器中中的自动套用格式函数的支持，因为不再*表*可以托管生成的自动套用格式选项的样式特性的元素。


<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a>ListView 控件增强功能

*ListView*控件变得更轻松地在 ASP.NET 4 中使用。 指定包含与已知 ID 的服务器控件的布局模板被必需的早期版本的控件 以下标记显示如何使用的典型示例*ListView* ASP.NET 3.5 中的控件。

[!code-aspx[Main](overview/samples/sample79.aspx)]

在 ASP.NET 4 中， *ListView*控件不需要布局模板。 可以使用以下标记替换上一示例中所示的标记：

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a>CheckBoxList 和 RadioButtonList 控件增强功能

可以在 ASP.NET 3.5 中，指定布局*CheckBoxList*并*RadioButtonList*使用以下两个设置：

- *流*。 该控件将呈现*s p a n*元素以包含其内容。
- *表*。 该控件将呈现*表*元素以包含其内容。

下面的示例演示这些控件的每个标记。

[!code-aspx[Main](overview/samples/sample81.aspx)]

默认情况下，控件呈现 HTML 与下面类似：

[!code-html[Main](overview/samples/sample82.html)]

因为这些控件包含的项，以呈现在语义上是正确的 HTML 列表就会呈现使用 HTML 列表及其内容 (*li*) 元素。 这使得更容易读取网页使用辅助技术，并使控件能够更轻松地使用 CSS 样式的用户。

在 ASP.NET 4 中， *CheckBoxList*并*RadioButtonList*控件支持的以下新值*RepeatLayout*属性：

- *OrderedList* – 内容呈现为*li*中的元素*ol*元素。
- *UnorderedList* – 内容呈现为*li*中的元素*ul*元素。

下面的示例演示如何使用这些新值。

[!code-aspx[Main](overview/samples/sample83.aspx)]

上述标记将生成以下 HTML:

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> 请注意是否您设置*RepeatLayout*到*OrderedList*或*UnorderedList*，则*RepeatDirection*属性不再可用，并且将如果标记或代码中设置该属性，则引发运行时异常。 属性将具有任何值，因为这些控件的可视布局而使用 CSS 进行定义。


<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a>菜单控件改进

在 ASP.NET 4 中前,*菜单*呈现控件的一系列 HTML 表。 这变得更困难，应用 CSS 样式设置内联属性之外，也是不符合可访问性标准。

在 ASP.NET 4 中，该控件现在呈现 HTML 中使用的未排序的列表和列表元素组成的语义标记。 下面的示例演示在 ASP.NET 页面的标记*菜单*控件。

[!code-aspx[Main](overview/samples/sample85.aspx)]

当页面呈现时，该控件生成以下 HTML ( *onclick*为清楚起见已省略代码):

[!code-html[Main](overview/samples/sample86.html)]

除了呈现的改进，已使用焦点管理得到改进的菜单的键盘导航。 当*菜单*控件获得焦点，则可以使用箭头键导航元素。 *菜单*控件现在还将附加可访问富 internet 应用程序 (ARIA) 角色和属性 follo[wing](http://www.w3.org/TR/wai-aria-practices/#menu "菜单 ARIA 准则")为了改进可访问性。

样式块中位于顶部的页上，而不是根据呈现的 HTML 元素呈现菜单控件的样式。 如果你想要完全控制控件的样式，则可以设置新*IncludeStyleBlock*属性设置为*false*，在这种情况下，将不发出样式块。 若要使用此属性的一种方法是使用 Visual Studio 设计器中的自动套用格式功能设置菜单的外观。 然后可以运行页、 开放源代码的页，然后将呈现的样式块复制到外部 CSS 文件。 在 Visual Studio 中，撤消样式设置和组*IncludeStyleBlock*到*false*。 结果是在外部样式表中使用样式定义菜单外观。

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a>向导和 CreateUserWizard 控件

ASP.NET*向导*并*CreateUserWizard*控件支持允许你定义所呈现的 HTML 的模板。 (*CreateUserWizard*派生自*向导*。)下面的示例演示完全模板化的标记*CreateUserWizard*控件：

[!code-aspx[Main](overview/samples/sample87.aspx)]

该控件将呈现 HTML 与下面类似：

[!code-html[Main](overview/samples/sample88.html)]

在 ASP.NET 3.5 SP1 中，尽管您可以更改模板的内容，您仍然有限地控制的输出*向导*控件。 在 ASP.NET 4 中，您可以创建*LayoutTemplate*模板和 insert*占位符*控制 （使用保留的名称） 来指定要如何*向导控件*来呈现。 以下示例演示了此：

[!code-aspx[Main](overview/samples/sample89.aspx)]

此示例包含以下命名中的占位符*LayoutTemplate*元素：

- *headerPlaceholder* – 在运行时，这将替换为的内容*HeaderTemplate*元素。
- *sideBarPlaceholder* – 在运行时，这将替换为的内容*SideBarTemplate*元素。
- *wizardStepPlaceHolder* – 在运行时，这将替换为的内容*WizardStepTemplate*元素。
- *navigationPlaceholder* – 在运行时，这将替换为已定义的任何导航模板。

在以下示例中使用占位符的标记 （而不实际在模板中定义的内容） 呈现以下 HTML:

[!code-html[Main](overview/samples/sample90.html)]

是只是现在不是用户定义的 HTML *s p a n*元素。 (我们预计，将来版本中，甚至*s p a n*元素将不会呈现。)现在可以完全控制由生成的几乎所有内容*向导*控件。

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a>ASP.NET MVC

ASP.NET MVC 是作为外接程序框架到 ASP.NET 3.5 SP1 中引入 2009 年 3 月。 Visual Studio 2010 包括 ASP.NET MVC 2，其中包括新特性和功能。

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a>区域支持

区域可以组控制器和视图为部分以相对其他部分隔离的大型应用程序。 每个区域可以作为一个单独的 ASP.NET MVC 项目，然后可由主应用程序引用实现。 这可帮助构建大型应用程序时管理复杂性，并使多个团队能够在单个应用程序协同工作更轻松。

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a>数据注释属性验证支持

*DataAnnotations*属性，您可以通过使用元数据特性附加到模型的验证逻辑。 *DataAnnotations*属性在 ASP.NET 3.5 SP1 中的 ASP.NET 动态数据中引入。 这些属性已集成到默认模型联编程序，并且提供元数据驱动的方法来验证用户输入。

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a>模板化帮助器

模板化帮助器可自动关联的编辑和显示数据类型的模板。 例如，使用模板帮助器来指定自动为呈现日期选取器 UI 元素*System.DateTime*值。 这是类似于 ASP.NET 动态数据中的字段模板。

*Html.EditorFor*并*Html.DisplayFor*帮助器方法具有的内置支持的呈现标准数据类型具有多个属性也为复杂对象。 它们还通过自定义呈现让您可以之类的数据注释属性*DisplayName*并*ScaffoldColumn*到*ViewModel*对象。

通常，你想要自定义 UI 帮助程序更进一步的输出，并可以完全控制生成的内容。 *Html.EditorFor*并*Html.DisplayFor*帮助器方法支持此功能使用模板化机制，允许您定义外部模板，可以重写和控件呈现的输出。 为类，可以单独呈现模板。

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a>Dynamic Data — 动态数据

引入了动态数据中 2008 年年中的.NET Framework 3.5 SP1 版本。 此功能提供了用于创建数据驱动的应用程序，其中包括许多增强功能：

- 用于快速构建数据驱动网站的 RAD 体验。
- 基于数据模型中定义的约束的自动验证。
- 能够轻松地更改为中的字段生成的标记*GridView*并*DetailsView*使用动态数据项目的一部分的字段模板的控件。

> [!NOTE]
> 请注意有关详细信息，请参阅[动态数据文档](https://msdn.microsoft.com/library/cc488545.aspx)MSDN 库中。


为 ASP.NET 4 中，动态数据得到增强，使开发人员能够更强大的功能来快速构建数据驱动的网站。

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a>对于现有项目中启用动态数据

在.NET Framework 3.5 SP1 中提供的动态数据功能引入新功能，如下所示：

- 字段模板 – 这些将基于数据类型的模板提供的数据绑定控件。 字段模板提供更简单的方法来自定义比使用为每个字段的模板字段的数据控件的外观。
- 验证-动态数据，您可以在数据类使用属性来指定为必填的字段范围检查、 类型检查、 使用正则表达式匹配的模式的常见方案的验证和自定义验证。 由数据控件强制进行验证。

但是，这些功能具有以下要求：

- 数据访问层必须基于 Entity Framework 或 LINQ to SQL。
- 唯一的数据源控件支持这些功能已*EntityDataSource*或*LinqDataSource*控件。
- 功能需要使用动态数据或动态数据实体模板，以支持该功能所需的所有文件已创建的 Web 项目。

在 ASP.NET 4 中的动态数据支持的主要目标是能够为任何 ASP.NET 应用程序的新功能的动态数据。 下面的示例显示了可以在现有页面中充分利用动态数据功能的控件标记的。

[!code-aspx[Main](overview/samples/sample91.aspx)]

在代码页中，必须要使这些控件的动态数据支持添加以下代码：

[!code-csharp[Main](overview/samples/sample92.cs)]

当*GridView*控件处于编辑模式下，动态数据会自动验证输入的数据是格式正确。 如果不是，显示一条错误消息。

此功能还提供了其他权益，如能够指定默认值插入模式。 如果没有动态数据，要实现一个字段的默认值必须向事件附加，查找控件 (使用*FindControl*)，并将其值设置。 在 ASP.NET 4 中， *EnableDynamicData*调用支持第二个参数，可让你将任何字段的默认值传递对象，在此示例中所示：

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a>DynamicDataManager 控件声明性语法

*DynamicDataManager*控件已得到增强，以便可以将其配置以声明方式，与在 ASP.NET 中，而不是仅在代码的大多数控件一样。 有关标记*DynamicDataManager*控件的外观如以下示例所示：

[!code-aspx[Main](overview/samples/sample94.aspx)]

此标记启用动态数据行为中引用的 GridView1 控件*然后*一部分*DynamicDataManager*控件。

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a>实体模板

实体模板提供自定义而无需创建自定义页的数据的布局的新方法。 页上，使用模板*FormView*控件 (而不是*DetailsView*控制，因为在早期版本的动态数据中的页模板中使用) 和*DynamicEntity*要呈现实体模板的控件。 这为您提供了更好地控制由动态数据呈现的标记。

以下列表显示了包含实体模板的新项目目录布局：

[!code-console[Main](overview/samples/sample95.cmd)]

`EntityTemplate`目录包含有关如何显示的数据模型对象的模板。 默认情况下，通过使用呈现对象`Default.ascx`模板，其中提供了看上去如同创建的标记的标记*DetailsView* ASP.NET 3.5 SP1 中的动态数据使用的控件。 下面的示例演示的标记`Default.ascx`控件：

[!code-aspx[Main](overview/samples/sample96.aspx)]

若要更改整个站点的外观，可以编辑默认模板。 模板用于显示、 编辑和插入操作。 新的模板可以添加根据数据对象的名称才能更改外观和感觉的只是一种类型的对象。 例如，可以添加以下模板：

[!code-console[Main](overview/samples/sample97.cmd)]

该模板可能包含以下标记：

[!code-aspx[Main](overview/samples/sample98.aspx)]

新的实体模板显示在页面上使用新的*DynamicEntity*控件。 在运行时，此控件替换为实体模板的内容。 下面的标记演示*FormView*控制中`Detail.aspx`页使用的实体模板的模板。 请注意*DynamicEntity*标记中的元素。

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a>新的字段模板的 Url 和电子邮件地址

ASP.NET 4 引入了两个新内置字段模板`EmailAddress.ascx`和`Url.ascx`。 这些模板用于标记为字段*EmailAddress*或*Url*与*数据类型*属性。 有关*EmailAddress*对象，该字段显示为超链接，通过创建*mailto:* 协议。 当用户单击该链接时，打开用户的电子邮件客户端，并创建主干消息。 对象类型化为*Url*显示为普通的超链接。

下面的示例演示如何将标记字段。

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a>与 DynamicHyperLink 控件创建的链接

动态数据使用.NET Framework 3.5 SP1，以控制用户访问网站时，请参阅最终用户的 Url 中添加新路由功能。 新*DynamicHyperLink*控件，可以轻松地生成动态数据站点中页面的链接。 下面的示例演示如何使用*DynamicHyperLink*控件：

[!code-aspx[Main](overview/samples/sample101.aspx)]

此标记创建一个链接，指向的列表页`Products`表中定义的路由基于`Global.asax`文件。 该控件自动使用基于动态数据页的默认表名。

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a>对数据模型中继承的支持

实体框架和 LINQ to SQL 支持在其数据模型中继承。 出现这种可能是一个具有数据库`InsurancePolicy`表。 它还可能包含`CarPolicy`并`HousePolicy`具有相同的字段的表`InsurancePolicy`以及如何将多个字段。 动态数据已被修改，以了解数据模型中继承的对象并继承表中支持搭建基架。

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a>支持多对多关系 （仅适用于实体框架）

实体框架提供的丰富支持实现通过上公开作为集合的关系的表之间的多对多关系*实体*对象。 新`ManyToMany.ascx`和`ManyToMany_Edit.ascx`字段模板已添加用于显示和编辑多对多关系中涉及的数据提供支持。

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a>新属性来控制显示和支持枚举

*DisplayAttribute*已添加为您提供字段的显示方式的更多控制权。 *DisplayName*早期版本允许你更改用作字段标题的名称的动态数据中的属性。 新*DisplayAttribute*类，可以指定用于显示的字段，例如在其中会显示一个字段，以及是否将使用一个字段作为筛选器顺序的更多选项。 该属性还提供了用于标签的名称的独立控制*GridView*控制中使用的名称*DetailsView*控件，该字段的帮助文本，水印用于字段 （如果该字段接受输入的文本）。

*EnumDataTypeAttribute*类已添加，以便你可以将字段映射到枚举。 当此特性应用于字段时，指定枚举类型。 动态数据使用新`Enumeration.ascx`的字段模板来创建 UI，以显示和编辑枚举值。 该模板将映射到枚举中的名称来自数据库的值。

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a>对筛选器的增强的支持

动态数据 1.0 附带了内置布尔值列和外键列的筛选器。 筛选器不允许，可以指定是否显示它们，或以何种顺序显示它们。 新*DisplayAttribute*属性解决了这两的这些问题，请为您提供对某列是否显示为筛选器控制并以什么顺序显示。

其他增强功能是，筛选支持已被重新[编写为使用新](#0.2__QueryExtender "_QueryExtender") Web 窗体的功能。 这样可以创建筛选器，而无需了解的数据源控件的筛选器将与一起使用。 这些扩展，以及筛选器也已转换为模板控件，该编辑器可以添加新的。 最后， *DisplayAttribute*前面所述的类允许在相同中重写的默认筛选器的方式*UIHint*允许重写的列的默认字段模板。

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a>Visual Studio 2010 Web 开发改进

对于更高版本 CSS 兼容性，通过 HTML 和 ASP.NET 标记代码段和新动态 IntelliSense JavaScript 提高工作效率增强了 Visual Studio 2010 中的 web 开发。

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a>改进的 CSS 兼容性

Visual Studio 2010 中的 Visual Web Developer 设计器已更新，以提高 CSS 2.1 标准符合性。 在设计器更好地保留在 HTML 源的完整性和 Visual Studio 的早期版本相比更加可靠。 实质上，体系结构改进还进行了将会更好地启用中呈现、 布局和可维护性的未来增强功能。

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a>HTML 和 JavaScript 代码片段

在 HTML 编辑器中，IntelliSense 会自动完成的标记名称。 IntelliSense 代码段功能会自动完成整个标记和的详细信息。 在 Visual Studio 2010 中，IntelliSense 代码段支持 JavaScript 以及 C# 和 Visual Basic 中，这在 Visual Studio 的早期版本中受支持。

Visual Studio 2010 包括了超过 200 个代码段，可帮助你自动完成常见 ASP.NET 和 HTML 标记，包括必需的属性 (如 runat ="server") 和特定于标记的公共属性 (如*ID*， *DataSourceID*， *ControlToValidate*，和*文本*)。

您可以下载其他代码段，也可以编写您自己封装的你或你的团队使用的常见任务的标记块的代码段。

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a>JavaScript IntelliSense 增强功能

在 Visual 2010 中，JavaScript IntelliSense 经过重新设计，提供更丰富的编辑体验。 IntelliSense 现在可识别具有已动态生成的方法如对象*registerNamespace*和类似的技术使用的其他 JavaScript 框架。 要分析的脚本的大型库并使用很少或没有处理延迟显示 IntelliSense 改进了性能。 若要支持几乎所有第三方库，并以支持各种编码风格已极大地增加兼容性。 键入并立即利用 intellisense 时，现在进行分析文档注释。

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a>使用 Visual Studio 2010 的 web 应用程序部署

当 ASP.NET 开发人员部署 Web 应用程序时，他们经常发现他们会遇到以下问题：

- 部署到共享的托管站点需要技术，例如 FTP，可能会很慢。 此外，你必须手动执行任务，例如运行 SQL 脚本来配置数据库，必须更改 IIS 设置，例如，为应用程序中配置虚拟目录文件夹。
- 在企业环境中，除了部署 Web 应用程序文件，管理员经常必须修改 ASP.NET 配置文件和 IIS 设置。 数据库管理员必须运行一系列 SQL 脚本来获取运行的应用程序数据库。 此类安装耗费大量精力，通常需要数小时才能完成，并且必须仔细记载。

Visual Studio 2010 包括解决这些问题，以及允许用户无缝地将部署 Web 应用程序的技术。 这些技术之一是 IIS Web 部署工具 (MsDeploy.exe)。

Visual Studio 2010 中的 web 部署功能包括以下主要方面：

- Web 打包
- Web.config 转换
- 数据库部署
- 单击发布为 Web 应用程序

以下部分提供有关这些功能的详细信息。

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a>Web 打包

Visual Studio 2010 使用 MSDeploy 工具来创建应用程序，这被称为一个压缩 (.zip) 文件*Web 包*。 包文件包含有关你的应用程序以及以下内容的元数据：

- IIS 设置，其中包括应用程序池设置、 错误页设置等。
- 实际 Web 内容，其中包括 Web 页面、 用户控件、 静态内容 （映像和 HTML 文件） 等。
- SQL Server 数据库架构和数据。
- 安全证书，组件安装在 GAC、 注册表设置等。

可以复制到任何服务器，然后通过使用 IIS 管理器手动安装 Web 包。 或者，对于自动部署，包可安装使用命令行命令或使用部署 Api。

Visual Studio 2010 提供了内置的 MSBuild 任务和目标以创建 Web 包。 有关详细信息，请参阅[ASP.NET Web 应用程序项目部署概述](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx)MSDN 网站上和[10 + 20 原因为何应创建 Web 包](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html)在 Vishal Joshi 博客上。

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a>Web.config 转换

对于 Web 应用程序部署，Visual Studio 2010 引入了[XML 文档转换 (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)，这是一项功能，允许你转换`Web.config`开发设置中为生产设置的文件。 转换设置名为的转换文件中指定`web.debug.config`， `web.release.config`，依次类推。 （这些文件的名称匹配 MSBuild 配置。）转换文件包括只是需要对已部署进行的更改`Web.config`文件。 使用简单的语法指定所做的更改。

下面的示例显示了一部分`web.release.config`可能生成部署的发布配置文件。 在示例中的替换关键字在部署过程中指定*connectionString*中的节点`Web.config`文件将替换示例中列出的值。

[!code-xml[Main](overview/samples/sample102.xml)]

有关详细信息，请参阅[Web 应用程序项目部署的 Web.config 转换语法](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx)msdn <a id="0.2_a"> </a> Web 站点和[Web 部署： Web.Config 转换](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)Vishal Joshi 博客上。

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a>数据库部署

Visual Studio 2010 部署包可以包含 SQL Server 数据库上的依赖项。 为包定义的一部分，为源数据库提供连接字符串。 创建 Web 包时，Visual Studio 2010 创建 SQL 脚本 （可选） 为数据库架构和数据，，然后添加到包。 此外可以提供自定义 SQL 脚本，并指定其应运行在服务器的序列。 在部署时，提供了适合于目标服务器; 一个连接字符串然后，部署过程使用此连接字符串来运行脚本，创建数据库架构，并添加数据。

此外，通过使用一次单击发布，您可以配置部署应用程序发布到远程共享托管站点时，直接发布你的数据库。 有关详细信息，请参阅[如何： 部署数据库与 Web 应用程序项目](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx)MSDN 网站上和[VS 2010 使用的数据库部署](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)在 Vishal Joshi 博客上。

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a>单击发布为 Web 应用程序

Visual Studio 2010 还允许您使用的 IIS 远程管理服务发布到远程服务器的 Web 应用程序。 为你的托管帐户或测试服务器或暂存服务器，可以创建发布配置文件。 每个配置文件可以安全地保存相应的凭据。 你可以随后部署到任何目标服务器通过使用 Web 一次单击一次单击发布工具栏。 使用 Visual Studio 2010，您还可以通过使用 MSBuild 命令行发布。 这允许您配置您的团队生成环境，以持续集成模型中包括发布。

有关详细信息，请参阅[如何： 部署 Web 应用程序项目使用一键式发布和 Web 部署](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx)MSDN 网站上和[Web 一键式发布使用 VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html)在 Vishal Joshi 博客上。 若要在 Visual Studio 2010 中查看有关 Web 应用程序部署的视频演示，请参阅[VS 2010 Web 开发人员预览版](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html)在 Vishal Joshi 博客上。

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a>资源

以下网站提供有关 ASP.NET 4 和 Visual Studio 2010 的其他信息。

- [ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — MSDN 网站上的 ASP.NET 4 的官方文档。
- [https://www.asp.net/](https://www.asp.net/) — ASP.NET 团队的网站。
- [https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) 并[ASP.NET 动态数据内容映射](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx)— ASP.NET 团队网站和 ASP.NET 动态数据有关的正式文档中的在线资源。
- [https://www.asp.net/ajax/](../../ajax/index.md) — ASP.NET Ajax 开发主 Web 资源。
- [https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) — Visual Studio 2010 中包括有关功能的信息 Visual Web 开发人员团队博客。
- [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — ASP.NET 的预览版本的主要 Web 资源。

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a>免责声明

这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。

本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。 由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。

本白皮书仅用于提供信息。 MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。

遵守所有适用的著作权法是用户的责任。 未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。

对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。 除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。

除非另有说明，示例公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人物、 地点和事件属虚构的并且无意与任何真实的公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人员、 地点或事件无关，也应进行这方面的推断。

© 2009 Microsoft Corporation. 保留所有权利。

Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。

此处提到的真实公司和产品的名称可能是其各自所有者的商标。
