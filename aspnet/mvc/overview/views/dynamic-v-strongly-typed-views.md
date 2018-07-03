---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 动态类型化。 强类型视图 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2011
ms.topic: article
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 7622ca8248374da27f4190075df5a6bfc32bb2e6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389080"
---
<a name="dynamic-v-strongly-typed-views"></a>动态类型化。 强类型化的视图
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

有三种方法将信息从控制器传递到 ASP.NET MVC 3 中的视图：

1. 作为强类型化的模型对象。
2. 为动态类型 (使用@model动态)
3. 使用 ViewBag

我编写了一个简单的 MVC 3 顶部博客应用程序进行比较和对比动态和强类型化视图。 在控制器启动与一系列简单的博客：

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

IndexNotStonglyTyped() 方法中右键单击并添加 Razor 视图。

[![8475.NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

请确保**创建强类型化视图**框未选中。 生成的视图不包含很多：

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

因为我们使用的动态和不是强类型化的视图，intellisense 不会帮助我们。 已完成的代码如下所示：

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646.NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

现在我们将添加一个强类型化的视图。 将以下代码添加到控制器：

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]


请注意，它是完全相同返回 View(topBlogs);调用作为非强类型视图。 右键单击的内部*StonglyTypedIndex()* ，然后选择**添加视图**。 这次请选择**博客**模型类，然后选择**列表**为基架模板。

[![5658.StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

在新的视图模板中，我们将获得 intellisense 支持。

[![7002.intellesince [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)

可以下载 c# 项目[此处](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)。
