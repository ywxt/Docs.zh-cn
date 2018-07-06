---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
title: 检查 Edit 方法和编辑视图 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: aspnetcontent
ms.date: 08/28/2012
ms.assetid: 41eb99ca-e88f-4720-ae6d-49a958da8116
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: f8d66343ad74e45f167701f405c5e6e2fef0dd13
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824369"
---
<a name="examining-the-edit-methods-and-edit-view"></a>检查 Edit 方法和编辑视图
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。


在本部分中，将检查生成的操作方法和电影控制器的视图。 然后你将添加自定义搜索页。

运行应用程序，并浏览到`Movies`控制器通过追加 */Movies*到你的浏览器的地址栏中的 URL。 将鼠标指针悬停**编辑**链接以查看它链接到的 URL。

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**编辑**由生成链接`Html.ActionLink`中的方法*Views\Movies\Index.cshtml*视图：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

![Html.ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`对象是一个帮助程序，使用上的属性公开[System.Web.Mvc.WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx)基类。 `ActionLink`的帮助器方法，可轻松动态生成 HTML 超链接，链接到控制器上的操作方法。 第一个参数`ActionLink`方法是要呈现的链接文本 (例如， `<a>Edit Me</a>`)。 第二个参数是要调用的操作方法的名称。 最后一个参数是[匿名对象](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx)，它生成的路由数据 （在本例中为 4 的 ID）。

在上图中所示的生成的链接是`http://localhost:xxxxx/Movies/Edit/4`。 默认路由 (在中建立*应用程序\_Start\RouteConfig.cs*) 采用的 URL 模式`{controller}/{action}/{id}`。 因此，ASP.NET 将转换`http://localhost:xxxxx/Movies/Edit/4`成到请求`Edit`的操作方法`Movies`与参数的控制器`ID`等于 4。 检查中的以下代码*应用程序\_Start\RouteConfig.cs*文件。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

此外可以使用查询字符串的操作方法参数进行传递。 例如，URL`http://localhost:xxxxx/Movies/Edit?ID=4`还将传递参数`ID`为 4 到`Edit`操作方法的`Movies`控制器。

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

打开`Movies`控制器。 这两个`Edit`操作方法如下所示。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cs)]

请注意第二个 `Edit` 操作方法的前面是 `HttpPost` 特性。 此属性指定的该重载`Edit`可以仅针对发出的 POST 请求调用方法。 您可以应用`HttpGet`属性与第一个编辑方法，但是，它们是不必要，因为它是默认值。 (我们将引用的操作方法的隐式分配`HttpGet`属性为`HttpGet`方法。)

`HttpGet` `Edit`方法采用电影 ID 参数，查找使用 Entity Framework 电影`Find`方法，并将所选的电影返回到编辑视图。 ID 参数指定[默认值](https://msdn.microsoft.com/library/dd264739.aspx)为零的`Edit`不带参数调用方法。 如果无法找到电影， [HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx)返回。 当基架系统创建“编辑”视图时，它会检查 `Movie` 类并创建代码为类的每个属性呈现 `<label>` 和 `<input>` 元素。 下面的示例显示了已生成的编辑视图：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cshtml)]

请注意视图模板的方式`@model MvcMovie.Models.Movie`文件顶部的语句，这会指定视图期望的模型的视图模板的类型为`Movie`。

基架的代码使用多个*帮助器方法*来简化 HTML 标记。 [ `Html.LabelFor` ](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)帮助器显示的字段的名称 (&quot;标题&quot;， &quot;ReleaseDate&quot;，&quot;流派&quot;，或&quot;价格&quot;). [ `Html.EditorFor` ](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)帮助器呈现 HTML`<input>`元素。 [ `Html.ValidationMessageFor` ](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)帮助器将显示与该属性相关联的任何验证消息。

运行应用程序并导航到 */Movies* URL。 点击“编辑”链接。 在浏览器中查看页面的源。 窗体元素的 HTML 如下所示。

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html?highlight=7,10-11)]

`<input>`元素是在 HTML`<form>`元素的`action`属性设置为发布到 */Movies/Edit* URL。 窗体数据将发送到服务器时**编辑**单击按钮。

## <a name="processing-the-post-request"></a>处理 POST 请求

以下列表显示了 `Edit` 操作方法的 `HttpPost` 版本。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

