---
uid: web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-cs
title: 更新和删除现有的二进制数据 (C#) |Microsoft Docs
author: rick-anderson
description: 在之前的教程中我们已了解如何在 GridView 控件可以轻松地编辑和删除文本数据。 在本教程中我们看到如何在 GridView 控件还使...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/27/2007
ms.topic: article
ms.assetid: 35798f21-1606-434b-83f8-30166906ef49
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 2eb9b4cb9403f5d793605fe023e4e0757bcda6f4
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372007"
---
<a name="updating-and-deleting-existing-binary-data-c"></a>更新和删除现有的二进制数据 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_57_CS.exe)或[下载 PDF](updating-and-deleting-existing-binary-data-cs/_static/datatutorial57cs1.pdf)

> 在之前的教程中我们已了解如何在 GridView 控件可以轻松地编辑和删除文本数据。 在本教程中我们看到如何在 GridView 控件还可以编辑和删除该二进制数据是保存在数据库中还是文件系统中存储二进制数据。


## <a name="introduction"></a>介绍

在过去三个教程通过我们已添加一小段用于处理二进制数据的功能。 我们通过添加启动`BrochurePath`列添加到`Categories`表并相应地更新体系结构。 我们还添加了数据访问层和业务逻辑层方法，以便使用类别表 s 现有`Picture`列，包含图像文件的二进制内容 s。 我们已构建网页以提供类别的图片中所示的 GridView 中的二进制数据的小册子中，下载链接`<img>`元素并将其添加 DetailsView 以允许用户添加新类别，并将其手册和图片数据上传。

所有这些其余实现是编辑和删除现有类别，我们要完成的操作在本教程中使用的 GridView s 内置编辑和删除功能的能力。 在编辑某个类别时，用户将能够根据需要上传新图片或继续使用现有的类别。 为小册子中，他们可以选择使用现有的小册子中，将上传新的手册，或指示类别不再具有与之关联的手册。 让我们来开始 ！

## <a name="step-1-updating-the-data-access-layer"></a>步骤 1： 更新数据访问层

DAL 具有自动生成`Insert`， `Update`，并`Delete`方法，但这些方法生成的基于`CategoriesTableAdapter`s 主查询，这不包括`Picture`列。 因此，`Insert`和`Update`方法不包括的参数来指定类别的图片的二进制数据。 像执行[前面的教程](including-a-file-upload-option-when-adding-a-new-record-cs.md)，我们需要创建新的 TableAdapter 方法用于更新`Categories`表时指定的二进制数据。

打开类型化数据集，并从设计器中，右键单击`CategoriesTableAdapter`s 标头，然后选择添加查询从上下文菜单到 launche TableAdapter 查询配置向导。 此向导首先会向我们询问 TableAdapter 查询应如何访问数据库。 选择使用 SQL 语句，然后单击下一步。 下一步会提示为查询的类型生成。 由于我们重新创建要添加到新的记录的查询`Categories`表中，选择更新并单击下一步。


[![选择更新选项](updating-and-deleting-existing-binary-data-cs/_static/image1.gif)](updating-and-deleting-existing-binary-data-cs/_static/image1.png)

**图 1**： 选择更新选项 ([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image2.png))


现在，我们需要指定`UPDATE`SQL 语句。 该向导会自动建议`UPDATE`对应于 TableAdapter s 主查询的语句 (更新的那个`CategoryName`， `Description`，和`BrochurePath`值)。 更改的语句，以便`Picture`列则包含与`@Picture`参数，如下所示：


[!code-sql[Main](updating-and-deleting-existing-binary-data-cs/samples/sample1.sql)]

在向导的最后一个屏幕询问我们要将新的 TableAdapter 方法。 输入`UpdateWithPicture`并单击完成。


[![命名新的 TableAdapter 方法 UpdateWithPicture](updating-and-deleting-existing-binary-data-cs/_static/image2.gif)](updating-and-deleting-existing-binary-data-cs/_static/image3.png)

**图 2**： 新的 TableAdapter 方法命名`UpdateWithPicture`([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image4.png))


## <a name="step-2-adding-the-business-logic-layer-methods"></a>步骤 2： 添加业务逻辑层方法

除了更新 DAL，我们需要更新 BLL 可以包含用于更新和删除某个类别的方法。 这些是将从表示层调用的方法。

