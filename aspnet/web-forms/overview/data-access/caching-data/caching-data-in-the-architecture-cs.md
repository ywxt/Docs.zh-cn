---
uid: web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
title: 缓存体系结构 (C#) 中的数据 |Microsoft Docs
author: rick-anderson
description: 上一教程中我们介绍了如何将应用在表示层缓存。 在本教程中，我们将了解如何充分利用我们分层 architectu...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: d29a7c41-0628-4a23-9dfc-bfea9c6c1054
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
msc.type: authoredcontent
ms.openlocfilehash: 3971140aa7a6c829287e74df804694c19e34adcf
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830666"
---
<a name="caching-data-in-the-architecture-c"></a>在体系结构 (C#) 中缓存数据
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_59_CS.exe)或[下载 PDF](caching-data-in-the-architecture-cs/_static/datatutorial59cs1.pdf)

> 上一教程中我们介绍了如何将应用在表示层缓存。 在本教程中我们将了解如何充分利用我们的分层式体系结构在业务逻辑层的缓存数据。 为此，我们扩展体系结构，以包括缓存层。


## <a name="introduction"></a>介绍

正如我们看到在前面的教程中，缓存 ObjectDataSource 的数据只需设置几个属性。 遗憾的是，ObjectDataSource 适用缓存在表示层，紧密耦合的 ASP.NET 页面的缓存策略。 创建分层式体系结构的原因之一是允许这种一味为断开。 数据访问层将分离的数据访问详细信息时，业务逻辑层，例如，将从 ASP.NET 页中，业务逻辑相分离。 业务逻辑和数据访问详细信息的这种分离是首选方法，部分，因为它会使系统更具可读性、 更易于维护、 更灵活地更改。 它还允许适用于域知识和的表示层不 t 上的开发人员需要熟悉数据库 s 详细信息才能完成工作的工作划分。 分离表示层中的缓存策略提供了类似的优势。

在本教程中我们将提供了我们的体系结构来容纳*缓存层*（或简称 CL） 采用我们的缓存策略。 缓存层将包括`ProductsCL`等方法使用可以访问的产品信息的类`GetProducts()`， `GetProductsByCategoryID(categoryID)`，依次类推，调用时，将第一次尝试从缓存中检索数据。 如果缓存为空，则这些方法将调用相应`ProductsBLL`BLL，又将 DAL 从获取数据中的方法。 `ProductsCL`方法缓存从 BLL 返回之前对其检索的数据。

如图 1 所示，CL 驻留在演示文稿和业务逻辑层之间。


![缓存层 (CL) 是我们的体系结构中的另一层](caching-data-in-the-architecture-cs/_static/image1.png)

**图 1**: 缓存层 (CL) 是我们的体系结构中的另一层


## <a name="step-1-creating-the-caching-layer-classes"></a>步骤 1： 创建缓存层类

在本教程中我们将使用一个类中创建非常简单 CL`ProductsCL`具有少量的方法。 构建完成缓存层，整个应用程序需要创建`CategoriesCL`， `EmployeesCL`，和`SuppliersCL`类，并提供这些缓存层类中的 BLL 中每个数据访问或修改方法的方法。 使用的 BLL 和 DAL，缓存层应理想情况下实现作为一个单独的类库项目;但是，我们将它作为类实现中`App_Code`文件夹。

从 DAL 和 BLL 类的多个完全独立 CL 类，请让 s 创建新的子文件夹中`App_Code`文件夹。 右键单击`App_Code`文件夹在解决方案资源管理器，选择新的文件夹，并将新文件夹命名为`CL`。 创建此文件夹后, 向其添加一个名为的新类`ProductsCL.cs`。


![添加名为 CL 的新文件夹和一个名为 ProductsCL.cs 类](caching-data-in-the-architecture-cs/_static/image2.png)

**图 2**： 添加一个名为的新文件夹`CL`和一个名为类 `ProductsCL.cs`


`ProductsCL`类应包含组相同的数据访问和修改方法在其相应的业务逻辑层类中找到 (`ProductsBLL`)。 而不是创建所有这些方法，让的 s 构建几个此处以了解模式的使用由 CL。 具体而言，我们将添加`GetProducts()`并`GetProductsByCategoryID(categoryID)`在步骤 3 中的方法和一个`UpdateProduct`在步骤 4 中重载。 您可以添加剩余`ProductsCL`方法和`CategoriesCL`， `EmployeesCL`，和`SuppliersCL`类在方便的时候。

## <a name="step-2-reading-and-writing-to-the-data-cache"></a>步骤 2： 读取和写入到的数据缓存

ObjectDataSource 缓存功能在内部在前面的教程探讨了使用 ASP.NET 数据缓存来存储从 BLL 检索的数据。 数据缓存在从 ASP.NET 页代码隐藏类或 web 应用程序 s 体系结构中的类还可以以编程方式访问。 若要对读取和写入数据缓存从 ASP.NET page s 代码隐藏类，使用以下模式：


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample1.cs)]

