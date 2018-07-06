---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 使用控制器和视图实现列表/详细信息 UI |Microsoft Docs
author: microsoft
description: 步骤 4 显示了如何将控制器添加到应用程序充分利用我们的模型为用户提供对数据的列表/详细信息导航体验...
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 7a0a057efb52a869a72722b24d7283cb883db858
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37838580"
---
<a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>使用控制器和视图实现列表/详细信息 UI
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的第 4 步["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 4 显示了如何将控制器添加到应用程序充分利用我们的模型为用户提供 dinners 我们 NerdDinner 的网站上的数据列表/详细信息导航体验。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-step-4-controllers-and-views"></a>NerdDinner 步骤 4： 控制器和视图

与传统的 web 框架 （经典 ASP、 PHP、 ASP.NET Web 窗体等），传入的 Url 通常映射到磁盘上的文件中。 例如： 所示的请求 url"/ Products.aspx"或"/ Products.php"可能会处理由"Products.aspx"或"Products.php"文件。

基于 web 的 MVC 框架将 Url 映射到服务器代码中以略有不同的方式。 而不是将传入 Url 映射到文件，它们而是将 Url 映射到类上的方法。 这些类称为"控制器"和要负责处理传入的 HTTP 请求，处理用户输入、 检索和保存数据，并确定要发送的响应返回给客户端 （显示 HTML、 下载文件，将重定向到不同URL，等等）。

现在，我们已为 NerdDinner 应用程序生成基本模型，我们下一步将是将控制器添加到应用程序充分利用它来向用户提供 Dinners 我们的网站上的数据列表/详细信息导航体验。

### <a name="adding-a-dinnerscontroller-controller"></a>添加 DinnersController 控制器

我们将首先右键单击"控制器"文件夹中的 web 项目，并选择**Add-&gt;控制器**菜单命令 （您还可以执行此命令通过键入 Ctrl M、 Ctrl + C）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

这将显示"添加控制器"对话框：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

我们将命名的新控制器"DinnersController"，然后单击"添加"按钮。 然后，visual Studio 将添加我们 \Controllers 目录下的 DinnersController.cs 文件：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

它还会打开代码编辑器内的新 DinnersController 类。

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>向 DinnersController 类添加 index （） 和 Details() 操作方法

我们想要启用访问者使用我们的应用程序以浏览即将发布 dinners 的列表，使他们可以单击列表中的任何 Dinner，若要查看其特定详细信息。 我们将发布我们的应用程序从以下 Url 来执行此操作：

| **URL** | **目的** |
| --- | --- |
| */Dinners/* | 显示即将到来的 dinners 的 HTML 列表 |
| */Dinners/Details/[id]* | 显示有关特定 dinner 嵌入到 URL – 将匹配的数据库中 dinner DinnerID 中"id"参数指示的详细信息。 例如： /Dinners/Details/2 将显示有关 Dinner DinnerID 值为 2 的详细信息的 HTML 页。 |

通过将两个公共"操作方法"添加到我们 DinnersController 类，如下面，我们将发布这些 Url 的初始实现：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

然后，我们将运行 NerdDinner 应用程序，并使用浏览器来调用它们。 在中键入 *"/ Dinners /"* 的 URL 将导致我们*index （)* 方法运行，然后它将发送回以下响应：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

在中键入 *"/ Dinners/详细信息/2"* 的 URL 将导致我们*Details()* 方法来运行，并发送回以下响应：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

您可能想知道-ASP.NET MVC 是如何知道要创建我们的 DinnersController 类和调用这些方法？ 若要了解，让我们快速看一下如何路由的工作原理。

### <a name="understanding-aspnet-mvc-routing"></a>了解 ASP.NET MVC 路由

ASP.NET MVC 包括一个功能强大的 URL 路由引擎，提供大量灵活地控制如何将 Url 映射到 controller 类。 它允许我们完全自定义 ASP.NET MVC 如何选择要创建哪种方法来调用它，以及配置不同的方式，变量可以自动分析从 URL/查询字符串和传递给形式参数的方法的控制器类自变量。 它提供灵活地完全针对 SEO （搜索引擎优化） 进行优化站点以及发布任何我们想从应用程序的 URL 结构。

