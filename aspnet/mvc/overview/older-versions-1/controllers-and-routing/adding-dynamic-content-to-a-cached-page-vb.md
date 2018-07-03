---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: 将动态内容添加到缓存的页面 (VB) |Microsoft Docs
author: microsoft
description: 了解如何混合在同一页中的动态和缓存内容。 缓存后替换使您能够显示动态内容，例如横幅广告 o...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: a1747733b190048cac1cb9695dbc1ac24570ee42
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375346"
---
<a name="adding-dynamic-content-to-a-cached-page-vb"></a>将动态内容添加到缓存的页面 (VB)
====================
by [Microsoft](https://github.com/microsoft)

> 了解如何混合在同一页中的动态和缓存内容。 缓存后替换，可显示动态内容，例如横幅广告或中缓存已输出的页的新闻项。


通过利用输出缓存，可以极大地提高 ASP.NET MVC 应用程序的性能。 而不是重新生成页面每次请求页面时，可以生成一次并在多个用户的内存中缓存的页面。

但存在一个问题。 如果你需要在页中显示动态内容？ 例如，假设你想要在页中显示横幅广告。 您不希望被缓存，以便每个用户将看到完全相同的播发，横幅广告。 通过这种方式不会进行任何费用 ！

幸运的是，没有简单的解决方案。 您可以充分利用 ASP.NET 框架调用的一项功能*缓存后替换*。 缓存后替换可以替换已缓存在内存中的页中的动态内容。


通常情况下，您在输出时缓存使用的页面&lt;OutputCache&gt;属性页缓存在服务器和客户端 （web 浏览器）。 当使用缓存后替换时，仅在服务器上缓存页。


#### <a name="using-post-cache-substitution"></a>使用缓存后替换

使用缓存后替换需要两个步骤。 首先，需要定义返回一个字符串，表示你想要在缓存的页面中显示的动态内容的方法。 接下来，您调用 HttpResponse.WriteSubstitution() 方法来将动态内容注入到页面。

例如，假设你想要在缓存上随机显示不同的新闻项。 在列表 1 中的类公开了一个方法，名为 RenderNews() 随机从列表中的三个新闻项返回一个新闻项。

**代码清单 1 – Models\News.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

若要充分利用缓存后替换，则调用 HttpResponse.WriteSubstitution() 方法。 WriteSubstitution() 方法设置代码，以替换动态内容的缓存的页面区域。 WriteSubstitution() 方法用于在代码清单 2 中的视图中显示的随机新闻项。

**代码清单 2 – Views\Home\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

RenderNews 方法传递给 WriteSubstitution() 方法。 请注意，不会调用 RenderNews 方法。 而是对方法的引用被传递给 WriteSubstitution() AddressOf 运算符的帮助。

缓存索引视图。 该视图返回的清单 3 中的控制器。 请注意，index （） 操作用修饰&lt;OutputCache&gt;导致要缓存 60 秒的索引视图的属性。

**代码清单 3 – Controllers\HomeController.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

即使缓存索引视图，在请求索引页时显示不同的随机新闻项。 当请求索引页时，页所显示的时间将不会更改为 60 秒 （参见图 1）。 时间不会更改这一事实证明对页进行缓存。 但是，内容注入 WriteSubstitution() 方法-随机新闻项目-更改每个请求。

**图 1 – 将注入中缓存的页面的动态新闻项**

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>在帮助器方法中使用缓存后替换

充分利用缓存后替换的更简单方法是封装对自定义帮助程序方法内 WriteSubstitution() 方法的调用。 列表 4 中的帮助器方法进行了说明这种方法。

**列表 4 – Helpers\AdHelper.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

列表 4 包含公开两个方法的 Visual Basic 模块： RenderBanner() 和 RenderBannerInternal()。 RenderBanner() 方法表示实际的帮助器方法。 此方法，以便你可以在一个视图，就像任何其他帮助器方法中调用 Html.RenderBanner() 扩展标准的 ASP.NET MVC HtmlHelper 类。

RenderBanner() 方法调用将 RenderBannerInternal() 方法传递给 WriteSubsitution() 方法 HttpResponse.WriteSubstitution() 方法。

RenderBannerInternal() 方法为私有方法。 此方法不会公开为一个帮助器方法。 RenderBannerInternal() 方法随机从列表中的三个横幅广告图像返回一个横幅广告图像。

列表 5 中经过修改的索引视图说明了如何使用 RenderBanner() 帮助器方法。 请注意，额外&lt;%@ 导入 %&gt;指令，则包含要导入 MvcApplication1.Helpers 命名空间的视图的顶部。 如果忘记导入此命名空间，则 RenderBanner() 方法不会显示为 Html 属性上的方法。

**列表 5 – Views\Home\Index.aspx （与 RenderBanner() 方法）**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

不同横幅广告时请求由列表 5 中查看呈现的页，将显示的每个请求 （请参见图 2）。 对页进行缓存，但由 RenderBanner() 帮助器方法动态注入横幅广告。

**图 2 – 索引视图显示随机横幅广告**

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a>总结

本教程介绍了如何动态更新缓存的页面中的内容。 您学习了如何使用 HttpResponse.WriteSubstitution() 方法以启用要注入到缓存的页面中的动态内容。 您还学习了如何封装对 HTML 帮助器方法内 WriteSubstitution() 方法的调用。

利用缓存应尽可能 – 它会对 web 应用程序的性能产生重大影响。 在本教程中所述，您可以充分利用缓存甚至当您需要在页面中显示动态内容时。

> [!div class="step-by-step"]
> [上一页](improving-performance-with-output-caching-vb.md)
> [下一页](creating-a-controller-vb.md)
