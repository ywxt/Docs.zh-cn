---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: 使用 TagBuilder 类用于生成 HTML 帮助程序 (C#) |Microsoft Docs
author: StephenWalther
description: Stephen Walther 向您介绍 TagBuilder 类命名为 ASP.NET MVC 框架中的一个有用的实用工具类。 可以轻松地使用到的 TagBuilder 类...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ec50fca1d65d95aaf2baf00c84c080ba98bf333
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37383863"
---
<a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a>使用 TagBuilder 类用于生成 HTML 帮助程序 (C#)
====================
通过[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther 向您介绍 TagBuilder 类命名为 ASP.NET MVC 框架中的一个有用的实用工具类。 TagBuilder 类可用于轻松生成 HTML 标记。


ASP.NET MVC 框架包括名为可以使用时生成的 HTML 帮助程序的 TagBuilder 类的有用的实用工具类。 TagBuilder 类，如所示的类的名称，使您可以轻松地生成 HTML 标记。 在本简短教程随附的 TagBuilder 类概述并了解如何构建简单的 HTML 帮助器呈现 HTML 时使用此类&lt;i m g&gt;标记。

## <a name="overview-of-the-tagbuilder-class"></a>TagBuilder 类概述

TagBuilder 类都包含在 System.Web.Mvc 命名空间。 它具有五种方法：

- AddCssClass()-可以添加一个新*类 =""* 属性为标记。
- GenerateId()-可以向标记添加一个 id 属性。 此方法将自动替换 id 中的句点 （默认情况下，期间将被下划线取代）
- MergeAttribute()-可以将属性添加到一个标记。 有多个重载的此方法。
- SetInnerText()-可以设置标记的内部文本。 内部文本是自动 HTML 编码。
- Tostring （）-使您能够呈现标记。 您可以指定是否想要创建一个正常的标记、 开始标记、 结束标记或自结束标记。
  

TagBuilder 类具有四个重要属性：

- 属性 – 表示的所有标记的属性。
- IdAttributeDotReplacement-表示 GenerateId() 方法用于替换 （默认值为下划线） 的句号的字符。
- InnerHTML-表示标记的内部内容。 将字符串分配给此属性*却不*的字符串进行 HTML 编码。
- TagName-表示标记的名称。

这些方法和属性提供的所有基本方法和所需的 HTML 标记生成的属性。 实际上，不必使用 TagBuilder 类。 可以改为使用 StringBuilder 类。 但是，TagBuilder 类使您的生活更简单。

## <a name="creating-an-image-html-helper"></a>创建图像的 HTML 帮助器

创建 TagBuilder 类的实例时，你将传递你想要生成到 TagBuilder 构造函数的标记的名称。 接下来，您可以调用等 AddCssClass 和 MergeAttribute() 方法，若要修改的属性标记的方法。 最后，调用 tostring （） 方法以呈现标记。

例如，列表 1 中包含的图像的 HTML 帮助器。 图像帮助程序在内部实现与表示 HTML TagBuilder &lt;i m g&gt;标记。

**代码清单 1-Helpers\ImageHelper.cs**

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

在列表 1 中的类包含名为映像的两个静态重载的方法。 当调用 Image() 方法时，您可以传递或不表示一系列 HTML 特性的对象。

请注意如何使用 TagBuilder.MergeAttribute() 方法以将各个属性如 src 属性添加到 TagBuilder。 此外，请注意如何使用 TagBuilder.MergeAttributes() 方法向 TagBuilder 添加特性的集合。 MergeAttributes() 方法接受一个字典&lt;string，object&gt;参数。 RouteValueDictionary 类用于将表示为一个字典的属性集合的对象转换&lt;string，object&gt;。

创建图像帮助程序后，您可以就像任何其他标准 HTML 帮助程序一样在 ASP.NET MVC 视图中使用该帮助器。 代码清单 2 中的视图使用图像帮助程序两次显示 Xbox 的同一个图像 （参见图 1）。 Image() 帮助者称为使用或不 HTML 特性集合。

**代码清单 2-Home\Index.aspx**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]


[![新建项目对话框](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)

**图 01**： 使用图像帮助程序 ([单击以查看实际尺寸的图像](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))


请注意，必须导入 Index.aspx 视图顶部的图像帮助程序关联的命名空间。 使用以下指令导入帮助程序：

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> [上一页](creating-custom-html-helpers-cs.md)
> [下一页](creating-page-layouts-with-view-master-pages-cs.md)
