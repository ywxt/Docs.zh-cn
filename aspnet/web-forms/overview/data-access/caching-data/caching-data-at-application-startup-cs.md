---
uid: web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
title: 缓存数据在应用程序启动 (C#) |Microsoft Docs
author: rick-anderson
description: 在任何 Web 应用程序中的某些数据将频繁使用，将不常使用的某些数据。 我们可以改进我们的 ASP.NET 应用程序 b 的性能...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 22ca8efa-7cd1-45a7-b9ce-ce6eb3b3ff95
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
msc.type: authoredcontent
ms.openlocfilehash: 2c7d00a21663746964e086a75fd4b64ed211ed5f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825799"
---
<a name="caching-data-at-application-startup-c"></a>缓存数据在应用程序启动 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](caching-data-at-application-startup-cs/_static/datatutorial60cs1.pdf)

> 在任何 Web 应用程序中的某些数据将频繁使用，将不常使用的某些数据。 我们可以通过预先加载常用数据，称为的技术改进我们的 ASP.NET 应用程序的性能。 本教程演示了主动加载，这是将数据加载到应用程序启动时缓存的一种方法。


## <a name="introduction"></a>介绍

两个以前的教程介绍了在演示文稿和缓存层中缓存数据。 在中[使用 ObjectDataSource 缓存数据](caching-data-with-the-objectdatasource-cs.md)，我们了解了使用缓存在表示层中缓存数据的功能的 ObjectDataSource s。 [缓存体系结构中的数据](caching-data-in-the-architecture-cs.md)检查在缓存中新的、 独立缓存层。 这两个使用这些教程*反应加载*中使用的数据缓存。 与被动加载，每次请求数据时，系统首先检查它在缓存。 否则，它获取原始源，例如，数据库中的数据，然后将其存储在缓存中。 响应式加载的主要优点是实现其易用性。 在请求之间，其缺点之一是其性能不稳定。 假设使用前面教程中的缓存层来显示产品信息的页面。 当此页是第一次访问或缓存的数据已退出由于内存约束或具有已达到指定的到期后第一次访问过时，则必须从数据库检索的数据。 因此，这些用户请求将执行时间超过可以提供的用户请求的缓存。

*主动加载*提供替代缓存管理策略性能平滑处理在请求之间通过加载之前缓存的数据需要。 通常情况下，主动加载使用某些进程，可定期检查或已对基础数据的更新时收到通知。 然后，此过程更新缓存，以使其保持最新。 主动加载是特别有用，如果基础数据来自速度缓慢的数据库连接、 Web 服务或某些其他尤其缓慢的数据源。 但与主动加载这种方法是更难以实现，因为它需要创建、 管理和部署过程以检查更改并更新缓存。

另一种形式主动加载和我们将在本教程中探讨的类型将数据加载到应用程序启动时缓存。 这种方法是用于缓存静态数据，如数据库查找表中记录特别有用。