[ `Cache`类](https://msdn.microsoft.com/library/system.web.caching.cache.aspx)s [ `Insert`方法](https://msdn.microsoft.com/library/system.web.caching.cache.insert.aspx)具有大量的重载。 `Cache["key"] = value` 和`Cache.Insert(key, value)`是同义的同时将项添加到使用指定的密钥，而无需定义到期的缓存。 通常情况下，我们想要将项添加到缓存中，作为依赖项、 基于时间的过期时间或这两者时指定到期时间。 使用的另一个`Insert`的方法重载，可提供基于依赖项或时间的过期信息。

S 方法需要首先检查请求的数据是否在缓存中，如果是这样，在缓存层从该处返回它。 如果所请求的数据不在缓存中，需要调用适当的 BLL 方法。 它的返回值应缓存，则返回的值，如下面的序列图所示。


![缓存层的方法返回的数据缓存中如果它 s 可用](caching-data-in-the-architecture-cs/_static/image3.png)

**图 3**: 缓存层的方法返回的数据缓存中如果它 s 可用


图 3 中所示的序列是使用以下模式的 CL 类中实现的：


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample2.cs)]

在这里，*类型*是存储在缓存中的数据类型`Northwind.ProductsDataTable`，例如 while*密钥*是用于唯一标识的缓存项的键。 如果具有指定的项*键*不是在缓存中，然后*实例*将`null`将从适当的 BLL 方法检索数据，并将其添加到缓存。 按时间`return instance`到达时，*实例*包含数据，从缓存的引用，或从 BLL 中提取。

请务必从缓存访问数据时使用上面的模式。 下面的模式，这乍一看起来等效的包含引入了争用条件的细微差别。 争用条件很难调试，因为它们偶尔的面孔，并且难以重现。


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample3.cs)]

在此第二个中的差异，不正确的代码片段是而不是在本地变量中存储缓存项的引用，在条件语句中直接访问数据缓存*并*中`return`。 想象一下，当达到此代码时，`Cache["key"]`为非`null`，之前`return`到达语句、 系统逐出*密钥*缓存中。 在此极少数情况下，代码将返回`null`值而不是预期类型的对象。

> [!NOTE]
> 数据缓存是线程安全的因此您不需要线程的访问进行同步对于简单的读 / 写。 但是，如果需要多个对数据执行操作需要是原子在缓存中，你需负责实现的锁或其他机制来确保线程安全。 请参阅[同步访问 ASP.NET 缓存](http://www.ddj.com/184406369)有关详细信息。


项可以以编程方式从使用数据缓存逐出[`Remove`方法](https://msdn.microsoft.com/library/system.web.caching.cache.remove.aspx)如下所示：


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample4.cs)]

## <a name="step-3-returning-product-information-from-theproductsclclass"></a>步骤 3： 返回产品信息`ProductsCL`类

对于本教程让我们来实现两种方法来返回产品信息`ProductsCL`类：`GetProducts()`和`GetProductsByCategoryID(categoryID)`。 与处理方式一样`ProductsBL`业务逻辑层中的类`GetProducts()`CL 中的方法返回有关所有产品的信息`Northwind.ProductsDataTable`对象，而`GetProductsByCategoryID(categoryID)`从指定的类别返回的所有产品。

下面的代码演示中的方法的一部分`ProductsCL`类：


[!code-vb[Main](caching-data-in-the-architecture-cs/samples/sample5.vb)]

首先，请注意`DataObject`和`DataObjectMethodAttribute`应用于类和方法的特性。 这些特性向 ObjectDataSource 的向导中，指示哪些类和方法应出现在向导的 s 步骤中提供信息。 由于将从表示层中的 ObjectDataSource 访问 CL 类和方法，我添加了这些属性来增强的设计时体验。 回头[创建业务逻辑层](../introduction/creating-a-business-logic-layer-cs.md)教程，了解这些属性，其效果的更全面说明。

在中`GetProducts()`并`GetProductsByCategoryID(categoryID)`方法，从返回的数据`GetCacheItem(key)`方法分配给本地变量。 `GetCacheItem(key)`方法，我们将稍后介绍的从基于指定缓存中返回特定项*密钥*。 如果在缓存中未不找到任何此类数据，将从相应中检索`ProductsBLL`类方法，然后添加到缓存使用`AddCacheItem(key, value)`方法。

`GetCacheItem(key)`和`AddCacheItem(key, value)`方法分别接口使用的数据缓存、 读取和写入值。 `GetCacheItem(key)`方法较为简单的两个。 它只需返回传入的使用的缓存类中的值*密钥*:


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample6.cs)]

