---
uid: web-forms/overview/data-access/working-with-binary-files/uploading-files-cs
title: 上传文件 (C#) |Microsoft Docs
author: rick-anderson
description: 了解如何允许用户上传二进制文件 （如 Word 或 PDF 文档） 到其中可能会将它们存储在服务器的文件系统网站...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/27/2007
ms.topic: article
ms.assetid: b381b1da-feb3-4776-bc1b-75db53eb90ab
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/uploading-files-cs
msc.type: authoredcontent
ms.openlocfilehash: aaa81014a03fc04e68ea7b8014933cf87002af2e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388323"
---
<a name="uploading-files-c"></a>上传文件 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_54_CS.exe)或[下载 PDF](uploading-files-cs/_static/datatutorial54cs1.pdf)

> 了解如何允许用户上传二进制文件 （如 Word 或 PDF 文档），其中它们可能会在服务器的文件系统或数据库中存储您的网站。


## <a name="introduction"></a>介绍

所有这些教程我们 ve 检查到目前为止已以独占方式使用文本数据。 但是，许多应用程序必须捕获文本和二进制数据的数据模型。 联机的约会站点可能会允许用户上传图片将其配置文件相关联。 招聘网站可能会让用户将其恢复为 Microsoft Word 或 PDF 文档上传。

处理二进制数据将添加一组新的挑战。 我们必须决定如何在应用程序中存储二进制数据。 用于插入新记录的接口必须更新，以允许用户上传其计算机中的文件，并且必须采取额外步骤来显示或提供一个使下载记录 s 关联的二进制数据。 在本教程中下, 一步 3 中，我们将探讨如何难这些挑战。 在这些教程末尾我们将构建一个完全正常运行的应用程序，将图片和 PDF 小册子与每个类别相关联。 在本特定教程中我们将看看不同的技术来存储二进制数据，并探讨如何使用户能够从他们的计算机文件上传和已保存在 web 服务器文件系统上。

> [!NOTE]
> 是应用程序的数据模型的一部分的二进制数据有时称为[BLOB](http://en.wikipedia.org/wiki/Binary_large_object)，二进制大型对象的首字母缩写。 在这些教程中我已选择要使用的术语的二进制数据，虽然此术语 BLOB 为同义词。


## <a name="step-1-creating-the-working-with-binary-data-web-pages"></a>步骤 1： 使用二进制数据 Web 页创建工作

我们开始浏览与添加对二进制数据的支持的难题之前，让 s 先花点时间在我们的网站项目，我们需要为本教程中下, 一步 3 中创建 ASP.NET 页面。 首先，通过添加一个名为的新文件夹`BinaryData`。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将与每个页面相关联`Site.master`母版页：

- `Default.aspx`
- `FileUpload.aspx`
- `DisplayOrDownloadData.aspx`
- `UploadInDetailsView.aspx`
- `UpdatingAndDeleting.aspx`


![将 ASP.NET 页面添加二进制与数据相关的教程](uploading-files-cs/_static/image1.gif)

**图 1**： 将 ASP.NET 页面添加二进制与数据相关的教程


在其他文件夹中，喜欢`Default.aspx`在`BinaryData`文件夹将在其部分中列出的教程。 请记住，`SectionLevelTutorialListing.ascx`用户控件提供了此功能。 因此，此用户控件添加到`Default.aspx`通过从解决方案资源管理器中拖到页面上的设计视图中拖动。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](uploading-files-cs/_static/image2.gif)](uploading-files-cs/_static/image1.png)

**图 2**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](uploading-files-cs/_static/image2.png))


最后，将这些页面添加到条目为`Web.sitemap`文件。 具体而言，在提高后添加以下标记 GridView `<siteMapNode>`:


[!code-xml[Main](uploading-files-cs/samples/sample1.xml)]

更新后`Web.sitemap`，花点时间查看通过浏览器网站的教程。 在左侧菜单现在包含二进制数据教程使用的项。


![站点图现在包括二进制数据教程使用的条目](uploading-files-cs/_static/image3.gif)

