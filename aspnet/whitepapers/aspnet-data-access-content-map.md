---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET 数据访问-推荐的资源 |Microsoft Docs
author: rick-anderson
description: 本主题提供有关如何访问 ASP.NET web 应用程序中的数据主要是通过使用实体框架和 SQL Se 文档资源的链接...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 6993c17c8de890cbaa40c619bcd20f494bfd2f90
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825070"
---
<a name="aspnet-data-access---recommended-resources"></a>ASP.NET 数据访问-推荐的资源
====================
> 本主题提供有关如何访问 ASP.NET web 应用程序中的数据主要是通过使用实体框架和 SQL Server 的文档资源的链接。
> 
> 如果您知道很好的博客文章[堆栈溢出](http://stackoverflow.com)线程或都非常有用，任何其他链接[向我们发送一封电子邮件](mailto:aspnetue@microsoft.com?subject=Data Access Content Map)与链接。
> 
> 上次更新： 2014 年 4 月 3 日


本主题包含以下各节：

- [在 ASP.NET 中的数据访问入门](#gettingstarted)
- [使用实体框架](#ef)

    - [使用实体框架 Code First](#cf)
    - [使用 Entity Framework Code First 迁移](#efcfmigrations)
    - [首先使用 Entity Framework 数据库或模型优先 （EF 设计器）](#efdbf)
    - [加载实体框架 （延迟加载、 预先加载和显式加载） 中的相关的数据](#efrelateddata)
    - [优化实体框架性能](#optimizingef)
    - [中的实体框架应用程序的并发处理](#efconcurrency)
    - [有关实体框架的书籍](#efbooks)
    - [实体框架的其他资源](#otherefresources)
- [数据绑定在 ASP.NET Web 窗体应用程序](#wfdatabinding)

    - [使用 Web 窗体模型绑定](#wfmodelbinding)
    - [使用 Web 窗体数据源控件](#wfdsc)
    - [使用 Web 窗体数据绑定控件和数据绑定表达式](#wfdbc)
- [使用 SQL Server 数据库](#sqlserver)

    - [使用 SQL Server Express LocalDB 数据库](#sslocaldb)
    - [使用 SQL Server Express 数据库](#sse)
    - [使用 Windows Azure SQL 数据库](#ssdb)
    - [SQL Server 和 Windows Azure SQL 数据库之间进行选择](#ssdbchoosing)
- [使用 NoSQL 数据库管理系统](#nosql)
- [在 ASP.NET 应用程序中使用 LINQ 查询](#linq)
- [使用动态数据基架](#dd)
- [保护数据的访问](#securing)
- [优化数据访问性能](#optimizingdataaccess)
- [部署数据库](#deploying)
- [通过 Web 服务访问数据](#webservice)
- [其他资源](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>在 ASP.NET 中的数据访问入门

- [数据存储选项 （使用 Windows Azure 构建实际云应用）](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md)。 有关云开发的电子书的章节。 作为熟悉关系数据库的许多开发人员往往会忽视的替代方法，引入了 NoSQL 数据库。 显示内容时要考虑选择关系或 NoSQL，或选择特定平台的指导原则。
- [ASP.NET 数据访问选项](https://msdn.microsoft.com/library/ms178359.aspx)(MSDN)。 关系数据库的 ASP.NET 数据访问选项和如何选择平台并访问适用于你的方案的方法的指南简介。
- [关系数据库](http://en.wikipedia.org/wiki/Relational_database)。 维基百科）。 如果您没有用过关系数据库，请参阅本页的关系数据库术语和概念的简介。 有关 SQL Server 的简介中具体地讲就[使用 SQL Server 数据库](#sqlserver)本主题中更高版本。

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>使用实体框架

- [实体框架开发方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)(MSDN)。 有关如何进行选择的实体框架开发方法数据库优先，Model First 或 Code First 的指导。

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>使用实体框架 Code First
  

以下教程提供了可下载的示例应用程序：

- [开始使用 EF 6 使用 MVC 5](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 涵盖广泛的 Entity Framework Code First 的方案，包括迁移和 EF 6 连接复原、 命令拦截和异步等功能。 这是更新的版本[EF 5 / MVC 4 系列](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 早期的系列上的存储库和工作单元模式不包括在新系列中所含教程。
- [ASP.NET MVC 5 简介](../mvc/overview/getting-started/introduction/getting-started.md)。 介绍如何更窄的实体框架代码的范围内第一个方案，但更全面地介绍 MVC 功能。
- [模型绑定和 Web 窗体](https://go.microsoft.com/fwlink/?LinkId=286117)。 在 Web 窗体应用程序中使用代码优先。
- [开始使用 ASP.NET 4.5 Web 窗体](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 介绍 Web 窗体与某些范围的第一个代码。 使用模型绑定。
- [MVC Music 商店](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md)。 此外实现了成员身份和授权的电子商务 MVC 3 应用程序中使用代码优先。 MVC 版本和 ASP.NET 成员资格 （身份验证和授权） 系统此处使用是已过时;ASP.NET 成员资格的更多最新信息，请参阅[ https://asp.net/identity ](https://asp.net/identity)。

其他资源：

- [实体框架的代码首先对现有数据库](https://msdn.microsoft.com/data/jj200620)。 MSDN。 视频和演练，演示如何使用 Code First 与现有数据库。
- [数据开发人员中心-实体框架](https://msdn.microsoft.com/data/ef)。 MSDN。 已创建并由实体框架团队维护的实体框架文档的指南，请参阅[开始](https://msdn.microsoft.com/data/ee712907)链接。

另请参阅[有关实体框架的书籍](#efbooks)并[其他实体框架资源](#otherefresources)本主题中更高版本。

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>使用 Entity Framework Code First 迁移
  

大多数代码优先封面迁移上面列出的教程。 另请参阅以下资源。

- [使用 Visual Studio 的 ASP.NET Web 部署](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 两个部分构成的系列教程演示如何使用 Code First 迁移部署数据库。
- [使用成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 5 应用部署到 Windows Azure 网站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 Microsoft Azure)。 如何使用迁移到 Azure 部署成员资格和应用程序数据。
- [适用于 Visual Studio 和 ASP.NET 的 web 部署概述](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment)。 请参阅**Visual Studio 中配置数据库部署**部分，了解如何将 Code First 迁移集成到 Visual Studio web 部署功能的说明。
- [数据开发人员中心-Code First 迁移](https://msdn.microsoft.com/data/jj591621)(MSDN)。 实体框架团队的迁移文档。
- [迁移截屏视频系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。 EF 博客）。 Code First 迁移中的高级主题的三段视频。
- [Code First 迁移与 ASP.NET Web Pages 站点](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites)。 Mikesdotnetting 博客）。 演示如何通过将数据上下文放在 Visual Studio 类库项目中与 ASP.NET Web Pages 站点使用 Code First 迁移。

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>首先使用 Entity Framework 数据库或模型优先 （EF 设计器）

- [开始使用 Entity Framework 6 Database First 通过 MVC 5](../mvc/overview/getting-started/database-first-development/setting-up-database.md)。 在服务器资源管理器来创建数据库，运行脚本，然后使用实体框架设计器创建数据模型。 演示如何创建简单的 CRUD web 页面，以及为其他数据处理函数，因为 EF 的所有工作流使用相同的 DbContext API，可以按照代码优先的教程之一。

以下资源是较旧。 如果你想要使用 4.0 版实体框架中，并且你想要用于 Web 窗体应用程序中的数据绑定的数据源控件，很有用。

- [开始使用 Entity Framework 4.0](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)。 演示如何使用**EntityDataSource**控件。
- [与实体框架继续](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)(演示如何使用**ObjectDataSource**控件。 包括并发处理，EF 性能的教程和 EF 4.0 中新增的教程的教程。

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>处理相关的实体框架 （延迟加载、 预先加载和显式加载） 中的数据

- [读取相关的数据与 ASP.NET MVC 应用程序中的实体框架](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 代码优先，MVC 示例应用程序。 所示的方法也同样适用于 Web 窗体模型绑定和数据库优先工作流。
- [数据开发人员中心-加载相关的实体](https://msdn.microsoft.com/data/jj574232)(MSDN)。 有关加载的实体框架团队的文档与相关数据。

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>优化实体框架性能

- [ASP.NET 应用程序的高级 Entity Framework 方案](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。 演示如何执行您自己的 SQL 语句或调用存储的过程、 如何禁用更改检测，以及如何在保存更改时禁用验证。
- [实体框架 5 性能注意事项](https://msdn.microsoft.com/data/hh949853)(MSDN)。
- [性能注意事项 （实体框架）](https://msdn.microsoft.com/library/cc853327) (MSDN)。
- [使用实体框架在 ASP.NET Web 应用程序中性能最大化](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)。 适用于实体框架 4.0。
- 另请参阅[优化 ASP.NET 数据访问](#optimizingdataaccess)本主题中更高版本。

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>中的实体框架应用程序的并发处理

- [处理与实体框架在 ASP.NET MVC 应用程序中的并发](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 代码优先，DbContext API，使用 MVC 示例应用程序。
- [数据开发人员中心-乐观并发模式](https://msdn.microsoft.cus/data/jj592904)(MSDN)。 实体框架团队的并发文档。
- [处理与实体框架在 ASP.NET Web 应用程序中的并发](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)。 适用于实体框架 4.0。 数据库优先，ObjectContext API，使用 Web 窗体示例应用程序。

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>有关实体框架的书籍

- [Programming Entity Framework: DbContext](http://shop.oreilly.com/product/0636920022237.do) Julie Lerman 和 Rowan Miller 的。
- [Programming Entity Framework： 代码优先](http://shop.oreilly.com/product/0636920022220.do)Julie Lerman 和 Rowan Miller 的。

这两本书是与当前的推荐技术最新。 它们在 Internet 上提供的更全面而简单易懂的介绍实体框架比任何可用。 另一本书[Programming Entity Framework](http://shop.oreilly.com/product/9780596807252.do)作者： Julie Lerman 是更大、 更全面但它是较旧，权限的许多技术它涵盖了使用实体框架的建议的方法。 另请参阅实体框架团队的建议列表[数据开发人员中心-丛书](https://msdn.microsoft.com/data/aa937716)MSDN 站点上。

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>其他实体框架资源

- [Entity Framework (ADO.NET) 团队博客](https://blogs.msdn.com/b/adonet/)。 有关最新信息和公告的新的增强功能的最佳资源之一。 有关其他与 EF 相关的博客，请参阅在博客列表[开始使用实体框架](https://msdn.microsoft.com/data/ee712907)。
- [MSDN 杂志 》](https://msdn.microsoft.com/magazine/default.aspx)。 请参阅**数据点**列中，这往往是有关实体框架与相关的主题。

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>数据绑定在 ASP.NET Web 窗体应用程序

- [ASP.NET Web 窗体数据访问选项](https://msdn.microsoft.com/library/jj822927.aspx)(MSDN)<a id="wfmodelbinding"></a>。

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>使用 Web 窗体模型绑定

- [模型绑定和 Web 窗体](https://go.microsoft.com/fwlink/?LinkId=286117)。 使用 EF Code First 的系列教程。
- [Web 窗体模型绑定第 1 部分： 选择数据](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx)（Scott Guthrie 的博客）。 在这些较旧的博客文章，目前名为 ItemType 属性名为 ModelType，但它们所包含的信息的有效。
- [Web 窗体模型绑定第 2 部分： 筛选数据](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx)（Scott Guthrie 的博客）。
- [Web 窗体模型绑定第 3 部分： 更新和验证](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx)（Scott Guthrie 的博客）。
- [ASP.NET 4.5 Web 窗体模型绑定](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md)。 （视频）。
- [模型绑定第 1 部分-选择数据](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md)（视频）。
- [模型绑定第 2 部分-筛选](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md)（视频）。
- [获取开始使用 ASP.NET 4.5 Web 窗体的显示的数据项目和详细信息](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)。

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>使用 Web 窗体数据源控件

- [数据源 Web 服务器控件](https://msdn.microsoft.com/library/ms247258.aspx)(MSDN)。
- [宣布发布 Entity Framework 6 EntityDataSource 控件和动态数据提供程序的版本](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)（Microsoft Web 开发博客）。

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>使用 Web 窗体数据绑定控件和数据绑定表达式

- [模型绑定和 Web 窗体](https://go.microsoft.com/fwlink/?LinkId=286117)。 使用 EF Code First 的教程系列。
- [获取开始使用 ASP.NET 4.5 Web 窗体的显示的数据项目和详细信息](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)。
- [强类型数据控件](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx)（Scott Guthrie 的博客）。
- [强类型数据控件](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)（视频）。
- [ASP.NET 4.5 Web 窗体强类型数据控件](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)（视频）。
- [数据绑定的 Web 服务器控件](https://msdn.microsoft.com/library/ms228214.aspx)(MSDN)。
- [数据绑定表达式概述](https://msdn.microsoft.com/library/ms178366.aspx)(MSDN)。 此页，仅涵盖了**Eval**并**绑定**; 它尚未更新以包括**项**并**BindItem**。

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>使用 SQL Server 数据库

- [SQL Server 数据库功能](https://msdn.microsoft.com/library/hh230827.aspx)(MSDN)。 有关各种 SQL Server 主题的常规介绍，请参阅中的以下目录下的条目。
- [SQL Server 版本](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver)(MSDN)。 可用的 SQL Server 版本，其中包含指向有关每个详细信息的摘要。）
- [ASP.NET Web 应用程序的 SQL Server 连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)(MSDN)。
- [为 ASP.NET Web 应用程序使用 SQL Server Compact](https://msdn.microsoft.com/library/ms247257.aspx) (MSDN)。
- [Microsoft SQL Server： 数据库产品示例](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)。 示例 AdventureWorks 数据库。
- [安装示例数据库](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)。 除了此处所示的方法，你也可以下载一个示例.mdf 文件到应用\_数据文件夹的 web 项目中，将数据库转换为 LocalDB，并创建 LocalDB 连接字符串。 有关如何执行该操作的信息，请参阅[如何： 升级到 LocalDB](https://msdn.microsoft.com/library/hh873188.aspx)。

另请参阅以下各节关于使用 SQL Server Express 和 LocalDB 和 SQL Server 和 SQL 数据库之间进行选择。

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>使用 SQL Server Express LocalDB 数据库

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN)。 官方 MSDN 简介 LocalDB。
- [ASP.NET Web 应用程序的 SQL Server 连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)(MSDN)。
- [如何： 升级到 LocalDB](https://msdn.microsoft.com/library/hh873188.aspx) (MSDN)。 如何将从早期版本的 SQL Server Express.mdf 文件迁移到 LocalDB。 您还必须经历此过程，如果下载之一[SQL Server 2012 示例数据库](https://go.microsoft.com/fwlink/?linkid=117483)。
- [引入经改进的 SQL Express LocalDB](https://go.microsoft.com/fwlink/?LinkId=234375) （SQL Server Express 博客）。 具有更多背景信息不是包括在 MSDN 中为何创建 LocalDB。
- [LocalDB： 其中，是我的数据库？](https://go.microsoft.com/fwlink/?LinkId=234376) （SQL Server Express 博客）。 有关在其中创建 LocalDB 数据库文件的信息。
- [使用 LocalDB 与完整 IIS，第 1 部分： 用户配置文件](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx)（SQL Server Express 博客）。 LocalDB 不用于与 IIS 配合使用。 这一系列的博客文章介绍了这些问题和解决办法。

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>使用 SQL Server Express 数据库

- [ASP.NET Web 应用程序的 SQL Server 连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)(MSDN)。 如果使用 SQL Server Express 使用 AttachDBFileName 连接字符串设置，请参阅尤其是此页的用户实例部分。
- [如何在本地 SQL Server Express 2008 的所有权](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx)（SQL Server Express 博客）。 一个常见的问题不能够使用 SQL Server Express 数据库，因为你不是 SQL Server Express 实例上的管理员。 默认情况下，只有安装了 SQL Server Express 的用户是管理员。 此博客介绍了如何使自己的 SQL Server Express 管理员如果你是计算机上的管理员。
- [我的 ASP.NET web 应用程序是否可以在生产环境中使用 SQL Server Express 数据库？](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN)。

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>使用 Windows Azure SQL 数据库

- [包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 应用部署到 Windows Azure 网站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)（Microsoft Azure 网站）。
- [SQL 数据库](https://docs.microsoft.com/azure/sql-database/)（Microsoft Azure 网站）。 获取教程和操作方法指南。
- [Windows Azure SQL 数据库](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx)(MSDN)。 在 MSDN 中的 SQL 数据库的内容的表的顶级节点。
- [Windows Azure SQL 数据库 TechNet Wiki 文章索引](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx)（Microsoft TechNet 站点）。
- [暂时性故障处理应用程序块](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx)。 一个框架，使你能够处理暂时性网络故障和连接错误阻止该结果。 NuGet 包中提供： [Enterprise Library 5.0-临时故障处理应用程序块](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling)。
- [开始使用 SQL 数据库和 Entity Framework](https://msdn.microsoft.com/data/jj556244) (MSDN)。
- [Windows Azure 培训工具包](https://www.microsoft.com/download/details.aspx?id=8396)（Microsoft 下载中心）。 为 SQL 数据库包括动手实验。
- [Windows Azure SQL Database 社区论坛](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads)。
- [将移动到 Windows Azure SQL 数据库](https://msdn.microsoft.com/library/ff803375.aspx)(MSDN)。 由 Microsoft 模式和实践团队的全面的端到端方案的一章。 为什么你可能想要迁移的封面和如何将 SQL Server 迁移到 SQL 数据库。
- [将 SQL Server 数据库迁移到 Windows Azure SQL 数据库](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx)(MSDN)。
- [SQL Database 迁移向导](http://sqlazuremw.codeplex.com/)。 向 / 从 SQL 数据库的数据库迁移的开放源代码工具。

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>SQL Server 和 Windows Azure SQL 数据库之间进行选择

- [比较使用 Windows Azure SQL 数据库的 SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) （Microsoft TechNet 站点）。
- [数据迁移到 Windows Azure SQL Database： 工具和技术](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx)(MSDN)。 包括部分，比较 SQL Server 到 SQL 数据库，并提供指导用户何时将从 SQL Server 迁移到 SQL 数据库。
- [Windows Azure SQL Database 交付指南](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx)（Microsoft TechNet 站点）。
- [SQL Server 功能限制 （Windows Azure SQL 数据库）](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN)。
- [Windows Azure 表存储和 Windows Azure SQL 数据库-比较与对照](https://msdn.microsoft.com/library/jj553018.aspx)(MSDN)。 对于部署到 Windows Azure 的应用程序，Windows Azure 表存储可能是 Windows Azure SQL 数据库的替代方法。 本主题可帮助您决定这些备选方法之间。
- [Windows Azure SQL 数据库](https://msdn.microsoft.com/library/windowsazure/ee336279)(MSDN)。
- [指导原则和限制 （Windows Azure SQL 数据库）](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>使用 NoSQL 数据库管理系统

- [Windows Azure 数据服务](https://www.windowsazure.com/develop/net/data/)（Microsoft Azure 网站）。 请参阅[表服务功能指南](https://docs.microsoft.com/azure/)并**大数据**页部分。
- [ASP.NET 多层应用程序使用存储表、 队列和 Blob](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) （Microsoft Azure 网站）。 与使用 Windows Azure 存储 NoSQL 表的可下载的示例应用程序的端到端教程。

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>在 ASP.NET 应用程序中使用 LINQ 查询

- [ASP.NET 数据访问选项](https://msdn.microsoft.com/library/ms178359.aspx#linq)(MSDN)。 包括 LINQ 简介。
- [LINQ 培训视频](http://www.misfitgeek.com/windows-client-linq-training-videos-20/)（Joe Stagner 博客）。
- [ASP.NET 论坛主题以及指向动态 LINQ 资源](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq)。

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>使用动态数据基架

- [动态数据项目模板](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata)(MSDN)。 有关何时使用动态数据项目的指南。
- [ASP.NET 动态数据](https://msdn.microsoft.com/library/ee845452.aspx)(MSDN)。

<a id="securing"></a>

## <a name="securing-data-access"></a>保护数据的访问

- [保护在 ASP.NET 中的数据访问](https://msdn.microsoft.com/library/ms178375.aspx)(MSDN)。
- [安全注意事项 （实体框架）](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN)。
- [如何： 安全连接字符串时使用的数据源控件](https://msdn.microsoft.com/library/ms178372.aspx)(MSDN)。

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>优化数据访问性能

- [ASP.NET 性能概述](https://msdn.microsoft.com/library/cc668225.aspx)(MSDN)。
- [ASP.NET 缓存](https://msdn.microsoft.com/library/xsbfdd8c.aspx)(MSDN)。
- [提高 ASP.NET 性能](https://msdn.microsoft.com/library/ff647787)(MSDN)。 没有在此页上，顶部的"内容已停用"警告，但大部分信息仍适用，并且没有没有可比较更新后的资源。
- [提高 SQL Server 性能](https://msdn.microsoft.com/library/ff647793)(MSDN)。 为上一链接的同一个注释。

另请参阅[优化实体框架性能](#optimizingef)本主题前面的。

<a id="deploying"></a>

## <a name="deploying-a-database"></a>部署数据库

- [ASP.NET Web 部署-推荐的资源](aspnet-web-deployment-content-map.md)(MSDN)。

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>通过 Web 服务访问数据

- [通过 Web 服务访问数据](https://msdn.microsoft.com/library/ms178359.aspx#webservice)(MSDN)。 有关何时使用 Web API 与 WCF 的指南。
- [ASP.NET Web API 入门](../web-api/index.md)。
- [WCF 数据服务](https://msdn.microsoft.com/data/bb931106)(MSDN)。

<a id="additional"></a>

## <a name="additional-resources"></a>其他资源

- [ASP.NET 数据访问 FAQ](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN)。
- [ASP.NET Web 窗体教程-数据](../web-forms/overview/data-access/index.md)。 这些教程的大部分都是相对较旧;请确保阅读[ASP.NET 数据访问选项](https://msdn.microsoft.com/library/ms178359.aspx)并[数据存储选项 （构建实际云应用程序使用 Windows Azure）](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md)第一个，以便不会太远陷入不正确的数据访问方法为你的方案。
- [ASP.NET MVC 内容导航图](../mvc/overview/getting-started/recommended-resources-for-mvc.md)。
- [ASP.NET Web Pages 教程-数据](../web-pages/overview/data/index.md)。
- [在 Visual Studio 中访问数据](https://msdn.microsoft.com/library/wzabh8c4.aspx)(MSDN)。 提供了一系列类似的链接到此内容导航图，但重点是 Visual Studio 而不是 ASP.NET。
