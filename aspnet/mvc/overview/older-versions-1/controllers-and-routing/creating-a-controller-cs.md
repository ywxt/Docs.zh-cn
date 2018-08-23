---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: 创建控制器 (C#) |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 演示了如何将控制器添加到 ASP.NET MVC 应用程序。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: 6fe880775a5d477aefcf0fe6cedb3e719760ed90
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833473"
---
<a name="creating-a-controller-c"></a>创建控制器 (C#)
====================
通过[Stephen Walther](https://github.com/StephenWalther)

> 在本教程中，Stephen Walther 演示了如何将控制器添加到 ASP.NET MVC 应用程序。


本教程的目的是说明如何创建新的 ASP.NET MVC 控制器。 了解如何创建控制器通过使用 Visual Studio 添加的控制器菜单选项，以及通过手动创建的类文件。

### <a name="using-the-add-controller-menu-option"></a>使用添加控制器菜单选项

若要创建新的控制器的最简单方法是右键单击 Visual Studio 解决方案资源管理器窗口中的 Controllers 文件夹并选择**添加、 控制器**菜单选项 （请参阅图 1）。 选择此菜单选项将打开**添加控制器**对话框 （请参见图 2）。


[![新建项目对话框](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)

**图 01**： 添加新的控制器 ([单击以查看实际尺寸的图像](creating-a-controller-cs/_static/image2.png))


[![新建项目对话框](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)

**图 02**: 添加控制器对话框 ([单击以查看实际尺寸的图像](creating-a-controller-cs/_static/image4.png))


请注意，以突出显示，控制器名称的第一部分**添加控制器**对话框。 每个控制器名称必须以后缀结尾*控制器*。 例如，可以创建名为的控制器*ProductController*但不是名为的控制器*产品*。


如果您创建一个控制器缺失*控制器*后缀，然后你将无法调用控制器。 不执行此操作，我已经浪费无数小时的人生旅途之后再犯此错误。


**代码清单 1-Controllers\ProductController.cs**

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

您应始终创建 Controllers 文件夹中的控制器。 否则为将会违反 ASP.NET MVC 的约定和其他开发人员会更加困难时间来了解你的应用程序。

### <a name="scaffolding-action-methods"></a>操作方法的基架

当你创建一个控制器时，您可以选择自动生成创建、 更新和的详细信息的操作方法 （请参见图 3）。 如果选择此选项，则会生成代码清单 2 中的控制器类。


[![自动创建的操作方法](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)

**图 03**： 自动创建的操作方法 ([单击以查看实际尺寸的图像](creating-a-controller-cs/_static/image6.png))


**代码清单 2-Controllers\CustomerController.cs**

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

这些生成的方法是存根 （stub） 方法。 必须添加用于创建、 更新和显示详细信息的客户自己的实际逻辑。 但是，存根 （stub） 方法为您提供很好的起点。

### <a name="creating-a-controller-class"></a>创建控制器类

ASP.NET MVC 控制器是只是一个类。 如果您愿意，可以忽略方便 Visual Studio 控制器基架和手动创建的控制器类。 请执行这些步骤：

1. 右键单击 Controllers 文件夹，然后选择菜单选项**添加、 新建项**，然后选择**类**模板 （请参阅图 4）。
2. 命名新类 PersonController.cs，然后单击**添加**按钮。
3. 修改生成的类文件，使类继承自基 system.web.mvc.controller 中衍生类 （请参阅代码清单 3）。


[![创建一个新类](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)

**图 04**： 创建一个新类 ([单击以查看实际尺寸的图像](creating-a-controller-cs/_static/image8.png))


**代码清单 3-Controllers\PersonController.cs**

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

在清单 3 中的控制器公开一个名为 index （） 返回字符串"Hello World ！"的操作。 你可以通过运行应用程序并请求的 URL 如下所示调用此控制器操作：

`http://localhost:40071/Person`

> [!NOTE]
> 
> ASP.NET 开发服务器使用一个随机端口号 (例如，40071)。 当输入时要调用控制器的 URL，你将需要提供正确的端口号。 可以通过鼠标悬停在该图标在 Windows 通知区域 （在屏幕的右下方） 中的 ASP.NET 开发服务器确定端口号。
> 
> [!div class="step-by-step"]
> [上一页](adding-dynamic-content-to-a-cached-page-cs.md)
> [下一页](creating-an-action-cs.md)
