---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: 开始使用 AJAX 控件工具包 (C#) |Microsoft Docs
author: microsoft
description: 了解所有需要了解开始使用 AJAX 控件工具包。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 6ecf716b78a789ca72e8b35e0be3e1fd0b957052
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824878"
---
<a name="get-started-with-the-ajax-control-toolkit-c"></a>开始使用 AJAX 控件工具包 (C#)
====================
by [Microsoft](https://github.com/microsoft)

> 了解所有需要了解开始使用 AJAX 控件工具包。


AJAX 控件工具包包含 30 多个可用控件，可以在 ASP.NET 应用程序中使用。 在本教程中，您将学习如何下载 AJAX 控件工具包和工具包控件添加到 Visual Studio/Visual Web Developer 速成版工具箱。

## <a name="downloading-the-ajax-control-toolkit"></a>下载 AJAX 控件工具包

[AJAX 控件工具包](http://devexpress.com/act)由 ASP.NET 社区和 ASP.NET 团队的成员一个开放源代码项目开发。 


[![下载 AJAX 控件工具包](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)

**图 01**： 下载 AJAX 控件工具包 ([单击以查看实际尺寸的图像](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))


下载文件后，你需要取消阻止文件。 右键单击该文件，选择属性，然后单击**解除阻止**按钮 （请参见图 2）。


[![取消阻止 AJAX 控件工具包 ZIP 文件](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)

**图 02**： 取消阻止 AJAX 控件工具包 ZIP 文件 ([单击以查看实际尺寸的图像](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))


取消阻止文件后，你可以解压缩该文件： 右键单击该文件，然后选择**全部提取**菜单选项。 现在，我们已准备好工具包添加至 Visual Studio/Visual Web Developer 工具箱。

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>向工具箱添加 AJAX 控件工具包

使用 AJAX 控件工具包的最简单方法是工具包添加至您的 Visual Studio/Visual Web Developer 工具箱 （参见图 3）。 这样一来，您可以只需将工具包控件拖到页面时想要使用它。


[![AJAX 控件工具包将出现在工具箱](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)

**图 03**: AJAX 控件工具包将出现在工具箱 ([单击以查看实际尺寸的图像](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))


首先，需要将 AJAX 控件工具包选项卡添加到工具箱。 请按照下列步骤。

1. 通过选择菜单选项文件中，新的网站中创建新的 ASP.NET 网站。 双击解决方案资源管理器窗口中的 Default.aspx，以在编辑器中打开该文件。
2. 右键单击常规选项卡下的工具箱，然后选择菜单选项**添加选项卡**（请参阅图 4）。
3. 输入名为 AJAX 控件工具包的新选项卡。


[![添加一个新选项卡](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)

**图 04**： 添加一个新选项卡 ([单击以查看实际尺寸的图像](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))


接下来，您需要将 AJAX 控件工具包控件添加到新的选项卡。请执行这些步骤：

- AJAX 控件工具包选项卡下方右键单击，然后选择菜单选项**选择项 （请参见图 5）**。
- 浏览到解压缩 AJAX 控件工具包和选择 AjaxControlToolkit.dll 程序集的位置。


[![选择要添加到工具箱项](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)

**图 05**： 选择要添加到工具箱项 ([单击以查看实际尺寸的图像](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))


完成这些步骤后，所有工具包控件都将出现在工具箱中。

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>升级到新版本的工具包

如果已使用较旧版本的工具包，现在需要将移动到更高版本的建议的步骤是：

- 二进制文件-从您网站的 Bin 文件夹中删除 AjaxControlToolkit.dll 程序集的旧版本。
- 工具箱项-删除 AJAX 控件工具包选项卡，然后按照上述步骤来重新创建具有 AjaxControlToolkit.dll 程序集的新版本的选项卡。

> [!div class="step-by-step"]
> [下一篇](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