`GetCacheItem(key)` 不使用*键*值提供，而是调用`GetCacheKey(key)`方法，它将返回*密钥*前面带有 ProductsCache-。 `MasterCacheKeyArray`，其中包含字符串 ProductsCache，也可由`AddCacheItem(key, value)`方法，因为我们将马上就能看到。

一种 ASP.NET 页的代码隐藏类，从数据缓存可以使用访问`Page`类 s [ `Cache`属性](https://msdn.microsoft.com/library/system.web.ui.page.cache.aspx)，并允许进行类似的语法`Cache["key"] = value`、 在步骤 2 中所述。 从体系结构中的类，数据缓存可以使用访问任一`HttpRuntime.Cache`或`HttpContext.Current.Cache`。 [Peter Johnson](https://weblogs.asp.net/pjohnson/default.aspx)的博客文章[HttpRuntime.Cache vs。HttpContext.Current.Cache](https://weblogs.asp.net/pjohnson/httpruntime-cache-vs-httpcontext-current-cache)说明中使用的略微的性能优势`HttpRuntime`而不是`HttpContext.Current`; 因此，`ProductsCL`使用`HttpRuntime`。

> [!NOTE]
> 如果您的体系结构使用类库项目来实现，则将需要添加对的引用`System.Web`若要使用的程序集[HttpRuntime](https://msdn.microsoft.com/library/system.web.httpruntime.aspx)并[HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)类。


如果在缓存中，找不到该项`ProductsCL`类的方法从 BLL 获取数据并将其添加到缓存使用`AddCacheItem(key, value)`方法。 若要添加*值*到缓存中，我们可以使用以下代码，使用 60 秒的时间到期：


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample7.cs)]

`DateTime.Now.AddSeconds(CacheDuration)` 在未来的段中指定的基于时间的过期时间 60 秒[ `System.Web.Caching.Cache.NoSlidingExpiration` ](https://msdn.microsoft.com/library/system.web.caching.cache.noslidingexpiration(vs.80).aspx)指示即 s 任何滑动过期。 而这`Insert`方法重载具有输入参数的这两个绝对和可调到期，您只能提供两种状态之一。 如果你尝试指定一个绝对时间和时间跨度`Insert`方法将引发`ArgumentException`异常。

> [!NOTE]
> 此实现`AddCacheItem(key, value)`方法当前有一些缺点。 我们将解决并解决这些问题在步骤 4 中。


## <a name="step-4-invalidating-the-cache-when-the-data-is-modified-through-the-architecture"></a>步骤 4： 使缓存时的数据是修改通过体系结构

数据检索方法，以及缓存层需要提供相同的方法中，同时为 BLL 插入、 更新和删除数据。 CL 的数据修改方法不修改缓存的数据，但而不是调用的 BLL s 相应数据修改方法，然后使缓存失效的。 如我们在前面的教程中看到，这是相同 ObjectDataSource 应用中启用其缓存功能时的行为并将其`Insert`， `Update`，或`Delete`调用方法。

以下`UpdateProduct`重载说明了如何在 CL 中实现数据修改方法：


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample8.cs)]

调用适当的数据修改业务逻辑层方法，但返回其响应之前，我们需要使缓存失效。 遗憾的是，使缓存失效不是简单明了因为`ProductsCL`类 s`GetProducts()`并`GetProductsByCategoryID(categoryID)`方法每个将项添加到缓存具有不同键和`GetProductsByCategoryID(categoryID)`方法将不同的缓存项添加为每个唯一*categoryID*。

使缓存失效，当我们需要删除*所有*可能已添加的项的`ProductsCL`类。 这可以通过将相关联来实现*缓存依赖项*与每个项添加到缓存中`AddCacheItem(key, value)`方法。 一般情况下，缓存依赖项可以是缓存、 文件系统或 Microsoft SQL Server 数据库中的数据上的文件中的另一个项。 当依赖项发生更改或从缓存中删除，与之关联的缓存项会自动从缓存中逐出。 对于本教程中，我们想要通过添加所有项的缓存依赖项用作在缓存中创建的其他项`ProductsCL`类。 这样一来，所有这些项可以是从缓存中删除通过只需删除缓存依赖项。

Let 的 s 更新`AddCacheItem(key, value)`方法，以便每个项通过此方法添加到缓存是单个缓存依赖项与相关联：


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample9.cs)]

