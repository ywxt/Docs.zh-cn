---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: 第 3 部分： 视图和 Viewmodel |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 3 部分介绍 Views 和 ViewModels。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 828ff18abcc5932f82be71a45ebde589eeb051fa
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831059"
---
<a name="part-3-views-and-viewmodels"></a>第 3 部分： 视图和 Viewmodel
====================
通过[Jon Galloway](https://github.com/jongalloway)

> MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。  
>   
> MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。  
>   
> 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 3 部分介绍 Views 和 ViewModels。


到目前为止我们已经就已返回字符串的控制器操作。 这是一个好方法大致的控制器的工作方式，但不是将如何生成实际的 web 应用程序。 我们要想更好的方法来生成 HTML 返回到浏览器访问我们的站点 — 一个在其中我们可以使用模板文件更轻松地自定义 HTML 内容发送回。 这正是视图执行的操作。

## <a name="adding-a-view-template"></a>添加视图模板

若要使用视图模板，我们将更改 HomeController Index 方法，以返回一个 ActionResult，并使其返回 View()，类似如下：

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

上述更改表示而不是返回一个字符串，我们改为想要使用"视图"以生成返回的结果。

我们现在将为我们的项目中添加相应的视图模板。 为此我们将在索引操作方法中，将文本光标置于然后右键单击并选择"添加视图"。 这将打开添加视图对话框：

![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)

"添加视图"对话框可用于快速、 轻松地生成视图模板文件。 默认情况下，"添加视图"对话框预填充视图模板来创建，使其匹配将使用它的操作方法的名称。 由于我们使用我们 HomeController 的 index （） 操作方法中的"添加视图"上下文菜单，上述"添加视图"对话框的"索引"作为视图名称默认情况下预填充。 我们不需要更改任何在该对话框中的选项，因此请单击添加按钮。

当我们单击添加按钮时，Visual Web Developer 将创建新的 Index.cshtml 视图模板为我们在 \Views\Home 目录中，如果创建文件夹尚不存在。

![](mvc-music-store-part-3/_static/image2.png)

"Index.cshtml"文件的名称和文件夹位置是重要的是，并遵循的默认 ASP.NET MVC 命名约定。 目录名称、 \Views\Home，匹配的控制器的名为 HomeController。 视图模板名称，索引，匹配将显示该视图的控制器操作方法。

ASP.NET MVC，我们可以避免不得不显式指定的名称或视图模板的位置，当我们使用此命名约定可以返回视图。 它会默认情况下呈现 \Views\Home\Index.cshtml 视图模板时，我们编写类似下面的代码中我们 HomeController:

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

Visual Web Developer 中创建并打开"Index.cshtml"视图模板之后我们单击"添加视图"对话框中的"添加"按钮。 Index.cshtml 的内容如下所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

此视图使用 Razor 语法，这是比使用 ASP.NET Web 窗体和 ASP.NET MVC 的以前版本中的 Web 窗体视图引擎更简洁。 Web 窗体视图引擎在 ASP.NET MVC 3 中仍然可用，但许多开发人员查找 Razor 视图引擎的确非常适合 ASP.NET MVC 开发。

前三行设置页面标题使用 ViewBag.Title。 我们将看看这的工作原理更详细地推出，但首先让我们更新文本标题文本，并查看该页面。 更新&lt;h2&gt;标记可以说"这是主页上"，如下所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

运行我们的新文本可见的主页上，应用程序所示。

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a>有关通用站点元素中使用的布局

大多数网站有很多页间共享的内容： 导航、 页脚、 徽标图像、 样式表的引用，等等。Razor 视图引擎使这更容易地管理使用名为页\_Layout.cshtml 自动创建的对我们在/视图/共享文件夹。

![](mvc-music-store-part-3/_static/image4.png)

双击此文件夹以查看内容，如下所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

我们的单个视图中的内容将显示的@RenderBody（） 命令中，我们想要出现在之外的任何公共内容可以添加到\_Layout.cshtml 标记。 我们需要我们 MVC Music 商店到在站点中的所有页面上我们主页上和应用商店区域均具有链接的常见标头，以便我们将它添加到正上方的模板@RenderBody（） 语句。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a>更新了样式表

空项目模板包含一个非常简化的 CSS 文件只包括用来显示验证消息的样式。 我们的设计器提供了一些额外的 CSS 和图像，因此我们将添加中现在定义我们的站点，外观和感觉。

可在 MvcMusicStore Assets.zip 的内容目录中包含的更新后的 CSS 文件和映像[MVC Music 商店](https://github.com/evilDave/MVC-Music-Store)。 我们将在 Windows 资源管理器中选择这两个文件，并将其放入在 Visual Web Developer 中，我们的解决方案的 Content 文件夹中，如下所示：

![](mvc-music-store-part-3/_static/image5.png)

您将需要确认你是否要覆盖现有 Site.css 文件。 单击是。

![](mvc-music-store-part-3/_static/image6.png)

你的应用程序的 Content 文件夹现在将出现，如下所示：

![](mvc-music-store-part-3/_static/image7.png)

现在让我们运行该应用程序并查看我们更改的主页上的效果。

![](mvc-music-store-part-3/_static/image8.png)

- 让我们回顾一下会发生什么变化： HomeController 索引操作方法找到并显示 \Views\Home\Index.cshtmlView 模板，即使我们的代码称为"返回 View()"，因为我们查看模板遵循标准的命名约定。
- 主页上显示 \Views\Home\Index.cshtml 视图模板中定义一个简单的欢迎使用消息。
- 使用主页上我们\_Layout.cshtml 模板，因此欢迎使用消息包含在标准站点 HTML 布局。

## <a name="using-a-model-to-pass-information-to-our-view"></a>使用模型将信息传递到视图

只是显示了硬编码 HTML 的视图模板不会给非常有趣的 web 站点。 若要创建动态网站，我们将改为想要将信息从控制器操作传递到我们的视图模板。

在模型-视图-控制器模式中，的术语模型是指将对象表示在应用程序中的数据。 通常情况下，模型对象对应于表在数据库中，但他们就不需要。

返回一个 ActionResult 控制器操作方法可以将模型对象传递给视图。 这允许进行完全以生成响应，然后将此信息传递到视图模板所需的所有信息打包控制器用于生成相应的 HTML 响应。 这是最容易理解通过查看运行中，让我们开始吧。

首先，我们将创建一些模型类来表示在我们存储的类型和唱片集。 让我们首先创建一个类型的类。 右键单击你的项目中的"Models"文件夹中，选择"添加类"选项，并将文件命名"Genre.cs"。

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

然后将名称属性的公共字符串添加到已创建的类：

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

*注意： 在您想知道的情况下 {get; 设置;} 表示法进行 C# 的自动实现的属性功能的使用。这为我们提供一个属性的优点而无需我们声明支持字段。*

接下来，请按照相同的步骤来创建一个具有标题和流派属性的唱片集类 （名为 Album.cs）：

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

现在我们可以修改 StoreController 若要使用它显示我们的模型中的动态信息的视图。 如果-出于演示目的-现在我们名为我们根据请求 ID 的唱片集，我们无法显示该信息，如下面的视图中所示。

![](mvc-music-store-part-3/_static/image10.png)

我们将开始通过更改存储详细信息操作，因此它显示的是一个唱片集信息。 将"using"语句添加到顶部**StoreControllers**类，以包含 MvcMusicStore.Models 命名空间，因此我们无需键入 MvcMusicStore.Models.Album，每次我们想要使用的唱片集类。 此类的"using"部分现在应显示如下所示。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

接下来，我们将更新的详细信息控制器操作，以便它返回 ActionResult 而不是一个字符串，正如我们做了 HomeController 的索引方法。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

现在我们可以修改逻辑，以返回到视图的唱片集对象。 本教程中稍后我们将会从数据库检索数据 – 但现在我们将使用"虚拟数据"以开始。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

*注意： 如果您熟悉 C#，您可能会假定使用 var 意味着我们唱片集的变量是后期绑定。不正确-C# 编译器所使用类型推理基于什么我们要分配给该变量来确定该唱片集属于类型唱片集和编译本地唱片集变量作为唱片集类型，因此我们获得编译时检查的 Visual Studio 代码编辑器支持。*

让我们现在创建一个使用我们的唱片集来生成 HTML 响应的视图模板。 在此之前，我们需要生成项目，以便添加视图对话框知道我们新创建的唱片集类。 可以生成项目通过选择 Debug⇨Build MvcMusicStore 菜单项 （for 额外信用额度，你可以使用 Ctrl-Shift-B 快捷方式以生成项目）。

![](mvc-music-store-part-3/_static/image11.png)

现在，我们设置了我们支持类，我们可以开始构建我们的视图模板。 在详细信息方法内右键单击并从上下文菜单中选择"添加视图..."。

![](mvc-music-store-part-3/_static/image12.png)

我们要创建新的视图模板像 HomeController 与之前执行。 因为我们将从 StoreController 创建它将默认情况下生成 \Views\Store\Index.cshtml 文件中。

不同于之前，我们将选中"创建强类型"视图复选框。 然后将我们选择"视图数据类"下拉 downlist 中我们"唱片集"的类。 这将导致"添加视图"对话框来创建视图模板所需的对象将传递给它要使用的相册。

![](mvc-music-store-part-3/_static/image13.png)

当我们单击"添加"按钮时将创建我们 \Views\Store\Details.cshtml 视图模板，包含以下代码。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

请注意，该值指示此视图为强类型化为我们唱片集的类的第一行。 Razor 视图引擎能够理解，它已被传递唱片集对象，因此我们可以轻松访问模型属性，并甚至具有 Visual Web Developer 编辑器中的 IntelliSense 优势。

更新&lt;h2&gt;标记，以便它显示的唱片集标题属性修改的行才会显示，如下所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

请注意时输入超过这个有效期之后，会触发智能感知@Model关键字，显示的属性和唱片集类支持的方法。

让我们现在重新运行我们的项目，并访问应用商店/详细信息/5 URL。 我们将看到类似如下的相册的详细信息。

![](mvc-music-store-part-3/_static/image14.png)

现在我们将使应用商店浏览操作方法类似的更新。 更新的方法，使其返回一个 ActionResult，并修改方法逻辑，因此它将创建一个新的流派对象并将其返回到视图。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

浏览方法中右键单击并从上下文菜单中，选择"添加视图..."，然后添加了强类型化的视图将强类型化添加到流派类。

![](mvc-music-store-part-3/_static/image15.png)

更新&lt;h2&gt;视图中的元素中的代码 （/Views/Store/Browse.cshtml) 以显示类型信息。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

现在让我们重新运行我们的项目，并浏览到应用商店/浏览？Genre = Disco 的 URL。 我们将看到浏览页显示如下所示。

![](mvc-music-store-part-3/_static/image16.png)

最后，让我们进行的稍微复杂更新**存储索引**操作方法和视图，以显示我们的存储区中的所有影片类型列表。 我们将为我们的模型对象，而不只是单个流派使用流派列表来执行的操作。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

存储索引操作方法中右键单击并选择添加视图之前，选择流派作为模型类，并按添加按钮。

![](mvc-music-store-part-3/_static/image17.png)

首先我们将更改@model声明，以指示该视图将期望出现多个流派对象而不是只是一个。 更改 /Store/Index.cshtml 读取，如下所示的第一行：

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

这将告知 Razor 视图引擎，它将使用可以容纳多个流派对象的模型对象。 我们使用 IEnumerable&lt;流派&gt;而不是列表&lt;流派&gt;由于它是更通用，让我们能够将我们的模型类型更高版本更改为任何支持 IEnumerable 接口的对象类型。

接下来，我们将循环访问下面的代码已完成的视图中所示的模型中的类型对象。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

请注意，我们具有完全 IntelliSense 支持在进入此代码中，以便当我们键入"@Model。" 我们看到的所有方法和支持 IEnumerable of type Genre 的属性。

![](mvc-music-store-part-3/_static/image18.png)

在我们"foreach"循环中，Visual Web 开发人员知道，每个项的类型是类型，因此我们会看到 IntelliSense 每个流派类型。

![](mvc-music-store-part-3/_static/image19.png)

接下来，基架功能检查流派对象，并确定，每个将包含一个 Name 属性，因此它循环访问，并将其输出。它还会生成每个单个项目的编辑、 详细信息和删除链接。 我们将利用这一点，更高版本中我们商店经理处，但现在我们想要改为具有一个简单的列表。

当我们运行该应用程序，并浏览到 /Store 时，我们看到显示的计数和的类型列表。

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a>页之间添加链接

我们目前列出了流派的 /Store URL 只需以明文形式列出类型名称。 让我们来更改这使而不是纯文本我们改为具有流派名称链接到相应的应用商店/浏览 URL，以便单击某个音乐类型，如"Disco"将导航到应用商店/浏览？ genre = Disco URL。 我们无法更新 \Views\Store\Index.cshtml 视图模板为使用这些链接的代码类似如下的输出 **（不要键入考虑到这-我们将改进）**:

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

操作成功，但它可能会导致问题更高版本，因为它依赖于硬编码的字符串。 例如，如果我们想要重命名控制器，我们需要我们寻找需要更新的链接的代码中进行搜索。

我们可以使用一种替代方法是利用 HTML 帮助器方法。 ASP.NET MVC 包括可从我们的视图模板代码以执行各种常见任务，就像下面这样的 HTML 帮助器方法。 Html.ActionLink() 帮助器方法是一个特别有用，并轻松地生成 HTML &lt;&gt;链接，并负责令人讨厌的详细信息，如确保 URL 路径为正确编码的 URL。

Html.ActionLink() 有多个不同的重载，以允许指定尽可能为你的链接所需的信息。 在最简单的情况下，将提供只是链接文本和要在客户端上单击超链接时转到的操作方法。 例如，我们可以链接到"应用商店 /"链接文本"转到存储索引"使用以下调用存储详细信息页上的 index （） 方法：

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

*注意： 在这种情况下，我们不需要指定控制器名称，因为我们只链接到同一呈现当前视图的控制器内的另一个动作。*

我们浏览页面的链接需要传递一个参数，不过，因此我们将使用另一个重载采用三个参数的 Html.ActionLink 方法：

- 1. 链接文本，将显示类型名称
- 2. 控制器操作名称 （浏览）
- 3. 路由参数值，指定的名称 （类型） 和值 （类型名称）

将它们组合在一起此处向存储区索引视图，我们就将编写这些链接：

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

现在我们再次运行我们的项目并访问 /Store/ URL 时我们会看到影片类型列表。 每个流派是超链接 – 单击时它会引导我们完成到我们/Store/浏览？ genre =*[类型]* URL。

![](mvc-music-store-part-3/_static/image3.jpg)

流派列表的 HTML 如下所示：

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]


> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-2.md)
> [下一页](mvc-music-store-part-4.md)