**图 3**： 站点图现在包括二进制数据教程使用的条目


## <a name="step-2-deciding-where-to-store-the-binary-data"></a>步骤 2： 决定在何处存储二进制数据

与应用程序的数据模型关联的二进制数据可以存储在两个位置之一： 具有对该数据库; 中存储的文件的引用的 web 服务器的文件系统上或直接在数据库本身中 （请参阅图 4）。 每种方法有其自己的优点和缺点集，并需要更多详细的讨论。


[![可以存储二进制数据，在文件系统或直接在数据库中](uploading-files-cs/_static/image4.gif)](uploading-files-cs/_static/image3.png)

**图 4**： 可以存储二进制数据，在文件系统或直接在数据库中 ([单击以查看实际尺寸的图像](uploading-files-cs/_static/image4.png))


假设我们想要扩展 Northwind 数据库，以将图片与每个产品相关联。 是一种方法存储这些 web 服务器的文件系统上的图像文件，并记录中的路径`Products`表。 使用此方法时，我们 d 添加`ImagePath`列添加到`Products`类型的表`varchar(200)`，可能是。 当用户上传牛奶的图片时，可能会在 web 服务器的文件系统上存储该图片`~/Images/Tea.jpg`，其中`~`表示应用程序的物理路径。 也就是说，如果网站已取得 root 权限的物理路径处`C:\Websites\Northwind\`，`~/Images/Tea.jpg`等同于`C:\Websites\Northwind\Images\Tea.jpg`。 上传的图像文件以后, 我们 d 更新中的 Chai 记录`Products`表，以便其`ImagePath`引用列的新图像的路径。 我们可以使用`~/Images/Tea.jpg`或仅`Tea.jpg`如果产品的所有映像，将都放置在应用程序，我们决定`Images`文件夹。

将二进制数据存储在文件系统上的主要优点是：

- **简易的实施**我们稍后将看到的如存储和检索直接在数据库中存储的二进制数据涉及相比时使用的数据通过文件系统的更多代码。 此外，为了使用户可以查看或下载的二进制数据中它们必须显示指向该数据的 url。 如果数据驻留在 web 服务器文件系统上，该 URL 非常简单。 如果数据存储在数据库中，但是，web 页需要创建将检索，并从数据库中返回数据。
- **二进制数据的更广泛访问**二进制数据可能需要可供其他服务或应用程序，不能提取数据库中的数据的访问。 例如，与每个产品相关联的映像可能还需要可供用户通过[FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol)，在这种情况下 d 我们想要将二进制数据存储在文件系统。
- **性能**二进制数据存储在文件系统上，如果数据库服务器和 web 服务器之间按需和网络阻塞将少于如果直接在数据库中存储二进制数据。

将二进制数据存储在文件系统上的主要缺点是它分离了数据库中的数据。 如果从删除了记录`Products`表中，web 服务器的文件系统上关联的文件不会自动删除。 我们必须编写额外代码以删除该文件或文件系统将会变得杂乱的未使用的、 孤立的文件。 此外，当将数据库备份，我们必须确保文件系统上进行关联的二进制数据的备份。 将数据库移动到另一个站点或服务器会产生类似问题。

或者，二进制数据可以存储在 Microsoft SQL Server 2005 数据库中直接通过创建类型的列的`varbinary`。 像其他可变长度数据类型，您可以指定二进制数据可占用的最大长度此列中。 例如，若要保留最多 5,000 个字节使用`varbinary(5000)`;`varbinary(MAX)`允许的最大存储大小，大约 2 GB。

直接在数据库中存储二进制数据的主要优点是二进制数据和数据库记录之间的紧密耦合。 这极大地简化了数据库管理任务，如备份或将数据库移到另一个站点或服务器。 此外，自动删除一条记录会删除相应的二进制数据。 还有更多的在数据库中存储二进制数据的细微优势。 请参阅[存储二进制文件直接在数据库使用 ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/120606-1.aspx)有关更深入讨论。

> [!NOTE]
> 在 Microsoft SQL Server 2000 和早期版本中，`varbinary`数据类型有最大限制为 8000 个字节。 用于存储二进制数据的最多为 2 GB [ `image`数据类型](https://msdn.microsoft.com/library/ms187993.aspx)需要改为使用。 通过添加`MAX`在 SQL Server 2005，但是，`image`推荐使用的数据类型。 它 s 仍支持向后兼容性，但 Microsoft 宣布`image`将 SQL Server 的未来版本中删除数据类型。


如果你正在使用较旧的数据模型可能会看到`image`数据类型。 Northwind 数据库 s`Categories`表具有`Picture`可以用于存储二进制数据的类别的图像文件的列。 Northwind 数据库起源于 Microsoft Access 和 SQL Server 的早期版本，因为此列的类型是`image`。

对于本教程的下一步的三个，我们将使用这两种方法。 `Categories`表中已包含`Picture`列用于存储二进制内容的类别的图像。 我们将添加一个额外的列`BrochurePath`，以 pdf 格式的路径存储在 web 服务器的文件系统，可用于打印质量、 可媲美的类别概述。

## <a name="step-3-adding-thebrochurepathcolumn-to-thecategoriestable"></a>步骤 3： 添加`BrochurePath`列添加到`Categories`表

当前类别表中的只有四个列： `CategoryID`， `CategoryName`， `Description`，和`Picture`。 除了这些字段中，我们需要添加一个将指向类别的手册 （如果存在） 的新。 若要添加此列，请转到服务器资源管理器，向下钻取到表，右键单击`Categories`表，并选择打开表定义 （请参见图 5）。 如果看不到服务器资源管理器，使其通过从视图菜单中选择服务器资源管理器选项或按 Ctrl + Alt + S。

添加一个新`varchar(200)`列添加到`Categories`名为表`BrochurePath`，并允许`NULL`s 并单击保存图标 （或按 Ctrl + S）。


[![将 BrochurePath 列添加到类别表](uploading-files-cs/_static/image5.gif)](uploading-files-cs/_static/image5.png)

**图 5**： 添加`BrochurePath`列与`Categories`表 ([单击以查看实际尺寸的图像](uploading-files-cs/_static/image6.png))


## <a name="step-4-updating-the-architecture-to-use-thepictureandbrochurepathcolumns"></a>步骤 4： 更新以使用体系结构`Picture`和`BrochurePath`列

`CategoriesDataTable`数据访问层 (DAL) 中当前具有四个`DataColumn`定义的 s: `CategoryID`， `CategoryName`， `Description`，并`NumberOfProducts`。 我们最初设计中的此 DataTable[创建数据访问层](../introduction/creating-a-data-access-layer-cs.md)教程中，`CategoriesDataTable`只有前三个列;`NumberOfProducts`列中添加[母版/详细信息使用项目符号列表的详细信息 DataList 使用母版记录](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)教程。

如中所述*创建数据访问层*，在类型化数据集中数据表组成业务对象。 Tableadapter 是负责与数据库通信和填充查询结果与业务对象。 `CategoriesDataTable`由填充`CategoriesTableAdapter`，其中包含三个数据检索方法：

- `GetCategories()` 执行 TableAdapter s 主查询并返回`CategoryID`， `CategoryName`，并`Description`字段中的所有记录`Categories`表。 主查询是使用自动生成的`Insert`和`Update`方法。
- `GetCategoryByCategoryID(categoryID)` 返回`CategoryID`， `CategoryName`，并`Description`类别的字段的`CategoryID`等于*categoryID*。
- `GetCategoriesAndNumberOfProducts()` -返回`CategoryID`， `CategoryName`，并`Description`中的所有记录的字段`Categories`表。 此外可以使用子查询来返回与每个类别相关联的产品数量。

请注意，不能提供的查询返回`Categories`表 s`Picture`或`BrochurePath`列; 也不会`CategoriesDataTable`提供`DataColumn`s 为这些字段。 若要使用的图片和`BrochurePath`属性，我们需要首先将其添加到`CategoriesDataTable`，然后更新`CategoriesTableAdapter`类以返回这些列。

## <a name="adding-thepictureandbrochurepathdatacolumn-s"></a>添加`Picture`和`BrochurePath``DataColumn`s

首先，通过添加到这两个列`CategoriesDataTable`。 右键单击`CategoriesDataTable`s 标头，从上下文菜单中选择添加，然后选择列选项。 这将创建一个新`DataColumn`中名为的 DataTable `Column1`。 为此列重命名`Picture`。 从属性窗口中，设置`DataColumn`s`DataType`属性设置为`System.Byte[]`（这不是下拉列表中的一个选项; 你需要键入中）。


[![创建 DataColumn 名为图片数据类型与 System.Byte]](uploading-files-cs/_static/image6.gif)](uploading-files-cs/_static/image7.png)

**图 6**： 创建`DataColumn`命名`Picture`其`DataType`是`System.Byte[]`([单击以查看实际尺寸的图像](uploading-files-cs/_static/image8.png))


添加另一个`DataColumn`到 DataTable，其命名为`BrochurePath`使用默认`DataType`值 (`System.String`)。

## <a name="returning-thepictureandbrochurepathvalues-from-the-tableadapter"></a>返回`Picture`和`BrochurePath`TableAdapter 中的值

使用这两个`DataColumn`添加到的 s `CategoriesDataTable`，我们已准备好更新重新`CategoriesTableAdapter`。 我们可以有两个主要的 TableAdapter 查询中返回这些列的值，但此时会显示返回的二进制数据每次`GetCategories()`调用方法。 相反，let s 更新主的 TableAdapter 查询，以使重新`BrochurePath`并创建返回特定类别 s 的其他数据检索方法`Picture`列。

若要更新主 TableAdapter 查询，请右键单击`CategoriesTableAdapter`s 标头，然后从上下文菜单中选择配置选项。 这将显示表的适配器配置向导的我们 ve 许多过去的教程中所示。 更新查询，以使重新`BrochurePath`并单击完成。


[![更新也会返回 BrochurePath 的 SELECT 语句中的列列表](uploading-files-cs/_static/image7.gif)](uploading-files-cs/_static/image9.png)

**图 7**： 更新中的列列表`SELECT`也返回语句`BrochurePath`([单击以查看实际尺寸的图像](uploading-files-cs/_static/image10.png))


当使用 TableAdapter 临时 SQL 语句，更新主查询中的列列表的所有更新列列表`SELECT`查询 TableAdapter 中的方法。 这意味着`GetCategoryByCategoryID(categoryID)`方法已更新，以返回`BrochurePath`列中，这可能是我们的预期。 但是，它还更新中的列列表`GetCategoriesAndNumberOfProducts()`方法，删除子查询返回的每个类别的产品数量 ！ 因此，我们需要更新此方法，s`SELECT`查询。 右键单击`GetCategoriesAndNumberOfProducts()`方法中，选择配置，并还原`SELECT`回其原始值的查询：


[!code-sql[Main](uploading-files-cs/samples/sample2.sql)]

接下来，创建新的 TableAdapter 方法返回特定类别的`Picture`列的值。 右键单击`CategoriesTableAdapter`s 标头，并选择添加查询选项以启动 TableAdapter 查询配置向导。 此向导的第一步会要求我们是否我们要使用的临时 SQL 语句查询数据，一个新存储过程或一个现有。 选择使用 SQL 语句，然后单击下一步。 由于我们将返回行，选择选择第二个步骤中返回的行选项。


[![选择使用 SQL 语句选项](uploading-files-cs/_static/image8.gif)](uploading-files-cs/_static/image11.png)

**图 8**： 选择使用 SQL 语句选项 ([单击以查看实际尺寸的图像](uploading-files-cs/_static/image12.png))


[![由于从类别表，则查询将返回一条记录，选择选择其返回的行](uploading-files-cs/_static/image9.gif)](uploading-files-cs/_static/image13.png)

**图 9**： 由于该查询将从类别表中，选择选择返回的行返回一条记录 ([单击以查看实际尺寸的图像](uploading-files-cs/_static/image14.png))


在第三个步骤中，输入以下 SQL 查询，然后单击下一步:


[!code-sql[Main](uploading-files-cs/samples/sample3.sql)]

最后一步是选择新的方法的名称。 使用`FillCategoryWithBinaryDataByCategoryID`和`GetCategoryWithBinaryDataByCategoryID`填充 DataTable 并返回数据表模式，分别。 单击完成以完成向导。


[![选择 TableAdapter 的方法的名称](uploading-files-cs/_static/image10.gif)](uploading-files-cs/_static/image15.png)

**图 10**： 选择 TableAdapter 的方法的名称 ([单击以查看实际尺寸的图像](uploading-files-cs/_static/image16.png))


> [!NOTE]
> 表适配器查询配置向导完成后可能会看到一个对话框，通知您，新的命令文本返回具有架构的数据不同于主查询的架构。 简单地说，该向导注意的是，TableAdapter s 主查询`GetCategories()`返回比我们刚刚创建的一个不同的架构。 但这是我们希望的因此可以忽略此消息。


此外，请记住，如果使用临时 SQL 语句并且使用向导更改 TableAdapter s 有时更高版本的主查询中时，它将修改`GetCategoryWithBinaryDataByCategoryID`s 方法`SELECT`语句的列列表，以包括从仅对这些列主查询 (即，它将删除`Picture`查询中的列)。 您将必须手动更新要返回的列列表`Picture`列中，类似于我们所做的与`GetCategoriesAndNumberOfProducts()`之前在此步骤中的方法。

添加两个后`DataColumn`向`CategoriesDataTable`并`GetCategoryWithBinaryDataByCategoryID`方法`CategoriesTableAdapter`，类型化数据集设计器中的这些类应如图 11 所示的屏幕截图所示。


![数据集设计器包括新的列和方法](uploading-files-cs/_static/image11.gif)

**图 11**： 数据集设计器包括新的列和方法


## <a name="updating-the-business-logic-layer-bll"></a>正在更新业务逻辑层 (BLL)

与更新 DAL，剩下的就是来加强业务逻辑层 (BLL) 以囊括新方法`CategoriesTableAdapter`方法。 添加以下方法`CategoriesBLL`类：


[!code-csharp[Main](uploading-files-cs/samples/sample4.cs)]

## <a name="step-5-uploading-a-file-from-the-client-to-the-web-server"></a>步骤 5： 上传到 Web 服务器从客户端文件

当收集的二进制数据，通常由最终用户提供此数据。 若要捕获此信息，用户需要能够上传到 web 服务器从其计算机的文件。 上传的数据则需要与数据模型中，这可能意味着将文件保存到 web 服务器文件系统和将路径添加到数据库中的文件或二进制内容写入到数据库直接集成。 在此步骤中我们将探讨如何允许用户从他们的计算机到服务器的文件上传。 在下一教程中我们要将注意力转移到将上传的文件与数据模型相集成。

ASP.NET 2.0 新 s [FileUpload Web 控件](https://msdn.microsoft.com/library/ms227677(VS.80).aspx)提供了用户可以将文件从其计算机发送到 web 服务器的机制。 FileUpload 控件呈现为`<input>`元素的`type`属性设置为文件，浏览器将显示为文本框使用浏览按钮。 单击浏览按钮将显示一个对话框，用户可以从中选择一个文件。 当窗体回发时，所选的文件的内容与回发一起发送。 在服务器端上传的文件有关的信息是可通过 FileUpload 控件的属性访问。

若要演示上传文件，打开`FileUpload.aspx`页中`BinaryData`文件夹中，将一个 FileUpload 控件从工具箱拖到设计器中，并设置控制 s`ID`属性设置为`UploadTest`。 接下来，添加一个按钮 Web 控件，设置其`ID`并`Text`属性设置为`UploadButton`并分别将所选文件上传。 最后，将在按钮下方的标签 Web 控件放清除其`Text`属性并设置其`ID`属性设置为`UploadDetails`。


[![向 ASP.NET 页面添加 FileUpload 控件](uploading-files-cs/_static/image12.gif)](uploading-files-cs/_static/image17.png)

**图 12**： 将 FileUpload 控件添加到 ASP.NET 页面 ([单击以查看实际尺寸的图像](uploading-files-cs/_static/image18.png))


图 13 显示了此页时的浏览器查看。 请注意，单击浏览按钮将显示文件选择对话框中，这样就允许用户选择其计算机中的文件。 一旦选择了一个文件，单击上传所选文件按钮会将所选的文件 s 二进制内容发送到 web 服务器的回发。


[![用户可以选择要从其计算机上传到服务器的文件](uploading-files-cs/_static/image13.gif)](uploading-files-cs/_static/image19.png)

**图 13**： 用户可以从服务器到其计算机上传到选择一个文件 ([单击以查看实际尺寸的图像](uploading-files-cs/_static/image20.png))


在回发时上, 传的文件可以保存到文件系统或其二进制数据可以直接通过 Stream 得到使用。 对于此示例，让我们来创建`~/Brochures`文件夹和保存那里上传的文件。 首先，通过添加`Brochures`到站点作为子文件夹的根目录的文件夹。 接下来，创建的事件处理程序`UploadButton`s`Click`事件，并添加以下代码：


[!code-csharp[Main](uploading-files-cs/samples/sample5.cs)]

FileUpload 控件提供了各种用于处理上传的数据的属性。 例如， [ `HasFile`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.hasfile.aspx)指示文件是否已上传用户，而[`FileBytes`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.filebytes.aspx)的字节数组形式提供对上传的二进制数据的访问。 `Click`事件处理程序首先确保已上传一个文件。 如果已上传一个文件，则标签将显示上传的文件，以字节为单位，其大小和内容类型的名称。

> [!NOTE]
> 若要确保用户将可以检查文件上传`HasFile`属性，并显示一条警告，如果它 s `false`，或者也可以使用[RequiredFieldValidator 控件](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/validation/default.aspx)改为。


FileUpload s`SaveAs(filePath)`上传的文件保存到指定*filePath*。 *filePath*必须是*物理路径*(`C:\Websites\Brochures\SomeFile.pdf`) 而非*虚拟**路径*(`/Brochures/SomeFile.pdf`)。 [ `Server.MapPath(virtPath)`方法](https://msdn.microsoft.com/library/system.web.httpserverutility.mappath.aspx)将虚拟路径，并返回其对应的物理路径。 在这里的虚拟路径是`~/Brochures/fileName`，其中*文件名*是上传的文件的名称。 请参阅[使用 Server.MapPath](http://www.4guysfromrolla.com/webtech/121799-1.shtml)有关详细信息，在虚拟和物理路径和使用`Server.MapPath`。

完成后`Click`事件处理程序，请花费片刻时间来测试浏览器中的页。 单击浏览按钮并从您的硬盘中选择文件，然后单击上传所选文件按钮。 在回发会将所选文件的内容发送到 web 服务器，然后将显示有关文件的信息，然后将它保存到`~/Brochures`文件夹。 上传文件后, 返回到 Visual Studio 并单击解决方案资源管理器中的刷新按钮。 你应看到您只需上传 ~/Brochures 文件夹中的文件 ！


[![文件 EvolutionValley.jpg 已上载到 Web 服务器](uploading-files-cs/_static/image14.gif)](uploading-files-cs/_static/image21.png)

**图 14**： 文件`EvolutionValley.jpg`已上传到 Web 服务器 ([单击以查看实际尺寸的图像](uploading-files-cs/_static/image22.png))


![EvolutionValley.jpg 已保存到 ~/Brochures 文件夹](uploading-files-cs/_static/image15.gif)

**图 15**:`EvolutionValley.jpg`已保存到`~/Brochures`文件夹


## <a name="subtleties-with-saving-uploaded-files-to-the-file-system"></a>与将上传的文件保存到文件系统的微妙之处

有几个保存文件上传到 web 服务器文件系统时必须解决的微妙之处。 安全的第一个，此处问题。 若要将文件保存到文件系统，在其下执行 ASP.NET 页的安全上下文必须具有写入权限。 将当前的用户帐户的上下文中运行 ASP.NET 开发 Web 服务器。 如果使用的 Microsoft 的 Internet 信息服务 (IIS) 作为 web 服务器，安全上下文取决于 IIS 及其配置的版本。

将文件保存到文件系统的另一个挑战是围绕的文件命名。 目前，我们的页面将保存到已上载的文件的所有`~/Brochures`使用相同的名称作为客户端的计算机上的文件的目录。 如果用户 A 将上传具有名称手册`Brochure.pdf`，该文件将保存为`~/Brochure/Brochure.pdf`。 但如果一段时间更高版本用户 B 不同手册将文件上传的恰好具有相同的文件名 (`Brochure.pdf`)？ 使用代码我们现在，让的用户的文件将被覆盖用户 B s 上传。

有多种方法来解决文件名称冲突。 一种方法是禁止上传文件，如果已存在一个具有相同的名称。 使用此方法，当尝试将名为的文件上传用户 B `Brochure.pdf`，系统将不保存其文件，而是显示消息，告知用户 B，若要重命名该文件，然后重试。 另一种方法是使用唯一的文件名，这可能是保存该文件[全局唯一标识符 (GUID)](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)或数据库记录 s 主键列中相应的值 (假定与关联上传中特定行的数据模型）。 在下一教程中，我们将探讨更多详细信息中的这些选项。

## <a name="challenges-involved-with-very-large-amounts-of-binary-data"></a>所涉及的二进制数据量非常大的挑战

这些教程假定适度大小中捕获的二进制数据。 使用的是几兆字节的二进制数据文件的数量非常大或更大引入了新的挑战已超出这些教程的范围。 例如，默认情况下 ASP.NET 将拒绝上的传超过 4 mb，尽管这可以通过配置[`<httpRuntime>`元素](https://msdn.microsoft.com/library/e1f13641.aspx)中`Web.config`。 IIS 太施加其自身的文件上传大小限制。 请参阅[IIS 上传文件大小](http://vandamme.typepad.com/development/2005/09/iis_upload_file.html)有关详细信息。 此外，将大型文件上传所花的时间可能会超过默认值 110 秒，ASP.NET 将等待的请求。 也有处理大型文件时出现的内存和性能问题。

FileUpload 控件不适用于大型文件上传。 文件的内容正在发布到服务器，最终用户必须耐心地等待而无需任何确认，其上传时的进展情况。 处理较小的文件来上传在几秒钟内，但可以处理较大可能需要分钟才能上传的文件会出现问题时，这不是这么多问题。 有各种第三方文件上传控件更好地适合用于处理较大的上载和很多这些供应商提供的进度指示器和 ActiveX 上载管理器，从而提供更完善的用户体验。

如果你的应用程序需要处理大型文件，您需要仔细研究面临的挑战和查找针对特定需求的合适解决方案。

## <a name="summary"></a>总结

生成的应用程序需要捕获二进制数据引入了一系列挑战。 在本教程中我们探讨了前两个： 决定存储二进制数据的位置，并允许用户上传通过网页的二进制内容。 通过三个教程，我们将了解如何将上传的数据与数据库中记录相关联，以及如何显示以及它的文本数据字段的二进制数据。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [使用大值数据类型](https://msdn.microsoft.com/library/ms178158.aspx)
- [FileUpload 控件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/fileupload.aspx)
- [ASP.NET 2.0 FileUpload 服务器控件](http://www.wrox.com/WileyCDA/Section/id-292158.html)
- [文件上传在深端](http://www.aspnetresources.com/articles/dark_side_of_file_uploads.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Teresa Murphy 和伯纳黛特 Leigh。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一篇](displaying-binary-data-in-the-data-web-controls-cs.md)
