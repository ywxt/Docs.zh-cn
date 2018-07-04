---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: 通过数据库 (C#) 使用 CascadingDropDown |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中 anoth 值...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: 06ba008740da7e9cb6a058465154a38b65ccb39a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381611"
---
<a name="using-cascadingdropdown-with-a-database-c"></a>使用 CascadingDropDown 与数据库 (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)

> AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。 为了使此功能，必须创建一个特殊 web 服务。


## <a name="overview"></a>概述

AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。 （例如，一个列表提供了一系列我们状态，和与该状态中的主要城市然后填充下一个列表。）为了使此功能，必须创建一个特殊 web 服务。

## <a name="steps"></a>步骤

首先，数据源是必需的。 此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。 数据库是可选的组成部分 （包括速成版） 的 Visual Studio 安装，并且仍可单独下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。 AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。 若要设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，并将附加`AdventureWorks.mdf`数据库文件。

对于此示例中，我们假定 SQL Server 2005 Express Edition 的实例称为`SQLEXPRESS`和驻留在与 web 服务器; 在同一台计算机上这也是默认设置。 如果你的设置不同，您必须调整数据库的连接信息。

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (之内&lt; `form` &gt;元素):

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

在下一步中，两个 DropDownList 控件是必需的。 在此示例中，我们使用来自 AdventureWorks 的供应商和联系人信息，因此我们为可用的供应商，另一个可用的联系人用于创建一个列表：

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

然后，必须将两个 CascadingDropDown 扩展器添加到页面。 一个填充第一个 （供应商） 列表，并将另一个填充第二个 （联系人） 列表。 必须设置以下属性：

- `ServicePath`: Web 服务提供的列表项的 URL
- `ServiceMethod`: Web 方法提供的列表项
- `TargetControlID`: 下拉列表的 ID
- `Category`： 提交到 web 方法调用时类别信息
- `PromptText`： 以异步方式从服务器加载列表数据时显示的文本
- `ParentControlID`: (可选) 父下拉列表中列出的当前列表，触发器加载

具体取决于使用的编程语言，有问题的 web 服务的名称更改，但所有其他属性值是相同的。 下面是第一个下拉列表中的 CascadingDropDown 元素：

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

第二个列表的控件扩展程序需要设置`ParentControlID`属性，以便在加载供应商列表触发器中选择某一项关联的联系人列表中的元素。

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

在 web 服务中，按如下所示设置然后完成实际工作。 请注意，`[ScriptService]`使用属性，否则 ASP.NET AJAX 不能创建要从客户端脚本代码访问的 web 方法的 JavaScript 代理。

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

通过 CascadingDropDown 调用的 web 方法的签名如下所示：

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

因此，返回值必须是类型的数组`CascadingDropDownNameValue`其定义了控件工具包。 `GetVendors()`方法可以很容易地实现： 代码连接到 AdventureWorks 数据库并查询前 25 个供应商。 中的第一个参数`CascadingDropDownNameValue`构造函数是其值的列表项，第二个的标题 (以 html 格式的值特性&lt; `option` &gt;元素)。 下面是代码：

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

获取关联的联系人的供应商 (方法名称： `GetContactsForVendor()`) 则有点棘手。 首先，必须确定供应商的第一个下拉列表中选择。 控件工具包定义该任务的帮助器方法：`ParseKnownCategoryValuesString()`方法将返回`StringDictionary`具有下拉列表中数据元素：

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

出于安全原因，必须首先验证此数据。 因此，如果供应商条目 (因为`Category`的第一个 CascadingDropDown 元素的属性设置为`"Vendor"`)，可能会检索所选的供应商的 ID:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

方法的剩余部分就相当简单直接。 供应商的 ID 用作可检索有关该供应商相关联的所有联系人的 SQL 查询参数。 再次重申，该方法返回类型的数组`CascadingDropDownNameValue`。

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

加载 ASP.NET 页上，并且之后不久, 供应商列表填充包含 25 个条目。 选择一个条目，并请注意如何使用数据填充第二个下拉列表中。


[![自动填充第一个列表](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)

自动填充第一个列表 ([单击此项可查看原尺寸图像](using-cascadingdropdown-with-a-database-cs/_static/image3.png))


[![第二个列表填充根据第一个列表中选择](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)

第二个列表填充根据第一个列表中选择 ([单击此项可查看原尺寸图像](using-cascadingdropdown-with-a-database-cs/_static/image6.png))

> [!div class="step-by-step"]
> [上一页](filling-a-list-using-cascadingdropdown-cs.md)
> [下一页](presetting-list-entries-with-cascadingdropdown-cs.md)