如果删除某个类别，我们可以使用`CategoriesTableAdapter`自动生成的 s`Delete`方法。 添加以下方法`CategoriesBLL`类：


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample2.cs)]

对于本教程中，let s 创建两种方法来更新类别的期望二进制图片数据并调用`UpdateWithPicture`我们刚添加到方法`CategoriesTableAdapter`，另一个接受仅`CategoryName`， `Description`，和`BrochurePath`值，并使用`CategoriesTableAdapter`类自动生成的 s`Update`语句。 使用两种方法背后的基本原理是，在某些情况下，用户可能想要更新的类别的图片以及其其他字段，情况下，用户将需要在其中上传新的图片。 已上传的图片 s 二进制数据然后可在`UPDATE`语句。 在其他情况下，用户可能只关注中更新，例如，名称和说明。 但是，如果`UPDATE`语句等待的二进制数据`Picture`列，那么我们 d 需要提供这些信息。 这需要额外经历一次到数据库以使图片数据重新用于正在编辑的记录。 因此，我们希望两个`UPDATE`方法。 业务逻辑层将确定要使用哪一个基于图片数据以更新类别时提供。

若要实现此目的，两个将方法添加到`CategoriesBLL`类，这两名为`UpdateCategory`。 第一个应接受三个`string`s，`byte`数组和一个`int`作为其输入参数; 第二个，只需三个`string`s 和`int`。 `string`输入的参数仅适用于 s 类别名称、 说明和手册文件路径`byte`数组是二进制内容的类别的图片，并`int`标识`CategoryID`要更新的记录。 请注意，第一个重载会调用传入的第二个 if`byte`数组是`null`:


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample3.cs)]

## <a name="step-3-copying-over-the-insert-and-view-functionality"></a>步骤 3： 复制的插入和视图功能

在中[前面的教程](including-a-file-upload-option-when-adding-a-new-record-cs.md)我们创建一个名为页`UploadInDetailsView.aspx`，列出 GridView 中的所有类别，并提供说明如何将新类别添加到系统。 在本教程中我们将扩展 GridView，其中包括编辑和删除支持。 而不是继续使用从`UploadInDetailsView.aspx`，让 s 改为将放置在此教程的更改`UpdatingAndDeleting.aspx`同一文件夹中的页`~/BinaryData`。 复制并粘贴在声明性标记，代码从`UploadInDetailsView.aspx`到`UpdatingAndDeleting.aspx`。

首先打开`UploadInDetailsView.aspx`页。 复制的所有声明性语法中`<asp:Content>`元素，如图 3 中所示。 接下来，打开`UpdatingAndDeleting.aspx`并粘贴在此标记其`<asp:Content>`元素。 同样中的代码复制`UploadInDetailsView.aspx`页上为 s 代码隐藏类`UpdatingAndDeleting.aspx`。


[![将声明性标记从 UploadInDetailsView.aspx 复制](updating-and-deleting-existing-binary-data-cs/_static/image3.gif)](updating-and-deleting-existing-binary-data-cs/_static/image5.png)

**图 3**： 复制中的声明性标记`UploadInDetailsView.aspx`([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image6.png))


在复制后通过声明性标记和代码，请访问`UpdatingAndDeleting.aspx`。 应该会看到相同输出，并且具有相同的用户体验与使用`UploadInDetailsView.aspx`页上从上一教程。

## <a name="step-4-adding-deleting-support-to-the-objectdatasource-and-gridview"></a>步骤 4： 添加删除到 ObjectDataSource 和 GridView 支持

