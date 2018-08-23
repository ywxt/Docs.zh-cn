---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: 使用模型绑定和 web 窗体的项目添加业务逻辑层 |Microsoft Docs
author: tfitzmac
description: 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定使数据交互...更多直接-
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: 2c54c0a635c662c8740aa7f9b6bd02cd71913e24
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833478"
---
<a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a>使用模型绑定和 web 窗体的项目添加业务逻辑层
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定可以更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource） 的数据交互。 本系列开始介绍性材料，后续教程将移动到更高级的概念。
> 
> 本教程演示如何使用业务逻辑层模型绑定。 您将设置 OnCallingDataMethods 成员以指定当前页以外的其他对象用于调用数据方法。
> 
> 本教程中创建的项目为基础[早期](retrieving-data.md)在本系列的部分。
> 
> 你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整的项目 C# 或 vb。 可下载代码适用于 Visual Studio 2012 或 Visual Studio 2013。 它使用 Visual Studio 2012 模板，为在本教程中所示的 Visual Studio 2013 模板稍有不同。


## <a name="what-youll-build"></a>你将生成

模型绑定，可将数据交互代码放在 web 页的代码隐藏文件中或在单独的业务逻辑类中。 前面的教程已经演示了如何使用代码隐藏文件进行数据交互的代码。 此方法适用于小型站点，但它可能导致时维护大型站点代码重复和面临更大困难。 它可以是以编程方式测试由于没有抽象层驻留在代码隐藏文件中的代码非常困难。

若要集中进行数据交互代码，可以创建包含所有与数据进行交互的逻辑将业务逻辑层。 然后从您的 web 页面中调用业务逻辑层。 本教程介绍如何将所有已在前面的教程到业务逻辑层，编写的代码移动，然后使用该代码从页中。

在本教程中，你将：

1. 将代码从代码隐藏文件移到业务逻辑层
2. 更改数据绑定控件，以调用业务逻辑层中的方法

## <a name="create-business-logic-layer"></a>创建业务逻辑层

现在，您将创建在 web 页面中调用的类。 此类中的方法看起来类似于前面教程中使用的方法，并包括值提供程序属性。

首先，添加一个名为的新文件夹**BLL**。

![添加文件夹](adding-business-logic-layer/_static/image1.png)

在 BLL 文件夹中，创建一个名为的新类**SchoolBL.cs**。 它将包含所有原先位于代码隐藏文件中的数据操作。 方法是在代码隐藏文件中，方法几乎相同，但将包括一些更改。

请注意，最重要的更改是无法再执行中的实例中的代码**页**类。 页类包含**TryUpdateModel**方法并**ModelState**属性。 当此代码移到业务逻辑层中时，再也不调用这些成员的页类的实例。 若要解决此问题，必须添加**ModelMethodContext**访问 TryUpdateModel 或 ModelState 任何方法参数。 使用此 ModelMethodContext 参数来调用 TryUpdateModel 或检索 ModelState。 不需要更改 web 页后，可以为此新参数帐户中的任何内容。

将以下代码替换为 SchoolBL.cs 中的代码。

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a>修改现有页面以从业务逻辑层中检索数据

最后，将从在使用业务逻辑层的代码隐藏文件中使用查询来转换 Students.aspx、 AddStudent.aspx 和 Courses.aspx 的页。

面向学生、 AddStudent 和课程的代码隐藏文件，在删除或注释掉以下的查询方法：

- studentsGrid\_GetData
- studentsGrid\_UpdateItem
- studentsGrid\_DeleteItem
- addStudentForm\_InsertItem
- coursesGrid\_GetData

现在应在与数据操作相关的代码隐藏文件中具有任何代码。

**OnCallingDataMethods**事件处理程序，您可以指定要用于数据方法的对象。 Students.aspx，在添加该事件处理程序的值并将数据方法的名称更改为业务逻辑类中方法的名称。

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

在 Students.aspx 的代码隐藏文件，定义 CallingDataMethods 事件的事件处理程序。 在此事件处理程序中，指定数据操作的业务逻辑类。

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

在 AddStudent.aspx，进行类似更改。

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

在 Courses.aspx，进行类似更改。

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

运行应用程序，并注意到的所有页函数与在其之前。 验证逻辑也可以正常工作。

## <a name="conclusion"></a>结束语

在本教程中，你重新结构化应用程序以使用数据访问层和业务逻辑层。 指定数据控件使用不是当前页的数据操作的对象。

> [!div class="step-by-step"]
> [上一篇](using-query-string-values-to-retrieve-data.md)
