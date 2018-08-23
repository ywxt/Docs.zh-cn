---
uid: web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
title: 添加新记录 (C#) 时包括的文件上传选项 |Microsoft Docs
author: rick-anderson
description: 本教程演示如何创建一个 Web 界面，允许用户输入的文本数据的同时上传二进制文件。 为了说明选项可用 t...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 362ade25-3965-4fb2-88d2-835c4786244f
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
msc.type: authoredcontent
ms.openlocfilehash: c3887f920126d70b300de5a0d6e09474fd33c332
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834244"
---
<a name="including-a-file-upload-option-when-adding-a-new-record-c"></a>添加新记录 (C#) 时包括文件上传选项
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_56_CS.exe)或[下载 PDF](including-a-file-upload-option-when-adding-a-new-record-cs/_static/datatutorial56cs1.pdf)

> 本教程演示如何创建一个 Web 界面，允许用户输入的文本数据的同时上传二进制文件。 为了说明可用于存储二进制数据的选项，一个文件将保存在数据库中的其他存储在文件系统中时。


## <a name="introduction"></a>介绍

在前面的两个教程中我们探讨了用于存储应用程序的数据模型，介绍了如何使用 FileUpload 控件将文件从客户端发送到 web 服务器，并已了解如何在数据 W 中显示此二进制数据与关联的二进制数据的技术eb 控件。 我们还将讨论如何上传的数据将与相关联的数据模型，但 ve。

在本教程中我们将创建 web 页面以添加新类别。 除了为类别的名称和说明文本框中，此页将需要包含两个 FileUpload 控件中的新类别的图片的一个，另一个用于手册。 将直接在新的记录中存储已上传的图片`Picture`列中，而手册将保存到`~/Brochures`替换为保存新记录 s 中的文件的路径的文件夹`BrochurePath`列。

然后再创建此新的 web 页面，我们将需要更新体系结构。 `CategoriesTableAdapter` S 主查询不会检索`Picture`列。 因此，自动生成`Insert`方法仅有的输入`CategoryName`， `Description`，和`BrochurePath`字段。 因此，我们需要在所有四个提示的 TableAdapter 中创建的其他方法`Categories`字段。 `CategoriesBLL`业务逻辑层中的类还需要进行更新。

## <a name="step-1-adding-aninsertwithpicturemethod-to-thecategoriestableadapter"></a>步骤 1： 添加`InsertWithPicture`方法`CategoriesTableAdapter`

当我们创建了`CategoriesTableAdapter`回到[创建数据访问层](../introduction/creating-a-data-access-layer-cs.md)教程中，我们将其配置为自动生成`INSERT`， `UPDATE`，并`DELETE`语句基于主查询。 此外，我们指示 TableAdapter 以使用 DB 直接的方法，创建方法`Insert`， `Update`，和`Delete`。 这些方法来执行自动生成`INSERT`， `UPDATE`，和`DELETE`语句，因此，接受基于主查询所返回的列的输入的参数。 在中[将文件上载](uploading-files-cs.md)教程中我们增加`CategoriesTableAdapter`s 若要使用的主查询`BrochurePath`列。

由于`CategoriesTableAdapter`s 主查询未引用`Picture`列中，我们不能添加新记录或使用的值更新现有记录`Picture`列。 为了捕获此信息，我们可以创建一个新方法中专门用于插入具有二进制数据的记录的 TableAdapter，或者我们可以自定义自动生成`INSERT`语句。 自定义自动生成的问题`INSERT`语句是，我们会冒着覆盖由向导我们自定义项。 例如，假设我们自定义`INSERT`语句以包括使用`Picture`列。 这将更新的 TableAdapter s`Insert`方法以包括其他类别的图片 s 二进制数据的输入的参数。 我们然后可以在业务逻辑层，若要使用此 DAL 方法并调用此 BLL 方法通过表示层中创建一个方法和所有内容将运行非常好。 也就是说下, 一次之前我们配置了通过 TableAdapter 配置向导 TableAdapter。 此向导完成，我们的自定义设置时，就立即`INSERT`语句将被覆盖，`Insert`方法将恢复为原来的形式，和我们的代码将无法再编译 ！

> [!NOTE]
> 使用存储的过程而不临时 SQL 语句时，此麻烦是不产生问题。 以后的教程将探讨在数据访问层中使用而不是临时 SQL 语句的存储的过程。


若要避免这种可能性难题，而不是自定义自动生成 SQL 语句，请让 s 改为创建 TableAdapter 的新方法。 此方法，名为`InsertWithPicture`，将接受的值`CategoryName`， `Description`， `BrochurePath`，并`Picture`列并执行`INSERT`将所有四个值存储在一条新记录中的语句。

打开类型化数据集，并从设计器中，右键单击`CategoriesTableAdapter`s 标头，然后从上下文菜单中选择添加查询。 这将启动 TableAdapter 查询配置向导的说明进行操作，它首先会询问我们 TableAdapter 查询应如何访问数据库。 选择使用 SQL 语句，然后单击下一步。 下一步会提示为查询的类型生成。 由于我们重新创建要添加到新的记录的查询`Categories`表中，选择 INSERT 并单击下一步。


[![选择插入选项](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.png)

**图 1**： 选择插入选项 ([单击以查看实际尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.png))


现在，我们需要指定`INSERT`SQL 语句。 该向导会自动建议`INSERT`对应于 TableAdapter s 主查询的语句。 在这种情况下，它 s`INSERT`语句将插入`CategoryName`， `Description`，和`BrochurePath`值。 Update 语句，以便`Picture`列则包含与`@Picture`参数，如下所示：


[!code-sql[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample1.sql)]

在向导的最后一个屏幕询问我们要将新的 TableAdapter 方法。 输入`InsertWithPicture`并单击完成。


[![命名新的 TableAdapter 方法 InsertWithPicture](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.png)

**图 2**： 新的 TableAdapter 方法命名`InsertWithPicture`([单击以查看实际尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.png))


## <a name="step-2-updating-the-business-logic-layer"></a>步骤 2： 更新业务逻辑层

由于表示层只应与业务逻辑层进行交互，而不是我们跳过它来直接转到数据访问层，需要创建调用 DAL 方法我们刚刚创建的 BLL 方法 (`InsertWithPicture`)。 对于本教程中，创建中的方法`CategoriesBLL`名为类`InsertWithPicture`接受作为输入的三`string`s 和`byte`数组。 `string`输入的参数仅适用于 s 类别名称、 说明和手册文件路径，而`byte`数组是类别的图片的二进制内容。 如以下代码所示，此 BLL 方法将调用相应的 DAL 方法：


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample2.cs)]

> [!NOTE]
> 请确保你已添加之前保存类型化数据集`InsertWithPicture`向 BLL 方法。 由于`CategoriesTableAdapter`类的代码是自动生成基于类型化数据集，如果 don t 首先将所做的更改保存到类型化数据集`Adapter`赢得 t 属性了解`InsertWithPicture`方法。


## <a name="step-3-listing-the-existing-categories-and-their-binary-data"></a>步骤 3： 列出现有的类别和二进制数据

在本教程中我们将创建一个页面，让最终用户能够将新类别添加到系统中，为新类别提供的图片和手册。 在中[前面的教程](displaying-binary-data-in-the-data-web-controls-cs.md)我们用于 GridView 使用 templatefield 进一步和 ImageField 显示每个类别的名称，说明、 图片和链接以下载其手册。 让我们来为本教程中，创建一个页面，同时列出了所有现有的类别，并允许创建新的复制该功能。

首先打开`DisplayOrDownload.aspx`页上从`BinaryData`文件夹。 请转到源视图并将复制的 GridView 和 ObjectDataSource s 声明性语法，将其中粘贴`<asp:Content>`中的元素`UploadInDetailsView.aspx`。 此外，不要忘了将复制`GenerateBrochureLink`中的代码隐藏类方法`DisplayOrDownload.aspx`到`UploadInDetailsView.aspx`。


[![复制并粘贴到 UploadInDetailsView.aspx 从 DisplayOrDownload.aspx 的声明性语法](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.png)

**图 3**： 复制并粘贴从声明性语法`DisplayOrDownload.aspx`到`UploadInDetailsView.aspx`([单击以查看实际尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.png))


复制的声明性语法后并`GenerateBrochureLink`方法转移到`UploadInDetailsView.aspx`页上，查看该网页通过浏览器以确保所有内容已通过正确复制。 应会看到列出的八个类别一个 GridView，包括用于下载手册，以及类别的图片的链接。


[![现在应看到每个类别以及其二进制数据](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.png)

**图 4**： 您应现在请参阅每个类别沿其二进制数据 ([单击以查看实际尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.png))


## <a name="step-4-configuring-thecategoriesdatasourceto-support-inserting"></a>步骤 4： 配置`CategoriesDataSource`支持插入

`CategoriesDataSource` ObjectDataSource 使用`Categories`GridView 当前不提供插入数据的能力。 为了支持此数据源控件通过插入，我们需要映射其`Insert`其基础对象中的方法的方法`CategoriesBLL`。 具体而言，我们想要将其映射到`CategoriesBLL`方法返回在步骤 2 中，我们添加了`InsertWithPicture`。

通过单击 ObjectDataSource s 智能标记中的配置数据源链接启动。 第一个屏幕显示数据源配置为使用，该对象`CategoriesBLL`。 保留此设置为-转到定义数据方法屏幕旁边单击。 将移动到插入选项卡并选择`InsertWithPicture`从下拉列表的方法。 单击完成以完成向导。


[![配置对象数据源使用 InsertWithPicture 方法](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.png)

**图 5**： 配置要使用 ObjectDataSource`InsertWithPicture`方法 ([单击以查看实际尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.png))


> [!NOTE]
> 完成该向导，时 Visual Studio 可能会要求是否想要刷新字段和密钥，这将重新生成数据 Web 控件的字段。 因为选择是将覆盖可能已做的任何字段自定义，请选择否，。


完成向导后，ObjectDataSource 现在将包括的值及其`InsertMethod`属性，以及`InsertParameters`对于四个类别列中，如下面的声明性标记所阐释：


[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample3.aspx)]

## <a name="step-5-creating-the-inserting-interface"></a>步骤 5： 创建插入接口

首次详见[概述的插入、 更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)，DetailsView 控件提供了使用支持插入的数据源控件时，可以利用内置插入接口。 让我们来将 DetailsView 控件添加到此页面上方 GridView 永久呈现其插入的界面，允许用户快速添加新的类别。 在 DetailsView 中添加新类别，在其下的 GridView 将自动刷新并显示新类别。

通过从工具箱拖到上面 GridView 中，设置设计器中拖动 DetailsView 开始其`ID`属性设置为`NewCategory`和清除`Height`和`Width`属性值。 从 DetailsView s 智能标记，请将其绑定到现有`CategoriesDataSource`，然后选中启用插入复选框。


[![将 DetailsView 绑定到 CategoriesDataSource 并启用插入](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.png)

**图 6**： 将绑定到 DetailsView`CategoriesDataSource`和启用插入 ([单击以查看实际尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image12.png))


若要永久呈现在其插入界面中的 DetailsView，设置其`DefaultMode`属性设置为`Insert`。

请注意，DetailsView 有五个 BoundFields `CategoryID`， `CategoryName`， `Description`， `NumberOfProducts`，并`BrochurePath`尽管`CategoryID`BoundField 插入界面中不进行呈现，因为其`InsertVisible`属性设置为`false`。 因为它们是返回的列，这些 BoundFields 存在`GetCategories()`方法，即 ObjectDataSource 调用以检索其数据。 用于插入，但是，我们不想让用户指定的值`NumberOfProducts`。 此外，我们需要以允许它们上传为新类别的图片，以及上传手册的 PDF。

删除`NumberOfProducts`DetailsView 中完全，然后更新从 BoundField`HeaderText`的属性`CategoryName`和`BrochurePath`BoundFields 类别和手册，分别。 接下来，将转换`BrochurePath`转换为 TemplateField BoundField 和添加新的图片，TemplateField 提供此新 TemplateField`HeaderText`图片的值。 移动`Picture`TemplateField 使之之间`BrochurePath`TemplateField 和 CommandField。


![将 DetailsView 绑定到 CategoriesDataSource 并启用插入](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.gif)

**图 7**： 将绑定到 DetailsView`CategoriesDataSource`并启用插入


如果你转换`BrochurePath`转换为通过编辑字段对话框中的 TemplateField BoundField TemplateField 包括`ItemTemplate`， `EditItemTemplate`，和`InsertItemTemplate`。 仅`InsertItemTemplate`是需要但是，因此可以删除其他两个模板。 此时您 DetailsView s 声明性语法应如下所示：


[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample4.aspx)]

## <a name="adding-fileupload-controls-for-the-brochure-and-picture-fields"></a>添加 FileUpload 控件的手册和图片字段

目前， `BrochurePath` TemplateField s`InsertItemTemplate`包含一个文本框，虽然`Picture`TemplateField 不包含任何模板。 我们需要更新这些两个 TemplateField 的`InsertItemTemplate`以使用 FileUpload 控件。

从 DetailsView s 智能标记，选择编辑模板选项，然后选择`BrochurePath`TemplateField 的`InsertItemTemplate`从下拉列表。 删除文本框，然后将 FileUpload 控件从工具箱拖到模板。 设置 FileUpload 控件 s`ID`到`BrochureUpload`。 同样，添加到 FileUpload 控件`Picture`TemplateField 的`InsertItemTemplate`。 设置此 FileUpload 控件 s`ID`到`PictureUpload`。


[![向 InsertItemTemplate 添加 FileUpload 控件](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image13.png)

**图 8**： 添加到 FileUpload 控件`InsertItemTemplate`([单击以查看实际尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image14.png))


这些新增功能后，将为两个 TemplateField s 声明性语法：


[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample5.aspx)]

当用户将添加新类别时，我们想要确保的手册和图片的正确的文件类型。 对于小册子中，用户必须提供 PDF。 图中，我们需要用户上传图像文件，但我们允许*任何*图像文件或仅的特定类型，例如 Gif 或 Jpg 图像文件？ 若要允许不同的文件类型，d 需要扩展`Categories`架构以包括捕获的文件类型，以便可以向客户端通过发送此类型的列`Response.ContentType`中`DisplayCategoryPicture.aspx`。 由于我们不具有这样的列，它会是比较明智的做法将用户限制为仅提供特定的图像文件类型。 `Categories`表 s 现有映像是位图，但 Jpg 图像通过 web 提供服务的更合适文件格式。

如果用户上载不正确的文件类型时，我们需要可取消插入并显示一条消息，指示该问题。 添加下 DetailsView 标签 Web 控件。 设置其`ID`属性设置为`UploadWarning`，清除出其`Text`属性，则设置`CssClass`属性设置为警告，并`Visible`并`EnableViewState`属性设置为`false`。 `Warning` CSS 类中定义`Styles.css`并呈现大型、 红色、 斜体、 粗体的字体的文本。

> [!NOTE]
> 理想情况下，`CategoryName`和`Description`BoundFields 将被转换为 Templatefield 和自定义其插入接口。 `Description`插入接口，例如，可能可以更好地通过多行文本框。 和以来`CategoryName`列不接受`NULL`值，应添加一个 RequiredFieldValidator 以确保用户提供新的类别的名称的值。 这些步骤是留给大家练练手读取器。 回头[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)有关扩充数据修改界面的深入探讨。


## <a name="step-6-saving-the-uploaded-brochure-to-the-web-server-s-file-system"></a>步骤 6： 将上传的手册保存到 Web 服务器文件系统

当用户输入值的新类别，并单击插入按钮时，产生的回发和插入工作流展开。 首先，DetailsView s [ `ItemInserting`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserting.aspx)激发。 下一步，ObjectDataSource s`Insert()`调用方法时，这会导致新记录添加到`Categories`表。 此后，DetailsView s [ `ItemInserted`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserted.aspx)激发。

之前的 ObjectDataSource s`Insert()`调用方法，我们必须首先确保用户已上载适当的文件类型，然后将 PDF 小册子保存到 web 服务器的文件系统。 创建事件处理程序的 DetailsView s`ItemInserting`事件，并添加以下代码：


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample6.cs)]

事件处理程序以引用`BrochureUpload`FileUpload 控件的 DetailsView s 模板。 然后，如果已上传手册上, 传的文件的扩展检查。 如果扩展不是。显示 PDF，然后警告、 取消了插入，则和事件处理程序的执行结束。

> [!NOTE]
> 依赖于上传的文件的扩展不是一种确保上传的文件一个 PDF 文档的攻击性方法。 用户可能具有有效的 PDF 文档扩展名`.Brochure`，或无法拍摄非 PDF 文档并提供其`.pdf`扩展。 文件 s 二进制内容需要以编程方式进行检查以便更最终验证的文件类型。 这种全面的方法，不过，不是通常过于复杂了;检查扩展是足以满足大多数方案。


如中所述[将文件上载](uploading-files-cs.md)教程中，因此，一个用户 s 上传不会覆盖另一个 s，保存文件到文件系统时必须小心。 对于本教程中我们将尝试使用相同的名称作为上传的文件。 如果已存在的文件中`~/Brochures`同名目录的文件，但是，我们将追加一个数字末尾直到找到一个唯一的名称。 例如，如果用户将一个名为的手册文件上传`Meats.pdf`，但已存在名为的文件`Meats.pdf`中`~/Brochures`文件夹中，我们将更改保存到的文件名`Meats-1.pdf`。 如果存在，我们将尝试`Meats-2.pdf`，依此类推，直到找到唯一的文件名。

下面的代码使用[`File.Exists(path)`方法](https://msdn.microsoft.com/library/system.io.file.exists.aspx)来确定文件是否已存在具有指定的文件名称。 如果是这样，系统会继续尝试小册子中的新文件名称，直到找到不会发生冲突。


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample7.cs)]

