---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: 第 10 部分： 导航和站点设计，结束语的最终更新 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 10 部分介绍了导航和 S.的最终更新...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f32509701dd112053aa4f31d6552601f961c7413
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825042"
---
<a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a>第 10 部分： 导航和站点设计，结束语的最终更新
====================
通过[Jon Galloway](https://github.com/jongalloway)

> MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。  
>   
> MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。  
>   
> 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 10 部分介绍如何导航和站点设计，结束语的最终更新。


我们已经为我们的站点，完成所有主要功能，但我们仍有一些功能，可添加到 site navigation — 站点导航、 主页页面和应用商店浏览页。

## <a name="creating-the-shopping-cart-summary-partial-view"></a>创建购物车摘要分部视图

我们想要跨整个站点中公开用户的购物车中的项目数。

![](mvc-music-store-part-10/_static/image1.png)

我们可以轻松实现这通过创建分部视图添加到我们 Site.master。

如先前所示，购物车控制器包含 CartSummary 操作方法，它将返回分部视图：

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

若要创建 CartSummary 分部视图，右键单击视图/ShoppingCart 文件夹，然后选择添加视图。 视图 CartSummary 命名并选中"创建分部视图"复选框，如下所示。

![](mvc-music-store-part-10/_static/image2.png)

CartSummary 分部视图是非常简单-只是一个链接到购物车索引视图显示购物车中的项的数目。 CartSummary.cshtml 的完整代码如下所示：

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

我们可以通过使用 Html.RenderAction 方法包括站点主站点中的所有页面中包含分部视图。 RenderAction 需要我们指定的操作名称 ("CartSummary") 和控制器名称 ("ShoppingCart") 作为下面。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

将此添加到站点布局之前, 我们还将创建流派菜单上以便我们可以将所有我们 Site.master 更新一次。

## <a name="creating-the-genre-menu-partial-view"></a>创建分部视图的流派菜单

我们可以使用户通过添加一个流派菜单，其中列出了所有流派可用在我们的存储中存储导航更容易。

![](mvc-music-store-part-10/_static/image3.png)

我们将遵循相同的步骤还创建了 GenreMenu 分部视图，然后我们可以将这两个添加到站点 master。 首先，将以下 GenreMenu 控制器操作添加到 StoreController:

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

此操作会返回可以从我们将在下一步创建的分部视图将显示影片类型列表。

*注意： 我们添加了 [ChildActionOnly] 属性对该控制器操作，这表示我们只需要此操作以用于从分部视图。此属性将阻止执行通过浏览到 /Store/GenreMenu 的控制器操作。这不是必需的分部视图，但它是不错的做法，因为我们想要确保我们的控制器操作来按照我们的意图。我们还将返回 PartialView 而不是视图中，以便了解它不应为此视图中，使用布局的其他视图中包括的视图引擎。*

右键单击 GenreMenu 控制器操作并创建名为 GenreMenu 是强类型，如下所示使用流派视图数据类的分部视图。

![](mvc-music-store-part-10/_static/image4.png)

更新要显示的项，如下所示使用未排序的列表的 GenreMenu 分部视图的视图代码。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a>更新站点布局，以显示我们的分部视图

我们可以将我们的分部视图添加到站点布局 (/视图/共享/\_Layout.cshtml) 通过调用 Html.RenderAction()。 我们将添加这两个在中，以及一些其他的标记来显示它们，如下所示：

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

现在当我们运行该应用程序，我们将看到左侧的导航区域中的流派和顶部车摘要。

## <a name="update-to-the-store-browse-page"></a>更新到应用商店浏览页

存储浏览页正常运行，但不会看起来非常不错。 我们可以更新页后，可以更好的布局中显示唱片集，通过更新视图中的代码 （/Views/Store/Browse.cshtml），如下所示：

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

此处我们将使用的 Url.Action 而不是 Html.ActionLink，以便我们可以将应用特殊格式设置为包含唱片集作品的链接。

*注意： 我们要显示这些唱片集的泛型唱片集封面。此信息存储在数据库中，通过存储管理器可编辑。你也可以添加您自己的作品。*

现在我们浏览到一种流派，我们将看到包含唱片集图片的网格中所示唱片集。

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a>更新主页显示顶部销售相册

我们想要功能我们最畅销的唱片集在主页上，来提高销量。 我们将为我们处理此问题，并添加一些其他的图形中的 HomeController 进行一些更新。

首先，我们会将导航属性添加到我们唱片集的类，以便让 EntityFramework 知道它们关联。 最后几行我们**唱片集**类现在应如下所示：

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

*注意： 这将需要添加 using 语句，以便在 System.Collections.Generic 命名空间中。*

首先，我们将添加 storeDB 字段和 MvcMusicStore.Models using 语句，如我们其他控制器中所示。 接下来，我们将向它查询数据库以查找根据 OrderDetails 顶部销售相册 HomeController 中添加以下方法。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

这是一个私有方法，因为我们不想将其作为控制器操作提供。 我们会将其包括在为简单起见，HomeController，但建议将您的业务逻辑移到相应的单独的服务类。

使用此操作后，我们可以更新索引控制器操作可以查询前 5 种销售唱片集并将其返回到视图。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

更新 HomeController 的完整代码如下所示。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

最后，我们将需要更新主页索引视图，以便它可以通过更新模型类型和唱片集列表添加到底部显示的唱片集列表。 我们将利用此机会来还向页面添加标题和升级部分。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

现在当我们运行该应用程序，我们会看到顶部销售 album 和我们的促销消息与我们更新后的主页。

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a>结束语

我们所见，ASP.NET MVC 可以轻松创建复杂的网站具有数据库访问，成员身份，AJAX，等等。 很快就会变。 希望本教程提供若要开始构建你自己的 ASP.NET MVC 应用程序所需的工具 ！


> [!div class="step-by-step"]
> [上一篇](mvc-music-store-part-9.md)
