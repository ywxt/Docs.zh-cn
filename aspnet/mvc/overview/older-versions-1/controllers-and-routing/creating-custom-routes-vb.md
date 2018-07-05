---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: 创建自定义路由 (VB) |Microsoft Docs
author: microsoft
description: 了解如何将自定义路由添加到 ASP.NET MVC 应用程序。 在本教程中，您将学习如何修改 Global.asax 文件中的默认路由表。
ms.author: aspnetcontent
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: 3d6125f93d99acc695be319bd000ff65ab4a1159
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829695"
---
<a name="creating-custom-routes-vb"></a>创建自定义路由 (VB)
====================
by [Microsoft](https://github.com/microsoft)

> 了解如何将自定义路由添加到 ASP.NET MVC 应用程序。 在本教程中，您将学习如何修改 Global.asax 文件中的默认路由表。


在本教程中，您将学习如何将自定义的路由添加到 ASP.NET MVC 应用程序。 了解如何修改自定义的路由在 Global.asax 文件中的默认路由表。

在 ASP.NET MVC 应用程序中的默认路由表将就可以正常工作。 但是，可能会发现有专门的路由的需要。 在这种情况下，可以创建自定义路由。

例如，假设您要生成的博客应用程序。 你可能想要处理传入的请求，如下所示：

/ 存档/12-25-2009 年

当用户输入此请求时，你想要返回到日期相对应的博客条目 2009 年 12 月 25 日。 若要处理这种类型的请求，需要创建一个自定义路由。

在列表 1 中的 Global.asax 文件包含一个新的自定义路由，名为博客，看起来像 /Archive/ 哪些句柄请求*条目日期*。

**代码清单 1-Global.asax （具有自定义路由）**

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

您将添加到路由表路由的顺序非常重要。 我们新的自定义博客路由添加到之前的现有默认路由。 如果您颠倒顺序，则默认路由始终将获取调用而不是自定义路由。

自定义博客路由匹配的开头/存档/任何请求。 因此，它与匹配所有以下 Url:

- / 存档/12-25-2009 年

- / 存档/10-6-2004

- / 存档/apple

自定义的路由将传入请求映射到名为存档的控制器，并调用 Entry() 操作。 当调用 Entry() 方法时，条目日期在作为一个名为 entryDate 参数传递。

可以使用在代码清单 2 中的控制器使用博客自定义路由。

**代码清单 2-ArchiveController.vb**

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

请注意，代码清单 2 中的 Entry() 方法接受类型为 DateTime 的参数。 MVC 框架非常智能，可自动将条目日期从 URL 转换 DateTime 值。 如果 URL 中的条目日期参数不能转换为日期时间，将引发错误 （请参阅图 1）。

**图 1-通过转换参数错误**


[![新建项目对话框](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)

**图 01**： 通过转换参数的错误 ([单击以查看实际尺寸的图像](creating-custom-routes-vb/_static/image2.png))


## <a name="summary"></a>总结

本教程的目的是演示如何创建自定义路由。 您学习了如何将自定义的路由添加到表示博客条目在 Global.asax 文件中的路由表。 我们讨论了如何将请求的博客条目映射到名为 ArchiveController 的控制器和名为 Entry() 的控制器操作。

> [!div class="step-by-step"]
> [上一页](asp-net-mvc-controller-overview-vb.md)
> [下一页](creating-a-route-constraint-vb.md)
