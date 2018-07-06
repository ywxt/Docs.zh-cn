---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
title: 使用 DropDownList (C#) 进行筛选母版/详细信息 |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将了解如何在 DropDownList 控件和 GridView 中的所选的列表项的详细信息中显示的主记录。
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: 53e659cc-eefb-40c1-a1dc-559481c99443
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
msc.type: authoredcontent
ms.openlocfilehash: c2bf3156840c378e554eef3a0629705c059f2777
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833327"
---
<a name="masterdetail-filtering-with-a-dropdownlist-c"></a>使用 DropDownList (C#) 进行筛选母版/详细信息
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_7_CS.exe)或[下载 PDF](master-detail-filtering-with-a-dropdownlist-cs/_static/datatutorial07cs1.pdf)

> 在本教程中我们将了解如何在 DropDownList 控件和 GridView 中的所选的列表项的详细信息中显示的主记录。


## <a name="introduction"></a>介绍

报表的通用类型是*母版/详细信息报表*中的报表开始通过显示某些组的"主"的记录。 用户可以然后向下钻取到一个主机记录，从而查看该主记录的"详细信息。" 母版/详细信息报告是用于可视化一对多关系，如报表的理想之选显示所有类别，并允许用户选择特定的类别并显示其相关联的产品。 此外，母版/详细信息报表可用于显示来自特别"宽型"表 （是有大量的列） 的详细的信息。 例如，母版/详细信息报表的"主"级别可能会显示在数据库中，只是产品名称和单位产品的价格并向下钻取特定产品会显示其他产品字段 (类别、 供应商、 每个单元，数量和等）。

有许多方法可以用于实现母版/详细信息报表。 通过这和接下来三个教程中，我们将介绍在不同的母版/详细信息报表。 在本教程中，我们将了解如何显示中的主记录[DropDownList 控件](https://msdn.microsoft.com/library/dtx91y0z.aspx)和 GridView 中的所选的列表项的详细信息。 具体而言，本教程中的母版/详细信息报告将列出类别和产品信息。

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>步骤 1： 在 DropDownList 中显示类别

我们的母版/详细信息报表将列出与所选的列表项的产品显示在下拉列表中，类别在 GridView 的页中进一步向下。 然后，领先于我们的第一个任务是已在 DropDownList 中显示的类别。 打开`FilterByDropDownList.aspx`页中`Filtering`文件夹中，从工具箱拖到页面的设计器中，将在 DropDownList 上并设置其`ID`属性设置为`Categories`。 接下来，单击选择数据源链接从 DropDownList 的智能标记。 这将显示数据源配置向导。


[![指定 DropDownList 的数据源](master-detail-filtering-with-a-dropdownlist-cs/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image1.png)

**图 1**： 指定 DropDownList 的数据源 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image3.png))


选择将添加名为新 ObjectDataSource `CategoriesDataSource` ，它调用`CategoriesBLL`类的`GetCategories()`方法。


[![添加名为 CategoriesDataSource 新 ObjectDataSource](master-detail-filtering-with-a-dropdownlist-cs/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image4.png)

**图 2**： 添加新对象数据源名为`CategoriesDataSource`([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image6.png))


[![选择使用 CategoriesBLL 类](master-detail-filtering-with-a-dropdownlist-cs/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image7.png)

**图 3**： 选择使用`CategoriesBLL`类 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image9.png))


[![配置对象数据源使用 GetCategories() 方法](master-detail-filtering-with-a-dropdownlist-cs/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image10.png)

**图 4**： 配置为使用 ObjectDataSource`GetCategories()`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image12.png))


配置的 ObjectDataSource 我们仍然需要指定应在 DropDownList 中显示哪些数据源字段和后一个应为列表项的值相关联。 具有`CategoryName`字段与显示和`CategoryID`为每个列表项的值。


[![作为值的类别名称字段和使用 CategoryID 使 DropDownList 显示](master-detail-filtering-with-a-dropdownlist-cs/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image13.png)

**图 5**： 使 DropDownList 显示`CategoryName`字段并使用`CategoryID`作为值 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image15.png))


现在我们有从记录将填充 DropDownList 控件`Categories`表 （全部在大约六秒钟内完成）。 图 6 显示了我们到目前为止的浏览器查看时。


[![下拉列表列出了当前类别](master-detail-filtering-with-a-dropdownlist-cs/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image16.png)

**图 6**: 下拉列表列出了当前类别 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image18.png))


## <a name="step-2-adding-the-products-gridview"></a>步骤 2： 添加产品 GridView

我们的母版/详细信息报表的最后一步是列出与所选类别关联的产品。 若要完成此操作，向页添加 GridView 并创建名为新 ObjectDataSource `productsDataSource`。 具有`productsDataSource`控件中搜集从其数据`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。


[![选择 GetProductsByCategoryID(categoryID) 方法](master-detail-filtering-with-a-dropdownlist-cs/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image19.png)

**图 7**： 选择`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image21.png))


选择此方法之后, 该 ObjectDataSource 向导会提示我们的方法的值*`categoryID`* 参数。 若要使用的所选的值`categories`DropDownList 项设置参数源为控件和到 ControlID `Categories`。