如后面所述[概述的插入、 更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程中，GridView 提供内置的删除功能，并可在一个复选框的刻度线启用这些功能，如果网格 s 基础数据源支持删除。 当前 ObjectDataSource GridView 绑定到 (`CategoriesDataSource`) 不支持删除。

若要解决此问题，单击从 ObjectDataSource s 智能标记的配置数据源选项，以启动向导。 第一个屏幕显示对象数据源配置为使用`CategoriesBLL`类。 单击下一步。 目前，仅的 ObjectDataSource s`InsertMethod`和`SelectMethod`指定属性。 但是，该向导自动填充具有更新和删除选项卡中的下拉列表`UpdateCategory`和`DeleteCategory`方法，分别。 这是因为在`CategoriesBLL`我们标记使用这些方法的类`DataObjectMethodAttribute`与更新和删除的默认方法。

现在，请设置为 （无） 的更新选项卡的下拉列表，但将删除选项卡的下拉列表设置为保持为`DeleteCategory`。 我们将返回到该向导将在步骤 6 中添加更新的支持。


[![配置对象数据源使用 DeleteCategory 方法](updating-and-deleting-existing-binary-data-cs/_static/image4.gif)](updating-and-deleting-existing-binary-data-cs/_static/image7.png)

**图 4**： 配置为使用 ObjectDataSource`DeleteCategory`方法 ([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image8.png))


> [!NOTE]
> 完成该向导，时 Visual Studio 可能会要求是否想要刷新字段和密钥，这将重新生成数据 Web 控件的字段。 因为选择是将覆盖可能已做的任何字段自定义，请选择否，。


ObjectDataSource 现在将包括的值及其`DeleteMethod`属性以及`DeleteParameter`。 回想一下，当使用向导指定的方法，Visual Studio 将设置 ObjectDataSource s`OldValuesParameterFormatString`属性设置为`original_{0}`，这会导致问题的更新和删除方法调用。 因此，完全清除此属性或其重置为默认情况下， `{0}`。 如果你需要刷新此对象数据源属性上的内存，请参阅[概述的插入、 更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程。

完成向导并修复后`OldValuesParameterFormatString`，ObjectDataSource s 声明性标记应类似如下所示：


[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample4.aspx)]

配置 ObjectDataSource 之后, 删除通过将功能添加到 GridView 从 GridView s 智能标记的启用删除复选框。 这将添加到 GridView 的 CommandField 其`ShowDeleteButton`属性设置为`true`。


[![在 GridView 中删除为启用支持](updating-and-deleting-existing-binary-data-cs/_static/image5.gif)](updating-and-deleting-existing-binary-data-cs/_static/image9.png)

**图 5**： 启用对 GridView 中删除的支持 ([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image10.png))


请花费片刻时间来测试删除功能。 没有间的外键`Products`表 s`CategoryID`并`Categories`表的`CategoryID`，因此如果尝试删除的任何前八个类别，你会收到外键约束冲突异常。 若要测试此功能扩展，添加新类别，提供的手册和图片。 图 6 所示我测试类别包括一个名为测试手册文件`Test.pdf`和测试图片。 图 7 显示了 GridView 后添加测试类别。


[![添加带有手册和图像的测试类别](updating-and-deleting-existing-binary-data-cs/_static/image6.gif)](updating-and-deleting-existing-binary-data-cs/_static/image11.png)

**图 6**： 添加一个带有手册和图像的测试类别 ([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image12.png))


[![插入后测试类别，它会显示在 GridView](updating-and-deleting-existing-binary-data-cs/_static/image7.gif)](updating-and-deleting-existing-binary-data-cs/_static/image13.png)

**图 7**： 插入后测试类别，它会显示在 GridView ([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image14.png))


在 Visual Studio 中，刷新解决方案资源管理器。 现在应看到新的文件中`~/Brochures`文件夹中， `Test.pdf` （请参阅图 8）。

接下来，单击测试类别行，从而导致要回发的页面中的删除链接并`CategoriesBLL`类的`DeleteCategory`方法来触发。 这将调用 DAL s`Delete`方法，使相应`DELETE`语句发送到数据库。 然后，重新将数据绑定到 GridView 和标记发送回客户端不再存在的测试类别。

删除工作流已成功删除从测试类别记录时`Categories`表中，未从 web 服务器的文件系统中删除其手册文件。 刷新解决方案资源管理器，然后，你将看到`Test.pdf`仍处于`~/Brochures`文件夹。


![未从 Web 服务器文件系统中删除 Test.pdf 文件](updating-and-deleting-existing-binary-data-cs/_static/image8.gif)

**图 8**:`Test.pdf`未从 Web 服务器的文件系统中删除文件


## <a name="step-5-removing-the-deleted-category-s-brochure-file"></a>步骤 5： 删除已删除的类别的手册文件

存储数据库外部的二进制数据的缺点之一是必须执行额外步骤以删除关联的数据库记录时清理这些文件。 GridView 和 ObjectDataSource 提供之前并执行删除命令后激发的事件。 我们实际上需要创建前和操作后事件的事件处理程序。 之前`Categories`删除记录，我们需要确定其 PDF 文件的路径，但我们不想删除 pdf 文件，然后在没有某种异常，并且不会删除该类别的情况下删除类别。

GridView s [ `RowDeleting`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx)触发调用 ObjectDataSource s delete 命令之前，尽管其[`RowDeleted`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleted.aspx)后会激发。 创建使用下面的代码这两个事件的事件处理程序：


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample5.cs)]

