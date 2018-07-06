---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: 创建可读 Url 在 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本指南介绍了中的 ASP.NET Web Pages (Razor) 网站，以及如何这样便可以使用更具可读性且更适合 SEO 的 Url 的路由。 您的将...
ms.author: aspnetcontent
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 3304a226e374618a567e69ac72448a9964a34c47
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809866"
---
<a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a>在 ASP.NET Web Pages (Razor) 站点中创建可读 Url
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本指南介绍了中的 ASP.NET Web Pages (Razor) 网站，以及如何这样便可以使用更具可读性且更适合 SEO 的 Url 的路由。
> 
> 你将学习：
> 
> - 如何 ASP.NET 使用路由来使您可以用更具可读性和可搜索 Url。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 3
>   
> 
> 本教程还适用于 ASP.NET Web Pages 2。


## <a name="about-routing"></a>有关路由

在你的站点中的页面的 Url 可以影响程度网站正常工作。 URL 的&quot;友好&quot;可以更轻松的人们能够使用该站点。 它还有助于使用搜索引擎搜索引擎优化 (SEO) 的站点。 ASP.NET 网站包括能够自动使用友好的 Url。

ASP.NET 允许您创建有意义描述用户操作而不是仅指向服务器上的文件的 Url。 请考虑这些 Url 为虚构的博客：

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

比较于以下的这些 Url:

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

在第一对中，用户必须知道使用显示博客*blog.cshtml*页，然后将不得不构造一个查询字符串，获取正确的类别或日期范围。 示例的第二个集是更易于理解和创建。

在第一个示例 Url 还直接指向特定文件 (*blog.cshtml*)。 如果出于某种原因博客移到另一个文件夹的服务器上，或者如果博客进行了重新编写为使用不同的页，就是错误的链接。 第二个集的 Url 未指向特定页，因此，即使博客实现或位置发生更改，Url 将仍将有效。

ASP.NET Web Pages 中，您可以创建类似于上面的示例中的更友好 Url 因为 ASP.NET 使用*路由*。 路由从可以完成请求的 URL 为某页 （或页面） 中创建逻辑映射。 由于映射逻辑 （不是物理，对特定文件），路由提供了极其灵活地为您的网站定义 Url 的方式。

## <a name="how-routing-works"></a>路由的工作原理

当 ASP.NET 处理的请求时，它会读取来确定如何将其路由的 URL。 ASP.NET 会尝试匹配三个部分，我们从左到右在磁盘上，文件的 URL。 如果没有匹配项，在 URL 中剩余的任何内容传递给与页面*路径信息*。

假设有人使用此 URL 的请求：

`http://www.contoso.com/a/b/c`

搜索如下所示：

1. 是否有具有的路径和名称的文件 */a/b/c.cshtml*？ 如果是这样，运行该页面，并向其传递任何信息。 否则为...
2. 是否有具有的路径和名称的文件 */a/b.cshtml*？ 如果因此，运行该页面并将值传递`c`到它。 否则为...
3. 是否有具有的路径和名称的文件 */a.cshtml*？ 如果因此，运行该页面并将值传递`b/c`到它。

如果找到不精确的搜索匹配的 *.cshtml*其指定文件夹中的文件，ASP.NET 仍继续查找这些文件反过来：

1. */a/b/c/default.cshtml* （没有路径信息）。
2. */a/b/c/index.cshtml* （没有路径信息）。

> [!NOTE]
> 为了清楚起见，特定页的请求 (即，请求： 其包括 *.cshtml*文件扩展名) 起作用就像你所期望的一样。 所示的请求`http://www.contoso.com/a/b.cshtml`将运行页面*b.cshtml*得很好。


在页上，就可以通过页面的路径信息`UrlData`属性，它是一个字典。 假设您有一个名为文件*ViewCustomers.cshtml*和你的站点获取此请求：

`http://mysite.com/myWebSite/ViewCustomers/1000`

上述规则中所述，请求将转到你的页面。 在页上，可以使用如下所示的代码，以获取并显示路径信息 (在此情况下，值&quot;1000年&quot;):

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> 由于路由不会涉及完整的文件名称，可能存在二义性如果页面具有相同名称但具有不同文件扩展名 (例如， *MyPage.cshtml*并*MyPage.html*). 为了避免出现路由问题，最好是确保没有页面的名称仅在其扩展插件中不同的站点中。


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

[WebMatrix-Url、 UrlData 和路由 SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)。 由 Mike Brind 此博客文章提供路由的工作原理 ASP.NET Web Pages 中的某些其他详细信息。