一旦已找到有效的文件名，需要该文件保存到文件系统和 ObjectDataSource 的`brochurePath``InsertParameter`值需要进行更新，以便此文件的名称写入到数据库。 返回中可以看到*将文件上载*教程中，保存该文件可以使用 FileUpload 控件的`SaveAs(path)`方法。 若要更新的 ObjectDataSource s`brochurePath`参数，请使用`e.Values`集合。


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample8.cs)]

## <a name="step-7-saving-the-uploaded-picture-to-the-database"></a>步骤 7： 将上传的图片保存到数据库

若要在新存储已上传的图片`Categories`记录，我们需要将已上传二进制内容分配到 ObjectDataSource s `picture` DetailsView s 中的参数`ItemInserting`事件。 我们执行此分配之前，但是，我们需要首先确保已上传的图片是不某些其他图像类型和 JPG。 如步骤 6 所示让我们来使用已上传的图片的文件扩展名来确定其类型。

虽然`Categories`table 允许`NULL`值`Picture`列，当前所有类别都有一个图片。 让我们来强制用户在添加新的类别，通过此页面时提供图片。 下面的代码检查以确保已上传图片，并且具有相应的扩展。


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample9.cs)]

此代码应置于*之前*步骤 6 中的代码，以便如果与图片上传问题，事件处理程序将终止之前手册文件保存到文件系统。