在中`RowDeleting`事件处理程序`CategoryID`的行在从 GridView s 获取正在删除`DataKeys`集合，可通过此事件处理程序中访问`e.Keys`集合。 下一步，`CategoriesBLL`类的`GetCategoryByCategoryID(categoryID)`调用以返回有关要删除的记录的信息。 如果返回`CategoriesDataRow`对象具有一个非`NULL``BrochurePath`值则存储在该页面变量`deletedCategorysPdfPath`，以便可以在删除该文件`RowDeleted`事件处理程序。

> [!NOTE]
> 而不是检索`BrochurePath`详细信息`Categories`记录中删除`RowDeleting`事件处理程序，我们可以或者添加`BrochurePath`到 GridView 的`DataKeyNames`属性和访问记录的值通过`e.Keys`集合。 执行此操作将稍有增加的 GridView 的视图状态大小，但会减少所需的代码和将行程保存到数据库。


ObjectDataSource 调用 s 基础 delete 命令，GridView s 后`RowDeleted`触发事件处理程序。 如果不没有删除数据中的任何异常，并且没有为`deletedCategorysPdfPath`，则从文件系统删除 pdf 文件。 请注意，不需要此额外代码以清理其图片与关联的类别 s 二进制数据。 该 s 由于图片数据存储直接在数据库中，因此删除`Categories`行也会删除该类别的图片数据。

添加后两个事件处理程序，再次运行此测试用例。 当删除该类别，也会删除其关联的 PDF。

更新现有的记录相关联的 s 二进制数据提供了一些有趣的挑战。 本教程的其余部分深入介绍将更新功能添加到的手册和图片。 步骤 6 探讨了步骤 7 所示在更新该图片的同时更新手册信息的方法。

## <a name="step-6-updating-a-category-s-brochure"></a>步骤 6： 更新类别的手册

如中所述[概述的插入、 更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程中，GridView 提供内置行级编辑支持，如果其基础数据源是可由一个复选框的计时周期实现适当地配置。 目前， `CategoriesDataSource` ObjectDataSource 尚未配置以包括更新的支持，因此让 s 添加，在。

单击 ObjectDataSource 的向导中的配置数据源链接并继续执行第二个步骤。 由于`DataObjectMethodAttribute`中使用`CategoriesBLL`，更新下拉列表应自动填充了`UpdateCategory`接受四个输入参数的重载 (所有列，但`Picture`)。 此更改，以便它使用带有五个参数的重载。


[![配置对象数据源使用 UpdateCategory 包含的方法的参数的图片](updating-and-deleting-existing-binary-data-cs/_static/image9.gif)](updating-and-deleting-existing-binary-data-cs/_static/image15.png)

**图 9**： 配置为使用 ObjectDataSource`UpdateCategory`包括的参数的方法`Picture`([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image16.png))


ObjectDataSource 现在将包括的值及其`UpdateMethod`属性以及对应`UpdateParameter`s。 步骤 4 中所述，Visual Studio 将设置 ObjectDataSource s`OldValuesParameterFormatString`属性设置为`original_{0}`时使用配置数据源向导。 这将导致问题的更新和删除方法调用。 因此，完全清除此属性或其重置为默认情况下， `{0}`。

完成向导并修复后`OldValuesParameterFormatString`，ObjectDataSource s 声明性标记应如下所示：


[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample6.aspx)]

若要打开 GridView s 内置编辑功能，请从 GridView s 智能标记启用编辑选项。 这会设置 CommandField s`ShowEditButton`属性设置为`true`，从而导致添加了编辑按钮 （和所编辑的行的更新和取消按钮）。


[![配置为支持编辑 GridView](updating-and-deleting-existing-binary-data-cs/_static/image10.gif)](updating-and-deleting-existing-binary-data-cs/_static/image17.png)

