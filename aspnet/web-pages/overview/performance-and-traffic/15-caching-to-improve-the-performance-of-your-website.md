---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: 在 ASP.NET Web 中缓存数据页 (Razor) 站点的更好的性能 |Microsoft Docs
author: tfitzmac
description: 你可以加快你的网站通过存储程序，即缓存的结果通常会需要大量时间来检索或处理的数据...
ms.author: aspnetcontent
ms.date: 02/14/2014
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 28be9194bbd95e896311700ddcf89379a82ee636
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805191"
---
<a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a>更好的性能的缓存的 ASP.NET Web Pages (Razor) 站点中的数据
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何使用缓存信息的帮助程序进行更快的性能，在 ASP.NET Web Pages (Razor) 的网站中。 可以通过存储来加快你的网站&#8212;，即缓存&#8212;的数据，通常那样会花费相当长的时间来检索或处理并不经常更改的结果。
> 
> **你将学习：** 
> 
> - 如何使用缓存来提高你的网站的响应能力。
> 
> 下面是在本文中引入的 ASP.NET 功能：
> 
> - `WebCache`帮助器。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 3
>   
> 
> 本教程还适用于 ASP.NET Web Pages 2。


每次有人从您的网站请求页面时，web 服务器必须执行一些操作才能完成请求。 对于某些页面中，服务器可能需要执行需要 （相对） 长时间，如从数据库检索数据的任务。 即使这些任务不采用长绝对意义上讲，如果您的网站遇到大量流量，一整个系列的会导致 web 服务器来执行复杂的或速度缓慢的任务的单个请求最多可添加了大量工作。 这最终会影响站点的性能。

若要提高此类情况下在你性能的一种方法是网站的缓存数据。 如果你的站点获取重复的请求相同的信息，和不需为每个人员修改信息并不是时间敏感的而不是重新提取或重新计算它，您可以一次提取数据，然后将结果存储。 下一次为此，传入某个请求的信息，您只会收到其从缓存。

一般情况下，你将缓存不会频繁更改的信息。 当将信息放在缓存中时，它存储在 web 服务器上的内存中。 您可以指定它应缓存多长，从秒到几天。 当缓存时间到期时，会自动从缓存删除信息。

> [!NOTE]
> 缓存中的项可能会删除原因以外，它们已过期。 例如，web 服务器可能会暂时内存不足，并且它可以回收内存的一种方法是通过从缓存中引发的条目。 正如您将看到，即使已将信息放入缓存，您必须检查以确保它仍是在需要时。


假设网站有一个显示当前温度和天气预报页面。 若要获取此类型的信息，可能会向外部服务发送请求。 因为此信息不会更改很多 （在两小时时间段，例如） 由于外部调用需要时间和带宽，那么是的良好候选项的缓存。

## <a name="adding-caching-to-a-page"></a>添加到页面缓存

ASP.NET 包括`WebCache`帮助器，轻松地向站点添加缓存，并将数据添加到缓存。 在此过程中，你将创建一个页面，缓存的当前时间。 这不是实际的示例中，由于当前时间是内容的情况下，会更改，而且并不复杂计算。 但是，它是为了说明中的缓存的好方法。

1. 添加一个名为的新页*WebCache.cshtml*到网站。
2. 将以下代码和标记添加到页面：

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    当您缓存数据时，您将其放入缓存使用的名称这是唯一的网站。 在这种情况下，将使用名为某个缓存项`CachedTime`。 这是`cacheItemKey`代码示例中所示。

    代码首先读取`CachedTime`缓存条目。 如果 （即，如果缓存条目不为 null） 返回一个值，则代码只是将时间变量的值设置为缓存数据。

    但是，如果不存在的缓存项 （即，它为 null），代码设置的时间值、 将其添加到缓存中，并设置为 1 分钟的到期值。 1 分钟之后，该缓存项将被放弃。 （在缓存中的项的默认过期值是 20 分钟。）该命令`WebCache.Set(cacheItemKey, time, 1, false)`演示如何将当前的时间值添加到缓存并设置为 1 分钟的到期日期。 设置*slidingExpiration*参数`false`意味着每次请求时它不续订过期时间。 完全在 1 分钟后它最初添加到缓存到期时间。 如果将此值设置为`true`1 分钟到期时间从缓存中请求的值每次重置。

    此代码说明了在缓存数据时应始终使用的模式。 您从缓存中获取的内容之前，始终先检查是否`WebCache.Get`方法已返回 null。 请记住该缓存项可能已过期，或可能被删除，出于其他某种原因，因此永远不会保证任何给定的项目存在于缓存中。
3. 运行*WebCache.cshtml*在浏览器中。 (请确保的页中选择**文件**工作区之前运行它。)第一次请求页上，时间数据不在缓存中，和的代码具有要添加到缓存的时间值。

    ![缓存-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. 刷新*WebCache.cshtml*在浏览器中。 这一次，时间数据是在缓存中。 请注意，自上次查看页面以来尚未更改的时间。

    ![缓存 2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. 稍等片刻，在清空缓存，并刷新页。 页面再次指示时间数据并不在缓存中，找到并更新的时间添加到缓存。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源


- [在图表中显示数据](https://go.microsoft.com/fwlink/?LinkId=202895)
- [WebCache API 参考](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx)(MSDN)