假设已上载相应文件，将已上传二进制内容分配到图片参数的值与以下代码行：


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample10.cs)]

## <a name="the-completeiteminsertingevent-handler"></a>完整`ItemInserting`事件处理程序

为了保持完整性，下面是`ItemInserting`完整的事件处理程序：


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample11.cs)]

## <a name="step-8-fixing-thedisplaycategorypictureaspxpage"></a>步骤 8： 修复`DisplayCategoryPicture.aspx`页

允许 s 请花费片刻时间来测试出插入接口和`ItemInserting`在最近几个步骤创建的事件处理程序。 请访问`UploadInDetailsView.aspx`页上通过浏览器并尝试添加一个类别，但要忽略该图片，或者指定非 JPG 图片或非 PDF 小册子。 在任何这些情况下，将显示一条错误消息，插入工作流被取消。


[![一条警告消息是显示如果上传文件类型无效](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image15.png)

**图 9**: 警告消息是显示如果上传无效的文件类型 ([单击以查看实际尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image16.png))


一次您已验证的页面要求图片要上传和获胜的 t 接受非 PDF 或非 JPG 文件，添加具有有效的 JPG 图片的新类别将手册字段留空。 单击插入按钮后，页面将回发，一条新记录将添加到`Categories`表直接在数据库中存储的已上载的图像 s 二进制内容。 GridView 更新，并显示新添加的类别中，对应的行，但如图 10 所示，新类别的图片未正确呈现。


[![新的类别不显示图片的 s](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image17.png)

**图 10**： 不显示图片的新类别 s ([单击以查看实际尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image18.png))


不显示新图片的原因在于`DisplayCategoryPicture.aspx`返回指定的类别的图片的页被配置为处理具有 OLE 标头的位图。 从去除此 78 字节的标头`Picture`列 s 二进制内容之前发送回客户端。 但只需上传新类别的 JPG 文件不具有此 OLE 标头中;因此，有效的、 需要字节正在删除从图像 s 二进制数据。

由于现在有两个 OLE 标头和 Jpg 中的位图`Categories`表中，我们需要更新`DisplayCategoryPicture.aspx`，以便其不去除原始八个类别的 OLE 标头，绕过此最小化的较新类别的记录。 在我们的下一教程，我们将介绍如何更新现有记录的映像，以及我们将更新的所有旧类别图片以便 Jpg。 现在，不过，使用下面的代码`DisplayCategoryPicture.aspx`以仅为这些原始的八个类别的 OLE 标头：


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample12.cs)]