**图 10**： 配置为支持编辑 GridView ([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image18.png))


访问通过浏览器页面并单击其中一个行的编辑按钮。 `CategoryName`和`Description`BoundFields 呈现为文本框。 `BrochurePath` TemplateField 缺少`EditItemTemplate`，因此它将继续显示其`ItemTemplate`小册子中的链接。 `Picture` ImageField 呈现为文本框的`Text`属性分配值为 ImageField s`DataImageUrlField`值，在这种情况下`CategoryID`。


[![GridView 缺少 BrochurePath 编辑界面](updating-and-deleting-existing-binary-data-cs/_static/image11.gif)](updating-and-deleting-existing-binary-data-cs/_static/image19.png)

**图 11**: GridView 缺少的编辑界面`BrochurePath`([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image20.png))


## <a name="customizing-thebrochurepaths-editing-interface"></a>自定义`BrochurePath`s 编辑接口

我们需要创建的用于编辑界面`BrochurePath`TemplateField，允许用户为：

- 将保留为类别的手册-，
- 通过上传新的手册，更新分类的手册或
- （在类别不再具有关联的手册的情况下） 中完全删除分类的手册。

我们还需要更新`Picture`ImageField s 编辑界面，但我们会谈到这在步骤 7 中。

从 GridView s 智能标记，单击编辑模板链接并选择`BrochurePath`TemplateField 的`EditItemTemplate`从下拉列表。 将 RadioButtonList Web 控件添加到此模板中，设置其`ID`属性设置为`BrochureOptions`并将其`AutoPostBack`属性设置为`true`。 从属性窗口中，单击中的椭圆`Items`属性，这将显示`ListItem`集合编辑器。 添加具有以下三个选项`Value`的 1、 2 和 3，分别：

- 使用当前的手册
- 删除当前手册
- 上传新的手册

设置第一个`ListItem`s`Selected`属性设置为`true`。


![将三个 Listitem 添加到 RadioButtonList](updating-and-deleting-existing-binary-data-cs/_static/image12.gif)

**图 12**： 添加三个`ListItem`到 RadioButtonList


在 RadioButtonList，下面添加一个名为 FileUpload 控件`BrochureUpload`。 设置其`Visible`属性设置为`false`。


[![将 RadioButtonList 和 FileUpload 控件添加到 EditItemTemplate](updating-and-deleting-existing-binary-data-cs/_static/image13.gif)](updating-and-deleting-existing-binary-data-cs/_static/image21.png)

**图 13**： 添加 RadioButtonList 和 FileUpload 控件`EditItemTemplate`([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image22.png))


此 RadioButtonList 提供用户的三个选项。 其理念是仅当选择最后一个选项上, 传新小册子中，将显示 FileUpload 控件。 若要实现此目的，创建事件处理程序的 RadioButtonList s`SelectedIndexChanged`事件，并添加以下代码：


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample7.cs)]

由于 RadioButtonList 和 FileUpload 控件模板中，我们必须编写一些代码以编程方式访问这些控件。 `SelectedIndexChanged`事件处理程序传递的引用中 RadioButtonList`sender`输入的参数。 若要获取 FileUpload 控件，我们需要得到 RadioButtonList 的父控件，并且使用`FindControl("controlID")`从那里的方法。 FileUpload RadioButtonList 和 FileUpload 控件的引用后，控制 s`Visible`属性设置为`true`仅当 RadioButtonList s`SelectedValue`等于 3，这是`Value`有关上传新的手册`ListItem`.

利用此代码，请花费片刻时间来测试编辑界面。 单击编辑按钮的行。 最初，应选择当前使用的手册选项。 更改所选的索引会导致回发。 如果选择第三个选项，则显示 FileUpload 控件，否则其处于隐藏状态。 图 14 显示了编辑界面，首先单击编辑按钮; 时图 15 显示了界面后选择上传新手册选项。


[![最初，使用当前小册子中选择选项](updating-and-deleting-existing-binary-data-cs/_static/image14.gif)](updating-and-deleting-existing-binary-data-cs/_static/image23.png)

**图 14**： 最初，使用当前小册子中选择选项 ([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image24.png))


