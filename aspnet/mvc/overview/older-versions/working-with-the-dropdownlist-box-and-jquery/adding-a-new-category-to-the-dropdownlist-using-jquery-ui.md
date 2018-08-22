---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: 将新类别添加到使用 jQuery UI DropDownList |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 9a893bf55070adde575d223cd527b02d6f0d470c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824838"
---
<a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a>将新类别添加到使用 jQuery UI DropDownList
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

HTML`Select`标记非常适合呈现固定的类别数据列表，但通常情况下您需要添加新的类别。 假设我们想要添加到我们的数据库中的类别的流派"Opera"？ 在本部分中，我们将使用的 jQuery UI 添加一个对话框，可用于添加新的类别。 下图显示了如何将用户界面显示在浏览器中。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

如果用户选择**添加新流派**链接，弹出对话框中提示用户输入新的类型名称 （和可选说明）。 下面显示的图像**添加流派**弹出对话框中。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

当输入新的类型名称和**保存**按钮后，将发生以下事件：

1. AJAX 调用将数据发送到流派控制器，它将新类型保存到数据库，并返回新流派信息 （类型名称和 ID） 作为 JSON 的 Create 方法。
2. JavaScript 将新的类型数据添加到选择列表。
3. JavaScript 将新流派所选的项。

   在下图**Opera**已添加到数据库和中所选**流派**下拉列表中。 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

打开*Views\StoreManager\Create.cshtml*文件和流派标记替换为以下下面的代码：

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

`_ChooseGenre`分部视图将包含所有用于挂接的 JavaScript 和 jQuery 用于实现新添加的类型功能的逻辑。 我们完成后将可以轻松执行同样的艺术家 UI 的代码。

在解决方案资源管理器，右键单击*Views\StoreManager*文件夹，然后选择**添加**，然后**视图**。 在中**视图名称**输入、 输入`_ChooseGenre`然后选择**添加**。 替换中的标记*Views\StoreManager\\_ChooseGenre.cshtml*具有以下文件：

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

第一行代码声明我们传入的`Album`作为我们的模型，完全相同的模型中创建视图的语句。 接下来的几个行都**标签**帮助程序标记中。 下一行是**DropDownList**帮助器调用，如下所示的原始创建视图完全相同。 下一行将具有名称的链接添加`Add New Genre`，并设置其样式类似于按钮。 行包含`ValidationMessageFor`复制直接从创建视图。 以下代码行：

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

创建隐藏的 div，id 为`genreDialog`。 我们将使用 jQuery 来挂接我们**添加流派**对话框中的 id`genreDialog`中此 div。 最后两个脚本标记包含我们将使用为实现添加的新流派功能的 JavaScript 文件的链接。 */Scripts/chooseGenre.js*文件是提供有关你的项目中，我们将检查它本教程的后面。

运行应用程序并单击**添加新流派**按钮。 在中**添加流派**对话框框中，输入**Opera**中**名称**输入的框。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

单击“保存”按钮。 AJAX 调用创建 Opera 类别然后填充 Opera，下拉列表并设置为所选流派 Opera。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

输入艺术家、 标题和价格，然后选择**创建**按钮。 如果输入小于 8.99 美元的价格，新的唱片集将出现在索引视图的顶部。 验证新的唱片集条目已保存在数据库中。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

尝试使用只有一个字母创建的新流派。 下面的代码中*Models\Genre.cs*文件设置的类型名称的最小值和最大长度。

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

客户端验证报告必须输入介于 2 到 20 个字符之间的字符串。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a>检查如何新类型添加到数据库和选择列表中。

打开*Scripts\chooseGenre.js*文件并检查代码。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

第二行使用 ID`genreDialog`上的 div 标记中创建一个对话框*Views\StoreManager\\_ChooseGenre.cshtml*文件。 命名参数的大多数都是自解释性。 `autoOpen`参数设置为 false，选择**创建流派**按钮将显式打开对话框 （这介绍后一种上）。 对话框有两个按钮**保存**并**取消**。 **取消**按钮关闭对话框。 下面的代码演示**保存**按钮函数。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

`var createGenreForm`从所选`createGenreForm`id。 `createGenreForm` ID 已在中的以下代码中设置*Views\Genre\\_CreateGenre.cshtml*文件。

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

[Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx)中使用的帮助程序重载*Views\Genre\\_CreateGenre.cshtml*文件的操作属性包含要提交窗体的 URL 生成 HTML。 您可以看到这通过在浏览器中显示创建唱片集页并在浏览器中选择显示源。 以下标记显示了生成包含窗体标记的 HTML。

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

JQuery`$.post`行进行 AJAX 调用到操作属性 (`/StoreManager/Create`)，并将从数据中传递**创建流派**对话框。 数据包含的名称的新流派和可选描述。 如果 AJAX 调用成功，新类型名称和值添加到选择的标记和新流派设置为所选的值。 由于这是动态生成的标记，通过在浏览器中查看源，不能看到新选择的选项。 可以看到与 IE 9 F12 开发人员工具的新 HTML。 要在 Internet Explorer 9 中查看新选择的选项，请按 F12 键以启动 F12 开发人员工具。 导航到创建页，并添加新流派，以便在流派选择列表中选择新流派。 中的 F12 开发人员工具：

1. 选择 HTML 选项卡。
2. 按刷新图标。  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. 在搜索框中，输入 GenreID。
4. 使用下一步图标，   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   导航到以下 select 标记：

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. 展开的最后一个选项值。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

下面的代码中*Scripts\chooseGenre.js*文件演示如何**添加新流派**按钮获取连接到了 click 事件，以及如何**添加新流派**对话框创建。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

第一行创建附加到的单击函数**添加新流派**按钮。 以下标记从 Views\StoreManager\\_ChooseGenre.cshtml 文件显示了如何**添加新流派**创建按钮：

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

Load 方法创建和打开添加类型对话框并调用 jQuery`parse`方法，以便在对话框中输入的数据时执行客户端验证。

在本部分介绍了如何创建一个对话框，可用于将新类别数据添加到选择列表。 可以按照相同的过程来创建用于向艺术家选择列表中添加新的艺术家 UI。 本教程提供的使用 ASP.NET MVC HTML 帮助器概述**DropDownList**。 有关使用的其他信息**DropDownList**，请参阅添加引用部分下。 请让我们知道是否本教程中对你有所帮助。

Rick.Anderson[at]Microsoft.com

### <a name="additional-references"></a>其他参考

- [ASP.NET MVC – 级联下拉列表中列出了教程](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx)通过[Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)
- [所选](http://harvesthq.github.com/chosen/)JavaScript 插件，支持多选和筛选。

### <a name="contributors"></a>参与者

- [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)
- Jean Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)

### <a name="reviewers"></a>审阅者

- Jean Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)
- Mike 教皇
- Tom Dykstra

> [!div class="step-by-step"]
> [上一篇](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
