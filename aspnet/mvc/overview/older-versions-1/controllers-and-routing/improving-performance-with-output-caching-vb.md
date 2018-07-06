---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: 提高性能与输出缓存 (VB) |Microsoft Docs
author: microsoft
description: 在本教程中，您学习如何你可以显著提升性能的 ASP.NET MVC web 应用程序通过利用的输出缓存。 您...
ms.author: aspnetcontent
ms.date: 01/27/2009
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: 72d73067f6f7dabe4644a35c8d9462bfbc7a93ed
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807325"
---
<a name="improving-performance-with-output-caching-vb"></a>使用输出缓存 (VB) 提高性能
====================
by [Microsoft](https://github.com/microsoft)

> 在本教程中，您学习如何你可以显著提升性能的 ASP.NET MVC web 应用程序通过利用的输出缓存。 了解如何缓存，以便相同的内容不需要创建新用户调用该操作的每个时间的控制器操作返回的结果。


本教程的目的是说明如何可以极大地改善性能 ASP.NET MVC 应用程序通过利用输出缓存。 输出缓存可以缓存由控制器操作返回的内容。 这样一来，相同的内容不需要为其生成每个调用相同的控制器操作的时间。

例如，假设您的 ASP.NET MVC 应用程序在名为索引视图中显示的数据库记录列表。 通常情况下，每个用户调用返回索引视图的控制器操作的时间的数据库记录集必须是从数据库中检索通过执行数据库查询。

如果您手动，充分利用输出缓存则可以避免每次任何用户调用相同的控制器操作时执行数据库查询。 该视图可以检索从而不是从控制器操作正在重新生成缓存。 你可以避免执行冗余缓存启用在服务器上工作。

#### <a name="enabling-output-caching"></a>启用输出缓存

启用输出缓存通过添加&lt;OutputCache&gt;属性为单独的控制器操作或整个控制器类。 例如，在列表 1 中的控制器将公开名为 index （） 操作。 Index （） 操作的输出缓存 10 秒。

**代码清单 1 – Controllers\HomeController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]