[![将类别 id 参数设置为 Categories DropDownList 的值](master-detail-filtering-with-a-dropdownlist-cs/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image22.png)

**图 8**： 设置*`categoryID`* 的值的参数`Categories`DropDownList ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image24.png))


请花费片刻时间来了解我们在浏览器中的进度。 当首次访问的页面，这些产品属于所选类别 （饮料） 会显示 （如图 9 中所示），但更改 DropDownList 不会更新数据。 这是因为必须 GridView 来更新在回发。 若要实现此目的我们具有两个选项 （这两者都不需要编写任何代码）：

- **设置类别 DropDownList 的**[AutoPostBack 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**为 True。** （您可以实现此目的通过检查 DropDownList 的智能标记中的启用自动回发选项。）这会触发回发，只要 DropDownList 的选中用户更改项。 因此，当用户从下拉列表中选择新类别时回发将会随之发生，并将使用新选择的类别的产品更新 GridView。 （这是我在本教程中使用的方法）。
- **添加一个按钮 Web 控件旁边 DropDownList。** 设置其`Text`刷新属性或类似的内容。 使用此方法时，用户将需要选择新类别，然后单击该按钮。 单击按钮将会导致回发，并更新 GridView，其中列出所选类别的产品。

图 9 和 10 说明了操作中的母版/详细信息报表。


[![当首次访问的页面，显示饮料产品](master-detail-filtering-with-a-dropdownlist-cs/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image25.png)

**图 9**： 当首次访问的页面，显示饮料产品 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image27.png))


[![选择一种新产品 （生成） 将自动导致回发，更新 GridView](master-detail-filtering-with-a-dropdownlist-cs/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image28.png)

**图 10**： 选择一种新产品 （生成） 将自动导致回发，更新 GridView ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image30.png))


## <a name="adding-a----choose-a-category----list-item"></a>添加"--选择一个类别-"列表项

首次访问时`FilterByDropDownList.aspx`页 DropDownList 的第一个列表项 （饮料） 选择默认情况下，在 GridView 中显示的饮料产品的类别。 而不是显示第一个类别的产品，我们可能想要改为具有 DropDownList 项选择的显示类似于"--选择一个类别-"的内容。

若要向 DropDownList 添加新列表项，请转到属性窗口，然后单击中的椭圆`Items`属性。 添加的新列表项`Text`"--选择一个类别-"和`Value` `-1`。


[![添加--选择列表项的 Category-](master-detail-filtering-with-a-dropdownlist-cs/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image31.png)

**图 11**： 添加--列表项中选择一个类别-([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image33.png))


或者，可以通过将以下标记添加到下拉列表添加列表项：

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample1.aspx)]

此外，我们需要设置 DropDownList 控件`AppendDataBoundItems`设为 True，因为从 ObjectDataSource 类别绑定到 DropDownList 时它们将覆盖任何手动添加列表项，如果`AppendDataBoundItems`不是 True。


![AppendDataBoundItems 属性设置为 True](master-detail-filtering-with-a-dropdownlist-cs/_static/image34.png)

**图 12**： 设置`AppendDataBoundItems`属性设为 True


之后这些更改，首次访问的页面选择"--选择一个类别-"选项并不显示任何产品时。


[![无产品都会显示在加载初始页](master-detail-filtering-with-a-dropdownlist-cs/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image35.png)

**图 13**： 显示在初始页面负载否产品 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image37.png))


因为选择了"--选择一个类别-"列表项时显示任何产品的原因是它的值是`-1`并且与数据库中有任何产品`CategoryID`的`-1`。 如果这是你想在此时完成，然后的行为 ！ 如果你想要显示的但是*所有*个类别时选择"--选择一个类别-"列表项时，返回到`ProductsBLL`类和自定义`GetProductsByCategoryID(categoryID)`方法，使其调用`GetProducts()`方法如果传递中*`categoryID`* 参数小于零：

[!code-csharp[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample2.cs)]

此处使用的方法是类似于我们用来显示所有供应商的方法返回[声明性参数](../basic-reporting/declarative-parameters-cs.md)教程中，尽管我们对于此示例使用的值为`-1`指示应在所有记录而不是检索`null`。 这是因为*`categoryID`* 参数的`GetProductsByCategoryID(categoryID)`方法需要作为整数值传递，而声明性参数教程中我们已传入的字符串输入参数。

图 14 显示了的屏幕截图`FilterByDropDownList.aspx`如果选择"--选择一个类别-"选项。 在这里，默认情况下显示的所有产品，用户可以通过选择特定类别，缩小显示。


[![所有产品都现在列出默认情况下](master-detail-filtering-with-a-dropdownlist-cs/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image38.png)

**图 14**： 所有产品都现在列出默认情况下 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image40.png))


## <a name="summary"></a>总结

显示按层次结构相关数据时，它通常用于呈现使用主/详细信息报表，用户可以从中启动仔细阅读的层次结构顶部的数据和向下钻取到详细信息数据。 在本教程中，我们探讨构建一个简单的母版/详细信息报告，显示所选的类别的产品。 这被通过使用 DropDownList 的类别和 GridView 属于所选类别的产品列表。

在中[下一教程](master-detail-filtering-with-two-dropdownlists-cs.md)我们将进一步 DropDownList 接口的一个步骤，使用两个 Dropdownlist。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [下一篇](master-detail-filtering-with-two-dropdownlists-cs.md)
