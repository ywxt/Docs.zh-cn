---
uid: web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
title: 显示数据 Web 中的二进制数据控件 (VB) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们看一下在 Web 页上，包括显示的图像文件和下载链接 f 的预配上显示二进制数据的选项...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/27/2007
ms.topic: article
ms.assetid: 9201656a-e1c2-4020-824b-18fb632d2925
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: a9d298ef328e951f235a6cfcd41b73fafefb0dfb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37373102"
---
<a name="displaying-binary-data-in-the-data-web-controls-vb"></a>显示数据 Web 控件 (VB) 中的二进制数据
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_55_VB.exe)或[下载 PDF](displaying-binary-data-in-the-data-web-controls-vb/_static/datatutorial55vb1.pdf)

> 在本教程中我们查看一下在 Web 页上，包括显示的图像文件和 PDF 文件预配的下载链接上显示二进制数据的选项。


## <a name="introduction"></a>介绍

在前面的教程，我们探讨了用于将二进制数据与应用程序 s 基础数据模型相关联的两个技术并使用 FileUpload 控件从浏览器到 web 服务器文件系统的文件上传。 我们 ve 尚未若要了解如何将上传的二进制数据与数据模型相关联。 也就是说上, 传一个文件并将其保存到文件系统后，该文件的路径必须存储在相应的数据库记录。 如果直接在数据库中存储数据上, 传的二进制数据需要不会保存到文件系统，但必须插入到数据库。

我们看一下将数据与数据模型相关联之前，不过，让 s 首先看一下如何向最终用户提供的二进制数据。 提供文本数据非常简单，但二进制数据的存在方式？ 它取决于，当然，二进制数据的类型。 对于映像，我们可能想要显示的图像;对于 pdf 文件，Microsoft Word 文档、 ZIP 文件和其他类型的二进制数据，提供下载链接是可能更合适。

在本教程中我们将探讨如何显示以及使用数据及其关联的文本数据的二进制数据 Web 控件如 GridView 和 DetailsView。 在下一教程中我们要将注意力转移到将上传的文件与数据库相关联。

## <a name="step-1-providingbrochurepathvalues"></a>步骤 1： 提供`BrochurePath`值

