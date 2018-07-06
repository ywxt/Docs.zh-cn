---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: 验证使用 IDataErrorInfo 接口 (C#) |Microsoft Docs
author: StephenWalther
description: Stephen Walther 演示了如何通过在 model 类中实现 IDataErrorInfo 接口显示自定义验证错误消息。
ms.author: aspnetcontent
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: d3d3e379e5b2cfdd1385d724c0d9bf2a83ce339a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836022"
---
<a name="validating-with-the-idataerrorinfo-interface-c"></a>使用 IDataErrorInfo 接口 (C#) 进行验证
====================
通过[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther 演示了如何通过在 model 类中实现 IDataErrorInfo 接口显示自定义验证错误消息。


本教程的目的是说明一种方法在 ASP.NET MVC 应用程序中执行验证。 了解如何防止有人将 HTML 窗体提交而无需为所需的窗体字段提供值。 在本教程中，您将学习如何使用 IErrorDataInfo 接口来执行验证。

## <a name="assumptions"></a>假设

在本教程中，我将使用 MoviesDB 数据库和电影数据库表。 此表包含以下列：

<a id="0.5_table01"></a>


| **列名称** | **数据类型** | **允许 null 值** |
| --- | --- | --- |
| Id | Int | False |
| 标题 | Nvarchar(100) | False |
| 主管 | Nvarchar(100) | False |
| DateReleased | DateTime | False |


在本教程中，我可以使用 Microsoft 实体框架来生成我的数据库模型类。 实体框架生成的 Movie 类显示在图 1 中。


[![电影实体](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)

**图 01**: 电影实体 ([单击以查看实际尺寸的图像](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))


> [!NOTE] 
> 
> 若要了解有关使用实体框架生成您的数据库模型类的详细信息，请参阅我的教程，标题为使用 Entity Framework 创建模型类。


## <a name="the-controller-class"></a>控制器类

我们使用主控制器到列表的电影，并创建新影片。 此类的代码包含在列表 1 中。

**代码清单 1-Controllers\HomeController.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

在列表 1 中的 Home 控制器类包含两个 create （） 操作。 第一个操作会显示用于创建新的电影的 HTML 窗体。 第二个 create （） 操作执行新电影的实际插入到数据库。 显示的第一个 create （） 操作的窗体提交到服务器时，将调用第二个 create （） 操作。

请注意第二个 create （） 操作中包含以下代码行：

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

验证错误时，IsValid 属性返回 false。 在这种情况下，重新创建视图，它包含用于创建电影的 HTML 窗体。

## <a name="creating-a-partial-class"></a>创建一个分部类

由实体框架生成的 Movie 类。 展开解决方案资源管理器窗口中的 MoviesDBModel.edmx 文件并在代码编辑器中打开 MoviesDBModel.Designer.cs 文件访问时，可以看到 Movie 类的代码 （请参见图 2）。


[![电影实体的代码](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)

**图 02**： 电影实体的代码 ([单击以查看实际尺寸的图像](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))


Movie 类是分部类。 这意味着，我们可以添加具有相同名称的扩展的 Movie 类功能的另一个分部类。 我们将向新的分部类添加我们的验证逻辑。

向 Models 文件夹中添加清单 2 中的类。

**代码清单 2-Models\Movie.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

请注意，代码清单 2 中的类包含*分部*修饰符。 任何方法或属性将添加到此类成为由实体框架生成的 Movie 类的一部分。

## <a name="adding-onchanging-and-onchanged-partial-methods"></a>添加 OnChanging 和 OnChanged 分部方法

当实体框架生成的实体类时，实体框架分部方法向类添加了自动。 实体框架生成 OnChanging 和 OnChanged 对应于每个属性的类的分部方法。

对于 Movie 类，实体框架将创建以下方法：

- OnIdChanging
- OnIdChanged
- OnTitleChanging
- OnTitleChanged
- OnDirectorChanging
- OnDirectorChanged
- OnDateReleasedChanging
- OnDateReleasedChanged

相应的属性发生更改之前，OnChanging 方法称为右。 OnChanged 方法调用正确后更改的属性。

您可以利用这些分部方法以将验证逻辑添加到电影类。 更新列表 3 中的 Movie 类验证的标题和主管属性分配非空值。

> [!NOTE] 
> 
> 分部方法是不需要实现的类中定义的方法。 如果未实现分部方法，编译器会删除方法签名，并因此方法的所有调用都是没有与分部方法关联的运行时成本。 在 Visual Studio 代码编辑器中，您可以通过键入关键字添加的分部方法*分部*跟一个空格，若要查看的部分实现列表。


**代码清单 3-Models\Movie.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

例如，如果尝试将空字符串分配到的 Title 属性，然后一条错误消息分配给一个名为词典\_错误。

在此情况下，执行任何操作实际上将空字符串分配到的 Title 属性，但发生错误添加到私有\_错误字段。 我们需要实现 IDataErrorInfo 接口来公开这些验证错误到 ASP.NET MVC 框架。

## <a name="implementing-the-idataerrorinfo-interface"></a>实现 IDataErrorInfo 接口

自第一个版本，IDataErrorInfo 接口已经成为.NET framework 的一部分。 此接口是一个非常简单的接口：

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

如果一个类实现 IDataErrorInfo 接口，ASP.NET MVC 框架将创建类的实例时使用此接口。 例如，主页控制器 create （） 操作接受 Movie 类的实例：

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

ASP.NET MVC 框架创建电影使用模型联编程序 (DefaultModelBinder) 传递给 create （） 操作的实例。 模型联编程序负责通过将 HTML 窗体字段绑定到 Movie 对象的实例创建电影对象的实例。

DefaultModelBinder 检测类实现 IDataErrorInfo 接口。 如果一个类实现此接口的模型联编程序会调用类的每个属性的 IDataErrorInfo.this 索引器。 如果索引器返回一条错误消息的模型联编程序将添加到模型状态自动此错误消息。

DefaultModelBinder 还会检查 IDataErrorInfo.Error 属性。 此属性用于表示与类关联的非属性特定验证错误。 例如，你可能想要强制实施依赖于的 Movie 类的多个属性的值的验证规则。 在这种情况下，您将从错误属性返回验证错误。

列表 4 中更新的 Movie 类实现 IDataErrorInfo 接口。

**列表 4-Models\Movie.cs （实现 IDataErrorInfo）**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

列表 4 中的索引器属性检查\_错误集合，以查看它是否包含属性名称对应的密钥传递给索引器。 如果没有与属性关联的验证错误则返回空字符串。

不需要修改主控制器，以任何方式使用修改后的 Movie 类。 图 3 中显示的页说明了当标题或总监窗体字段中不输入任何值时，会发生什么情况。


[![自动创建的操作方法](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)

**图 03**： 具有缺失值的窗体 ([单击以查看实际尺寸的图像](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))


请注意 DateReleased 值自动进行验证。 因为 DateReleased 属性不接受 NULL 值，DefaultModelBinder 验证错误，此属性会自动生成时它不具有值。 如果你想要修改的错误消息的 DateReleased 属性，则需要创建自定义模型联编程序。

## <a name="summary"></a>总结

在本教程中，您学习了如何使用 IDataErrorInfo 接口生成验证错误消息。 首先，我们创建了部分的 Movie 类的部分实体框架所生成的 Movie 类功能进行扩展。 接下来，我们的 Movie 类 OnTitleChanging() 和 OnDirectorChanging() 分部方法添加验证逻辑。 最后，我们实现了 IDataErrorInfo 接口以便公开这些验证消息到 ASP.NET MVC 框架。

> [!div class="step-by-step"]
> [上一页](performing-simple-validation-cs.md)
> [下一页](validating-with-a-service-layer-cs.md)