进行此更改后，JPG 图像现在能够正确 GridView 中显示。


[![新的类别的 JPG 图像是正确呈现](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image19.png)

**图 11**： 新的类别的 JPG 图像会正确呈现 ([单击以查看实际尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image20.png))


## <a name="step-9-deleting-the-brochure-in-the-face-of-an-exception"></a>步骤 9： 删除在遇到异常时手册

Web 服务器文件系统上存储二进制数据的挑战之一是它引入了数据模型，其二进制数据之间的连接断开。 因此，只要删除了记录，必须还删除在文件系统上的相应二进制数据。 这可以派上用场插入，以及时。 请考虑以下方案： 用户将添加一个新类别，指定有效的图片和手册。 单击插入按钮，产生的回发和 DetailsView 的`ItemInserting`事件触发时，将手册保存到 web 服务器的文件系统。 下一步，ObjectDataSource s`Insert()`调用方法时，它调用`CategoriesBLL`类 s`InsertWithPicture`方法，后者调用`CategoriesTableAdapter`s`InsertWithPicture`方法。

现在，如果数据库处于脱机状态，会发生什么情况或是否在错误`INSERT`SQL 语句？ 清楚地插入将失败，因此没有新的类别行将添加到数据库。 但我们仍保留在 web 服务器文件系统上的已上传的手册文件 ！ 此文件需要面对插入工作流过程中出现异常时删除。

中所述以前[处理 BLL-和 DAL 级别 ASP.NET 页面中的异常](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)教程中，在各层通过弹出的体系结构的深度中从引发异常。 在表示层中，我们可以确定是否从 DetailsView s 发生了异常`ItemInserted`事件。 此事件处理程序还提供了 ObjectDataSource s 的值`InsertParameters`。 因此，我们可以创建的事件处理程序`ItemInserted`事件检查是否出现异常，如果是这样，删除由 ObjectDataSource s 指定的文件`brochurePath`参数：


[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample13.cs)]