> [!NOTE]
> 有关主动和被动加载的优点、 缺点和实现的建议列表之间的差异的深入信息，请参阅[管理缓存的内容](https://msdn.microsoft.com/library/ms978503.aspx)一部分[缓存的.NET Framework 应用程序的体系结构指南](https://msdn.microsoft.com/library/ms978498.aspx)。


## <a name="step-1-determining-what-data-to-cache-at-application-startup"></a>步骤 1： 确定哪些应用程序启动时缓存的数据

使用被动加载缓存示例中，我们探讨在以前的两个教程工作良好的数据可能会定期更改，而不使用 exorbitantly 长生成。 但是，如果缓存的数据永远不会更改，过期日期由反应加载多余。 同样，如果要缓存的数据采用非常长的时间才能生成，则检索这些用户的请求查找必须经受基础数据时耗时较长等待缓存为空。 请考虑缓存静态数据和所用的特别长时间来在应用程序启动时生成的数据。

当数据库都有很多动态时，频繁地更改值，但大多数还有大量的静态数据。 例如，几乎所有数据模型都具有包含特定值从一组固定的选项的一个或多个列。 一个`Patients`数据库表可能具有`PrimaryLanguage`列，其组的值可能是英语、 西班牙语、 法语、 俄语、 日语和等等。 通常，使用实现这些类型的列*查找表*。 而不是存储英语或法语中的字符串`Patients`表中，第二个表将创建一个常见的是，带有两个列中的唯一标识符和字符串说明-与每个可能值的记录。 `PrimaryLanguage`中的列`Patients`表查找表中存储的相应的唯一标识符。 在图 1 中，患者 John Doe s 主要语言是英语，而 Ed Johnson s 是俄语。


![语言表是通过患者表使用查找表](caching-data-at-application-startup-cs/_static/image1.png)

**图 1**:`Languages`表是通过使用查找表`Patients`表


编辑或创建新的患者的用户界面将包括允许语言中的记录所填充的下拉列表`Languages`表。 不使用缓存功能，此接口是每次访问系统必须查询`Languages`表。 如果这是浪费和不必要由于查找表值极少更改过。

我们无法缓存`Languages`数据使用相同的响应式加载方法，检查在前面的教程。 响应式加载，但是，使用静态查找表数据，不需要基于时间的到期。 虽然缓存使用响应式加载会比无缓存更好，最好的方法是主动的查找表数据加载到应用程序启动时缓存。

在本教程将探讨如何缓存查找表数据和其他静态信息。

## <a name="step-2-examining-the-different-ways-to-cache-data"></a>第 2 步： 检查缓存数据的不同方式

可以使用多种方法的 ASP.NET 应用程序中以编程方式缓存信息。 我们 ve 已经看到了如何在前面的教程中使用的数据缓存。 或者，可以以编程方式缓存对象使用*静态成员*或*应用程序状态*。

在使用一个类，通常类必须首先实例化之前可以访问其成员。 例如，为了调用一种方法从我们的业务逻辑层中的类之一，我们必须首先创建类的实例：


[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample1.cs)]

我们可以调用之前*SomeMethod*或使用*SomeProperty*，我们必须先创建的类实例`new`关键字。 *SomeMethod*并*SomeProperty*与特定实例相关联。 这些成员的生存期取决于其关联的对象的生存期。 *静态成员*，但是，将变量、 属性和方法之间共享*所有*类的实例，因此，具有长达类的生存期。 静态成员表示由关键字`static`。

除了静态成员，可以使用应用程序状态缓存数据。 每个 ASP.NET 应用程序维护名称/值集合的所有用户和应用程序的页面之间共享该 s。 可以使用访问此集合[`HttpContext`类](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)s [ `Application`属性](https://msdn.microsoft.com/library/system.web.httpcontext.application.aspx)，并从一种 ASP.NET 页的代码隐藏类如下所示：


[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample2.cs)]

数据缓存的缓存数据，提供的基于时间和依赖关系的满、 缓存项优先级等机制提供了多更丰富的 API。 使用静态成员和应用程序状态，此类功能必须由页面开发人员手动添加。 当应用程序的生存期内缓存在应用程序启动的数据，但是，数据缓存的优点是毫无意义了。 在本教程中我们将介绍用于缓存静态数据使用所有这三种技术的代码。

## <a name="step-3-caching-thesupplierstable-data"></a>步骤 3： 缓存`Suppliers`表数据

Northwind 数据库表我们已实施方法与日期不包括任何传统的查找表。 实现四个 DataTables DAL 中其值为非静态的所有模型表。 而不是花费时间来将一个新的 DataTable 添加到 DAL 的新类并向 BLL，方法为本教程只是让 s 伪装的`Suppliers`表的数据是静态的。 因此，我们无法缓存此数据在应用程序启动。

若要开始，创建一个名为的新类`StaticCache.cs`在`CL`文件夹。


![CL 文件夹中创建 StaticCache.cs 类](caching-data-at-application-startup-cs/_static/image2.png)

**图 2**： 创建`StaticCache.cs`类中`CL`文件夹


我们需要添加一个方法，在启动时将数据加载到合适的缓存存储区，以及从此缓存中返回数据的方法。


[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample3.cs)]

上面的代码中使用静态成员变量`suppliers`，以保留的结果`SuppliersBLL`类 s`GetSuppliers()`方法，从调用`LoadStaticCache()`方法。 `LoadStaticCache()`方法应该在应用程序的启动期间被调用。 此数据加载在应用程序启动后，可以调用需要与供应商数据协同工作的任何页面`StaticCache`类的`GetSuppliers()`方法。 因此，对数据库的调用以获取供应商只出现一次启动应用程序时。

