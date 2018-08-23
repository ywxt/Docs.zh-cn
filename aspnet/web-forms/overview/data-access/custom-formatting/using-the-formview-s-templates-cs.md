---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-cs
title: 使用 FormView 的模板 (C#) |Microsoft Docs
author: rick-anderson
description: 与不同的 DetailsView，不由字段组成 FormView。 相反，使用模板呈现 FormView。 在本教程中我们将探讨使用 F....
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d3f062af-88cf-426d-af44-e41f32c41672
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-cs
msc.type: authoredcontent
ms.openlocfilehash: 1a7cf17d8cbd0a5a17a387b9a70336a1b06efde7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831672"
---
<a name="using-the-formviews-templates-c"></a>使用 FormView 的模板 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_14_CS.exe)或[下载 PDF](using-the-formview-s-templates-cs/_static/datatutorial14cs1.pdf)

> 与不同的 DetailsView，不由字段组成 FormView。 相反，使用模板呈现 FormView。 在本教程中我们将介绍使用 FormView 控件向呈现以显示不太严格的数据。


## <a name="introduction"></a>介绍

在最后两个教程中我们已了解如何自定义使用 Templatefield GridView 和 DetailsView 控件的输出。 Templatefield 允许的内容的特定字段进行高度自定义，但最后的 GridView 和 DetailsView 具有相当 boxy、 类似于网格的外观。 很多情况下，此类的类似网格的布局是理想的但有时需要更多的流畅、 不太严格的显示。 当显示一条记录，则可能使用 FormView 控件布局流畅。

与不同的 DetailsView，不由字段组成 FormView。 不能将 BoundField 或 TemplateField 添加到 FormView。 相反，使用模板呈现 FormView。 FormView 视为包含单个 TemplateField 的 DetailsView 控件。 FormView 支持以下模板：

- `ItemTemplate` 用于呈现特定的记录显示在 FormView
- `HeaderTemplate` 用来指定可选的标头行
- `FooterTemplate` 用来指定可选的页脚行
- `EmptyDataTemplate` 时 FormView`DataSource`缺少任何记录，`EmptyDataTemplate`用来代替`ItemTemplate`用于呈现控件的标记
- `PagerTemplate` 可用于为具有已启用分页的 FormViews 自定义分页界面
- `EditItemTemplate` / `InsertItemTemplate` 用于为 FormViews 支持此类功能的自定义的编辑界面或插入接口

在本教程中我们将介绍使用 FormView 控件向呈现以显示不太严格的产品。 而不是字段的名称、 类别、 供应商和 so on，FormView`ItemTemplate`将显示使用的标头元素组合这些值和一个`<table>`（参见图 1）。


[![在 DetailsView 中看到类似于网格的布局的细分的 FormView](using-the-formview-s-templates-cs/_static/image2.png)](using-the-formview-s-templates-cs/_static/image1.png)

**图 1**: FormView 跳出 Grid-Like 布局看到在 DetailsView 中 ([单击以查看实际尺寸的图像](using-the-formview-s-templates-cs/_static/image3.png))


## <a name="step-1-binding-the-data-to-the-formview"></a>步骤 1： 将数据绑定到 FormView

打开`FormView.aspx`页上，将从工具箱拖到设计器的 FormView。 当首次添加 FormView 它将显示为灰色的框，指示我们的`ItemTemplate`需要。


[![不能在设计器中呈现 FormView，直到提供 ItemTemplate](using-the-formview-s-templates-cs/_static/image5.png)](using-the-formview-s-templates-cs/_static/image4.png)

**图 2**: FormView 不能在设计器直到呈现`ItemTemplate`提供 ([单击以查看实际尺寸的图像](using-the-formview-s-templates-cs/_static/image6.png))


`ItemTemplate`可以 （通过声明性语法） 手动创建也可以是自动创建通过将 FormView 绑定到数据源控件通过设计器。 此自动创建`ItemTemplate`包含的列表的名称的每个字段和一个标签控件的 HTML`Text`属性绑定到字段的值。 此方法还自动-创建`InsertItemTemplate`和`EditItemTemplate`，这两种都填入输入控件为每个返回的数据源控件的数据字段。

如果你想要自动创建模板，FormView 的智能标记中添加的新 ObjectDataSource 控件调用`ProductsBLL`类的`GetProducts()`方法。 这将创建与 FormView `ItemTemplate`， `InsertItemTemplate`，和`EditItemTemplate`。 从源视图中，删除`InsertItemTemplate`和`EditItemTemplate`由于我们未关注创建 FormView 支持编辑或尚未插入。 下一步，清除标记内`ItemTemplate`，以便能够从在干净状态。

