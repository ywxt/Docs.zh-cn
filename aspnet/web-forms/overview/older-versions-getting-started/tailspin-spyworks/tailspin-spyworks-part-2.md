---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 第 2 部分： 数据访问层 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 2 部分介绍如何添加数据访问层。
ms.author: aspnetcontent
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: c1d61681952cbf1f0587f0e42da21f8436d79ebb
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37812027"
---
<a name="part-2-data-access-layer"></a>第 2 部分： 数据访问层
====================
通过[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。 它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。
> 
> 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 2 部分介绍如何添加数据访问层。


## <a id="_Toc260221668"></a>  添加数据访问层

我们的电子商务应用程序将依赖于两个数据库。

对于客户信息，我们将使用标准 ASP.NET 成员资格数据库。 我们的购物车和产品目录，我们将按如下所示实现 SQL Express 数据库。

![](tailspin-spyworks-part-2/_static/image1.jpg)

在应用程序的应用程序中创建数据库 (Commerce.mdf)\_我们可以继续创建使用.NET Entity Framework 数据访问层的数据文件夹。

我们将创建一个名为"数据\_访问"和它们在该文件夹上右键单击并选择"添加新项"。

在"安装模板"项，然后选择"ADO.NET 实体数据模型"输入 EDM\_Commerce.edmx 作为名称，然后单击"添加"按钮。

![](tailspin-spyworks-part-2/_static/image2.jpg)

选择"从数据库生成"。

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

保存并生成。

现在我们已准备好添加我们第一项功能 – 产品类别菜单。

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-1.md)
> [下一页](tailspin-spyworks-part-3.md)