默认情况下，新的 ASP.NET MVC 项目附带了已注册的 URL 路由规则的预配置集。 这使我们能够轻松地开始使用应用程序而无需显式配置的任何内容。 我们的项目 – 我们可以通过双击"Global.asax"文件的我们的项目根目录中打开的"应用程序"类中找不到默认路由规则注册：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

此类的"RegisterRoutes"方法中注册的默认 ASP.NET MVC 路由规则：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

"路由。MapRoute()"上面的方法调用注册的默认路由规则将传入 Url 映射到 controller 类使用的 URL 格式:"/ {controller} / {action} / {id}"– 其中"controller"是要实例化，控制器类的名称"action"是的名称公共方法来调用它，然后"id"是嵌入到该方法可以作为参数传递到 URL 中的一个可选参数。 传递给"MapRoute()"方法调用的第三个参数是一组的默认值，以便使用它们不存在在 URL 中进行的控制器/操作/id 值 (控制器 ="主页"，操作 ="Index"，Id ="")。

下面是一个表，其中演示如何各种 Url 使用默认值映射"<em>/ {控制器} / {action} / {id}"</em>路由规则：

| **URL** | **控制器类** | **操作方法** | **传递的参数** |
| --- | --- | --- | --- |
| */Dinners/Details/2* | DinnersController | Details(id) | id=2 |
| */Dinners/Edit/5* | DinnersController | Edit(id) | id=5 |
| */Dinners/Create* | DinnersController | Create （) | 不可用 |
| */ Dinners* | DinnersController | Index （) | 不可用 |
| */ 主页* | HomeController | Index （) | 不可用 |
| */* | HomeController | Index （) | 不可用 |

最后三行显示的默认值 (控制器 = 主页，操作 = 索引，Id ="") 正在使用。 因为如果未指定，"Index"方法注册为默认操作名称"/ Dinners"和"/home"Url 原因 index （） 操作方法及其控制器类上调用。 因为如果未指定，"Home"控制器已注册为默认控制器，"/"URL 使 HomeController 要创建和 index （） 操作方法来调用它。

如果您不喜欢这些默认 URL 路由规则，好消息是它们很容易更改-只需在上面的 RegisterRoutes 方法中对其进行编辑。 NerdDinner 应用程序，不过，我们不打算更改任何默认 URL 路由规则 – 我们将只需使用它们作为-是。

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>使用从我们 DinnersController DinnerRepository

让我们现在将为我们的 DinnersController 的当前实现 index （） 和 Details() 操作方法与使用我们的模型的实现。

我们将使用我们之前生成以实现行为的 DinnerRepository 类。 我们将首先添加引用"NerdDinner.Models"命名空间的"using"语句，然后作为字段，在我们的 DinnerController 类声明的我们 DinnerRepository 实例。

本章稍后我们将介绍"依赖关系注入"的概念并展示控制器能够获取对启用更好单元 DinnerRepository 引用另一种方法，测试 – 但右侧的现在只需创建我们 DinnerRepository 实例如下面的内联。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

现在我们已准备好生成 HTML 响应使用我们检索到的数据模型对象。

### <a name="using-views-with-our-controller"></a>使用视图和控制器

虽然可以编写在组装 HTML，然后使用我们操作方法中的代码*response.write （)* 帮助器方法来将其发送回客户端，该方法变得相当不便于快速。 更好的方法是为我们只能执行应用程序和数据逻辑内我们 DinnersController 的操作方法，并将然后传递要呈现到单独的"视图"模板，它负责将输出 HTML 形式呈现的 HTML 响应所需的数据它。 正如我们稍后将看到，"查看"模板是文本文件，通常包含 HTML 标记和嵌入的呈现代码的组合。

我们的控制器逻辑分开我们视图呈现带来了几大好处。 特别是它可帮助应用程序代码和 UI 设置的格式呈现代码之间强制清除"关注点分离"。 这样，可以更容易地中隔离单元测试应用程序逻辑与 UI 呈现逻辑。 它可以更轻松地更高版本修改 UI 呈现模板，而无需更改应用程序代码。 它可以方便开发人员和设计人员共同协作的项目。

我们可以更新我们 DinnersController 类，以指示我们想要查看模板用于通过更改我们的两个操作方法的方法签名中具有返回类型为"void"改为具有返回类型为"ActionResult"发回 HTML UI 响应。 然后，我们可以调用*View()* 控制器基类要返回上的帮助器方法"ViewResult"对象如下所示：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

签名*View()* 我们使用上面的帮助器方法类似于下面：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

第一个参数*View()* 帮助器方法是我们想要用于呈现 HTML 响应的视图模板文件的名称。 第二个参数是包含在视图模板呈现的 HTML 响应所需的数据的模型对象。

我们 index （） 操作方法中，我们将调用*View()* 帮助器方法并指示我们想要呈现的 HTML 列表的 dinners 使用"索引"视图模板。 我们要传递视图模板 Dinner 对象生成的列表中的序列：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

我们 Details() 操作方法中，我们尝试检索 Dinner 对象使用的 URL 中提供的 id。 如果我们调用找到有效的 Dinner *View()* 帮助器方法，指明我们想要使用"详细信息"视图模板来呈现检索到的 Dinner 对象。 如果请求无效 dinner，则我们呈现有用的错误消息，指示 Dinner 不存在使用"NotFound"视图模板 (和重载的版本*View()* 帮助器方法，只需将模板名称):

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

现在让我们来实现"NotFound"、"详细信息"和"索引"视图模板。

### <a name="implementing-the-notfound-view-template"></a>实现"NotFound"查看模板

我们将开始通过实现"NotFound"视图模板-其中显示了一个友好的错误消息，表明找不到请求的 dinner。

我们将通过定位在控制器操作方法中，我们文本光标创建新的视图模板，然后右键单击并选择"添加视图"菜单命令 （我们还可以执行此命令通过键入 Ctrl-M，Ctrl + V）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

此时会弹出如下面的"添加视图"对话框。 默认情况下该对话框将预填充要创建的视图的名称以与操作方法的名称匹配光标时所在对话框启动 （在本例中"的详细信息"）。 由于我们想要首先实现"NotFound"模板，我们将重写此视图的名称，并将其改为"找不到"设置为：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

当我们单击"添加"按钮时，Visual Studio 将创建一个新"NotFound.aspx"视图模板为我们中的"\Views\Dinners"目录 （它还将创建如果目录尚不存在）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

它还将打开代码编辑器内我们新"NotFound.aspx"查看模板：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

默认情况下的视图模板有两个"内容区域"我们可以在其中添加内容和代码。 第一个可用于自定义"title"的 HTML 页发回。 第二个可用于自定义的"主要内容"HTML 页发回。

若要实现"NotFound"视图模板，我们将添加一些基本内容：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

我们可以再尝试在浏览器中。 若要执行此操作让我们请求 *"/ Dinners/详细信息/9999"* URL。 这将引用 dinner，当前不存在在数据库中，并将导致我们 DinnersController.Details() 操作方法以呈现我们"NotFound"查看模板：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

您会注意到在上面的屏幕截图中的一件事是我们的基本视图模板已继承了一系列 HTML 围绕在屏幕上的主要内容。 这是因为我们视图模板使用的使我们能够一致布局适用于站点上的所有视图的"母版页"模板。 我们将讨论如何母版页的工作原理的本教程后面部分中提供了更多。

### <a name="implementing-the-details-view-template"></a>实现"详细信息"视图模板

现在让我们来实现的"详细信息"视图模板-将单个 Dinner 模型生成的 HTML。

我们将执行此操作通过定位在详细信息操作方法中，我们文本光标然后右键单击并选择"添加视图"菜单命令 （或按 Ctrl-M、 Ctrl + V）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

这将显示"添加视图"对话框。 我们将保留的默认视图名称 （"详细信息"）。 我们还将在对话框中选择"创建强类型视图"复选框，然后选择 （使用组合框下拉列表中） 到该视图从控制器传入的模型类型的名称。 此视图的传入 Dinner 对象 (此类型的完全限定的名称是:"NerdDinner.Models.Dinner"):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

与上面的模板，其中我们选择创建"空视图"，的此时我们将自动选择"创建基架"视图使用"详细信息"的模板。 我们可以通过更改"视图内容"下拉列表中上述对话框指示这一点。

"基架"将生成基于我们要将它们传递给它的 Dinner 对象详细信息视图模板的初始实现。 这提供了用于轻松对我们能够快速开始我们的视图模板实现。

当我们单击"添加"按钮时，Visual Studio 将创建一个新"Details.aspx"视图模板文件为我们我们"\Views\Dinners"目录中：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

它还会打开代码编辑器内我们新的"Details.aspx"视图模板。 它将包含基于 Dinner 模型的详细信息视图的初始基架实现。 基架引擎使用.NET 反射来看看传递，在类上公开的公共属性，并将添加基于找到每种类型的相应内容：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

我们可以请求 *"/ Dinners/详细信息/1"* URL 即可查看此"详细信息"基架实现在浏览器中的样子。 使用此 URL 将显示我们手动添加到我们的数据库时我们首次创建的 dinners 之一：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

这很快就会变我们启动并运行，并为我们提供了我们 Details.aspx 视图的初始实现。 我们然后可以转到并进行调整，以自定义用户界面，以我们的满意度。

当我们更紧密地查看 Details.aspx 模板时，我们会发现，它包含静态 HTML，以及嵌入呈现代码。 &lt;%%&gt;代码片段执行代码时呈现的视图模板，并&lt;%= %&gt;代码片段执行其中所包含的代码，并随后呈现到输出流的模板的结果。

我们可以访问的"Dinner"模型对象，我们使用从控制器的强类型化"模型"属性传递我们视图内编写代码。 Visual Studio 为我们提供了在具有完整的代码 intellisense 时访问此"模型"属性编辑器中：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

让我们进行一些调整，以便我们最终的详细信息视图模板的源类似于下面：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

当我们访问 *"/ Dinners/详细信息/1"* URL 再次它现在将呈现如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>实现"索引"视图模板

现在让我们来实现"索引"视图模板-这会导致生成即将推出 Dinners 的列表。 待办事项这我们在索引操作方法中，我们文本光标的位置，然后右键单击并选择"添加视图"菜单命令 （或按 Ctrl-M，Ctrl + V）。

在"添加视图"对话框中，我们将保留视图模板名为"Index"，并选择"创建强类型视图"复选框。 这次我们将选择自动生成"列表"视图模板，然后选择"NerdDinner.Models.Dinner"作为模型类型传递给视图 (其中因为我们已表明我们要创建基架将导致假定我们添加视图对话框的"列表"Dinner 对象的序列将从传递控制器到视图）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

当我们单击"添加"按钮时，Visual Studio 将新的"Index.aspx"视图模板文件为我们创建我们"\Views\Dinners"目录中。 它将"搭建基架"提供了我们向视图传递的 Dinners HTML 表列表中的初始实现。

当我们运行的应用程序和访问权限 *"/ Dinners /"* 它会呈现我们 dinners 的列表的 URL 如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

上面的表解决方案为我们提供了我们的 Dinner 数据 – 这并不完全是我们希望我们消费型 Dinner 列表类似于网格的布局。 我们可以更新 Index.aspx 视图模板并修改它以列表更少的数据列，并使用&lt;ul&gt;元素来呈现它们而不是使用下面的代码对表：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

如我们循环访问每个 dinner 在我们的模型中，我们将使用在上面的 foreach 语句中的"var"关键字。 熟悉 C# 3.0 的那些可能会认为，使用"var"意味着 dinner 对象是后期绑定。 而是意味着编译器所使用类型推理针对强类型化的"模型"属性 (它属于类型"IEnumerable&lt;Dinner&gt;") 和编译为 Dinner 类型 – 这意味着我们获得完整的本地"dinner"变量intellisense 和编译时在代码块内检查：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

当我们点击刷新 */Dinners*我们更新的视图现在看起来像下面我们浏览器中的 URL:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