如果您而是将生成`ItemTemplate`手动，可以添加并配置 ObjectDataSource 通过从工具箱拖到设计器拖动。 但是，不设置 FormView 的数据源从设计器。 相反，请转到源视图，并手动设置 FormView`DataSourceID`属性设置为`ID`ObjectDataSource 的值。 接下来，手动添加`ItemTemplate`。

无论使用哪种方法，您决定要充分，此时 FormView 的声明性标记应看起来：


[!code-aspx[Main](using-the-formview-s-templates-cs/samples/sample1.aspx)]

请花费片刻时间来检查 FormView 的智能标记; 中的启用分页复选框这将添加`AllowPaging="True"`FormView 的声明性语法的属性。 此外，还要设置`EnableViewState`属性设置为 False。

## <a name="step-2-defining-theitemtemplates-markup"></a>步骤 2： 定义`ItemTemplate`的标记

使用 FormView 绑定到 ObjectDataSource 控件，以及配置为支持分页，我们已准备好指定的内容`ItemTemplate`。 对于本教程，让我们产品的名称显示在`<h3>`标题。 接下来，让我们使用对应的 HTML`<table>`显示四列表，其中第一个和第三个列列出属性名称，第二个和第四个列出它们的值中剩余的产品属性。

可以通过在设计器中的 FormView 的模板编辑界面中输入或通过声明性语法手动输入此标记。 使用模板时我通常会更快地直接使用声明性语法，但可使用您最熟悉的任何技术。

以下标记显示 FormView 声明性标记后的`ItemTemplate`的结构已完成：


[!code-aspx[Main](using-the-formview-s-templates-cs/samples/sample2.aspx)]

请注意，数据绑定语法中- `<%# Eval("ProductName") %>`，对于示例可以直接注入到模板的输出。 也就是说，它需要将分配给标签控件的`Text`属性。 例如，我们有`ProductName`中显示值`<h3>`元素使用`<h3><%# Eval("ProductName") %></h3>`，这对于产品 Chai 将呈现为`<h3>Chai</h3>`。

`ProductPropertyLabel`并`ProductPropertyValue`CSS 类用于指定的产品属性名称和值中的样式`<table>`。 这些 CSS 类中定义`Styles.css`，并导致要是加粗和右对齐，并添加右填充属性值的属性名称。

由于没有任何 CheckBoxFields 附带 FormView，以便显示`Discontinued`值必须为一个复选框添加自己的复选框控件。 `Enabled`属性设置为 False，只读的使其和的复选框`Checked`属性绑定到的值`Discontinued`数据字段。

使用`ItemTemplate`完成后，产品信息是更为流畅的方式显示。 与 FormView (图 4) 在本教程中生成的输出进行比较的最后一个教程 (图 3) 的 DetailsView 输出。


[![刚性 DetailsView 输出](using-the-formview-s-templates-cs/_static/image8.png)](using-the-formview-s-templates-cs/_static/image7.png)

**图 3**： 刚性 DetailsView Output ([单击以查看实际尺寸的图像](using-the-formview-s-templates-cs/_static/image9.png))


[![流畅的 FormView 输出](using-the-formview-s-templates-cs/_static/image11.png)](using-the-formview-s-templates-cs/_static/image10.png)

**图 4**： 流体 FormView Output ([单击以查看实际尺寸的图像](using-the-formview-s-templates-cs/_static/image12.png))


## <a name="summary"></a>总结

GridView 和 DetailsView 控件可以有自定义使用 Templatefield 其输出，而同时仍以类似网格的 boxy 格式呈现其数据。 当需要显示一条记录以便使用不太严格的布局，FormView 是理想之选。 DetailsView，如 FormView 呈现来自单个记录其`DataSource`，但与 DetailsView 不同，它由只是个模板组成，不支持字段。

正如我们看到在本教程中，FormView 允许更灵活的布局时显示一条记录。 将来我们将介绍 DataList 和 Repeater 控件，这提供相同级别的 FormsView，所需的灵活性，但可以显示多个记录 （如 GridView) 的教程。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程是 E.R.导致审阅者 Gilmore。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](using-templatefields-in-the-detailsview-control-cs.md)
> [下一页](displaying-summary-information-in-the-gridview-s-footer-cs.md)
