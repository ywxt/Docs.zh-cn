---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体的第 8 部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用实体框架的 ASP.NET Web 窗体应用程序。 示例应用程序是...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: f5ad2c1caf6036a0d8ee2ebbd07de60009090f1b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374047"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a>Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体的第 8 部分
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。 有关教程系列的信息，请参阅[系列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a>使用动态数据功能进行格式化和验证数据

在上一教程中，您将实现存储的过程。 本教程将演示如何动态数据功能可提供以下优势：

- 字段是自动的基于其数据类型的显示格式。
- 字段将自动验证基于其数据类型。
- 可以在要自定义格式设置和验证行为的数据模型中添加元数据。 当执行此操作，可以只在一个位置添加格式设置和验证规则，并且它们正在自动应用无处不在您访问使用动态数据控件字段。

为了阐释其工作方式，将更改用于显示和编辑现有字段的控件*Students.aspx*页上，并且您会将格式设置和验证元数据添加到的名称和日期字段`Student`实体类型。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a>使用 DynamicField 和 DynamicControl 控件

打开*Students.aspx*页并在`StudentsGridView`控件替换**名称**并**注册日期**`TemplateField`元素使用以下标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

此标记使用`DynamicControl`控件来代替`TextBox`并`Label`学生中的控件名称模板字段，并使用`DynamicField`注册日期的控件。 不指定任何格式字符串。

添加`ValidationSummary`后控制`StudentsGridView`控件。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

在`SearchGridView`控件替换的标记**名称**并**注册日期**作为您的列中的操作`StudentsGridView`控件，但省略`EditItemTemplate`元素。 `Columns`元素的`SearchGridView`控件现在包含以下标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

打开*Students.aspx.cs*并添加以下`using`语句：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

添加一个处理程序的页面的`Init`事件：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

此代码指定动态数据将提供格式设置和在这些数据绑定控件中的字段的验证`Student`实体。 如果在运行页面时收到一条错误消息，如下例所示，则通常意味着已忘记调用`EnableDynamicData`中的方法`Page_Init`:

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

运行页。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)

在中**注册日期**列中，因为属性类型为时间除了日期显示`DateTime`。 需要修复的更高版本。

现在，请注意，动态数据自动提供了基本的数据验证。 例如，单击**编辑**，清除日期字段中，单击**更新**，并查看，动态数据自动使此必填的字段因为值不是数据模型中可以为 null。 字段和中的错误消息后，该页面显示星号`ValidationSummary`控件：

[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)

可以省略`ValidationSummary`管理，因为您可以将鼠标指针拖通过星号可查看错误消息：

[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)

动态数据还将验证输入中的数据**注册日期**字段是有效的日期：

[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)

正如您所看到的这是一般性错误消息。 下一节中您将了解如何自定义消息，以及验证和格式设置规则。

## <a name="adding-metadata-to-the-data-model"></a>将元数据添加到数据模型

通常情况下，你想要自定义动态数据提供的功能。 例如，可能会更改数据的显示方式和错误消息的内容。 你通常还自定义数据验证规则，以提供比动态数据提供更多的功能自动基于数据类型。 若要执行此操作，您创建对应于实体类型的分部类。

在中**解决方案资源管理器**，右键单击**ContosoUniversity**项目，选择**添加引用**，并添加对引用`System.ComponentModel.DataAnnotations`。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)

在中*DAL*文件夹中，创建一个新类文件，将其命名*Student.cs*，并在其中的模板代码替换为以下代码。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

此代码将创建的分部类`Student`实体。 `MetadataType`特性应用于此分部类标识你要用于指定元数据的类。 元数据类可以具有任何名称，但使用实体名称加"元数据"是一种常见做法。

应用于元数据类中的属性的属性指定格式化、 验证、 规则和错误消息。 如下所示的属性将具有以下结果：

- `EnrollmentDate` 将显示为日期 （不含时间）。
- 这两个名称字段必须是 25 个字符或小于长度和自定义错误消息中提供。
- 这两个名称字段是必需的并提供自定义错误消息。

运行*Students.aspx*页，并查看现在没有时间的情况下显示日期：

[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)

编辑行并尝试进行清除名称字段中的值。 只要将一个字段，然后再单击显示，指示字段错误星号**更新**。 当您单击**更新**，页将显示你指定的错误消息文本。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)

尝试输入长度超过 25 个字符的名称，单击**更新**，和页显示您指定的错误消息文本。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)

现在，已设置了数据模型元数据中的这些格式设置和验证规则，规则将自动应用，用于显示或允许对这些字段，更改每一页上，只要您使用`DynamicControl`或`DynamicField`控件。 这将减少必须编写，后者将编程和测试更加轻松、 冗余代码量，它可确保数据格式设置和验证是在应用程序保持一致。

## <a name="more-information"></a>详细信息

本系列如何开始使用实体框架的教程到此结束。 对于可帮助你了解如何使用实体框架的更多资源，请继续[下一步的实体框架教程系列中的第一个教程](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)或访问以下站点：

- [实体框架常见问题](http://www.ef-faq.org/introduction.html)
- [实体框架团队博客](https://blogs.msdn.com/b/adonet/)
- [MSDN 库中的实体框架](https://msdn.microsoft.com/library/bb399572.aspx)
- [MSDN 数据开发人员中心中的实体框架](https://msdn.microsoft.com/data/ef.aspx)
- [MSDN 库中的 EntityDataSource Web 服务器控件概述](https://msdn.microsoft.com/library/cc488502.aspx)
- [EntityDataSource 控件的 MSDN Library 中的 API 参考](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [MSDN 上的 entity Framework 论坛](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [Julie Lerman 的博客](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [上一篇](the-entity-framework-and-aspnet-getting-started-part-7.md)