这查找更好，但尚未完全到位。 我们最后一步是启用最终用户可以单击列表中的单个 Dinners，看到它们的详细信息。 我们将呈现链接到我们 DinnersController 的详细信息操作方法的 HTML 超链接元素进行实现。

我们中有两种，索引视图中，我们可以生成这些超链接。 第一种是手动创建的 HTML &lt;&gt;元素类似下面，我们将嵌入&lt;%%&gt;内阻止&lt;&gt; HTML 元素：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

我们可以使用一种替代方法是利用在 ASP.NET MVC 支持以编程方式创建 HTML 中的内置"Html.ActionLink()"帮助程序方法&lt;&gt;链接到另一个操作方法的元素控制器：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Html.ActionLink() 帮助器方法的第一个参数是要显示的链接文本 （在本例中标题的 dinner），第二个参数是我们想要生成的链接 （在本例中的详细信息的方法），控制器操作名称，第三个参数是要将发送到 （实现为具有属性名称/值的匿名类型） 的操作的参数集。 我们在这种情况下指定的 dinner 我们想要链接到，并且由于 ASP.NET MVC 中的默认 URL 路由规则的"id"参数"{Controller} / {Action} / {id}"Html.ActionLink() 帮助器方法将生成以下输出：

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

Index.aspx 视图中，我们将使用 Html.ActionLink() 帮助器方法的方法，并具有指向适当的详细信息 URL 的列表中的每个 dinner:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