## <a name="summary"></a>总结

有多个必须提供一个基于 web 的界面，用于添加包括二进制数据的记录执行的步骤。 如果直接到数据库中存储二进制数据，很可能你将需要更新体系结构中，添加特定的方法以处理插入二进制数据的情况。 一旦更新体系结构下, 一步创建的插入接口，可使用自定义以包括二进制数据的每个字段的 FileUpload 控件的 DetailsView 来完成。 上传的数据然后可以保存到 web 服务器的文件系统或分配给 DetailsView s 中的数据源参数`ItemInserting`事件处理程序。

将二进制数据保存到文件系统需要比将数据保存到数据库直接更多的规划。 为了避免覆盖另一个 s 的一个用户 s 上传，必须选择命名方案。 此外，必须采取额外步骤来删除已上传的文件，如果数据库插入失败。

我们现在可以将新类别添加到用于手册和图片，但我们系统 ve 尚未以看看如何更新现有类别 s 二进制数据或如何正确删除已删除的类别的二进制数据。 在下一教程中，我们将探讨以下两个主题。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Dave Gardner、 Teresa Murphy 和伯纳黛特 Leigh。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](displaying-binary-data-in-the-data-web-controls-cs.md)
> [下一页](updating-and-deleting-existing-binary-data-cs.md)