[![选择此选项可以显示在上传新小册子 FileUpload 控件](updating-and-deleting-existing-binary-data-cs/_static/image15.gif)](updating-and-deleting-existing-binary-data-cs/_static/image25.png)

**图 15**： 选择此选项可以显示在上传新小册子 FileUpload 控件 ([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image26.png))


## <a name="saving-the-brochure-file-and-updating-thebrochurepathcolumn"></a>正在保存手册文件和更新`BrochurePath`列

单击 GridView s 更新按钮时，其`RowUpdating`事件触发。 ObjectDataSource 调用 s 更新命令，然后 GridView 的`RowUpdated`事件触发。 像与删除的工作流，我们需要为这两种事件创建事件处理程序。 在中`RowUpdating`事件处理程序，我们需要确定要执行的操作根据`SelectedValue`的`BrochureOptions`RadioButtonList:

- 如果`SelectedValue`为 1，我们想要继续使用相同`BrochurePath`设置。 因此，我们需要设置 ObjectDataSource s`brochurePath`到现有的参数`BrochurePath`要更新的记录的值。 ObjectDataSource s`brochurePath`参数可以设置使用`e.NewValues["brochurePath"] = value`。
- 如果`SelectedValue`为 2，则我们想要设置的记录 s`BrochurePath`值设为`NULL`。 这可以通过设置 ObjectDataSource s 来实现`brochurePath`参数`Nothing`，这会导致数据库`NULL`中正在使用`UPDATE`语句。 如果没有要删除的现有手册文件，我们需要删除现有文件。 但是，我们只想要执行此操作，如果在更新完成并且不会引发异常。
- 如果`SelectedValue`为 3，则我们想要确保用户已经上传的 PDF 文件然后将其保存到文件系统并更新记录的`BrochurePath`列的值。 此外，如果要替换的现有手册文件，我们需要删除以前的文件。 但是，我们只想要执行此操作，如果在更新完成并且不会引发异常。

当完成所需的步骤 RadioButtonList s`SelectedValue`是 3 个几乎完全相同，到使用的 DetailsView 的`ItemInserting`事件处理程序。 在 DetailsView 控件中添加之间添加新类别记录时执行此事件处理程序[前一篇教程](including-a-file-upload-option-when-adding-a-new-record-cs.md)。 因此，它理应我们可以重构为单独的方法扩展此功能。 具体而言，我移出的常见功能为两个方法：

- `ProcessBrochureUpload(FileUpload, out bool)` FileUpload 控件实例和一个输出布尔值，指定是否在删除或编辑操作应继续执行或不应由于一些验证错误将其取消，则接受作为输入。 此方法返回的已保存文件的路径或`null`如果没有文件已保存。
- `DeleteRememberedBrochurePath` 删除指定的页面变量中路径的文件`deletedCategorysPdfPath`如果`deletedCategorysPdfPath`不是`null`。

这两种方法的代码如下所示。 请注意之间的相似性`ProcessBrochureUpload`和 DetailsView 的`ItemInserting`上一教程中的事件处理程序。 在本教程中，我已更新 DetailsView 的事件处理程序以使用这些新方法。 下载与本教程，若要查看对 DetailsView 的事件处理程序的修改关联的代码。


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample8.cs)]

GridView s`RowUpdating`并`RowUpdated`事件处理程序用`ProcessBrochureUpload`和`DeleteRememberedBrochurePath`方法，如以下代码所示：


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample9.cs)]

请注意如何`RowUpdating`事件处理程序使用一系列条件语句以执行相应的操作根据`BrochureOptions`RadioButtonList 的`SelectedValue`属性值。

使用此代码，可以编辑类别，并让它使用其当前手册、 不使用任何手册或上传新。 请继续并试用。在中设置断点`RowUpdating`和`RowUpdated`事件处理程序，了解工作流。

## <a name="step-7-uploading-a-new-picture"></a>步骤 7： 上传新的图片

`Picture` ImageField s 编辑接口呈现为文本框中的值填充其`DataImageUrlField`属性。 在编辑工作流，GridView 将参数传递给参数名称为 s ObjectDataSource ImageField s 的值`DataImageUrlField`属性和参数 s 值的文本框中编辑界面中输入的值。 图像另存为文件系统上的文件时，此行为是适合和`DataImageUrlField`包含图像的完整 URL。 使用这种情况下，编辑界面在文本框中，用户可以更改并保存回数据库中显示的图像的 URL。 当然，此默认接口不允许用户上传新映像，但它确实允许它们将从当前值的图像的 URL 更改为另一个。 对于本教程，但是，编辑界面 ImageField 的默认不满足需要因为`Picture`直接在数据库中存储二进制数据并`DataImageUrlField`属性包含只`CategoryID`。

