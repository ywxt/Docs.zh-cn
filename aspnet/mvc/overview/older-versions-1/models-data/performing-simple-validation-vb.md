---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
title: 执行简单验证 (VB) |Microsoft Docs
author: StephenWalther
description: 了解如何在 ASP.NET MVC 应用程序中执行验证。 在本教程中，Stephen Walther 引入到模型状态和验证 HTML 帮助程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: df6cf4b7-0bb3-4c4e-b17a-bd78a759a6bc
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 26900229630b25affe21a5bb801ef0247711d26b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399456"
---
<a name="performing-simple-validation-vb"></a>执行简单验证 (VB)
====================
通过[Stephen Walther](https://github.com/StephenWalther)

> 了解如何在 ASP.NET MVC 应用程序中执行验证。 在本教程中，Stephen Walther 引入到模型状态和验证 HTML 帮助程序。


本教程的目的是说明如何执行验证的 ASP.NET MVC 应用程序中。 例如，您将了解如何防止有人提交窗体不包含必填字段的值。 了解如何使用模型状态和验证 HTML 帮助程序。

## <a name="understanding-model-state"></a>了解模型状态

使用模型状态-或模型状态字典的更准确地说，来表示验证错误。 例如，在列表 1 中的 create （） 操作将产品类添加到数据库之前会验证产品类的属性。


我这里不建议将你验证或数据库的逻辑添加到控制器。 控制器应包含仅与应用程序流控制相关的逻辑。 我们正采取一种快捷方式为简单起见。


**代码清单 1-Controllers\ProductController.vb**

[!code-vb[Main](performing-simple-validation-vb/samples/sample1.vb)]

在列表 1 中，Product 类的名称、 说明和 UnitsInStock 属性进行验证。 如果这些属性的任何失败的验证测试到模型状态字典 （由控制器类的 ModelState 属性） 添加一个错误。

如果在模型状态中有任何错误 ModelState.IsValid 属性返回 false。 在这种情况下，创建一个新的产品的 HTML 窗体将重新显示。 否则，如果没有任何验证错误，则新产品添加到数据库中。

## <a name="using-the-validation-helpers"></a>使用验证帮助程序

ASP.NET MVC 框架包括两个验证帮助程序： Html.ValidationMessage() 帮助器和 Html.ValidationSummary() 帮助器。 在视图中使用这两个帮助显示验证错误消息。

由 ASP.NET MVC 基架自动生成的创建和编辑视图中使用的 Html.ValidationMessage() 和 Html.ValidationSummary() 帮助器。 请按照下列步骤生成的创建视图：

1. 右键单击产品控制器中的 create （） 操作，然后选择菜单选项**添加视图**（参见图 1）。
2. 在中**添加视图**对话框中，选中复选框标记为**创建强类型化视图**（请参见图 2）。
3. 从**查看数据类**下拉列表中，选择 Product 类。
4. 从**查看内容**下拉列表中，选择创建。
5. 单击“添加”按钮。


请确保生成应用程序之前添加的视图。 否则，类的列表不会显示在**查看数据类**下拉列表中。


[![新建项目对话框](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)

**图 01**： 添加视图 ([单击以查看实际尺寸的图像](performing-simple-validation-vb/_static/image2.png))


[![新建项目对话框](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)

**图 02**： 创建强类型化视图 ([单击以查看实际尺寸的图像](performing-simple-validation-vb/_static/image4.png))


完成这些步骤后，在代码清单 2 中获取创建视图。

**代码清单 2-Views\Product\Create.aspx**

[!code-aspx[Main](performing-simple-validation-vb/samples/sample2.aspx)]

在代码清单 2 Html.ValidationSummary() 帮助器调用立即上方的 HTML 窗体。 此帮助器用于显示验证错误消息的列表。 Html.ValidationSummary() 帮助程序呈现项目符号列表中的错误。

Html.ValidationMessage() 帮助器旁边的 HTML 窗体字段的每个调用。 此帮助器用于显示窗体字段的右边一条错误消息。 在代码清单 2 的情况下 Html.ValidationMessage() 帮助程序错误时显示一个星号。

图 3 中的页说明了呈现的验证帮助程序，在窗体提交使用缺少的字段和无效值时的错误消息。


[![新建项目对话框](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)

**图 03**： 提交问题与创建视图 ([单击以查看实际尺寸的图像](performing-simple-validation-vb/_static/image6.png))


请注意，HTML 的外观输入验证错误时，还会修改字段。 Html.TextBox() 帮助器呈现*类 ="输入验证错误"* 属性验证错误时由 Html.TextBox() 帮助器呈现的属性与相关联。

有用于控制的验证错误的外观的三个级联样式表类：

- 输入验证错误的应用于&lt;输入&gt;Html.TextBox() 帮助程序呈现的标记。
- 字段验证错误的应用于&lt;s p a n&gt; Html.ValidationMessage() 帮助程序呈现的标记。
- 验证摘要错误-应用于&lt;ul&gt; Html.ValidationSumamry() 帮助程序呈现的标记。

可以修改这些级联样式表类，并因此通过修改 Site.css 文件内容的文件夹中修改的验证错误，外观。

> [!NOTE] 
> 
> HtmlHelper 类包括只读的静态属性，检索验证的名称与相关的 CSS 类。 ValidationInputCssClassName、 ValidationFieldCssClassName 和 ValidationSummaryCssClassName 命名这些静态属性。


## <a name="prebinding-validation-and-postbinding-validation"></a>Prebinding 验证和 Postbinding 验证

如果提交用于创建一种产品，HTML 窗体和 price 字段和库存量字段没有值输入值无效，则将获得图 4 中显示的验证消息。 这些验证错误消息来自何处？


[![新建项目对话框](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)

**图 04**: Prebinding 验证错误 ([单击以查看实际尺寸的图像](performing-simple-validation-vb/_static/image8.png))


有两种类型实际验证错误消息的那些之前 HTML 窗体字段绑定到一个类，这些生成的窗体字段绑定到类后生成。 换而言之，有 prebinding 验证错误和 postbinding 验证错误。

在列表 1 中在产品控制器公开的 create （） 操作接受产品类的实例。 创建方法的签名如下所示：

[!code-vb[Main](performing-simple-validation-vb/samples/sample3.vb)]

创建窗体中的 HTML 窗体字段的值由称为模型绑定器绑定到 productToCreate 类。 默认模型联编程序将添加一条错误消息到模型状态自动时它不能将窗体字段绑定到窗体属性。

默认模型联编程序不能绑定到 Product 类的价格属性字符串"apple"。 无法将字符串分配给十进制属性。 因此，模型绑定器将错误添加到模型状态。

默认模型联编程序也不能将值执行任何操作给不接受值执行任何操作的属性。 具体而言，模型绑定器不能分配值执行任何操作的 UnitsInStock 属性。 再次重申，模型联编程序将放弃运行，并将一条错误消息添加到模型状态。

如果你想要自定义这些外观 prebinding 错误消息，然后需要创建这些消息的资源字符串。

## <a name="summary"></a>总结

本教程的目的是验证的介绍基本的 ASP.NET MVC 框架中机制。 您学习了如何使用模型状态和验证 HTML 帮助程序。 我们还讨论了 prebinding 和 postbinding 验证之间的区别。 在其他教程中，我们将讨论移动您的验证代码超出你的控制器和为模型类的各种策略。

> [!div class="step-by-step"]
> [上一页](displaying-a-table-of-database-data-vb.md)
> [下一页](validating-with-the-idataerrorinfo-interface-vb.md)
