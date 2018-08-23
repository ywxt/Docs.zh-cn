---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 第 1 部分： 概述和创建项目 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: 0e4021402e8deccd2395f23b6b512679b5e9d281
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834580"
---
<a name="part-1-overview-and-creating-the-project"></a>第 1 部分： 概述和创建项目
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

Entity Framework 是一个对象/关系映射框架。 它将在代码中的域对象映射到关系数据库中的实体。 大多数情况下，您无需担心数据库层，因为实体框架将为您处理它。 你的代码操作对象，并更改保存到数据库。

## <a name="about-the-tutorial"></a>有关本教程

在本教程中，将创建一个简单的应用商店应用程序。 有两个主要部分： 应用程序。 普通用户可以查看产品，并创建订单：

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

管理员可以创建、 删除或编辑产品：

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a>你将学习的技能

下面是你将了解：

- 如何使用实体框架和 ASP.NET Web API。
- 如何使用 knockout.js 创建动态客户端 UI。
- 如何使用与 Web API 的窗体身份验证来对用户进行身份验证。

虽然本教程是自包含，但你可能想要先阅读以下教程：

- [第一个 ASP.NET Web API](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [创建 Web API 支持 CRUD 操作](../creating-a-web-api-that-supports-crud-operations.md)

有一定的了解[ASP.NET MVC](../../../../mvc/index.md)也会有所帮助。

## <a name="overview"></a>概述

在高级别中，下面是应用程序的体系结构：

- ASP.NET MVC 为客户端生成的 HTML 页。
- ASP.NET Web API 公开的数据 （产品和订单） 的 CRUD 操作。
- 实体框架将转换成数据库的实体使用 Web API 的 C# 模型。

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

下图显示了如何在应用程序的各层表示域对象： 数据库层、 对象模型中，并最后连网格式，它用于传输到客户端通过 HTTP 的数据。

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a>创建 Visual Studio 项目

可以创建使用 Visual Web Developer 速成版或 Visual Studio 的完整版本的教程项目。

从**启动**页上，单击**新项目**。

在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。 下**Visual C#**，选择**Web**。 在项目模板列表中选择**ASP.NET MVC 4 Web 应用程序**。 命名项目"ProductStore"，然后单击**确定**。

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**然后单击**确定**。

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

"Internet 应用程序"模板创建支持窗体身份验证的 ASP.NET MVC 应用程序。 如果您运行应用程序现在，它已包含一些功能：

- 新用户可以通过单击右上角的"注册"链接注册。
- 已注册的用户可以通过单击"登录"链接登录。

会自动创建的数据库中保留成员身份信息。 有关在 ASP.NET MVC 中的窗体身份验证的详细信息，请参阅[演练： 在 ASP.NET MVC 中使用 Forms 身份验证](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)。

## <a name="update-the-css-file"></a>更新 CSS 文件

此步骤是表面的但它将使呈现等早期的屏幕截图的页。

在解决方案资源管理器，展开内容文件夹并打开名为 Site.css 文件。 添加以下 CSS 样式：

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [下一篇](using-web-api-with-entity-framework-part-2.md)