若要更好地了解发生在我们的教程用户编辑 ImageField 具有的行时，请考虑下面的示例： 用户编辑具有的行`CategoryID`10，从而导致`Picture`ImageField 呈现为文本框值为 10。 假设用户在此文本框中的值更改为 50，并单击更新按钮。 产生的回发和 GridView 最初创建一个名为参数`CategoryID`值 50。 但是，GridView 发送此参数之前 (和`CategoryName`并`Description`参数)，它将从值中添加`DataKeys`集合。 因此，它将覆盖`CategoryID`参数与当前行 s 基础`CategoryID`值 10。 简单地说，编辑界面 ImageField s 产生任何影响编辑工作流上为本教程因为名称 ImageField s`DataImageUrlField`属性和网格的`DataKey`值是否相同。

尽管 ImageField 使得变得更容易地显示基于数据库数据的映像，我们不想要提供一个文本框中编辑界面。 相反，我们想要提供 FileUpload 控件，最终用户可以用于更改类别的图片。 与不同`BrochurePath`值，这些教程中我们已决定要求每个类别，必须具有一个图片。 因此，我们不需要允许用户指示，没有任何关联的图片用户可能会将.vhd 文件的新图片或保留当前的图片作为-是。

若要自定义 ImageField s 编辑界面，我们需要将其转换为 TemplateField。 从 GridView s 智能标记，单击编辑列链接选择 ImageField，并单击转换此字段转换为 TemplateField 链接。


![ImageField 转换为 TemplateField](updating-and-deleting-existing-binary-data-cs/_static/image16.gif)

**图 16**: ImageField 转换为 TemplateField


ImageField 转换为 TemplateField 以这种方式生成 TemplateField 与两个模板。 如下面的声明性语法所示，`ItemTemplate`包含图像 Web 控件`ImageUrl`属性分配使用数据绑定语法基于 ImageField s`DataImageUrlField`和`DataImageUrlFormatString`属性。 `EditItemTemplate`包含一个文本框其`Text`属性绑定到指定的值`DataImageUrlField`属性。


[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample10.aspx)]

我们需要更新`EditItemTemplate`使用 FileUpload 控件。 从 GridView s 智能标记单击编辑模板链接，然后选择`Picture`TemplateField 的`EditItemTemplate`从下拉列表。 在模板中应看到此项中删除一个文本框。 接下来，将 FileUpload 控件从工具箱拖到该模板后，设置其`ID`到`PictureUpload`。 此外添加文本以更改类别的图片，请指定新图片。 若要保留相同类别的图片，字段留空模板。


[![向 EditItemTemplate 添加 FileUpload 控件](updating-and-deleting-existing-binary-data-cs/_static/image17.gif)](updating-and-deleting-existing-binary-data-cs/_static/image27.png)

**图 17**： 添加到 FileUpload 控件`EditItemTemplate`([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image28.png))


自定义后编辑界面，在浏览器中查看进度。 查看时行在只读模式下，类别的图像显示之前，但单击编辑按钮将图片列呈现为与 FileUpload 控件的文本。


[![编辑界面包括 FileUpload 控件](updating-and-deleting-existing-binary-data-cs/_static/image18.gif)](updating-and-deleting-existing-binary-data-cs/_static/image29.png)

**图 18**： 编辑界面包括 FileUpload 控件 ([单击以查看实际尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image30.png))


回想一下对象数据源配置为调用`CategoriesBLL`类 s`UpdateCategory`接受作为输入的图片作为二进制数据的方法`byte`数组。 此数组是否`null`值，但是，备用`UpdateCategory`调用重载，哪些问题`UPDATE`不会修改的 SQL 语句`Picture`列，从而使类别 s 当前图片不变。 因此，在 GridView s`RowUpdating`事件处理程序，我们需要以编程方式引用`PictureUpload`FileUpload 控件并确定文件已上传。 如果其中一个未上载，那么我们要做*不*想要为指定值`picture`参数。 另一方面，如果文件已上传中`PictureUpload`FileUpload 控件中，我们想要确保它是一个 JPG 文件。 如果是，则我们可以将其二进制内容发送到通过 ObjectDataSource`picture`参数。

