---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 实现高效数据分页 |Microsoft Docs
author: microsoft
description: 步骤 8 显示了如何将分页支持添加到我们 /Dinners URL，以便而不是显示数千次 dinners，我们将仅显示在 10 个即将推出 dinners...
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: bcd7fdf59fac8328752aa2ebab61c1d50a8b6b0d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842138"
---
<a name="implement-efficient-data-paging"></a>实现高效数据分页
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的步骤 8 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 8 显示了如何将分页支持添加到我们 /Dinners URL，以便而不是显示数千次 dinners，我们将仅显示一次-10 即将推出 dinners 并允许最终用户返回页和向前浏览整个列表以 SEO 友好的方式。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-step-8-paging-support"></a>NerdDinner 步骤 8： 分页支持

如果我们的站点成功，它将具有数千个即将推出 dinners。 我们需要确保我们的 UI 可进行缩放以处理所有这些 dinners，并允许用户对其进行浏览。 若要启用此功能，我们将添加到的分页支持我们 */Dinners* URL 以代替的 dinners 的 1000 次为单位显示在一次，我们将仅一次-显示 10 个即将推出 dinners 和允许最终用户页后和向前浏览整个列表中SEO 友好的方式。

### <a name="index-action-method-recap"></a>Index （） 操作方法回顾

Index （） 操作方法中我们 DinnersController 类目前看起来如下所示：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

当请求 */Dinners* URL，它检索所有即将推出 dinners 的列表，然后呈现出所有的列表：

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iquerablelttgt"></a>了解 IQuerable&lt;T&gt;

*IQueryable&lt;T&gt;* 是作为.NET 3.5 的一部分引入了 LINQ 的接口。 这样，我们可以充分利用实现分页支持的功能强大的"延迟执行"方案。

在我们 DinnerRepository 中我们要返回 IQueryable&lt;Dinner&gt;序列从我们 FindUpcomingDinners() 方法：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

IQueryable&lt;Dinner&gt;我们 FindUpcomingDinners() 方法返回的对象将封装查询以从我们使用 LINQ to SQL 的数据库中检索 Dinner 对象。 重要的是，它不会执行对数据库进行查询，直到我们尝试访问/遍历数据，在查询中，或者我们对其调用 tolist （） 方法。 调用我们 FindUpcomingDinners() 方法的代码可以选择性地将更多"链接"操作/筛选器添加到 IQueryable&lt;Dinner&gt;执行查询前的对象。 然后，LINQ to SQL 是智能，它能够组合针对数据库执行查询时所请求的数据。

若要实现分页逻辑我们可以更新我们 DinnersController index （） 操作方法，以便它将额外的"跳过"和"Take"运算符应用于返回 IQueryable&lt;Dinner&gt;之前对其调用 tolist （） 的序列：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

上面的代码通过在数据库中，前 10 个即将推出 dinners 跳过，然后返回 20 dinners。 LINQ to SQL 是不够智能，无法构造执行此跳过逻辑 SQL 数据库-中并不在 web 服务器的优化的 SQL 查询。 这意味着，即使我们在数据库中具有数以百万计的即将推出 Dinners，我们想要的 10 将检索 （使其成为高效、 可缩放） 此请求的一部分。

### <a name="adding-a-page-value-to-the-url"></a>向 URL 添加一个"page"值

而不是硬编码的特定页范围，我们需要我们 Url 以包含一个"page"参数，指示用户正在请求哪个 Dinner 范围。

#### <a name="using-a-querystring-value"></a>使用查询字符串值

下面的代码演示，我们可以如何更新以支持查询字符串参数并启用 Url 等我们 index （） 操作方法 */Dinners？ 页 = 2*:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

上面的 index （） 操作方法具有一个名为"page"参数。 参数声明为可为 null 的整数 (这是什么 int？ 指示)。 这意味着 */Dinners？ 页 = 2* URL 将导致"2"作为参数值传递的值。 */Dinners* URL （不带查询字符串值） 将导致传递的 null 值。

