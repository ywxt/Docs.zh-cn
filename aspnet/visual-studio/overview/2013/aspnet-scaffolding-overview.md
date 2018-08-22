---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: 在 Visual Studio 2013 的 ASP.NET 基架 |Microsoft Docs
author: tfitzmac
description: ASP.NET 基架是包括在 Visual Studio 2013 的新功能。
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: c554f592e57f2e6017f7fcfcc9b4c98051e21b37
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824871"
---
<a name="aspnet-scaffolding-in-visual-studio-2013"></a>在 Visual Studio 2013 的 ASP.NET 基架
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET 基架是包括在 Visual Studio 2013 的新功能。


## <a name="overview"></a>概述

ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。 Visual Studio 2013 包括 MVC 和 Web API 项目的预安装的代码生成器。 当你想要快速添加与数据模型交互的代码基架添加到项目。 使用基架可以减少开发你的项目中的标准数据操作的时间量。

默认情况下，Visual Studio 2013 不支持的 Web 窗体项目，生成代码，但可以使用 Web 窗体中使用基架通过向项目添加 MVC 依赖项或安装扩展。 下面显示了这两种方法。

Visual Studio 2013 Update 2 (当前 RC) 提供的功能来扩展 ASP.NET 基架以满足你的方案的要求。 使用此功能，可以创建自定义基架模板并将其添加到对话框中添加新的基架。 在自定义模板中，指定将添加基架的项时生成的代码。 有关详细信息，请参阅[用于 Visual Studio 中创建自定义基架](https://go.microsoft.com/fwlink/p/?LinkId=395029)。

## <a name="prerequisites"></a>系统必备

若要使用 ASP.NET 基架，您必须具有：

- Microsoft Visual Studio 2013
- Web 开发人员工具 （默认 Visual Studio 2013 安装的一部分）
- ASP.NET Web 框架和工具 2013 （默认 Visual Studio 2013 安装的一部分）

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a>将基架的项添加到 MVC 或 Web API

若要添加基架，请右键单击项目或在项目中，一个文件夹并选择**外**–**新基架项**下, 图中所示。

![添加基架项](aspnet-scaffolding-overview/_static/image1.png)

从**添加基架**窗口中，选择的基架添加的类型。

![选择类型的基架](aspnet-scaffolding-overview/_static/image2.png)

**添加控制器**窗口使您能够选择用于生成控制器，包括是否想要使用 Entity Framework 6 的新异步功能的选项。

![添加控制器](aspnet-scaffolding-overview/_static/image3.png)

你的方案为创建相关的类和页面。 例如下, 图显示了 MVC 控制器和视图通过名为电影模型类的基架创建的。

![创建的文件](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a>将基架的项添加到 Web 窗体

若要添加基架生成 Web 窗体代码，必须安装到 Visual Studio 扩展或添加 MVC 依赖项。 这两种方法如下所示，但只需执行其中一种方法。

### <a name="web-forms-scaffolding-extension"></a>Web 窗体基架扩展

你可以安装 Visual Studio 扩展中，您可以使用 Web 窗体项目中使用基架。 在 Visual Studio 中，选择**工具**，然后**扩展和更新**。 在此对话框中搜索有关 Visual Studio 库**Web 窗体基架**。

![安装 web 窗体基架](aspnet-scaffolding-overview/_static/image5.png)

有关详细信息，请参阅[Web 窗体基架](https://go.microsoft.com/fwlink/p/?LinkId=396478)。

### <a name="mvc-dependencies"></a>MVC 依赖项

若要添加 MVC 依赖项，请选择**外** - **新基架项**。 在添加基架窗口中，选择**MVC 依赖项**，如下所示。

![添加 MVC 依赖项](aspnet-scaffolding-overview/_static/image6.png)

有两个选项基架 MVC;最小和完全。 如果你选择最小，NuGet 包和 ASP.NET MVC 的引用添加到你的项目。 如果选择完全选项，添加最小依赖项，以及对于 MVC 项目所需的内容文件。 若要轻松地使用基架，请选择完整的依赖项。

![选择全部依赖项](aspnet-scaffolding-overview/_static/image7.png)

添加依赖项之后, 您将看到**readme.txt**文件。 请仔细按照此文件中的说明，以确保你的项目正常运行。

完成 readme.txt 文件中的步骤后，可以添加新的基架的项，如有关 MVC 和 Web API 在上一部分中所示。 自动生成的视图和控制器将在项目中正常工作。

## <a name="tutorials"></a>教程

若要创建自定义基架，请参阅[用于 Visual Studio 中创建自定义基架](https://go.microsoft.com/fwlink/p/?LinkId=395029)。

若要自定义生成的文件，请参阅[如何自定义生成的文件从新建基架项对话框](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx)。

有关使用与基架的示例**Database First 开发**，请参阅[EF Database First 使用 ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md)。

有关使用中的基架的示例**MVC**项目，请参阅[Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。

有关使用中的基架的示例**Web API**项目，请参阅[使用 Web API 2 中的属性路由创建 REST API](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md)。