[ASP.NET MVC 模型绑定器](https://msdn.microsoft.com/magazine/hh781022.aspx)已发布的表单值，并创建`Movie`作为传递的对象`movie`参数。 `ModelState.IsValid` 方法验证表单中提交的数据是否可以用于修改（编辑或更新）`Movie` 对象。 如果数据有效，电影数据保存到`Movies`的集合`db(MovieDBContext`实例)。 新的电影数据保存到数据库上，通过调用`SaveChanges`方法的`MovieDBContext`。 在保存后的数据，代码将重定向到用户`Index`操作方法的`MoviesController`类，其中显示的电影集合，包括刚才所做的更改。

如果已发布的值不是有效的它们将重新显示在窗体中。 `Html.ValidationMessageFor`中的帮助程序*Edit.cshtml*视图模板负责显示相应的错误消息。

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

> [!NOTE]
> 若要支持 jQuery 验证的非英语区域设置，请使用逗号 (&quot;，&quot;) 必须包含小数点， *globalize.js*和您的特定*cultures/globalize.cultures.js*文件 (从[ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 和 JavaScript 使用`Globalize.parseFloat`。 下面的代码演示对 Views\Movies\Edit.cshtml 文件用于修改&quot;-FR&quot;区域性：


[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

十进制字段可能需要一个逗号，而不是十进制点。 作为临时的修补程序，可以将 globalization 元素添加到项目根 web.config 文件。 下面的代码显示了与设置为英语 （美国） 区域性的全球化元素。

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.xml)]

所有`HttpGet`方法遵循类似的模式。 它们获取电影对象 (或列表中的大小写的对象， `Index`)，并将模型传递给视图。 `Create`方法将空的电影对象传递给 Create 视图。 在方法的 `HttpPost` 重载中，创建、编辑、删除或以其他方式修改数据的所有方法都执行此操作。 在 HTTP GET 方法中修改数据是安全风险，如博客文章文章中所述[ASP.NET MVC 提示 #46 – 不使用删除链接，因为他们创建的安全漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。 在 GET 方法中修改数据也违反了 HTTP 最佳做法和架构[REST](http://en.wikipedia.org/wiki/Representational_State_Transfer)模式，后者指定 GET 请求不应更改应用程序的状态。 换句话说，执行 GET 操作应是没有任何隐患的安全操作，也不会修改持久数据。

## <a name="adding-a-search-method-and-search-view"></a>添加搜索方法和搜索视图

在本部分中将添加`SearchIndex`操作方法，您可以搜索电影的流派或名称。 这将是可使用 */Movies/SearchIndex* URL。 该请求将显示包含用户可以输入以搜索电影的输入的元素的 HTML 窗体。 当用户提交窗体时，操作方法将获取用户发布的搜索值，并使用值在数据库中搜索。

## <a name="displaying-the-searchindex-form"></a>显示 SearchIndex 窗体

首先，通过添加`SearchIndex`到现有的操作方法`MoviesController`类。 该方法将返回一个包含 HTML 窗体视图。 下面是代码：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

第一行`SearchIndex`方法将创建以下[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查询用于选择电影：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cs)]

该查询在此情况下，定义，但尚未尚未针对数据存储在运行。

如果`searchString`参数包含一个字符串，电影查询则修改要筛选的搜索字符串，使用下面的代码的值：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample11.cs)]

上面的 `s => s.Title` 代码是 [Lambda 表达式](https://msdn.microsoft.com/library/bb397687.aspx)。 Lambda 在基于方法的用于[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查询用作标准查询运算符方法的参数，如[其中](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx)上述代码中使用的方法。 进行定义或通过调用一个方法，如修改后不会执行 LINQ 查询`Where`或`OrderBy`。 相反，延迟查询执行，这意味着表达式的计算延迟，直到真正循环访问其实现的值或[ `ToList` ](https://msdn.microsoft.com/library/bb342261.aspx)调用方法。 在`SearchIndex`示例 SearchIndex 视图中执行查询。 有关延迟执行查询的详细信息，请参阅[Query Execution](https://msdn.microsoft.com/library/bb738633.aspx)（查询执行）。

现在可以实现`SearchIndex`将向用户显示窗体的视图。 内右击`SearchIndex`方法，然后单击**添加视图**。 在中**添加视图**对话框框中，指定要传递`Movie`视图模板与它模型的类的对象。 在中**基架模板**列表中，选择**列表**，然后单击**添加**。

![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image5.png)

当您单击**外**按钮， *Views\Movies\SearchIndex.cshtml*创建视图模板。 因为所选**列表**中**基架模板**列表中，Visual Studio 自动生成 （已搭建基架） 视图中的某些默认标记。 基架创建的 HTML 窗体。 检查您的代码`Movie`类并创建的代码来呈现`<label>`类的每个属性的元素。 以下列表显示已生成的创建视图：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cshtml)]

运行应用程序并导航到 */Movies/SearchIndex*。 将查询字符串（如 `?searchString=ghost`）追加到 URL。 筛选的电影将显示出来。

![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image6.png)

