---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 使用数据批注验证程序 (VB) 验证 |Microsoft Docs
author: microsoft
description: 充分利用数据批注模型联编程序来执行验证的 ASP.NET MVC 应用程序中。 了解如何使用不同类型的验证程序...
ms.author: aspnetcontent
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 9d76596ede0763bde3c84dca4a545be250a3062c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837418"
---
<a name="validation-with-the-data-annotation-validators-vb"></a>使用数据批注验证程序 (VB) 验证
====================
by [Microsoft](https://github.com/microsoft)

> 充分利用数据批注模型联编程序来执行验证的 ASP.NET MVC 应用程序中。 了解如何使用不同类型的验证程序属性和 Microsoft 实体框架中处理它们。


在本教程中，您将学习如何使用数据批注验证程序在 ASP.NET MVC 应用程序中执行验证。 使用数据批注验证程序的优点是它们使您能够执行验证，只需通过添加一个或多个属性 – 例如，Required 或 StringLength 属性 – 目标设定为类属性。

可以使用数据批注验证程序之前，必须下载数据批注模型联编程序。 可以通过单击从 CodePlex 网站下载数据批注模型绑定器示例[此处](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)。


请务必了解数据批注模型联编程序不是 Microsoft ASP.NET MVC 框架的正式组成部分。 尽管数据批注模型联编程序由 Microsoft ASP.NET MVC 团队创建的但 Microsoft 不提供对数据批注模型联编程序的官方产品支持所述和本教程中使用。


## <a name="using-the-data-annotation-model-binder"></a>使用数据批注模型联编程序

若要在 ASP.NET MVC 应用程序中使用数据批注模型联编程序，首先需要添加对该 Microsoft.Web.Mvc.DataAnnotations.dll 程序集 System.ComponentModel.DataAnnotations.dll 程序集的引用。 选择菜单选项**项目中，添加引用**。 接下来，单击**浏览**选项卡上，浏览到下载 （并解压缩） 数据批注模型联编程序示例的位置 (请参阅**图 1**)。

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**图 1**： 添加对数据批注模型联编程序的引用 ([单击以查看实际尺寸的图像](validation-with-the-data-annotation-validators-vb/_static/image3.png))

选择 Microsoft.Web.Mvc.DataAnnotations.dll 程序集和 System.ComponentModel.DataAnnotations.dll 程序集，然后单击**确定**按钮。


不能使用与数据批注模型联编程序的.NET Framework Service Pack 1 中包含的 System.ComponentModel.DataAnnotations.dll 程序集。 您必须使用数据批注模型绑定器示例下载中包含的 System.ComponentModel.DataAnnotations.dll 程序集的版本。


最后，您需要在 Global.asax 文件中注册 DataAnnotations 模型联编程序。 将以下代码行添加到应用程序\_start （） 事件处理程序，以便应用程序\_start （） 方法如下所示：

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

这行代码将 DataAnnotationsModelBinder 注册为整个 ASP.NET MVC 应用程序的默认模型联编程序。

## <a name="using-the-data-annotation-validator-attributes"></a>使用数据注释验证程序属性

当您使用数据批注模型联编程序时，使用验证程序属性来执行验证。 System.ComponentModel.DataAnnotations 命名空间包含以下验证程序属性：

- 范围-可以验证是否属性的值介于指定的值范围之间。
- ReqularExpression – 可以验证是否属性的值与指定正则表达式模式相匹配。
- 所需 – 使你能够将标记为必需属性。
- StringLength – 可用于指定字符串属性的最大长度。
- 验证-所有验证程序属性的基类。

> [!NOTE] 
> 
> 如果验证需求不满足任何标准的验证程序然后始终必须通过从基本的验证特性继承新的验证程序属性创建自定义验证程序属性的选项。


中的产品类**清单 1**演示了如何使用这些验证程序属性。 名称、 说明和 UnitPrice 属性标记所需的方式。 名称属性必须是少于 10 个字符的字符串长度。 最后，UnitPrice 属性必须与表示货币金额的正则表达式模式匹配。

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**代码清单 1**: Models\Product.vb

Product 类说明了如何使用一个附加属性： DisplayName 属性。 DisplayName 属性，可修改的属性的名称，当属性显示在一条错误消息。 而不是显示错误消息"单价字段必填"可以显示错误消息"价格字段是必填"。

> [!NOTE] 
> 
> 如果你想要完全自定义验证程序显示的错误消息然后可以将此类验证程序的 ErrorMessage 属性分配自定义错误消息： `<Required(ErrorMessage:="This field needs a value!")>`


可以使用中的产品类**清单 1** create （） 控制器操作中使用**代码清单 2**。 模型状态包含的任何错误时，此控制器操作重新显示创建视图。

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**代码清单 2**: Controllers\ProductController.vb

最后，您可以创建中的视图**清单 3**右键单击 create （） 操作并选择菜单选项**添加视图**。 作为模型类使用 Product 类来创建强类型化视图。 选择**创建**视图内容的下拉列表中 (请参阅**图 2**)。

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**图 2**： 添加创建视图

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**代码清单 3**: Views\Product\Create.aspx

> [!NOTE] 
> 
> 从生成的创建表单中删除 Id 字段**添加视图**菜单选项。 Id 字段对应于一个标识列，因为您不想允许用户输入此字段的值。


如果提交的窗体创建产品，并且不执行操作的必填字段，输入值则中的验证错误消息**图 3**显示。

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**图 3**： 缺少必填的字段

如果输入无效的货币金额，则中的错误消息**图 4**显示。

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**图 4**： 无效的货币金额

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>通过 Entity Framework 使用数据批注验证程序

如果使用 Microsoft 实体框架来生成模型的数据类不能将验证程序特性应用直接向您的类。 由于实体框架设计器生成的模型类，的下次在设计器中进行任何更改将覆盖在 model 类的任何更改。

如果你想要使用实体框架生成的类中使用验证程序然后您需要创建元数据类。 将验证程序应用于元数据类，而不是应用的实际类验证程序。

例如，假设您创建使用实体框架的 Movie 类 (请参阅**图 5**)。 此外，假设你想要使电影标题和主管属性所需的属性。 在这种情况下，可以创建的分部类和元数据类中的**清单 4**。

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**图 5**： 实体框架所生成的 Movie 类

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**列表 4**: Models\Movie.vb

中的文件**清单 4**包含名为电影和 MovieMetaData 的两个类。 Movie 类是分部类。 它对应于由 DataModel.Designer.vb 文件中包含的实体框架生成的分部类。

目前，.NET framework 不支持部分属性。 因此，没有办法将验证程序特性应用于电影类 DataModel.Designer.vb 文件来将验证程序特性应用到在文件中定义的 Movie 类的属性定义的属性**清单 4**.

请注意，使用指向 MovieMetaData 类利用 MetadataType 特性修饰的电影分部类。 MovieMetaData 类包含属性的 Movie 类的代理属性。

验证程序属性应用于 MovieMetaData 类的属性。 所有标记为必需属性的标题、 总监和 DateReleased 属性。 必须将总监属性分配一个字符串，包含不超过 5 个字符。 最后，DisplayName 特性应用于 DateReleased 属性来显示错误消息，例如"日期已发布字段是必需"。 而不是错误"DateReleased 字段是必需。"

> [!NOTE] 
> 
> 请注意，不需要 MovieMetaData 类中的代理属性来表示相同的 Movie 类中的相应属性类型。 例如，主管属性是 Movie 类中的字符串属性和 MovieMetaData 类中的对象属性。


中的页**图 6**说明了电影属性的输入无效值时返回的错误消息。

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**图 6**： 通过 Entity Framework 使用验证程序 ([单击以查看实际尺寸的图像](validation-with-the-data-annotation-validators-vb/_static/image14.png))

## <a name="summary"></a>总结

在本教程中，您学习了如何利用数据批注模型联编程序来执行验证的 ASP.NET MVC 应用程序中。 您学习了如何使用不同类型的验证程序属性，例如，Required 和 StringLength 属性。 您还学习了如何使用 Microsoft 实体框架时使用这些属性。

> [!div class="step-by-step"]
> [上一篇](validating-with-a-service-layer-vb.md)
