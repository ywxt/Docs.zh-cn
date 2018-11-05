---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: 更新、 删除和创建数据与模型绑定和 web 窗体 |Microsoft Docs
author: Rick-Anderson
description: 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定使数据交互...更多直接-
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 127543b0696b01f136b340d07f6f806b6a6fb1eb
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021568"
---
<a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a>更新、 删除和创建数据与模型绑定和 web 窗体
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定可以更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource） 的数据交互。 本系列开始介绍性材料，后续教程将移动到更高级的概念。
> 
> 本教程演示如何创建、 更新和删除与模型绑定的数据。 您将设置以下属性：
> 
> - DeleteMethod
> - InsertMethod
> - UpdateMethod
> 
> 这些属性接收处理相应的操作的方法的名称。 在该方法中，你提供的逻辑与数据进行交互。
> 
> 本教程基于第一个中创建的项目[一部分](retrieving-data.md)在本系列。
> 
> 你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整的项目 C# 或 vb。 可下载代码适用于 Visual Studio 2012 或 Visual Studio 2013。 它使用 Visual Studio 2012 模板，为在本教程中所示的 Visual Studio 2013 模板稍有不同。


## <a name="what-youll-build"></a>你将生成

在本教程中，你将：

1. 添加动态数据模板
2. 通过模型绑定方法启用更新和删除数据
3. 将数据验证规则应用-启用在数据库中创建一个新的记录

## <a name="add-dynamic-data-templates"></a>添加动态数据模板

若要提供最佳用户体验和最大程度减少代码重复，将使用动态数据模板。 通过安装 NuGet 包可以轻松地将预建的动态数据模板集成到您的现有网站。

从**管理 NuGet 包**，安装**DynamicDataTemplatesCS**。

![动态数据模板](updating-deleting-and-creating-data/_static/image1.png)

请注意，你的项目现在包含一个名为文件夹**DynamicData**。 在该文件夹中，您将找到自动应用于 web 窗体中的动态控件的模板。

![动态数据文件夹](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a>启用更新和删除

使用户能够更新和删除数据库中的记录是检索数据的过程非常相似。 在中**UpdateMethod**并**DeleteMethod**属性，指定执行这些操作，方法的名称。 GridView 控件后，您还可以指定自动生成的编辑和删除按钮。 以下突出显示的代码显示了对 GridView 代码新增的内容。

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

在代码隐藏文件中，添加 using 语句**System.Data.Entity.Infrastructure**。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

然后，添加以下更新和删除方法。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

**TryUpdateModel**方法将 web 窗体中匹配的数据绑定值应用于数据项。 根据 id 参数的值检索数据项目。

## <a name="enforce-validation-requirements"></a>强制实施验证要求

将数据更新时，会自动强制执行应用于 Student 类中的 FirstName、 LastName 和 Year 属性的验证特性。 DynamicField 控件添加验证特性所基于的客户端和服务器验证程序。 FirstName 和 LastName 属性都是必需。 名字不能超过 20 个字符的长度，并且姓氏不能超过 40 个字符。 年份必须是有效的 AcademicYear 枚举值。

如果用户不符合验证要求之一，将不会继续更新。 若要查看错误消息，请添加 GridView 上方的一个 ValidationSummary 控件。 若要显示从模型绑定验证错误，请设置**ShowModelStateErrors**属性设置为**true**。 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

运行 web 应用程序，并更新和删除的任何记录。

![更新数据](updating-deleting-and-creating-data/_static/image3.png)

请注意，如果在编辑模式下年属性的值自动呈现为一个下拉列表。 Year 属性是枚举值，并枚举值的动态数据模板指定一个下拉列表以进行编辑。 您可以找到该模板通过打开**枚举\_Edit.ascx**中的文件**DynamicData**/**FieldTemplates**文件夹。

如果你提供有效的值，在更新成功完成。 如果您违反验证要求之一，更新将不会继续并中网格之上显示一条错误消息。

![错误消息](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a>添加新记录

GridView 控件不包括**InsertMethod**属性，因此不能使用与模型绑定添加一个新的记录。 您可以找到在 InsertMethod 属性**FormView**， **DetailsView**，或**ListView**控件。 在本教程中，您将使用 FormView 控件添加新记录。

首先，将链接添加到新页面将创建用于添加新记录。 ValidationSummary 上方添加：

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

在学生页上的内容的顶部将显示新的链接。

![新链接](updating-deleting-and-creating-data/_static/image5.png)

然后，添加新 web 窗体使用母版页，并将其命名**AddStudent**。 选择 Site.Master 作为主页面。

将呈现用于添加新的学生使用的字段**DynamicEntity**控件。 DynamicEntity 控件呈现 ItemType 属性中指定的类中的可编辑的属性。 StudentID 属性标记有 **[scaffoldcolumn （false)]** 属性以便不呈现。 在 AddStudent 页上的主要内容占位符，添加以下代码。

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

在代码隐藏文件 (AddStudent.aspx.cs) 中，添加**使用**语句**ContosoUniversityModelBinding.Models**命名空间。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

然后，添加以下方法来指定如何插入一条新记录和取消按钮的事件处理程序。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

保存的所有更改。

运行 web 应用程序并创建新的学生。

![添加新学生](updating-deleting-and-creating-data/_static/image6.png)

单击**插入**并注意已创建的新学生。

![显示新学生](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a>结束语

在本教程中，您可以启用更新、 删除和创建数据。 确保验证规则将应用与数据交互时。

在接下来[教程](sorting-paging-and-filtering-data.md)在本系列中，将启用排序、 分页和筛选数据。

> [!div class="step-by-step"]
> [上一页](retrieving-data.md)
> [下一页](sorting-paging-and-filtering-data.md)
