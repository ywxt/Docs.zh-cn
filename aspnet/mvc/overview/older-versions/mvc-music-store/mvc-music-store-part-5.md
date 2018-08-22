---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 第 5 部分： 编辑窗体和模板化 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 5 部分介绍如何编辑窗体和模板化。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: c1065dcb45b6d28672edba32b95c7fc476c8b944
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823571"
---
<a name="part-5-edit-forms-and-templating"></a>第 5 部分： 编辑窗体和模板化
====================
通过[Jon Galloway](https://github.com/jongalloway)

> MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。  
>   
> MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。
> 
> 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 5 部分介绍如何编辑窗体和模板化。


在过去的章中，我们已从数据库加载数据并显示它。 在本章中，我们还将启用编辑数据。

## <a name="creating-the-storemanagercontroller"></a>创建 StoreManagerController

我们将首先创建名为的新控制器**StoreManagerController**。 此控制器中，我们将充分利用 ASP.NET MVC 3 Tools Update 中提供的基架功能。 设置添加控制器对话框的选项，如下所示。

![](mvc-music-store-part-5/_static/image1.png)

当你单击添加按钮时，会看到 ASP.NET MVC 3 基架机制为您完成大量的工作：

- 它使用实体框架局部变量创建新 StoreManagerController
- 它将 StoreManager 文件夹添加到项目的 Views 文件夹
- 它将添加 Create.cshtml、 Delete.cshtml、 Details.cshtml、 Edit.cshtml 和 Index.cshtml 视图中，强类型化为唱片集类

![](mvc-music-store-part-5/_static/image2.png)

新 StoreManager 控制器类包括 CRUD （创建、 读取、 更新、 删除） 控制器操作在其知道如何处理与唱片集的模型和我们的 Entity Framework 上下文用于数据库访问权限。

## <a name="modifying-a-scaffolded-view"></a>修改基架生成的视图

请务必记住，虽然我们已生成此代码，这是标准的 ASP.NET MVC 代码，就像已在本教程中，我们已编写的一样。 它可用于为你节省将会花费的时间编写样板控制器代码和手动创建强类型化的视图，但这不是生成的代码可能会看到前面加上有关如何不能更改的注释中的可怕警告类型代码。 这是你的代码，并且你应将其更改。

因此，让我们先快速编辑到 StoreManager 索引视图 (/ Views/StoreManager/Index.cshtml)。 此视图将显示一个表，该表列出了在我们的存储与编辑相册 / 详细信息 / 删除的链接，并包含唱片集的公共属性。 我们将删除 AlbumArtUrl 字段，因为它不是在此显示中非常有用。 中&lt;表&gt;部分的查看代码中，删除&lt;th&gt;并&lt;td&gt;元素周围 AlbumArtUrl 引用，如以下突出显示的行所示：

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

经过修改的视图代码将如下所示：

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a>初步了解存储管理器

现在运行应用程序并浏览到/StoreManager /。 此时将显示存储管理器我们只需修改索引，其中包含用于编辑的详细信息，和删除链接的存储中显示的唱片集列表。

![](mvc-music-store-part-5/_static/image3.png)

单击编辑链接显示的唱片集、 流派和艺术家包括下拉列表的字段的编辑窗体。

![](mvc-music-store-part-5/_static/image4.png)

单击"返回到列表"链接，在底部，然后单击唱片集的详细信息链接。 这将显示单个唱片集的详细信息。

![](mvc-music-store-part-5/_static/image5.png)

同样，单击列表链接回，然后单击删除链接。 此时将显示确认对话框中，显示的唱片集详细信息并询问我们要确保我们想要将其删除。

![](mvc-music-store-part-5/_static/image6.png)

单击底部的删除按钮，将删除唱片集，并使你返回到索引页，其中显示了已删除的唱片集。

我们还没有完成与存储管理器，但我们具有有效的控制器和视图的 CRUD 操作从启动代码。

## <a name="looking-at-the-store-manager-controller-code"></a>查看存储管理器控制器代码

存储管理器控制器包含大量的代码。 让我们通过此从上到下。 该控制器包含一个 MVC 控制器，以及对我们的模型命名空间的引用的某些标准命名空间。 控制器有 MusicStoreEntities，使用每个控制器操作进行数据访问的专用实例。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a>存储管理器索引和详细信息操作

索引视图中检索唱片集，包括每个唱片集的被引用的流派和艺术家信息，正如我们以前看到的应用商店浏览方法上工作时的列表。 索引视图，以便它可以使控制器进行高效的查询的原始请求中的此信息显示每个唱片集的类型名称和艺术家姓名关注对所链接的对象的引用。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

StoreManager 控制器的详细信息控制器操作的工作方式，我们编写了以前为-它会询问是否唱片集的存储控制器的详细信息操作完全相同的 ID 使用 find （） 方法，然后将其返回到视图。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a>创建操作方法

创建操作方法是稍有不同的为止，我们所看到的因为它们处理窗体输入。 当用户首次访问时 /StoreManager/创建/他们将看到一个空窗体。 此 HTML 页将包含&lt;窗体&gt;元素，其中包含下拉列表中，文本框中输入的元素可在其中输入唱片集的详细信息。

唱片集窗体值中填充用户后，他们可以按"保存"按钮提交这些更改回我们的应用程序保存在数据库中。 当用户按"保存"按钮&lt;窗体&gt;将执行 HTTP POST 回 /StoreManager/创建/URL，并提交&lt;窗体&gt;作为 HTTP POST 的一部分的值。

ASP.NET MVC 使我们能够轻松地通过使我们能够实现两个单独的"创建"操作方法中我们 StoreManagerController 类-另一个用于处理初始的 HTTP GET 浏览到 /StoreManager/Create 拆分这两个 URL 调用方案的逻辑/ URL 和其他处理 HTTP POST 提交的更改。

### <a name="passing-information-to-a-view-using-viewbag"></a>将信息传递给视图使用 ViewBag

我们之前在本教程中已使用 ViewBag 但探讨它得还不够。 ViewBag 使我们能够将信息传递给视图，而无需使用强类型化的模型对象。 在这种情况下，需要将这两个流派和艺术家的列表传递给窗体来填充下拉列表中，我们编辑 HTTP-GET 控制器操作和执行此操作的最简单方法是将其返回作为 ViewBag 项。

ViewBag 是动态对象，这意味着你可以无需编写代码来定义这些属性键入 ViewBag.Foo 或 ViewBag.YourNameHere。 在这种情况下，控制器代码使用 ViewBag.GenreId 和 ViewBag.ArtistId，以便处理该窗体提交的下拉列表中值将 GenreId 和 ArtistId，即会设置它们的唱片集属性。

这些下拉列表中的值返回到窗体使用 SelectList 对象，它专门为此目的。 这是使用如下代码：

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

您可以看到从操作方法代码，三个参数是要用于创建此对象：

- 将显示在下拉列表中的项的列表。 请注意，这并不只是一个字符串-我们传入影片类型列表。
- 下一个参数传递给 SelectList 是所选的值。 此 SelectList 如何知道如何预选择列表中的项。 这将是更易于理解时我们了解一下编辑窗体，这是非常相似。
- 最后一个参数是要显示的属性。 在这种情况下，这指示 Genre.Name 属性什么将向用户显示。

这一点后，然后，创建 HTTP GET 操作是非常简单-两个 SelectLists 添加到 ViewBag，并没有模型对象传递给窗体 （因为它尚未创建）。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a>若要在创建视图中显示在删除列表的 HTML 帮助器

由于我们已经讨论过的下拉列表值传递到视图的方式，让我们快速看一下视图以查看这些值的显示方式。 查看代码中 (/ Views/StoreManager/Create.cshtml)，可以看到进行以下调用以显示流派下拉列表。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

这被称为 HTML 帮助器的实用工具方法，后者将执行一项常见视图任务。 HTML 帮助程序是在保持简洁和可读的我们查看代码中非常有用。 Html.DropDownList 帮助程序提供的 ASP.NET MVC 中，但我们稍后会看到它是可以创建适用于查看代码，我们将在我们的应用程序中重复使用我们的帮助程序。

Html.DropDownList 调用只需告知两件事-何处进行 get 列表后，若要显示，和哪些值 （如果有） 应预先选择。 第一个参数，GenreId，告知 DropDownList 以寻找名 GenreId 为模型或 ViewBag 中的值。 第二个参数用于指示要显示的值最初在下拉列表中选择。 由于此窗体是创建窗体，因此没有要预先选择的值，并传递 String.Empty。

### <a name="handling-the-posted-form-values"></a>处理发布窗体值

如之前所述，有两个操作方法与每个窗体相关联。 第一个处理 HTTP GET 请求，并显示该窗体。 第二个处理 HTTP POST 请求，其中包含的提交的窗体值。 请注意控制器操作具有 [HttpPost] 属性，它将告诉 ASP.NET MVC 它只应响应 HTTP POST 请求。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

此操作有四个职责：

- 1. 读取窗体值
- 2. 检查窗体值是否传递的任何验证规则
- 3. 如果表单提交有效，将数据保存并显示更新的列表
- 4. 如果提交窗体不是有效的重新显示具有验证错误的窗体

#### <a name="reading-form-values-with-model-binding"></a>使用模型绑定的读取窗体值

控制器操作正在处理包括用于标题、 价格和 AlbumArtUrl GenreId 和 ArtistId 值 （从下拉列表） 和文本框值的窗体提交。 可以直接访问窗体值时，更好的方法是使用内置到 ASP.NET MVC 模型绑定功能。 模型类型作为参数的控制器操作时，ASP.NET MVC 将尝试填充该类型使用窗体输入 （以及路由和查询字符串值） 的对象。 此查找的值名称匹配的模型对象的属性，例如，它会设置新的唱片集对象的 GenreId 值时，它会查找与名称 GenreId 的输入。 创建 ASP.NET MVC 中使用的标准方法的视图时，将始终为输入的字段名称，使用属性名称，因此此字段名称将只匹配呈现窗体。

#### <a name="validating-the-model"></a>验证模型

通过简单调用 ModelState.IsValid 验证模型。 我们尚未向我们唱片集的类添加任何验证规则，但-我们将执行在位-好了，现在这一检查没有太大关系。 重要的是此 ModelStat.IsValid 检查将适应，我们在我们的模型，以便将来对验证规则的更改将不需要任何更新到控制器操作代码的验证规则。

#### <a name="saving-the-submitted-values"></a>保存已提交的值

如果提交窗体通过验证，就可以将值保存到数据库。 使用实体框架，只需将模型添加到唱片集集合并调用 SaveChanges。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

实体框架生成相应的 SQL 命令，以保留的值。 在保存后的数据，我们将重定向回唱片集的列表，我们可以看到我们的更新。 这是通过返回 RedirectToAction 与我们要显示的控制器操作的名称。 在这种情况下，这是 Index 方法。

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a>显示无效的窗体提交带有验证错误

在无效的窗体输入的情况下的下拉列表中值添加到 ViewBag （如 HTTP GET） 和绑定的模型值传递回视图进行显示。 验证错误将自动显示使用@Html.ValidationMessageFor的 HTML 帮助器。

#### <a name="testing-the-create-form"></a>测试创建窗体

若要测试此扩展，运行的应用程序和浏览到 /StoreManager/创建 /-这将显示您 StoreController 创建 HTTP GET 方法返回的空白表单。

填写一些值并单击创建按钮提交窗体。

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a>处理编辑

编辑操作对 （HTTP GET 和 HTTP POST） 都非常类似于我们刚了解的创建操作方法。 由于编辑方案涉及使用现有的相册，编辑 HTTP-GET 方法加载的唱片集基于"id"参数传递通过路由中。 如我们以前介绍了中的详细信息控制器操作，这段代码用于检索通过 AlbumId 唱片集都是相同的。 创建与 / HTTP GET 方法，通过 ViewBag 返回的下拉列表值。 这使得我们可以将唱片集作为我们的模型对象返回到视图 （这强类型化的唱片集类） 时通过 ViewBag 传递其他数据 （例如影片类型列表）。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

编辑 HTTP POST 操作是非常类似于创建 HTTP POST 操作。 唯一的区别是，而不是向数据库添加新唱片集。唱片集集合中，我们要查找唱片集的当前实例使用 db。Entry(album) 并将其状态设置为已修改。 这会告诉实体框架，我们正在修改现有而不是创建一个新的相册。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

我们可以通过运行应用程序并浏览到/StoreManger/，然后单击唱片集的编辑链接它进行测试。

![](mvc-music-store-part-5/_static/image9.png)

此时将显示所示编辑 HTTP GET 方法的编辑表单。 填写一些值并单击保存按钮。

![](mvc-music-store-part-5/_static/image10.png)

此发布窗体、 保存值，并返回我们到唱片集列表中，显示已更新值。

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a>处理删除

删除遵循与编辑和创建，使用一个控制器操作可以确认窗体，显示和另一个控制器操作来处理提交窗体相同的模式。

HTTP GET 删除控制器操作正是我们之前的存储管理器详细信息控制器操作相同。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

我们显示为唱片集类型，使用 Delete 视图内容模板的强类型化的窗体。

![](mvc-music-store-part-5/_static/image12.png)

删除模板显示所有字段的模型，但我们可以相当简化该列表。 更改为以下 /Views/StoreManager/Delete.cshtml 中的查看代码。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

此时将显示简化的删除确认。

![](mvc-music-store-part-5/_static/image13.png)

单击删除按钮后，窗体会回发到服务器，执行 DeleteConfirmed 操作。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

我们 HTTP POST 删除控制器操作将执行以下操作：

- 1. 加载的唱片集的 ID
- 2. 将其删除唱片集并保存更改
- 3. 重定向到显示唱片集已从列表中删除的索引

若要测试这一点，运行该应用程序，并浏览到 /StoreManager。 从列表中选择唱片集，然后单击删除链接。

![](mvc-music-store-part-5/_static/image14.png)

此时会显示我们删除确认屏幕。

![](mvc-music-store-part-5/_static/image15.png)

单击删除按钮移除唱片集，并返回我们为存储管理器索引页，其中显示了已删除的唱片集。

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a>使用自定义 HTML 帮助器要截断的文本

我们有一个潜在的问题与我们的存储管理器索引页。 唱片集标题和艺术家姓名属性都可以是时间足够长，它们可能会引发关闭我们表格的格式。 我们将创建自定义的 HTML 帮助程序，以便我们能够轻松地截断这些和我们的视图中的其他属性。

![](mvc-music-store-part-5/_static/image17.png)

Razor 的@helper语法变得很容易在视图中创建您自己使用的帮助器函数。 打开 /Views/StoreManager/Index.cshtml 视图，并添加以下代码直接后的@model行。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

此帮助程序方法采用一个字符串，以允许的最大长度。 帮助程序提供的文本是短于指定的长度，如果将其作为输出的是。 如果长度，然后它将截断的文本，并且"..."剩余时间内呈现。

现在我们可以使用我们截断的帮助器以确保不超过 25 个字符的唱片集标题和艺术家姓名的属性。 使用我们新的截断帮助程序的完整视图代码如下所示。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

现在当我们浏览 /StoreManager/ URL 时，唱片集和标题保留下面我们最大长度。

![](mvc-music-store-part-5/_static/image18.png)

注意： 这将显示创建和使用一个帮助程序在一个视图中的简单情况。 若要了解有关创建可在整个站点的帮助程序的详细信息，请参阅我的博客文章： [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)


> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-4.md)
> [下一页](mvc-music-store-part-6.md)