而不是作为缓存存储区中使用的静态成员变量，我们也可以或者使用应用程序状态或数据缓存。 下面的代码显示了进行重组以使用应用程序状态的类：


[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample4.cs)]

在中`LoadStaticCache()`，供应商信息存储到程序变量*密钥*。 它返回为相应的类型 (`Northwind.SuppliersDataTable`) 从`GetSuppliers()`。 虽然可以使用的 ASP.NET 页的代码隐藏类中访问应用程序状态`Application["key"]`，在我们必须使用的体系结构`HttpContext.Current.Application["key"]`以获取当前`HttpContext`。

同样，数据缓存可以用作缓存存储区中，如以下代码所示：


[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample5.cs)]

若要将项添加到其任何基于时间的到期时间的数据缓存，请使用`System.Web.Caching.Cache.NoAbsoluteExpiration`和`System.Web.Caching.Cache.NoSlidingExpiration`作为输入参数的值。 这一特定的数据缓存的重载`Insert`已选择的方法，以便我们可以指定*优先级*的缓存项。 优先级用于确定哪些项目清理从缓存中，当可用内存不足。 此处，我们使用优先级`NotRemovable`，这可确保此缓存项赢得 t 被清理。

> [!NOTE]
> 此教程的下载实现`StaticCache`类使用静态成员变量方法。 应用程序状态和数据缓存技术的代码位于类文件中的注释。


## <a name="step-4-executing-code-at-application-startup"></a>步骤 4： 执行代码在应用程序启动

若要执行代码的 web 应用程序首次启动时，我们需要创建一个名为的特殊文件`Global.asax`。 此文件可以包含的应用程序-，会话的事件处理程序和请求级事件，它是此处我们可以在其中添加每次应用程序启动时执行的代码。

添加`Global.asax`网站项目名称，在 Visual Studio 的解决方案资源管理器中右键单击并选择添加新项在 web 应用程序的根目录下的文件。 从添加新项对话框中，选择应用程序的全局类项类型，然后单击添加按钮。

> [!NOTE]
> 如果已有`Global.asax`文件在项目中，不会在添加新项对话框中列出项类型在全局应用程序类。


[![Global.asax 文件添加到 Web 应用程序的根目录](caching-data-at-application-startup-cs/_static/image4.png)](caching-data-at-application-startup-cs/_static/image3.png)

**图 3**： 添加`Global.asax`为 s 的 Web 应用程序根目录的文件 ([单击以查看实际尺寸的图像](caching-data-at-application-startup-cs/_static/image5.png))


默认值`Global.asax`文件模板包括在服务器端中的五种方法`<script>`标记：

- **`Application_Start`** 执行 web 应用程序首次启动时
- **`Application_End`** 当应用程序关闭时运行
- **`Application_Error`** 每当未处理的异常到达应用程序执行
- **`Session_Start`** 执行时创建一个新会话
- **`Session_End`** 在运行时的会话已过期或已放弃

`Application_Start` S 应用程序生命周期内仅一次调用事件处理程序。 在应用程序启动第一次 ASP.NET 资源请求从应用程序，并继续运行，直到重新启动该应用程序时，其可能会通过修改的内容`/Bin`文件夹中，修改`Global.asax`，修改在内容`App_Code`文件夹，或修改`Web.config`文件，其他原因。 请参阅[ASP.NET 应用程序生命周期概述](https://msdn.microsoft.com/library/ms178473.aspx)有关应用程序生命周期的更多详细讨论。

这些教程中我们只需将代码添加到`Application_Start`方法，因此，可随时删除。 在中`Application_Start`，只需调用`StaticCache`类的`LoadStaticCache()`方法，它将加载并缓存供应商信息：


[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample6.aspx)]

该 s 都在这里就简单 ！ 在应用程序启动时，`LoadStaticCache()`方法将获取从 BLL，供应商信息，并将其存储在静态成员变量 (或任何缓存存储您最终会在中使用`StaticCache`类)。 若要验证此行为中, 设置断点`Application_Start`方法并运行应用程序。 请注意应用程序启动时命中断点。 后续请求中，但是，不会导致`Application_Start`要执行的方法。