像在步骤 6 中使用的代码，与很多已此处所需的代码存在于 DetailsView 的`ItemInserting`事件处理程序。 因此，我已将常见功能重构为新方法`ValidPictureUpload`，并更新`ItemInserting`事件处理程序以使用此方法。

将以下代码添加到 GridView 的开头`RowUpdating`事件处理程序。 它非常重要的是此代码将放在之前的代码，因为我们不会将手册文件保存想要保存到 web 服务器的文件系统的手册，如果无效的图片文件上传。


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample11.cs)]

`ValidPictureUpload(FileUpload)`方法使用 FileUpload 控件作为其唯一的输入参数中，并检查以确保上传的文件是 JPG s 上传的文件扩展名; 如果上传图片文件，则仅调用。 如果不上载任何文件，则图片参数未设置属性，并因此使用其默认值为`null`。 如果已上传图片并`ValidPictureUpload`返回`true`，则`picture`参数分配的二进制数据的上传的映像; 如果该方法返回`false`、 已取消更新工作流和事件处理程序已退出。

`ValidPictureUpload(FileUpload)`方法代码，从 DetailsView s 重构`ItemInserting`事件处理程序遵循：


[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample12.cs)]

## <a name="step-8-replacing-the-original-categories-pictures-with-jpgs"></a>步骤 8： 替换 JPGs 原始类别图片

请记住，原始的八个类别图片包装在 OLE 标头的位图文件。 现在，我们已添加的功能，若要编辑现有记录的图片，请花费片刻时间使用 Jpg 替换这些位图。 如果你想要继续使用当前类别图片，可以直接将它们转换为 Jpg，通过执行以下步骤：

1. 将位图图像保存到您的硬盘。 请访问`UpdatingAndDeleting.aspx`在浏览器中和前八个类别的每个页上，右键单击该图像，选择要保存此图片。
2. 在所选图像编辑器中打开该映像。 可以使用 Microsoft 画图，例如。
3. 将位图另存为 JPG 图像。
4. 更新通过使用 JPG 文件的编辑界面的类别的图片。

后编辑某个类别并上传 JPG 图像，图像将不会呈现在浏览器中因为`DisplayCategoryPicture.aspx`页去除的前八个类别的图片中的第一个 78 字节。 通过删除 OLE 标头剥离执行的代码来解决此问题。 执行此操作，操作之后`DisplayCategoryPicture.aspx``Page_Load`事件处理程序应具有只会将以下代码：


[!code-vb[Main](updating-and-deleting-existing-binary-data-cs/samples/sample13.vb)]

> [!NOTE]
> `UpdatingAndDeleting.aspx`页 s 插入和编辑接口可以使用多做一些工作。 `CategoryName`和`Description`BoundFields DetailsView 和 GridView 中的应转换为 Templatefield。 由于`CategoryName`不允许`NULL`值，应添加一个 RequiredFieldValidator。 和`Description`文本框可能应转换为多行文本框。 我为您作为练习保留这些完成收尾工作了。


## <a name="summary"></a>总结

本教程中完成我们了解了如何对二进制数据。 在本教程和以前的三个，我们了解了如何二进制数据可以存储在文件系统上或直接在数据库中。 用户从他们的硬盘中选择一个文件并将其上载到 web 服务器，其中可以存储在文件系统或插入到数据库通过提供到系统的二进制数据。 ASP.NET 2.0 包括可以提供此类接口一样简单的拖放的 FileUpload 控件。 但是，如中所述[将文件上载](uploading-files-cs.md)教程中，FileUpload 控件才适合相对较小的文件上传，理想情况下不超过一兆字节。 我们还探讨了如何将上传的数据与基础数据模型中，相关联，以及如何编辑和删除现有记录中的二进制数据。

我们接下来的教程探讨了各种缓存技术。 缓存提供了一种改进应用程序 s 成本高昂的操作的结果并将其存储在可更快地访问的位置的整体性能。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](including-a-file-upload-option-when-adding-a-new-record-cs.md)
> [下一页](uploading-files-vb.md)