和现在当我们点击 */Dinners* dinner 列表类似于下面的 URL:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

当我们单击任一列表中 Dinners 我们导航以查看其详细信息：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>基于约定的命名和 \Views 目录结构

默认情况下的 ASP.NET MVC 应用程序使用基于约定的目录解析视图模板时命名结构。 这允许开发人员无需完全限定位置路径引用从控制器类中的视图时。 默认情况下 ASP.NET MVC 将查找视图模板文件内 * \Views\[ControllerName]\*应用程序下面的目录。

例如，我们一直在努力 DinnersController 类 – 它显式引用三个视图模板:"索引"、"详细信息"和"NotFound"。 ASP.NET MVC 将默认情况下查找中的这些视图*\Views\Dinners*目录下我们应用程序根目录：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

请注意上面这里是当前项目中的三个控制器类 (DinnersController、 HomeController 和 AccountController – 最后两个默认情况下我们在创建项目时添加)，并且有三个子目录 （一个用于每个控制器） \Views 目录中。

从主页和帐户控制器中引用的视图将自动解析及其各自的视图模板*\Views\Home*并*\Views\Account*目录。 *\Views\Shared*子目录提供了一种方法来存储跨多个控制器应用程序中重复使用的视图模板。 当 ASP.NET MVC 尝试解析视图模板时，它将首先检查内*\Views\[控制器]* 特定目录，并且如果它找不到视图模板那里它看起来将中*\Views\共享*目录。

命名单个视图模板时，推荐的指导是已导致要呈现的操作方法同名的视图模板。 例如，以上我们的"索引"操作方法使用"索引"视图来呈现视图结果，而"详细信息"操作方法使用"详细信息"视图来呈现其结果。 这样，可以轻松快速查看哪些模板是与每个操作相关联。

开发人员不需要显式指定视图模板名称，当视图模板具有与所调用的控制器上的操作方法相同的名称。 我们可以改为只是该模型对象传递给"View()"帮助器方法 （如果不指定视图名称），和 ASP.NET MVC 将自动推断我们想要使用*\Views\[ControllerName]\[ActionName]* 视图模板来呈现它的磁盘上。

这样，我们有点，清理我们的控制器代码并避免重复两次在代码中的名称：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

上面的代码是实现很好 Dinner 列表/详细信息所需的所有站点体验。

#### <a name="next-step"></a>下一步

现在，我们有很好的 Dinner 浏览生成的体验。

让我们现在启用 CRUD （创建、 读取、 更新、 删除） 数据窗体编辑支持。

> [!div class="step-by-step"]
> [上一页](build-a-model-with-business-rule-validations.md)
> [下一页](provide-crud-create-read-update-delete-data-form-entry-support.md)
