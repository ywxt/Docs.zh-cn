---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: 检查 ASP.NET MVC 如何支持 DropDownList 帮助程序 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 542790b7f475cc641ed26ff3187c25c25118e0ed
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577842"
---
<a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a>检查 ASP.NET MVC 如何支持 DropDownList 帮助程序
====================
通过[Rick Anderson]((https://twitter.com/RickAndMSFT))

在中**解决方案资源管理器**，右键单击*控制器*文件夹，然后选择**添加控制器**。 将控制器命名**StoreManagerController**。 设置的选项**添加控制器**对话框如下图所示。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

编辑*StoreManager\Index.cshtml*查看和删除`AlbumArtUrl`。 删除`AlbumArtUrl`使演示文稿更具可读性。 完成的代码如下所示。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

打开*Controllers\StoreManagerController.cs*文件并查找`Index`方法。 添加`OrderBy`子句，以便将价格按排序唱片集。 完整代码如下所示。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

价格按排序将更加轻松地测试对数据库进行更改。 时测试编辑和创建方法，可以使用较低的价格，因此已保存的数据将显示第一个。

打开*StoreManager\Edit.cshtml*文件。 恰好在图例标记之后添加以下行。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

下面的代码显示了此更改的上下文：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

`AlbumId`需对唱片集记录进行更改。

按 Ctrl+F5 运行应用程序。 选择**管理员**链接，然后选择**创建新**链接创建新的唱片集。 验证已保存的唱片集信息。 编辑唱片集，并验证所做的更改会保留。

### <a name="the-album-schema"></a>唱片集架构

`StoreManager`控制器创建的 MVC 基架机制允许 CRUD （创建、 读取、 更新、 删除） 访问相册中的音乐应用商店数据库。 唱片集信息的架构如下所示：

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

`Albums`表不存储的唱片集流派和说明，将其存储到外的键`Genres`表。 `Genres`表包含类型名称和说明。 同样，`Albums`唱片集艺术家名称，但外键的表不包含`Artists`表。 `Artists`表包含艺术家姓名。 如果您检查中的数据`Albums`表中，您可以看到每个行包含的外键`Genres`表和外键的`Artists`表。 下图显示从某些表数据`Albums`表。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a>HTML 选择标记

HTML`<select>`元素 (由 HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)帮助程序) 用于显示值 （如流派列表） 的完整列表。 编辑窗体，当已知的当前值时，选择列表可以显示的当前值。 当我们将所选的值设置为此前文所示**喜剧**。 选择列表非常适合用于显示类别或外键数据。 `<select>`流派外键的元素显示可能的类型名称的列表，但保存窗体时流派属性将更新为流派外键的值，而不是显示的类型名称。 在下图中，是所选流派**Disco**艺术家是**Donna 夏季**。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a>检查 ASP.NET MVC 基架代码

打开*Controllers\StoreManagerController.cs*文件并查找`HTTP GET Create`方法。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

`Create`方法将添加两个[SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx)对象添加到`ViewBag`，另一个用于包含类型信息，另一个用于包含艺术家信息。 [SelectList](https://msdn.microsoft.com/library/dd505286.aspx)上面使用的构造函数重载采用三个参数：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. *项*: [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx)包含列表中的项。 在上面的示例中，通过返回的流派列表`db.Genres`。
2. *dataValueField*： 在属性的名称**IEnumerable**列表，其中包含的密钥值。 在上述示例中，`GenreId`和`ArtistId`。
3. *dataTextField*： 在属性的名称**IEnumerable**列表，其中包含要显示的信息。 在艺术家和流派表`name`使用字段。

打开*Views\StoreManager\Create.cshtml*文件并检查`Html.DropDownList`genre 字段的帮助器标记。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

第一行显示了创建视图，采用`Album`模型。 在中`Create`上面所示方法，传递没有模型，因此视图获取**null** `Album`模型。 此时我们将创建新的唱片集，因此我们不需要任何`Album`其数据。

[Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)如上所示的重载采用要绑定到模型的字段的名称。 它还使用此名称来查找**ViewBag**对象，其中包含[SelectList](https://msdn.microsoft.com/library/dd505286.aspx)对象。 使用此重载，将要求你将为名称**ViewBag SelectList**对象`GenreId`。 第二个参数 (`String.Empty`) 是当未不选定任何项时要显示的文本。 这正是我们想要创建新的唱片集时。 如果删除第二个参数，并使用以下代码：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

选择列表在我们的示例值默认为第一个元素或 Rock。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

检查`HTTP POST Create`方法。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

此重载`Create`方法采用`album`创建 ASP.NET MVC 模型绑定系统从发布的表单值的对象。 当用户提交新的唱片集，如果模型状态无效，并且没有数据库错误时，添加新唱片集数据库。 下图显示了创建新的唱片集。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

可以使用[fiddler 工具](http://www.fiddler2.com/fiddler2/)若要检查的已发布的表单值的 ASP.NET MVC 模型绑定使用来创建唱片集对象。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png)。

### <a name="refactoring-the-viewbag-selectlist-creation"></a>重构 ViewBag SelectList 创建

这两个`Edit`方法和`HTTP POST Create`方法具有相同的代码来设置**SelectList**中**ViewBag**。 中的精神[DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself)，我们将重构此代码。 我们将使用此重构代码更高版本。

创建一个新的方法来添加流派和艺术家**SelectList**到**ViewBag**。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

将两个行设置为`ViewBag`中的每个`Create`并`Edit`方法通过调用`SetGenreArtistViewBag`方法。 完成的代码如下所示。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

创建新的唱片集和编辑某个唱片集以验证正常运行所做的更改。

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a>显式传递到 DropDownList SelectList

创建和编辑视图创建的 ASP.NET MVC 基架使用以下**DropDownList**重载：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

`DropDownList`创建视图标记，如下所示。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

因为`ViewBag`属性`SelectList`名为`GenreId`，则**DropDownList**帮助程序将使用`GenreId` **SelectList**中**ViewBag**. 在下面的示例**DropDownList**重载，`SelectList`中显式传递。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

打开*Views\StoreManager\Edit.cshtml*文件，并更改**DropDownList**调用显式传递**SelectList**，使用更高版本的重载。 执行此操作流派类别。 已完成的代码如下所示：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

运行应用程序，然后单击**管理员**链接，然后导航到 Jazz 唱片集，然后选择**编辑**链接。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

而被显示为当前所选流派 Jazz Rock 会显示。 当字符串自变量 （要绑定的属性） 和**SelectList**对象具有相同的名称，则不使用所选的值。 浏览器时不没有提供任何所选的值，默认为中的第一个元素**SelectList**(即**Rock**在上面的示例)。 这是一个已知的限制**DropDownList**帮助器。

打开*Controllers\StoreManagerController.cs*文件，并更改**SelectList**对象名称传递给`Genres`和`Artists`。 已完成的代码如下所示：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

流派和艺术家的名称是更好的类别的名称，因为它们包含多个只是每个类别的 ID。 我们之前所做的重构回报。 而不是更改**ViewBag**在四个方法中，我们更改被隔离到`SetGenreArtistViewBag`方法。

更改**DropDownList**调用中创建和编辑视图，以使用新**SelectList**名称。 编辑视图的新标记如下所示：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

创建视图需要用于防止 SelectList 中的第一个项显示的空字符串。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

创建新的唱片集和编辑某个唱片集以验证正常运行所做的更改。 通过选择唱片集的非 Rock genre 测试编辑代码。

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a>与 DropDownList 帮助器使用视图模型

在名为 ViewModels 文件夹中创建一个新类`AlbumSelectListViewModel`。 中的代码替换为`AlbumSelectListViewModel`以下类：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

`AlbumSelectListViewModel`构造函数采用相册、 艺术家和流派的列表，并创建一个对象，包含唱片集和一个`SelectList`流派和艺术家。

生成项目，因此`AlbumSelectListViewModel`当我们在下一步中创建视图时才可用。

添加`EditVM`方法`StoreManagerController`。 完成的代码如下所示。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

右键单击`AlbumSelectListViewModel`，选择**解决**，然后**使用 MvcMusicStore.ViewModels;**。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

或者，可以添加以下 using 语句：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

右键单击`EditVM`，然后选择**添加视图**。 使用如下所示的选项。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

选择**外**，然后替换内容*Views\StoreManager\EditVM.cshtml*具有以下文件：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

`EditVM`标记是非常类似于原始`Edit`标记有以下例外。

- 模型中的属性`Edit`视图都将窗体`model.property`(例如， `model.Title` )。 模型中的属性`EditVm`视图都将窗体`model.Album.property`(例如， `model.Album.Title`)。 这是因为`EditVM`视图为传递容器`Album`，而非`Album`如`Edit`视图。
- **DropDownList**第二个参数来自视图模型中，不**ViewBag**。
- **BeginForm**中的帮助程序`EditVM`视图显式回发到`Edit`操作方法。 通过发布回`Edit`操作，我们无需编写`HTTP POST EditVM`操作并可以重复使用`HTTP POST``Edit`操作。

运行应用程序和编辑唱片集。 更改 URL 以使用`EditVM`。 更改字段，然后点击**保存**按钮以验证代码是否正常工作。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a>您应该使用哪种方法？

显示所有三种方法是可接受的。 许多开发人员更愿意使用 explictily pass`SelectList`到`DropDownList`使用`ViewBag`。 此方法具有附加的优势的让你灵活地使用找不到更合适的名称。 一个需要注意的是不能将命名`ViewBag SelectList`对象模型属性与相同的名称。

一些开发人员更喜欢 ViewModel 方法。 其他人考虑更冗长的标记，并生成 HTML 视图模型方法的缺点。

在本部分中我们已经认识到这三种方法使用**DropDownList**类别数据。 在下一部分中，我们将介绍如何添加新的类别。

> [!div class="step-by-step"]
> [上一页](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [下一页](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)
