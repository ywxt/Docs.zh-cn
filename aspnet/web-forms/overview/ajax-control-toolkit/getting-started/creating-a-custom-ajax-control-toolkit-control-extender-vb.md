---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: 创建自定义 AJAX 控件工具包扩展程序控件 (VB) |Microsoft Docs
author: microsoft
description: 自定义扩展程序，可以自定义和扩展的 ASP.NET 控件的功能而无需创建新的类。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 7f0cbee47b541e31f3e9f01e42afeabcd7b9769f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833475"
---
<a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a>创建自定义 AJAX 控件工具包扩展程序控件 (VB)
====================
by [Microsoft](https://github.com/microsoft)

> 自定义扩展程序，可以自定义和扩展的 ASP.NET 控件的功能而无需创建新的类。


在本教程中，您将学习如何创建自定义 AJAX 控件工具包控件扩展程序。 我们创建一个简单，但更改按钮的状态从禁用启用时文本框中键入文本的有用、 新的扩展程序。 阅读本教程之后, 你将能够扩展 ASP.NET AJAX 工具包使用您自己控件扩展器。

您可以创建自定义控件扩展程序使用 Visual Studio 或 Visual Web Developer （请确保具有最新版本的 Visual Web Developer）。

## <a name="overview-of-the-disabledbutton-extender"></a>DisabledButton 扩展程序的概述

我们新的控件扩展程序名称为 DisabledButton 扩展程序。 此扩展器将具有三个属性：

- TargetControlID-控件扩展的文本框。
- TargetButtonIID-已禁用或启用的按钮。
- DisabledText-最初在按钮中显示的文本。 当您开始键入时，按钮将显示按钮文本属性的值。

可以将挂接到文本框和按钮控件 DisabledButton 扩展器。 键入的任何文本之前，将禁用的按钮和文本框和按钮如下所示：


[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

([单击此项可查看原尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))


开始键入文本后，启用该按钮和文本框和按钮如下所示：


[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

([单击此项可查看原尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))


若要创建我们控件扩展程序，我们需要创建以下三个文件：

- DisabledButtonExtender.vb-此文件是将管理创建您的扩展器，并允许您在设计时设置的属性的服务器端控件类。 它还定义了可以在您的扩展器设置的属性。 这些属性可通过代码和设计时访问和 DisableButtonBehavior.js 文件中定义的属性匹配。
- DisabledButtonBehavior.js-此文件是您将添加所有客户端脚本逻辑。
- DisabledButtonDesigner.vb-此类使设计时功能。 如果你想要正常使用 Visual Studio/Visual Web Developer 设计器的控件扩展程序，则需要此类。

因此控件扩展程序包含服务器端控件、 客户端的行为和服务器端设计器类。 了解如何在以下各节中创建所有这三个这些文件。

## <a name="creating-the-custom-extender-website-and-project"></a>创建自定义扩展程序网站和项目

第一步是在 Visual Studio/Visual Web Developer 中创建一个类库项目和网站。 我们将在类库项目中创建自定义扩展程序和网站中测试自定义扩展程序。

让我们来开始与网站。 请按照下列步骤以创建网站：

1. 选择菜单选项**文件，新的 Web 站点**。
2. 选择**ASP.NET Web 站点**模板。
3. 新网站命名*Website1*。
4. 单击**确定**按钮。

接下来，我们需要创建将包含控件扩展程序的代码类库项目：

1. 选择菜单选项**文件中，添加新项目**。
2. 选择**类库**模板。
3. 具有名称命名的新类库**CustomExtenders**。
4. 单击**确定**按钮。

完成这些步骤后，在解决方案资源管理器窗口应如图 1 所示。


[![与网站和类的类库项目的解决方案](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)

**图 01**： 与网站和类的类库项目的解决方案 ([单击以查看实际尺寸的图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))


接下来，您需要添加所有必要的程序集引用对类库项目：

1. 右键单击 CustomExtenders 项目，然后选择菜单选项**添加引用**。
2. 选择.NET 选项卡。
3. 添加对下列程序集的引用：

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. System.Web.Extensions.Design.dll
4. 选择浏览选项卡。
5. 添加对 AjaxControlToolkit.dll 程序集的引用。 此程序集位于在其中下载 AJAX 控件工具包的文件夹中。

你可以验证，你已添加所有正确引用通过右键单击项目，选择属性，然后单击引用选项卡 （请参见图 2）。


[![使用所需的引用引用文件夹](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)

**图 02**： 与所需的引用引用文件夹 ([单击以查看实际尺寸的图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))


## <a name="creating-the-custom-control-extender"></a>创建自定义控件扩展程序

现在，我们有我们的类库，我们可以开始构建我们的扩展程序控件。 让我们来开始准系统的自定义扩展程序控件类 （请参阅代码清单 1）。

**代码清单 1-MyCustomExtender.vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

有几种您注意到有关列表 1 中的控件扩展程序类的方法。 首先，请注意该类继承 ExtenderControlBase 类的基类。 所有 AJAX 控件工具包扩展程序控件都派生自这个基类。 例如，基本类包括为每个控件扩展程序的必需的属性的 TargetID 属性。

接下来，请注意，类包含与客户端脚本相关的以下两个属性：

- WebResource-导致文件以将其包含在程序集中嵌入的资源。
- ClientScriptResource-会导致要从程序集中检索的脚本资源。

WebResource 属性用于编译自定义扩展器时，将 MyControlBehavior.js JavaScript 文件嵌入到程序集。 ClientScriptResource 属性用于在网页中使用自定义扩展器时，从该程序集检索 MyControlBehavior.js 脚本。


为了使 WebResource 和 ClientScriptResource 属性，若要运行，必须作为嵌入资源编译 JavaScript 文件。 选择解决方案资源管理器窗口中的文件，打开属性页中，并将该值赋*嵌入的资源*到**生成操作**属性。


请注意，控件扩展程序还包含 TargetControlType 属性。 此属性用于指定由扩展程序控件扩展的控件的类型。 列表 1 中，对于控件扩展程序用于扩展一个文本框。

最后，请注意，自定义扩展器包括名为 MyProperty 的属性。 该属性用 ExtenderControlProperty 特性标记。 GetPropertyValue() 和 SetPropertyValue() 方法用于将属性值从服务器端控件扩展程序传递到客户端的行为。

让我们来继续操作并实现我们 DisabledButton 扩展程序的代码。 可以在代码清单 2 中找到此扩展器的代码。

**代码清单 2-DisabledButtonExtender.vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

列表 2 中的 DisabledButton 扩展器具有两个名为 TargetButtonID 和 DisabledText 的属性。 应用于 TargetButtonID 属性 IDReferenceProperty 防止将按钮控件的 ID 以外的任何分配给此属性。

WebResource 和 ClientScriptResource 属性将位于名为 DisabledButtonBehavior.js 此扩展器的文件中的客户端的行为相关联。 我们将讨论下一节中的此 JavaScript 文件。

## <a name="creating-the-custom-extender-behavior"></a>创建自定义扩展器行为

控件扩展程序的客户端组件称为一种行为。 禁用和启用该按钮的实际逻辑包含在 DisabledButton 行为。 行为的 JavaScript 代码包含在列表 3 中。

**代码清单 3-DisabledButton.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

列表 3 中的 JavaScript 文件包含一个名为 DisabledButtonBehavior 的客户端类。 此类，如其服务器端孪生，包括两个属性名为 TargetButtonID 并使用户能够使用 DisabledText 获取\_TargetButtonID/set\_TargetButtonID 并获取\_DisabledText/设置\_DisabledText。

Initialize （） 方法的行为的目标元素相关联的 keyup 事件处理程序。 与此行为关联的文本框中键入字母每次 keyup 处理程序执行。 Keyup 处理程序可以启用或禁用按钮具体取决于是否包含任何文本与该行为关联的文本框。

请记住，必须编译 JavaScript 文件作为嵌入资源清单 3 中。 选择解决方案资源管理器窗口中的文件，打开属性页中，并将该值赋*嵌入的资源*到**生成操作**属性 （请参见图 3）。 此选项是在 Visual Studio 和 Visual Web Developer 中可用。


[![添加一个 JavaScript 文件作为嵌入资源](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)

**图 03**： 添加一个 JavaScript 文件作为嵌入资源 ([单击以查看实际尺寸的图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))


## <a name="creating-the-custom-extender-designer"></a>创建自定义扩展程序设计器

没有一个我们需要进行创建，以完成我们的扩展程序的最后一个类。 我们需要在列表 4 中创建设计器类。 此类是使扩展器与 Visual Studio/Visual Web Developer 设计器正常运行所必需的。

**列表 4-DisabledButtonDesigner.vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

将列表 4 中的设计器与使用设计器属性 DisabledButton 扩展程序相关联。需要将设计器特性应用于 DisabledButtonExtender 类如下：

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a>使用自定义扩展程序

现在，我们已完成创建 DisabledButton 扩展程序控件，就可以在我们的 ASP.NET 网站中使用它。 首先，我们需要向工具箱添加自定义扩展程序。 请执行这些步骤：

1. 通过双击解决方案资源管理器窗口中的页中打开 ASP.NET 页。
2. 右键单击工具箱，然后选择菜单选项**选择项**。
3. 在选择工具箱项对话框中，浏览到 CustomExtenders.dll 程序集。
4. 单击**确定**按钮以关闭对话框。

完成这些步骤后，DisabledButton 控件扩展程序应显示在工具箱中 （请参阅图 4）。


[![在工具箱 DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)

**图 04**： 在工具箱中 DisabledButton ([单击以查看实际尺寸的图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))


接下来，我们需要创建一个新的 ASP.NET 页面。 请执行这些步骤：

1. 创建一个名为 ShowDisabledButton.aspx 的新 ASP.NET 页。
2. 将 ScriptManager 拖到绘图页上。
3. 将 TextBox 控件拖到绘图页上。
4. 将按钮控件拖到绘图页上。
5. 在属性窗口中，将按钮 ID 属性更改为值<em>btnSave</em>的值的 Text 属性*保存\**。
  

我们使用标准 ASP.NET 文本框和按钮控件创建一个页面。

接下来，我们需要扩展具有 DisabledButton 扩展程序的文本框控件：

1. 选择**添加扩展程序**任务选项以打开扩展程序向导对话框 （请参见图 5）。 请注意，该对话框包含我们自定义 DisabledButton 扩展程序。
2. 选择 DisabledButton 扩展器，然后单击**确定**按钮。


[![扩展程序向导对话框](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)

**图 05**： 在扩展器向导对话框 ([单击以查看实际尺寸的图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))


最后，我们可以设置 DisabledButton 扩展程序的属性。 可以通过修改的 TextBox 控件的属性来修改 DisabledButton 扩展程序属性：

1. 在设计器中选择文本框中。
2. 在属性窗口中，展开的扩展程序节点 （请参阅图 6）。
3. 将该值赋*保存*DisabledText 属性以及值*btnSave* TargetButtonID 属性。


[![设置扩展程序属性](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)

**图 06**： 设置扩展程序属性 ([单击以查看实际尺寸的图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))


（按 F5） 运行页面时，按钮控件最初处于禁用状态。 一旦您开始在文本框中输入文本，则控件被启用的按钮 （请参阅图 7）。


[![在操作中 DisabledButton 扩展器](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)

**图 07**: DisabledButton 扩展程序中操作 ([单击以查看实际尺寸的图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))


## <a name="summary"></a>总结

本教程的目的是说明如何扩展 AJAX 控件工具包与自定义扩展程序控件。 在本教程中，我们创建一个简单的 DisabledButton 控件扩展程序。 我们通过创建 DisabledButtonExtender 类、 DisabledButtonBehavior JavaScript 行为和 DisabledButtonDesigner 类实现此扩展器。 每当创建自定义控件扩展程序时遵循一组类似的步骤。

> [!div class="step-by-step"]
> [上一篇](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
