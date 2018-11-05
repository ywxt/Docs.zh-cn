---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: 与模型绑定和 web 窗体集成 JQuery UI Datepicker |Microsoft Docs
author: Rick-Anderson
description: 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定使数据交互...更多直接-
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: ff1b17295c58d40d55bdcd4346b83121b579bb4c
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020554"
---
<a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a>与模型绑定和 web 窗体集成 JQuery UI Datepicker
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定可以更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource） 的数据交互。 本系列开始介绍性材料，后续教程将移动到更高级的概念。
> 
> 本教程演示如何添加 JQuery UI[小组件](http://jqueryui.com/datepicker/)Web 窗体和使用模型绑定将使用所选的值更新数据库。
> 
> 本教程中创建的项目为基础[第一个](retrieving-data.md)并[第二个](updating-deleting-and-creating-data.md)在本系列的部分。
> 
> 你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整的项目 C# 或 vb。 可下载代码适用于 Visual Studio 2012 或 Visual Studio 2013。 它使用 Visual Studio 2012 模板，为在本教程中所示的 Visual Studio 2013 模板稍有不同。


## <a name="what-youll-build"></a>你将生成

在本教程中，你将：

1. 将属性添加到您的模型以记录该学生注册日期
2. 使用户可选择使用 JQuery UI Datepicker 小组件的注册日期
3. 个注册日期执行验证规则

JQuery UI Datepicker 小组件使用户能够轻松地从用户交互的字段时弹出一个日历选择一个日期。 使用此小组件可能会更便于用户比手动键入的日期。 将小组件集成到页面的数据操作中使用模型绑定要求只有少量的额外工作。

## <a name="add-a-new-property-to-the-model"></a>将新属性添加到模型

首先，您将添加**Datetime**让学生的属性的模型和迁移到数据库所做的更改。 打开**UniversityModels.cs**，并将突出显示的代码添加到学生模型。

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

**RangeAttribute**是包括在内，以强制实施验证规则的属性。 对于本教程中，我们将假定 Contoso University 成立于 2013 年 1 月 1 日，并因此早期注册日期不是有效。

在包管理窗口中，添加通过运行命令的迁移**添加迁移 AddEnrollmentDate**。 请注意，迁移代码向 Student 表中添加新的日期时间列。 若要匹配 RangeAttribute 中指定的值，将以下突出显示的代码中所示添加新列中，默认值。

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

将所做的更改保存到迁移文件。

不需要再次生成种子数据。 因此，打开**Configuration.cs** Migrations 文件夹中并删除或注释掉中的代码**种子**方法。 保存并关闭文件。

现在，运行命令**更新数据库**。 请注意，现在存在于数据库中列的所有现有记录具有默认值为 EnrollmentDate。

## <a name="add-dynamic-controls-for-enrollment-date"></a>将动态控件添加个注册日期

现在，您将添加用于显示和编辑注册日期的控件。 现在，通过文本框中编辑值。 在本教程后面将更改文本框中，为 JQuery Datepicker 小组件。

首先，务必请注意，不需要进行任何更改**AddStudent.aspx**文件。 DynamicEntity 控件将自动呈现新属性。

打开**Students.aspx**，并添加以下突出显示的代码。

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

运行应用程序，请注意，您可以通过键入日期设置注册日期的值。 添加新学生时：

![设置的日期](integrating-jquery-ui/_static/image1.png)

或者，编辑现有值：

![编辑日期](integrating-jquery-ui/_static/image2.png)

键入日期的工作原理，但它可能不是您希望提供的客户体验。 在下一部分中，您将启用选择通过日历日期。

## <a name="install-nuget-package-to-work-with-jquery-ui"></a>安装 NuGet 包以使用 JQuery UI

**汁 UI** NuGet 程序包可启用的 JQuery UI 小组件的轻松集成到 web 应用程序。 若要使用此包，请通过 NuGet 安装它。

![添加汁 UI](integrating-jquery-ui/_static/image3.png)

汁 UI 安装的版本可能与应用程序中的 JQuery 版本冲突。 本教程前，请尝试运行您的应用程序。 如果遇到 JavaScript 错误，您需要协调的 JQuery 版本。 可以将 JQuery 的预期的版本添加到脚本文件夹 （版本 1.8.2 在编写本教程中的时），或在 Site.master 指定 JQuery 文件的路径。

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a>自定义日期时间模板以包括小组件

会将小组件添加到动态数据模板以进行编辑的日期时间值。 通过将小组件添加到模板，自动呈现中添加新学生的这两个窗体和编辑学生在网格视图中。 打开**DateTime\_Edit.ascx**，并添加以下突出显示的代码。

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

在代码隐藏文件中，您将为 DatePicker 设置的最小和最大日期。 通过设置这些值，将阻止用户导航到无效的日期。 将检索中的最小和最大值**RangeAttribute**上的日期时间属性，如果提供。 打开**DateTime\_Edit.ascx.cs**，并将以下突出显示的代码添加到页面\_负载方法。

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

运行 web 应用程序并导航到 AddStudent 页面。 为字段提供值，请注意，如果您单击文本框中的注册日期，将显示日历。

![日期选取器](integrating-jquery-ui/_static/image4.png)

选择日期，并单击**插入**。 RangeAttribute 强制进行验证的服务器上。 通过设置 Datepicker minDate 属性，您在客户端上还应用验证。 日历不允许用户导航到之前的 minDate 值的日期。

当您编辑网格视图中的记录时，还会显示日历。

![在 GridView 中的 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a>结束语

在本教程中，您学习了如何使用模型绑定的 web 窗体中纳入 JQuery 小组件。

在接下来[教程](using-query-string-values-to-retrieve-data.md)，选择数据时，将使用查询字符串值。

> [!div class="step-by-step"]
> [上一页](sorting-paging-and-filtering-data.md)
> [下一页](using-query-string-values-to-retrieve-data.md)