在 ASP.NET MVC 的 Beta 版本中，输出缓存不适合的 URL，如[ http://www.MySite.com/ ](http://www.mysite.com/)。 相反，您必须输入的 URL，如[ http://www.MySite.com/Home/Index ](http://www.mysite.com/Home/Index)。


在列表 1 中，index （） 操作的输出缓存 10 秒。 如果您愿意，可以指定更长的时间的缓存持续时间。 例如，如果你想要缓存的一天的控制器操作输出则可以指定缓存持续时间为 86400 秒 (60 秒\*60 分钟\*24 小时)。

没有内容不能保证将你指定的时间量内缓存。 当内存资源变得较低时，缓存会自动启动正在收回的内容。

列表 1 中的主页控制器返回代码清单 2 中的索引视图。 并没有什么特别有关此视图。 索引视图仅显示当前时间 （请参阅图 1）。

**代码清单 2 – Views\Home\Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

**图 1 – 缓存索引视图**

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

如果通过在你的浏览器的地址栏中输入 URL /Home/索引调用 index （） 操作多个时间和重复达到你的浏览器中的刷新/重新加载按钮，然后显示索引视图的时间不会更改为 10 秒。 显示在同一时间，因为缓存视图。

请务必了解，为每个用户访问你的应用程序缓存相同的视图。 调用 index （） 操作的任何人将获得相同的缓存的版本的索引视图。 这意味着大幅减少 web 服务器提供的索引视图时必须执行的工作量。

代码清单 2 中的视图发生要做的一些非常简单。 该视图只显示当前时间。 但是，你可以同样轻松地缓存一个视图，显示一组数据库记录。 在这种情况下，组数据库记录不需要每次调用返回的视图的控制器操作时从数据库检索。 缓存可以减少您的 web 服务器和数据库服务器必须执行的工作量。

不使用的页面&lt;%@ OutputCache %&gt;指令在 MVC 视图。 此指令窜的 Web 窗体世界，并且不应使用 ASP.NET MVC 应用程序中。 

#### <a name="where-content-is-cached"></a>在其中缓存内容

默认情况下，当您使用&lt;OutputCache&gt;属性，内容缓存在三个位置中： web 服务器、 任何代理服务器和 web 浏览器。 您可以控制完全在其中缓存内容通过修改的 Location 属性&lt;OutputCache&gt;属性。

可以将位置属性设置为以下值之一：

> ·任何
> 
> ·客户端
> 
> ·下游
> 
> ·服务器
> 
> ·无
> 
> ·ServerAndClient


默认情况下，位置属性具有值 Any。 但是，有些情况下在其中可能要缓存仅在浏览器上或只能在服务器上。 例如，如果缓存的每个用户进行个性化设置的信息然后不应缓存在服务器上的信息。 如果您要为不同的用户显示不同的信息，则应缓存仅在客户端上的信息。

例如，清单 3 中的控制器将公开名为 GetName() 返回当前用户名称的操作。 如果 Jack 登录到该网站并调用 GetName() 操作然后操作返回的字符串"Hi Jack"。 如果以后，Jill 要登录到该网站并调用 GetName() 操作然后她还将获取字符串"Hi Jack"。 Jack 最初调用控制器操作后，该字符串缓存的所有用户在 web 服务器上。

**代码清单 3 – Controllers\BadUserController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

很可能在列表 3 中的控制器不适所需的方式。 您不希望向 Jill 显示消息"Hi Jack"。

你应该永远不会缓存服务器缓存中的个性化的内容。 但是，你可能想要将个性化的内容缓存在浏览器缓存以提高性能。 如果缓存在浏览器中的内容，并且用户可以多次调用相同的控制器操作，然后可从浏览器缓存中而不是服务器检索内容。

列表 4 中的已修改的控制器缓存 GetName() 操作的输出。 但是，仅在浏览器上并不是服务器上缓存内容。 这样一来，当多个用户调用 GetName() 方法时，每个人员获取其自己的用户名称并不是另一个用户的用户名。

**列表 4 – Controllers\UserController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

请注意， &lt;OutputCache&gt;列表 4 中的属性包括位置属性设置为值 OutputCacheLocation.Client。 &lt;OutputCache&gt;属性还包括 NoStore 属性。 NoStore 属性用于通知代理服务器和浏览器，它们不应存储在缓存内容的永久副本。

#### <a name="varying-the-output-cache"></a>不同的输出缓存

在某些情况下，您可能希望完全相同的内容的不同缓存的版本。 例如，假设要创建母版/详细信息页。 主页面显示电影标题的列表。 单击标题时，可以为所选电影获取详细信息。

如果缓存的详细信息页，然后将哪些电影无论您单击显示同一电影的详细信息。 将向所有将来的用户显示第一个用户所选的第一个影片。

可以通过利用的 VaryByParam 属性解决此问题&lt;OutputCache&gt;属性。 此属性，可创建不同的缓存的版本的完全相同的内容时窗体参数或查询字符串参数而异。

例如，在列表 5 中的控制器将公开名为 Master() 和 Details() 的两个操作。 Master() 操作返回的电影标题列表和 Details() 操作返回所选电影的详细信息。

**列表 5 – Controllers\MoviesController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

Master() 操作包括 VaryByParam 属性具有值"none"。 当查看的 Master() 调用操作，主节点的相同的缓存版本，则返回。 任何窗体参数或查询字符串参数被忽略 （见图 2）。

**图 2 – /Movies/Master 视图**

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

**图 3-/ Movies/详细信息视图**

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

Details() 操作包括具有值"Id"的 VaryByParam 属性。 如果不同的 Id 参数的值传递到控制器操作，生成不同的缓存的版本的详细信息视图。

它是必须了解使用 VaryByParam 属性结果在多个缓存的和不是失望。 每个不同版本的 Id 参数创建的详细信息视图的不同缓存的版本。

您可以将 VaryByParam 属性设置为以下值：

> \* = 创建不同的缓存的版本，只要窗体或查询字符串参数而异。
> 
> none = 从不创建不同的缓存的版本
> 
> 以分号的参数列表 = 创建不同的缓存的版本，只要任何窗体或查询字符串参数列表中各不相同


#### <a name="creating-a-cache-profile"></a>创建缓存配置文件

作为配置输出缓存属性的修改的属性的替代方法&lt;OutputCache&gt;属性，您可以在 web 配置 (web.config) 文件中创建的缓存配置文件。 在 web 配置文件中创建的缓存配置文件提供了几个重要优势。

首先，通过配置输出缓存的 web 配置文件中，可以控制如何控制器操作缓存在一个中心位置的内容。 可以创建一个缓存配置文件，并将该配置文件应用于多个控制器或控制器操作。

其次，您可以修改 web 配置文件无需重新编译你的应用程序。 如果你需要禁用缓存的应用程序已部署到生产环境，则可以只需修改 web 配置文件中定义的缓存配置文件。 将自动检测到并应用到 web 配置文件的任何更改。

例如，&lt;缓存&gt;列表 6 中的 web 配置节定义名为 Cache1Hour 的缓存配置文件。 &lt;缓存&gt;部分必须出现在&lt;system.web&gt; web 配置文件的部分。

**代码清单 6 – 缓存部分中的 web.config**

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

列表 7 中的控制器演示了如何将 Cache1Hour 配置文件应用到的控制器操作具有&lt;OutputCache&gt;属性。

**列表 7 – Controllers\ProfileController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

如果调用公开的清单 7 中的控制器的 index （） 操作然后将 1 个小时返回相同的时间。

#### <a name="summary"></a>总结

输出缓存提供的极大改善了 ASP.NET MVC 应用程序的性能非常简单的方法。 在本教程中，您学习了如何使用&lt;OutputCache&gt;要缓存的控制器操作的输出属性。 您还学习了如何修改的属性&lt;OutputCache&gt;如要修改内容获取缓存的持续时间和 VaryByParam 属性的属性。 最后，您学习了如何在 web 配置文件中定义缓存配置文件。

> [!div class="step-by-step"]
> [上一页](understanding-action-filters-vb.md)
> [下一页](adding-dynamic-content-to-a-cached-page-vb.md)
