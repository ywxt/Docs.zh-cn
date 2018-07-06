---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
title: 将数据传递到视图母版页 (C#) |Microsoft Docs
author: microsoft
description: 本教程的目的是说明如何向视图母版页，从控制器传递数据。 探讨如何将数据传递到视图 m 的两种策略...
ms.author: aspnetcontent
ms.date: 10/16/2008
ms.assetid: 5fee879b-8bde-42a9-a434-60ba6b1cf747
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: bd2d3e85ac518a066d72541d40ab87543b1a70d1
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818977"
---
<a name="passing-data-to-view-master-pages-c"></a>将数据传递到视图母版页 (C#)
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_CS.pdf)

> 本教程的目的是说明如何向视图母版页，从控制器传递数据。 我们将介绍两种策略用于向视图母版页传递数据。 首先，我们将讨论导致难以维护的应用程序的简单解决方案。 接下来，我们检查需要稍有更多的初始工作，但更易于维护的应用程序中的结果的更好的解决方案。


## <a name="passing-data-to-view-master-pages"></a>向视图母版页传递数据

本教程的目的是说明如何向视图母版页，从控制器传递数据。 我们将介绍两种策略用于向视图母版页传递数据。 首先，我们将讨论导致难以维护的应用程序的简单解决方案。 接下来，我们检查需要稍有更多的初始工作，但更易于维护的应用程序中的结果的更好的解决方案。

### <a name="the-problem"></a>问题

假设您要构建电影数据库应用程序，并且你想要在应用程序中每一页上显示电影类别列表 （见图 1）。 此外，假设电影类别的列表存储在数据库表中。 在这种情况下，最好从数据库检索类别和呈现的视图母版页中的电影类别列表。


[![在视图母版页中显示电影类别](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)

**图 01**： 在视图母版页中显示电影类别 ([单击以查看实际尺寸的图像](passing-data-to-view-master-pages-cs/_static/image3.png))


下面是此问题。 如何检索在母版页中的电影类别的列表？ 它很容易在母版页中直接调用模型类的方法。 换而言之，很容易就包括用于从数据库直接在主页面中检索数据的代码。 但是，绕过 MVC 控制器来访问数据库会违反是构建一个 MVC 应用程序的主要优点之一完全分离关注点。

在 MVC 应用程序，你想要由 MVC 控制器的 MVC 视图和 MVC 模型之间的所有交互。 此分离关注点会导致更易于维护、 可适应和可测试应用程序。

MVC 应用程序中传递给视图 （包括视图母版页） 的所有数据应通过控制器操作都传递给视图。 此外，应通过利用查看数据的传递数据。 在本教程的其余部分，我将介绍两种方法向视图母版页传递视图的数据。

### <a name="the-simple-solution"></a>简单的解决方案

让我们开始将视图数据从控制器传递到视图母版页的最简单解决方案。 最简单的解决方案是将每个控制器操作中传递的母版页的视图数据。

请考虑在列表 1 中的控制器。 它公开两个名为的操作`Index()`和`Details()`。 `Index()`操作方法返回电影数据库表中的每一部电影。 `Details()`操作方法返回特定电影类别中的每一部电影。

**代码清单 1 – `Controllers\HomeController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample1.cs)]

请注意，index （） 和 Details() 操作将添加两个项目，以查看数据。 Index （） 操作将添加两个密钥： 类别和电影。 类别键代表电影类别视图主页所显示的列表。 电影键表示索引视图页所显示的影片的列表。

Details() 操作还将添加名为类别和电影的两个密钥。 类别键中，再次重申，表示电影类别视图主页所显示的列表。 电影键表示电影的详细信息视图页所显示的特定类别的列表 （请参见图 2）。


[![详细信息视图](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)

**图 02**： 详细信息查看 ([单击以查看实际尺寸的图像](passing-data-to-view-master-pages-cs/_static/image6.png))


索引视图包含在代码清单 2 中。 它只是循环访问列表中查看数据的电影项所表示的电影。

**代码清单 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample2.aspx)]

视图主页面都包含在清单 3。 视图母版页迭代并呈现所有由类别项中查看数据表示电影类别。

**代码清单 3 – `Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample3.aspx)]

所有数据将都传递到的视图和视图母版页视图数据。 这是将数据传递给母版页的正确方法。

因此，为什么会这样使用此解决方案？ 问题是此解决方案违反了 DRY （不要自我重复） 原则。 每个控制器操作必须添加电影类别以查看数据的完全相同的列表。 在应用程序中具有重复代码使你的应用程序更难以维护、 适应和修改。

### <a name="the-good-solution"></a>很好的解决方案

在本部分中，我们检查将数据从控制器操作传递到视图母版页的替代，并更好，解决方案。 无需在每个控制器操作添加母版页的电影类别，我们添加电影类别查看数据一次。 应用程序控制器中添加了使用视图母版页的所有视图数据。

ApplicationController 类都包含在清单 4。

**列表 4 – `Controllers\ApplicationController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample4.cs)]

有三个您应注意到了列表 4 中的应用程序控制器的操作。 首先，请注意，类继承自基 system.web.mvc.controller 中衍生类。 应用程序控制器是控制器类。

其次，注意应用程序控制器类是一个抽象类。 一个抽象类是具体类必须实现一个类。 因为应用程序控制器是一个抽象类，不能调用的类中直接定义任何方法。 如果尝试直接调用应用程序类，然后将获取的找不到资源错误消息。

第三，请注意应用程序控制器包含将电影类别以查看数据的列表添加一个构造函数。 每个控制器类都继承自应用程序控制器将自动调用应用程序控制器的构造函数。 无论从应用程序控制器继承任何控制器上调用任何操作，电影类别是自动包含在视图数据。

列表 5 中的电影控制器继承自应用程序控制器。

**列表 5 – `Controllers\MoviesController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample5.cs)]

电影控制器，就像在上一节中讨论的主页控制器一样公开名为的两个操作方法`Index()`和`Details()`。 请注意，电影类别视图主页所显示的列表并不添加到视图中的数据`Index()`或`Details()`方法。 电影控制器继承自应用程序控制器，因为电影类别列表中的添加自动查看数据。

请注意，将视图母版页的视图数据添加到此解决方案不违反 DRY （不要自我重复） 原则。 若要查看数据的电影类别的列表添加的代码包含只在一个位置： 应用程序控制器的构造函数。

### <a name="summary"></a>总结

在本教程中，我们讨论了两种方法可以将视图数据从控制器传递到视图的母版页。 首先，我们探讨了一个简单，但难以维护的方法。 在第一个部分中，我们讨论了如何添加视图母版页的视图数据在每个每个控制器操作中应用程序中。 我们得出的结论是，这是错误的方法，因为它违反了 DRY （不要自我重复） 原则。

接下来，我们将探讨更理想的策略中添加数据视图母版页需查看数据。 无需在每个控制器操作添加的视图数据，我们添加了一次应用程序控制器中的视图数据。 这样一来，将数据传递到视图母版页中的 ASP.NET MVC 应用程序时，可以避免重复代码。

> [!div class="step-by-step"]
> [上一页](creating-page-layouts-with-view-master-pages-cs.md)
> [下一页](asp-net-mvc-views-overview-vb.md)