`MasterCacheKeyArray` 是一个字符串数组，包含单个值，ProductsCache。 首先，缓存项添加到缓存并分配的当前日期和时间。 如果缓存项已存在，它会更新。 接下来，创建一个缓存依赖项。 [ `CacheDependency`类](https://msdn.microsoft.com/library/system.web.caching.cachedependency(VS.80).aspx)s 构造函数具有数重载，但在此处使用的一个需要两个`string`数组的输入。 第一个指定要用作依赖项的文件组。 由于我们不需要使用任何基于文件的依赖关系，值为 t`null`用于第一个输入参数。 第二个输入的参数指定要用作依赖项的缓存键的集合。 我们在这里指定我们依赖项， `MasterCacheKeyArray`。 `CacheDependency`然后传递到`Insert`方法。

通过这种修改到`AddCacheItem(key, value)`、 invaliding 缓存非常简单，删除的依赖关系。


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample10.cs)]

## <a name="step-5-calling-the-caching-layer-from-the-presentation-layer"></a>步骤 5： 从表示层调用缓存层

缓存层的类和方法可用于处理数据使用的技术我们 ve 检查在这些教程。 为了说明如何使用缓存的数据，你将更改保存到`ProductsCL`类，然后打开`FromTheArchitecture.aspx`页中`Caching`文件夹并添加 GridView。 从 GridView s 智能标记，创建新对象数据源。 在向导 s 第一步应会看到`ProductsCL`类作为一个下拉列表中的选项。


[![ProductsCL 类包含在业务对象下拉列表](caching-data-in-the-architecture-cs/_static/image5.png)](caching-data-in-the-architecture-cs/_static/image4.png)

**图 4**:`ProductsCL`类包括在业务对象下拉列表 ([单击以查看实际尺寸的图像](caching-data-in-the-architecture-cs/_static/image6.png))


选择后`ProductsCL`，单击下一步。 下拉列表中选择的选项卡有两个项-`GetProducts()`并`GetProductsByCategoryID(categoryID)`和更新选项卡具有 sole`UpdateProduct`重载。 选择`GetProducts()`从选择选项卡的方法和`UpdateProducts`方法从该更新选项卡并单击完成。


[![在下拉列表中列出 ProductsCL 类的方法](caching-data-in-the-architecture-cs/_static/image8.png)](caching-data-in-the-architecture-cs/_static/image7.png)

**图 5**:`ProductsCL`的下拉列表中列出了类的方法 ([单击以查看实际尺寸的图像](caching-data-in-the-architecture-cs/_static/image9.png))


完成向导后，Visual Studio 将设置 ObjectDataSource s`OldValuesParameterFormatString`属性设置为`original_{0}`并将相应的字段添加到 GridView。 更改`OldValuesParameterFormatString`属性恢复为其默认值， `{0}`，并配置 GridView 以支持分页、 排序和编辑。 由于`UploadProducts`重载使用 CL 接受仅编辑的产品的名称和价格，限制 GridView，以便只有这些字段可编辑。

在前面的教程中，我们定义一个 GridView，其中包括的字段`ProductName`， `CategoryName`，和`UnitPrice`字段。 可随意复制此格式设置和结构，这种情况下您 GridView 和对象数据源的 s 声明性标记应如下所示：


[!code-aspx[Main](caching-data-in-the-architecture-cs/samples/sample11.aspx)]

现在我们有一个使用缓存层的页面。 若要查看操作中的缓存，在中设置断点`ProductsCL`类 s`GetProducts()`和`UpdateProduct`方法。 当从缓存中提取排序和分页才能看到数据，请访问浏览器和单步执行代码中的页面。 然后更新的记录，并请注意，缓存将失效，因此，它从 BLL 时检索数据重新绑定到 GridView。

> [!NOTE]
> 在本文随附下载中提供了缓存层不完整。 它仅包含一个类， `ProductsCL`，其中仅提供了一些方法。 此外，仅在单个 ASP.NET 页面使用 CL (`~/Caching/FromTheArchitecture.aspx`) 所有其他人仍在 BLL 直接引用。 如果您打算在应用程序中使用 CL，从表示层的所有调用应都转到 CL，这要求 （CL 的类，方法介绍了这些类和 BLL 当前由表示层中的方法。


## <a name="summary"></a>总结

虽然在表示层与 ASP.NET 2.0 的 SqlDataSource 和 ObjectDataSource 控件，可应用缓存，理想情况下缓存职责将委派给单独的图层体系结构中。 在本教程中我们创建了一个驻留在表示层和业务逻辑层之间的缓存层。 需要提供一组相同的类和方法的存在于 BLL，从表示层调用缓存层。

我们在此环境及前面的教程探讨了缓存层示例表现出*反应加载*。 响应式加载后，将数据加载到缓存，仅当数据请求和从缓存缺失了该数据时。 数据也可以是*主动加载*到缓存中，一种技术，将数据加载到缓存之前实际需要时。 在下一教程，我们将看到主动加载时我们看看如何将静态值存储在应用程序启动缓存的示例。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Teresa Murph。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](caching-data-with-the-objectdatasource-cs.md)
> [下一页](caching-data-at-application-startup-cs.md)