[![使用验证 Application_Start 事件处理程序正在执行的断点](caching-data-at-application-startup-cs/_static/image7.png)](caching-data-at-application-startup-cs/_static/image6.png)

**图 4**： 使用验证断点的`Application_Start`事件处理程序是正在执行 ([单击以查看实际尺寸的图像](caching-data-at-application-startup-cs/_static/image8.png))


> [!NOTE]
> 如果未达到`Application_Start`断点在首次开始调试时，这是因为你的应用程序已启动。 强制应用程序通过修改重启你`Global.asax`或`Web.config`文件，然后重试。 您可以只需添加 （或删除） 末尾的这些文件，以便快速重新启动该应用程序的一个空白行。


## <a name="step-5-displaying-the-cached-data"></a>步骤 5： 显示缓存的数据

此时`StaticCache`类具有可通过访问的应用程序启动时缓存的供应商数据的版本及其`GetSuppliers()`方法。 若要使用此来自表示层的数据，我们可以使用对象数据源，或以编程方式调用`StaticCache`类的`GetSuppliers()`从一种 ASP.NET 页的代码隐藏类的方法。 让我们来看看使用 ObjectDataSource 和 GridView 控件来显示缓存供应商信息。

首先打开`AtApplicationStartup.aspx`页中`Caching`文件夹。 将 GridView 从工具箱拖到设计器中，设置其`ID`属性设置为`Suppliers`。 接下来，从 GridView s 智能标记选择创建名为新 ObjectDataSource `SuppliersCachedDataSource`。 配置要使用 ObjectDataSource`StaticCache`类的`GetSuppliers()`方法。


[![配置对象数据源以使用 StaticCache 类](caching-data-at-application-startup-cs/_static/image10.png)](caching-data-at-application-startup-cs/_static/image9.png)

**图 5**： 配置要使用 ObjectDataSource`StaticCache`类 ([单击以查看实际尺寸的图像](caching-data-at-application-startup-cs/_static/image11.png))


[![使用 GetSuppliers() 方法来检索缓存的供应商数据](caching-data-at-application-startup-cs/_static/image13.png)](caching-data-at-application-startup-cs/_static/image12.png)

**图 6**： 使用`GetSuppliers()`方法来检索缓存供应商数据 ([单击以查看实际尺寸的图像](caching-data-at-application-startup-cs/_static/image14.png))


完成向导后，Visual Studio 将自动添加 BoundFields 中的数据字段的每个`SuppliersDataTable`。 在 GridView 和 ObjectDataSource s 声明性标记应类似于下面所示：


[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample7.aspx)]

图 7 显示时的浏览器查看的页。 输出是相同我们必须读取从 BLL 的数据`SuppliersBLL`类，但是使用`StaticCache`类返回作为缓存在应用程序启动时的供应商数据。 可以在中设置断点`StaticCache`类的`GetSuppliers()`方法以验证此行为。


[![在 GridView 中显示缓存供应商数据](caching-data-at-application-startup-cs/_static/image16.png)](caching-data-at-application-startup-cs/_static/image15.png)

**图 7**： 在 GridView 中显示缓存供应商数据 ([单击以查看实际尺寸的图像](caching-data-at-application-startup-cs/_static/image17.png))


## <a name="summary"></a>总结

大多数每个数据模型包含大量的静态数据，通常在查找表的形式来实现。 此信息是静态的因为这里的无需不断地访问数据库每次需要显示此信息。 此外，由于其静态特性，缓存数据时那里 s 到期时间不需要。 在本教程中我们已了解如何执行此类数据并将其缓存中的数据缓存，应用程序状态，并通过静态成员变量。 此信息缓存在应用程序启动，并保留在整个应用程序 s 生存期内缓存。

在本教程和过去的两个，我们已介绍了应用程序 s 生命周期的持续时间的缓存数据，以及使用基于时间的满。 当缓存数据库数据，不过，基于时间的过期可能不太理想。 而不是定期刷新的缓存，则会将仅修改基础数据库数据时逐出缓存的项最佳选择。 可以通过 SQL 缓存依赖关系，其中我们将介绍我们下一教程中使用这种理想状况。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Teresa Murphy 和 Zack Jones。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](caching-data-in-the-architecture-cs.md)
> [下一页](using-sql-cache-dependencies-cs.md)
