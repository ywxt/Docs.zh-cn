---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: 了解模型、 视图和控制器 (C#) |Microsoft Docs
author: StephenWalther
description: 有关模型、 视图和控制器感到迷惑吗？ 在本教程中，Stephen Walther 向您介绍到的 ASP.NET MVC 应用程序的不同部分。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: f5cf39e4652a3e487dcd79b2cf887efb992c2107
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376904"
---
<a name="understanding-models-views-and-controllers-c"></a>了解模型、 视图和控制器 (C#)
====================
通过[Stephen Walther](https://github.com/StephenWalther)

> 有关模型、 视图和控制器感到迷惑吗？ 在本教程中，Stephen Walther 向您介绍到的 ASP.NET MVC 应用程序的不同部分。


本教程提供简要介绍 ASP.NET MVC 的模型、 视图和控制器也是如此。 换而言之，它说明了 M，V，和 C 在 ASP.NET MVC 中。

阅读本教程之后，您应该了解 ASP.NET MVC 应用程序的不同部分是如何协同工作。 您还应了解与 ASP.NET Web 窗体应用程序或 Active Server Pages 应用程序的 ASP.NET MVC 应用程序的体系结构的区别。

## <a name="the-sample-aspnet-mvc-application"></a>示例 ASP.NET MVC 应用程序

用于创建 ASP.NET MVC Web 应用程序的默认 Visual Studio 模板包括可用于了解 ASP.NET MVC 应用程序的不同部分的极其简单的示例应用程序。 我们利用在本教程中此简单应用程序。

使用 MVC 模板中启动 Visual Studio 2008 创建新的 ASP.NET MVC 应用程序并选择文件菜单选项，新建项目 （请参见图 1）。 在新建项目对话框中，选择你喜欢的编程语言下项目类型 （Visual Basic 或 C#），然后选择**ASP.NET MVC Web 应用程序**下模板。 单击确定按钮。


[![新建项目对话框](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)

**图 01**: 新建项目对话框 ([单击以查看实际尺寸的图像](understanding-models-views-and-controllers-cs/_static/image2.png))


创建新的 ASP.NET MVC 应用程序时**创建单元测试项目**对话框 （请参见图 2）。 此对话框，可用于测试你的 ASP.NET MVC 应用程序在解决方案中创建一个单独的项目。 选择的选项**否，不创建单元测试项目**然后单击**确定**按钮。


[![创建单元测试对话框](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)

**图 02**： 创建单元测试对话框 ([单击以查看实际尺寸的图像](understanding-models-views-and-controllers-cs/_static/image4.png))


创建后新的 ASP.NET MVC 应用程序。 你将看到多个文件夹和解决方案资源管理器窗口中的文件。 具体而言，你将看到名为模型、 视图和控制器的三个文件夹。 您可能已经猜到的文件夹名称，这些文件夹包含用于实现模型、 视图和控制器的文件。

如果展开 Controllers 文件夹，你应看到一个名为 AccountController.cs 文件和一个名为 HomeController.cs 文件。 如果展开 Views 文件夹，应看到名为帐户，主页和共享的三个子文件夹。 如果展开主文件夹，您将看到两个名为 About.aspx 和 Index.aspx （请参见图 3） 的其他文件。 这些文件构成了默认的 ASP.NET MVC 模板中包含的示例应用程序。


[![解决方案资源管理器窗口](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)

**图 03**: 解决方案资源管理器窗口 ([单击以查看实际尺寸的图像](understanding-models-views-and-controllers-cs/_static/image6.png))


可以通过选择菜单选项来运行示例应用程序**调试、 启动调试**。 此外，您可以按 F5 键。

首次运行的 ASP.NET 应用程序时，会出现图 4 中的对话框，建议启用调试模式。 单击确定按钮，将运行该应用程序。


[![调试未启用的对话框](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)

**图 04**： 未启用调试对话框 ([单击以查看实际尺寸的图像](understanding-models-views-and-controllers-cs/_static/image8.png))


当您运行的 ASP.NET MVC 应用程序时，Visual Studio 将启动 web 浏览器中的应用程序。 示例应用程序只有两个页组成: 索引页和关于页面。 第一次启动应用程序，将显示索引页 （请参见图 5）。 可以通过单击顶部的菜单链接导航到关于页面右侧的应用程序。


[![索引页](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)

**图 05**: 索引页 ([单击以查看实际尺寸的图像](understanding-models-views-and-controllers-cs/_static/image11.png))


请注意，在浏览器地址栏中的 Url。 例如，当你单击关于菜单链接时，浏览器地址栏中的 URL 将变为 **/Home/有关**。

如果关闭浏览器窗口并返回到 Visual Studio，你将无法使用路径主页/关于查找的文件。 文件不存在。 这是如何实现？

## <a name="a-url-does-not-equal-a-page"></a>URL 不等于页面

传统的 ASP.NET Web 窗体应用程序或 Active Server Pages 应用程序生成时，没有一个 URL，另一个页面之间的一一对应关系。 如果请求名 SomePage.aspx 为从服务器的页，则有更好地有一个页面上名为 SomePage.aspx 磁盘。 如果 SomePage.aspx 文件不存在，则获取费解之处**404-找不到页面**错误。

当构建 ASP.NET MVC 应用程序，与此相反，没有任何浏览器的地址栏中键入的 URL 和应用程序中查找的文件之间的对应关系。 在 ASP.NET MVC 应用程序 URL 对应于而不是磁盘上页面的控制器操作。

在传统 ASP.NET 或 ASP 应用程序中，浏览器请求映射到页中。 ASP.NET MVC 应用程序中与此相反，浏览器请求映射到控制器操作。 ASP.NET Web 窗体应用程序是以内容为中心。 ASP.NET MVC 应用程序中，与此相反，是为中心的应用程序逻辑。

## <a name="understanding-aspnet-routing"></a>了解 ASP.NET 路由

将浏览器请求映射到通过一项功能的名为 ASP.NET 框架的控制器操作*ASP.NET 路由*。 ASP.NET MVC 框架使用 ASP.NET 路由*路由*传入到控制器操作的请求。

ASP.NET 路由使用路由表来处理传入的请求。 Web 应用程序首次启动时创建此路由表。 路由表是在 Global.asax 文件中的设置。 默认 MVC Global.asax 文件包含在列表 1 中。

**代码清单 1-Global.asax**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

当 ASP.NET 应用程序首次启动时，应用程序\_调用 start （） 方法。 在列表 1 中，此方法调用 RegisterRoutes() 方法和 RegisterRoutes() 方法创建默认路由表。

默认路由表包含一个路由。 此默认路由将分成三个段 （URL 段是正斜杠之间的任何内容） 的所有传入请求。 第一个段映射到的控制器的名称、 第二段映射到的操作名称和最后一段映射到参数传递给操作名为 id。

以下列 URL 为例：

/ 产品/详细信息/3

此 URL 解析为如下三个参数：

控制器 = 产品

操作 = 详细信息

id = 3

Global.asax 文件中定义的默认路由包括所有三个参数的默认值。 默认控制器是主页，默认操作是索引，默认 Id 是空字符串。 记住这些默认值，请看以下 URL 的分析方式：

/ 雇员

此 URL 解析为如下三个参数：

控制器 = 员工

操作 = 索引

Id =

最后，如果您打开 ASP.NET MVC 应用程序无需提供任何 URL (例如， `http://localhost`)，则将 URL 解析如下：

控制器 = 主页

操作 = 索引

Id =

请求路由到 HomeController 类上的 index （） 操作。

## <a name="understanding-controllers"></a>了解控制器

控制器负责控制用户与 MVC 应用程序交互的方式。 控制器包含一个 ASP.NET MVC 应用程序的流控制逻辑。 控制器确定要发送回的用户，当用户浏览器请求的响应。

控制器是只是一个类 （例如，Visual Basic 或 C# 类）。 示例 ASP.NET MVC 应用程序包含名为 HomeController.cs 控制器文件夹中的控制器。 列表 2 中重现的 HomeController.cs 文件的内容。

**代码清单 2-HomeController.cs**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

请注意 HomeController 有两个名为 index （） 和将 about （） 的方法。 这两种方法与在控制器公开的两个操作相对应。 URL /Home/索引调用 HomeController.Index() 方法和 URL /Home/有关调用 HomeController.About() 方法。

在控制器中的任何公共方法公开为控制器操作。 您需要注意相关信息。 这意味着在控制器中包含任何公共方法可由有权访问 Internet 的任何人都调用浏览器中输入正确的 URL。

## <a name="understanding-views"></a>了解视图

公开 HomeController 类，index （） 和将 about （），这两个控制器操作都返回一个视图。 视图包含 HTML 标记和发送到浏览器的内容。 使用 ASP.NET MVC 应用程序时，视图是一个页面的等效项。

必须在正确的位置中创建你的视图。 HomeController.Index() 操作将返回一个视图，在位于以下路径：

\Views\Home\Index.aspx

HomeController.About() 操作将返回一个视图，在位于以下路径：

\Views\Home\About.aspx

一般情况下，如果你想要返回的控制器操作的视图，然后需要使用与你的控制器相同的名称在 Views 文件夹中创建一个子文件夹。 在子文件夹，必须与同名的控制器操作来创建一个.aspx 文件。

列表 3 中的文件包含 About.aspx 视图。

**代码清单 3-About.aspx**

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

如果忽略清单 3 中的第一行，视图的其他部分包含的标准 HTML。 您可以通过输入您所需要的任何 HTML 来修改视图的内容。

视图是非常类似于 Active Server Pages 或 ASP.NET Web 窗体中的页。 视图可以包含 HTML 内容和脚本。 您可以编写脚本中最喜欢的.NET 编程语言 （例如，C# 或 Visual Basic.NET）。 使用脚本来显示动态内容，例如数据库数据。

## <a name="understanding-models"></a>了解模型

我们已讨论了控制器，我们已讨论了视图。 我们需要介绍的最后一个主题是模型。 MVC 模型是什么？

MVC 模型包含所有未包含在视图或控制器应用程序逻辑。 该模型应包含的所有应用程序业务逻辑、 验证逻辑和数据库访问逻辑。 例如，如果使用 Microsoft 实体框架来访问你的数据库，然后你将创建您的 Entity Framework 类 （在.edmx 文件） Models 文件夹中。

视图应包含仅与生成用户界面相关的逻辑。 控制器应只包含逻辑返回右视图或将用户重定向到另一个动作 （流控制） 所需的最低要求。 其他所有内容应包含在模型中。

一般情况下，您应尽量 fat 模型和瘦控制器。 控制器方法应包含只有少量的代码行。 如果控制器操作获取太 fat，则应考虑将逻辑移到模型文件夹中的新类。

## <a name="summary"></a>总结

本教程向你提供全面概述了 ASP.NET MVC 的不同部分的 web 应用程序。 您学习了如何 ASP.NET 路由传入浏览器将请求映射到特定控制器操作。 您学习了如何控制器协调视图如何返回到浏览器。 最后，您学习了如何模型包含应用程序业务、 验证和数据库访问逻辑。