如果您更改的签名`SearchIndex`方法，以使名为的参数`id`，则`id`参数将匹配`{id}`占位符默认路由中的设置*Global.asax*文件。

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample13.json)]

原始`SearchIndex`方法如下所示::

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cs)]

已修改`SearchIndex`方法看起来，如下所示：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cs?highlight=1,3)]

现可将搜索标题作为路由数据（ URL 段）而非查询字符串值进行传递。

![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image7.png)

但是，不能指望用户在每次要搜索电影时都修改 URL。 因此，现在您需要添加 UI 来帮助他们筛选电影。 如果已更改的签名`SearchIndex`方法来测试如何传递绑定路由的 ID 参数，将其更改回来，以使您`SearchIndex`方法采用字符串参数名为`searchString`:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

打开*Views\Movies\SearchIndex.cshtml*文件，并紧后面`@Html.ActionLink("Create New", "Create")`，添加以下：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml?highlight=2)]

下面的示例显示了一部分*Views\Movies\SearchIndex.cshtml*文件已添加的筛选标记。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cshtml?highlight=12-15)]

`Html.BeginForm`帮助程序将创建一个打开`<form>`标记。 `Html.BeginForm`帮助器后，窗体会发布到其自身，当用户通过单击提交窗体**筛选器**按钮。

运行应用程序并尝试搜索电影。

![](examining-the-edit-methods-and-edit-view/_static/image8.png)

没有任何`HttpPost`重载`SearchIndex`方法。 您不需要它，因为该方法不更改状态的应用程序，只需筛选数据。

可添加以下 `HttpPost SearchIndex` 方法。 在这种情况下，操作调用程序将匹配`HttpPost SearchIndex`方法，和`HttpPost SearchIndex`方法将运行下图中所示。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image9.png)

但是，即使添加 `SearchIndex` 方法的 `HttpPost` 版本，其实现方式也受到限制。 假设你想要将特定搜索加入书签，或向朋友发送一个链接，让他们单击链接即可查看筛选出的相同电影列表。 请注意，HTTP POST 请求的 URL 是 GET 请求 （localhost:xxxxx/Movies/SearchIndex） 的 URL 相同--没有 URL 本身中的搜索信息。 右现在，搜索字符串信息发送到服务器作为窗体字段值。 这意味着无法捕获该搜索信息加入书签或发送给朋友，在 URL 中。

解决方法是使用的重载`BeginForm`，用于指定 POST 请求，应将搜索信息添加到 URL 和应路由到的 HttpGet 版本`SearchIndex`方法。 替换现有无参数`BeginForm`使用以下方法：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cshtml)]

![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

现在提交搜索时，URL 包含搜索查询字符串。 即使具备 `HttpPost SearchIndex` 方法，搜索也将转到 `HttpGet SearchIndex` 操作方法。

![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image11.png)

## <a name="adding-search-by-genre"></a>添加按流派搜索

如果添加了`HttpPost`版本的`SearchIndex`方法，现在将其删除。

接下来，你将添加特定功能，让用户按流派搜索电影。 将 `SearchIndex` 方法替换为以下代码：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cs)]

此版本的`SearchIndex`方法采用附加参数，即`movieGenre`。 前的几行代码创建`List`对象以保存从数据库的电影流派。

下面的代码是一种 LINQ 查询，可从数据库中检索所有流派。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample22.cs)]

该代码使用`AddRange`方法的泛型`List`集合以添加到列表中的所有不同的流派。 (而无需`Distinct`修饰符，则添加重复的流派 — 例如，将在我们的示例中两次添加喜剧)。 然后代码将存储在流派列表的`ViewBag`对象。

下面的代码演示了如何检查`movieGenre`参数。 如果不为空，则代码进一步约束电影查询，以限制到指定类型的所选的电影。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample23.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>将标记添加到 SearchIndex 视图，以支持按流派搜索

添加`Html.DropDownList`到帮助程序*Views\Movies\SearchIndex.cshtml*文件，再`TextBox`帮助器。 完成的标记如下所示：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample24.cshtml?highlight=4)]

运行应用程序，并浏览到 */Movies/SearchIndex*。 按流派、 电影名称和这两个条件，请尝试搜索。

![](examining-the-edit-methods-and-edit-view/_static/image12.png)

在本部分中检查的 CRUD 操作方法和由框架生成的视图。 创建搜索操作方法和视图，以让用户搜索电影标题和流派。 在下一部分中，将探讨如何将属性添加到`Movie`模型以及如何添加初始值设定项将自动创建测试数据库。

> [!div class="step-by-step"]
> [上一页](accessing-your-models-data-from-a-controller.md)
> [下一页](adding-a-new-field-to-the-movie-model-and-table.md)