我们按页大小 （在这种情况下 10 行） 乘以页值，以确定多少 dinners，若要跳过。 我们将使用[C# null"合并"运算符 （？）](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx)处理可以为 null 的类型时，这很有用。 如果页参数为 null，上面的代码将页分配的值为 0。

#### <a name="using-embedded-url-values"></a>使用嵌入 URL 值

使用查询字符串值的替代方法是嵌入的实际 URL 本身中的页参数。 例如： */Dinners/Page/2*或 */Dinners/2*。 ASP.NET MVC 包括了功能强大的 URL 路由引擎，它可以更轻松地支持此类方案。

我们可以注册自定义的路由规则对我们想要任何控制器类或操作方法的任何传入的 URL 或 URL 格式的映射。 我们需要待办事项，只需打开我们的项目中的 Global.asax 文件：

![](implement-efficient-data-paging/_static/image2.png)

然后再注册新的映射规则使用 MapRoute() 帮助器方法，如首次调用的路由。MapRoute() 下面：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

更高版本，我们将注册一个名为"UpcomingDinners"的新路由规则。 我们要指出它具有 URL 格式"Dinners/页 / {页}"– 其中 {page} 是嵌入在 URL 中的参数值。 MapRoute() 方法的第三个参数指示我们应将采用这种格式向 DinnersController 类上的 index （） 操作方法的 Url 映射。

我们可以使用我们已经有了之前使用我们的查询字符串方案 – 但现在我们"page"参数将来自的 URL，并且不在查询字符串完全相同的 index （） 代码：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

现在我们运行该应用程序并在键入 */Dinners*我们将要看到的前 10 个即将推出 dinners:

![](implement-efficient-data-paging/_static/image3.png)

当我们键入 */Dinners/Page/1*我们将看到 dinners 的下一页面：

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>添加页导航用户界面

若要完成我们分页方案的最后一步将是实现"下一步"和"早期/之前"中的导航 UI 视图模板以使用户能够轻松地跳过 Dinner 数据。

若要正确实现此操作，我们需要知道 Dinners 的总数在数据库中，以及如何多页数据这会转换为。 然后，我们将需要以计算当前请求"页"的值是否开头或结尾的数据，以及显示或隐藏"上一个"和"下一步"UI 相应地。 我们 index （） 操作方法中，我们可以实现此逻辑。 或者我们可以向我们的更多重复使用的方式封装此逻辑的项目添加一个帮助器类。

下面是一个简单的"PaginatedList"帮助程序类派生自列表&lt;T&gt;集合类内置于.NET Framework。 它实现了可用于对任何的 IQueryable 数据序列进行分页的可重用集合类。 NerdDinner 应用程序中我们将它的工作通过 IQueryable&lt;Dinner&gt;的结果，但它可以很容易地对使用 IQueryable&lt;产品&gt;或 IQueryable&lt;客户&gt;导致其他应用程序方案：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

请注意上面如何计算，然后公开属性，例如"PageIndex"、"PageSize"、"TotalCount"和"TotalPages"。 它还公开两个帮助程序属性"HasPreviousPage"和"HasNextPage"，指示集合中的数据页的开头或原始序列的末尾。 上面的代码将导致两个 SQL 查询要运行的第一个要检索的 Dinner 对象总数的计数 （这不会返回的对象 – 它而是执行返回一个整数的"SELECT COUNT"语句），第二个要检索的行只是我们需要从我们的数据的当前页的数据库的数据。

然后，我们可以更新我们 DinnersController.Index() helper 方法来创建 PaginatedList&lt;Dinner&gt;从我们 DinnerRepository.FindUpcomingDinners()，并将其传递给视图模板：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

我们然后可以更新 \Views\Dinners\Index.aspx 视图模板继承 ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt; &gt;而不是 ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;，然后将以下代码添加到我们视图模板来显示或隐藏下一页和上一页导航用户界面的底部：

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

请注意上面如何我们正在使用 Html.RouteLink() 帮助器方法来生成我们的超链接。 此方法非常类似于我们以前已使用的 Html.ActionLink() 帮助器方法。 不同之处在于，我们要生成使用"UpcomingDinners"路由规则，我们在我们的 Global.asax 文件中设置的 URL。 这可确保我们将对具有格式我们 index （） 操作方法生成 Url: */Dinners/页 / {page}* – 其中 {page} 值是我们要提供上述基于当前 PageIndex 的变量。

现在当我们运行我们的应用程序时再次我们将看到一次 10 个 dinners 我们浏览器中：

![](implement-efficient-data-paging/_static/image5.png)

我们还有&lt; &lt; &lt;并&gt; &gt; &gt;导航用户界面底部的页，可用于跳过向前和向后通过我们的数据使用搜索引擎可访问的 Url:

![](implement-efficient-data-paging/_static/image6.png)

| **端主题： 了解 IQueryable 的含义&lt;T&gt;** |
| --- |
| IQueryable&lt;T&gt;是一个非常强大的功能，使各种有趣的延迟的执行方案 （例如分页和组合基于查询）。 为所有强大功能，你想要谨慎使用如何使用它并确保不被滥用。 务必要识别该返回 IQueryable&lt;T&gt;从你的存储库的结果使调用代码能够以附加链接的运算符方法，并使参与 ultimate 查询执行。 如果你不想要提供此功能的调用代码，则应返回返回 IList&lt;T&gt;或 IEnumerable&lt;T&gt;结果-包含已执行查询的结果。 为分页方案中，这将要求你将推送到存储库方法被调用的实际数据的分页逻辑。 在此方案中，我们可能会更新我们 FindUpcomingDinners() finder 方法，以使任何一个返回 PaginatedList 的签名： PaginatedList&lt; Dinner&gt; FindUpcomingDinners （int pageIndex，int pageSize） {} 或返回 IList&lt;Dinner&gt;，并使用"totalCount"out 参数返回 Dinners 的总计数： IList&lt;Dinner&gt; FindUpcomingDinners （int pageIndex，int pageSize 出 int totalCount） {} |

### <a name="next-step"></a>下一步

让我们现在看看如何我们可以将身份验证和授权支持添加到我们的应用程序。

> [!div class="step-by-step"]
> [上一页](re-use-ui-using-master-pages-and-partials.md)
> [下一页](secure-applications-using-authentication-and-authorization.md)