`Picture`中的列`Categories`表已包含的不同的类别图像的二进制数据。 具体而言，`Picture`为每个记录的列包含有纹理、 低质量、 16 色位图图像的二进制内容。 每个类别的图像为 172 个像素宽和 120 像素、 高，并使用大致 11 KB。 新增更多、 中的二进制内容`Picture`列中包含 78 字节[OLE](http://en.wikipedia.org/wiki/Object_Linking_and_Embedding)必须显示该映像之前去除的标头。 存在此标头信息是因为 Northwind 数据库起源于 Microsoft Access。 在 Access 中，使用此标头采取的 OLE 对象的数据类型存储二进制数据。 现在，我们将了解如何显示图片以去除这些低质量的图像中的标头。 在以后的教程，我们将构建一个接口，使更新类别的`Picture`列，并将为等效的 JPG 图像，而不必要的 OLE 标头与使用 OLE 标头这些位图图像。

在前面的教程中，我们已了解如何使用 FileUpload 控件。 因此，可以继续操作并将手册文件添加到 web 服务器文件系统。 这样做，但是，不会更新`BrochurePath`中的列`Categories`表。 在下一教程中，我们将了解如何实现此目的，但现在，我们需要手动为此列提供值。

本教程的下载内容中，您会发现中的七个 PDF 小册子文件`~/Brochures`文件夹，一个用于除 Seafood 类别中的每一个。 我有意省略了添加 Seafood 手册，为了说明如何处理方案具有关联并不是所有记录的二进制数据。 若要更新`Categories`使用这些值表中，右键单击`Categories`节点从服务器资源管理器，然后选择显示表数据。 然后，输入具有小册子中，如图 1 所示的每个类别的手册文件虚拟路径。 由于没有任何手册 Seafood 类别，将保留其`BrochurePath`作为列的值`NULL`。


[![手动输入类别表的 BrochurePath 列的值](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.png)

**图 1**： 手动输入的值`Categories`表 s`BrochurePath`列 ([单击以查看实际尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.png))


## <a name="step-2-providing-a-download-link-for-the-brochures-in-a-gridview"></a>步骤 2： 为小册子 GridView 中提供的下载链接

与`BrochurePath`提供的值`Categories`表中，我们准备就绪后，若要创建一个 GridView，列出了用于下载类别的手册的链接以及每个类别。 在步骤 4 中，我们将扩展此 GridView，其中还显示类别的图像。

首先，将从工具箱拖到设计器的 GridView`DisplayOrDownloadData.aspx`页中`BinaryData`文件夹。 设置 GridView s`ID`到`Categories`通过 GridView s 智能标记，选择将其绑定到新的数据源。 具体而言，将其绑定到名为 ObjectDataSource`CategoriesDataSource`检索数据使用的`CategoriesBLL`对象的`GetCategories()`方法。


[![创建名为 CategoriesDataSource 新 ObjectDataSource](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.png)

**图 2**： 创建新对象数据源命名`CategoriesDataSource`([单击以查看实际尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.png))


[![配置对象数据源以使用 CategoriesBLL 类](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.png)

**图 3**： 配置为使用 ObjectDataSource`CategoriesBLL`类 ([单击以查看实际尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.png))


[![检索使用 GetCategories() 方法的类别列表](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.png)

**图 4**： 检索列表的类别使用`GetCategories()`方法 ([单击以查看实际尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.png))


完成配置数据源向导后，Visual Studio 将自动添加到 BoundField `Categories` GridView `CategoryID`， `CategoryName`， `Description`， `NumberOfProducts`，并且`BrochurePath` `DataColumn` s。 继续操作并删除`NumberOfProducts`以来 BoundField`GetCategories()`的方法查询不会检索此信息。 此外删除`CategoryID`BoundField 和重命名`CategoryName`并`BrochurePath`BoundFields`HeaderText`为类别和手册，属性分别。 进行这些更改后，您的 GridView 和 ObjectDataSource s 的声明性标记应如下所示：


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample1.aspx)]

查看此页上的通过浏览器 （请参见图 5）。 列出的每个八个类别。 使用七种类别`BrochurePath`值具有`BrochurePath`各自 BoundField 中显示的值。 Seafood，具有`NULL`值为其`BrochurePath`，将显示空单元格。


[![列出每个类别的名称、 说明和 BrochurePath 值](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.png)

**图 5**： 每个类别的名称、 说明，并`BrochurePath`列出值 ([单击以查看实际尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.png))


而不是显示的文本`BrochurePath`列中，我们想要创建指向小册子中的链接。 若要完成此操作，删除`BrochurePath`BoundField 和将其替换为 HyperLinkField。 设置新 HyperLinkField s`HeaderText`属性设置为手册，其`Text`属性设置为视图小册子中，并将其`DataNavigateUrlFields`属性设置为`BrochurePath`。


![为 BrochurePath 添加 HyperLinkField](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.gif)

**图 6**： 添加为 HyperLinkField `BrochurePath`


如图 7 所示，这将添加一列链接到 GridView。 单击视图手册链接将直接在浏览器中显示 PDF 或提示用户下载的文件，具体取决于是否安装了 PDF 阅读器和浏览器的设置。


[![可通过单击查看手册链接查看类别的手册](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.png)

**图 7**： 通过单击查看手册链接的类别 s 可以查看手册 ([单击以查看实际尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.png))


[![显示类别的手册 PDF](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.png)

**图 8**： 显示手册 PDF 类别 s ([单击以查看实际尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image14.png))


## <a name="hiding-the-view-brochure-text-for-categories-without-a-brochure"></a>而无需手册的类别的隐藏视图手册文本

如图 7 所示， `BrochurePath` HyperLinkField 显示其`Text`属性值 （视图手册） 的所有记录，而不管是否那里 s 非`NULL`值`BrochurePath`。 当然，如果`BrochurePath`是`NULL`，该链接显示为文本，然后与 Seafood 类别情况一样 （请参阅回图 7）。 而不是显示的文本视图手册，可能会很棒而无需这些类别`BrochurePath`值显示一些备用文本，如无手册可用。

为了提供此行为，我们需要使用通过调用页面方法发出相应的输出基于在生成其内容为 TemplateField`BrochurePath`值。 我们先探讨了此格式设置方法返回[GridView 控件中使用 Templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md)教程。

选择将转换为 TemplateField HyperLinkField `BrochurePath` HyperLinkField，然后单击转换此字段转换为 TemplateField 链接在编辑列对话框中。


![HyperLinkField 转换为 TemplateField](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.gif)

**图 9**: HyperLinkField 转换为 TemplateField


这将创建使用 TemplateField `ItemTemplate` ，其中包含超链接 Web 控件`NavigateUrl`属性绑定到`BrochurePath`值。 将此标记对方法的调用替换为`GenerateBrochureLink`中的值传入`BrochurePath`:


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample2.aspx)]

接下来，创建`Protected`方法在 ASP.NET 页上名为 s 代码隐藏类`GenerateBrochureLink`，它返回`String`并接受`Object`作为输入参数。


[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample3.vb)]

此方法用于确定传入的`Object`值是一种数据库`NULL`和，如果是这样，将返回一个消息，指示该类别缺少手册。 否则为如果没有`BrochurePath`值，它显示超链接中的 s。 请注意，如果`BrochurePath`值是将其提交到传递的 s [ `ResolveUrl(url)`方法](https://msdn.microsoft.com/library/system.web.ui.control.resolveurl.aspx)。 此方法解析传入的*url*，并替换`~`字符与相应的虚拟路径。 例如，如果应用程序根节点`/Tutorial55`，`ResolveUrl("~/Brochures/Meats.pdf")`将返回`/Tutorial55/Brochures/Meat.pdf`。

图 10 应用这些更改后显示的页。 请注意，Seafood 类别的`BrochurePath`字段现在显示无手册可用的文本。


[![文本否手册可显示有关这些类别而无需手册](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image15.png)

**图 10**： 显示有关这些类别而无需手册的文本无手册可用 ([单击以查看实际尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image16.png))


## <a name="step-3-adding-a-web-page-to-display-a-category-s-picture"></a>步骤 3： 添加网页以显示类别的图片

当用户访问 ASP.NET 页面时，他们将收到 ASP.NET 页的 HTML。 收到的 HTML 只是文本，并且不包含任何二进制数据。 任何其他的二进制数据，如图像、 声音文件、 Macromedia Flash 应用程序、 嵌入 Windows Media Player 视频等，作为单独的 web 服务器上的资源存在。 HTML 包含对这些文件的引用，但不包括文件的实际内容。

例如，在 HTML`<img>`元素用于引用一张图片，与`src`指向图像文件的属性如下所示：


[!code-html[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample4.html)]

当浏览器收到此 HTML 时，它向 web 服务器以检索图像文件，并将结果显示在浏览器中的二进制内容发出另一个请求。 相同的概念适用于任何二进制数据。 在步骤 2 中，小册子中已不发送到浏览器页面的 HTML 标记的一部分。 而是，呈现的 HTML 提供超链接，单击，导致浏览器直接请求 PDF 文档。

若要显示或允许用户下载驻留在数据库中的二进制数据，我们需要创建一个单独的网页，返回的数据。 我们的应用程序，这里 s 只有一个直接存储在数据库类别的图片的二进制数据字段。 因此，我们需要一个页面，调用时，返回特定类别的图像数据。

添加到新的 ASP.NET 页`BinaryData`文件夹名为`DisplayCategoryPicture.aspx`。 这样做时，选择母版页复选框保持未选中状态。 此页需要`CategoryID`在查询字符串并返回该类别 s 的二进制数据值`Picture`列。 由于此页返回二进制数据和其他任何内容，因此它不需要的 HTML 部分中任何标记。 因此，单击左下角的源选项卡并删除所有页面的标记除外`<%@ Page %>`指令。 也就是说， `DisplayCategoryPicture.aspx` s 声明性标记应包含单个行：


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample5.aspx)]

如果您看到`MasterPageFile`属性中`<%@ Page %>`指令，将其删除。

在页面 + s 代码隐藏类中，以下代码添加到`Page_Load`事件处理程序：


[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample6.vb)]

此代码开始通过阅读`CategoryID`到一个名为变量的查询字符串值`categoryID`。 接下来，通过调用检索图片数据`CategoriesBLL`类的`GetCategoryWithBinaryDataByCategoryID(categoryID)`方法。 通过使用此数据返回到客户端`Response.BinaryWrite(data)`方法，但在此调用之前`Picture`必须删除列的值的 OLE 标头。 这通过创建实现`Byte`名为数组`strippedImageData`，将存放精确 78 个字符而不是在更少`Picture`列。 [ `Array.Copy`方法](https://msdn.microsoft.com/library/z50k9bft.aspx)用于中的数据复制`category.Picture`起始位置 78 转移到`strippedImageData`。

`Response.ContentType`属性指定[MIME 类型](http://en.wikipedia.org/wiki/MIME)被返回，以便在浏览器知道如何呈现的内容。 由于`Categories`表的`Picture`列是位图图像、 位图 MIME 类型使用此处 (image/bmp)。 如果省略的 MIME 类型，大多数浏览器仍将显示图像正确因为它们可以推断出基于内容的图像文件 s 二进制数据类型。 但是，它比较明智的做法包括 MIME s 键入在可能的情况。 请参阅[Internet 号码分配机构的网站](http://www.iana.org/)有关的完整列表[MIME 媒体类型](http://www.iana.org/assignments/media-types/)。

与创建此页，可以通过访问查看特定类别的图片`DisplayCategoryPicture.aspx?CategoryID=categoryID`。 图 11 显示了饮料类别的图中，可以通过查看`DisplayCategoryPicture.aspx?CategoryID=1`。


[![显示图片饮料类别 s](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image17.png)

**图 11**： 显示图片的饮料类别 s ([单击以查看实际尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image18.png))


如果在访问`DisplayCategoryPicture.aspx?CategoryID=categoryID`，收到异常，并显示无法为类型的对象强制转换为 System.DBNull type 'System.Byte []，这可能导致两件事情。 首先，`Categories`表 s`Picture`允许列`NULL`值。 `DisplayCategoryPicture.aspx`页上，但是，假定有一个非`NULL`值存在。 `Picture`的属性`CategoriesDataTable`如果有不能直接访问`NULL`值。 如果确实想要允许`NULL`值为`Picture`列中，d 你想要包括以下条件：


[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample7.vb)]

上面的代码假定一些图像名为文件即 s`NoPictureAvailable.gif`在`Images`想要显示这些类别，而无需图片的文件夹。

如果，也可能导致此异常`CategoriesTableAdapter`s `GetCategoryWithBinaryDataByCategoryID` s 方法`SELECT`语句已恢复主查询的列列表中，出现这种情况，如果正在使用的临时 SQL 语句，并且你已重新运行该向导的 TableAdapter s主查询。 检查以确保`GetCategoryWithBinaryDataByCategoryID`s 方法`SELECT`语句仍包含`Picture`列。

> [!NOTE]
> 每次`DisplayCategoryPicture.aspx`是访问时，对数据库进行访问，并返回指定的类别的图片数据。 如果自上次已查看更改类别的图片功能，那么 t，不过，这就是做很多无用功。 幸运的是，HTTP 允许*条件获取*。 条件性 GET 发出 HTTP 请求的客户端中将发送沿[ `If-Modified-Since` HTTP 标头](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)，它提供的日期和时间在客户端上次从 web 服务器中检索此资源。 如果内容未更改由于这指定日期，因此，web 服务器可能会响应[不会修改状态代码 (304)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)和放弃发回请求的资源的内容。 简单地说，此技术使无需发送资源的内容，如果它未被修改自客户端上次访问以来的 web 服务器。


若要实现此行为，但是，要求您添加`PictureLastModified`列添加到`Categories`表，以捕获时`Picture`检查代码以及上次更新列`If-Modified-Since`标头。 有关详细信息`If-Modified-Since`标头和条件 GET 工作流，请参阅[HTTP 条件 GET RSS 黑客](http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers)并[更深入地看看 ASP.NET 页中执行 HTTP 请求](http://aspnet.4guysfromrolla.com/articles/122204-1.aspx)。

## <a name="step-4-displaying-the-category-pictures-in-a-gridview"></a>步骤 4： 在 GridView 中显示的类别图片

现在，我们已有要显示特定类别的图片的网页，我们可以显示使用其[图像 Web 控件](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/image.aspx)或对应的 HTML`<img>`指向的元素`DisplayCategoryPicture.aspx?CategoryID=categoryID`。 可以在 GridView 或使用 ImageField DetailsView 中显示其 URL 将由数据库数据的图像。 包含 ImageField`DataImageUrlField`并`DataImageUrlFormatString`属性的工作方式类似 HyperLinkField s`DataNavigateUrlFields`和`DataNavigateUrlFormatString`属性。

让我们来扩充`Categories`中的 GridView`DisplayOrDownloadData.aspx`通过添加 ImageField 以显示每个类别的图片。 只需添加 ImageField 并设置其`DataImageUrlField`并`DataImageUrlFormatString`属性设置为`CategoryID`和`DisplayCategoryPicture.aspx?CategoryID={0}`分别。 这将创建 GridView 列呈现`<img>`元素的`src`属性引用`DisplayCategoryPicture.aspx?CategoryID={0}`，其中{0}替换为 GridView 行的`CategoryID`值。


![添加到 GridView ImageField](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.gif)

**图 12**: ImageField 添加到 GridView


以后将添加 ImageField，GridView s 声明性语法看起来应像 soothe 以下：


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample8.aspx)]

请花费片刻时间来查看此页上的通过浏览器。 请注意如何每条记录现在包含类别的图片。


[![为每个行显示类别的图片](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image19.png)

**图 13**： 为每个行显示图片的类别 s ([单击以查看实际尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image20.png))


## <a name="summary"></a>总结

在本教程中介绍了如何显示二进制数据。 数据的显示方式取决于数据的类型。 对于 PDF 小册子文件，我们向用户提供视图手册链接，单击时，用户直接所用的时间的 PDF 文件。 类别的图片，我们首先创建一个页面，检索并从数据库返回的二进制数据，并且然后使用该页面的 GridView 中显示每个类别的图片。

现在，我们已了解了如何显示二进制数据，我们准备就绪后，若要了解如何执行插入、 更新和删除针对数据库的二进制数据。 在下一教程中我们将介绍如何将上传的文件与相应的数据库记录相关联。 在这之后的教程，我们将了解如何更新现有的二进制数据，以及如何删除其关联的记录已删除的二进制数据。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Teresa Murphy 和 Dave Gardner。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](uploading-files-vb.md)
> [下一页](including-a-file-upload-option-when-adding-a-new-record-vb.md)
