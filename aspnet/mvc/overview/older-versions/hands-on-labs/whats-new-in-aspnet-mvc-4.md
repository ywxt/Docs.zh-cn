---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: 什么是 ASP.NET MVC 4 中的新增功能 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 是一个框架，用于构建可缩放的基于标准的 web 应用程序使用成熟设计模式和 ASP.NET 的强大功能和...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9d5a51a5887ecbbc96fce1416b88aa849bc3674e
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48912717"
---
# <a name="whats-new-in-aspnet-mvc-4"></a>什么是 ASP.NET MVC 4 中的新增功能

通过[Web 训练营团队](https://twitter.com/webcamps)

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4 是一个框架，用于构建可缩放的基于标准的 web 应用程序使用成熟设计模式和 ASP.NET 和.NET framework 的强大功能。 此新，第四个版本的 framework 侧重于提高移动 web 应用程序开发更容易。

开始时，创建新的 ASP.NET MVC 4 项目时现在可用于构建一款独立应用专用于移动设备的移动应用程序项目模板。 此外，ASP.NET MVC 4 与通过 jQuery.Mobile.MVC NuGet 程序包的 jQuery Mobile 集成。 jQuery Mobile 是用于开发 web 应用与所有主流移动设备平台，包括 Windows Phone、 iPhone、 Android 等兼容的基于 HTML5 的框架。 但是，如果你需要专用化，ASP.NET MVC 4 还可以提供适用于不同设备的不同视图，并提供特定于设备的优化。

在此动手实验中，将开始使用 ASP.NET MVC 4 &quot;Internet 应用程序&quot;项目模板创建照片库应用程序。 您将逐渐增强使用的 jQuery Mobile 和 ASP.NET MVC 4 的新功能，使其与不同的移动设备和桌面 web 浏览器兼容的应用。 你还将了解对代码生成和如何 ASP.NET MVC 4 可以更轻松地编写异步操作方法，通过支持任务的新代码方案&lt;ActionResult&gt;返回类型。

> [!NOTE]
> 在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。 特定于此实验室项目位于[What's New in ASP.NET 4.5 中的 Web 窗体](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)。

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验，您将学习如何：

- 充分利用 ASP.NET MVC 项目模板包括新的移动应用程序项目模板的增强功能
- 使用 HTML5 视区属性和 CSS 媒体查询来改善在移动设备上显示
- 使用 jQuery Mobile 的渐进式增强功能和用于构建触控优化的 web UI
- 创建移动特定视图
- 使用视图切换器组件来移动和桌面应用程序中的视图之间切换
- 创建使用任务支持异步控制器

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

必须具有要完成本实验的以下项：

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 B](#AppendixB)有关如何安装它的说明)。
- [ASP.NET MVC 4](../../../mvc4.md) （包含在 Microsoft Visual Studio 2012 安装）
- Windows Phone 仿真程序 (包含在[Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))
- 可选- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/)与**Electric Plum iPhone 模拟器**扩展 （仅适用于用来与 iPhone 模拟器中浏览 web 应用程序的练习 3)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>安装

在整个实验文档中，将指示您插入代码块。 为方便起见，该代码的大部分以 Visual Studio 代码段，可用于从 Visual Studio 内无需手动添加形式提供。

若要安装的代码片段：

1. 打开 Windows 资源管理器窗口并浏览到本实验**Source\Setup**文件夹。
2. 双击**Setup.cmd**此文件夹来安装 Visual Studio 代码段中的文件。

如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 a： 使用代码片段](#AppendixA)&quot;。

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [新的 ASP.NET MVC 4 项目模板](#Exercise1)
2. [创建照片库 Web 应用程序](#Exercise2)
3. [添加对移动设备的支持](#Exercise3)
4. [使用异步控制器](#Exercise4)

> [!NOTE]
> 每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。 如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。


估计的时间才能完成此实验： **60 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a>练习 1： 新的 ASP.NET MVC 4 项目模板

在此练习中，您将了解在 ASP.NET MVC 4 项目模板中的增强功能。 除了 Internet 应用程序模板，在 MVC 3 中已存在此版本现在包括用于移动应用程序单独的模板。 首先，您将查看每个模板的某些相关功能。 然后，将适用于通过使用适当的方法呈现页面在不同平台上正常运行。

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a>任务 1-浏览 Internet 应用程序模板

1. 打开**Visual Studio**。
2. 选择**文件 |新 |项目**菜单命令。 在中**新的项目**对话框中，选择**Visual C# |Web**在左窗格中的模板树，并选择**ASP.NET MVC 4 Web 应用程序。** 将项目命名**PhotoGallery**，选择一个位置 （或保留默认值），单击**确定**。

    > [!NOTE]
    > 稍后将自定义现在要创建的图片库 ASP.NET MVC 4 解决方案。

    ![创建新的项目](whats-new-in-aspnet-mvc-4/_static/image1.png "创建新的项目")

    *创建新的项目*
3. 在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**项目模板，然后单击**确定**。 请确保已选择 Razor 作为视图引擎。

    ![创建新 ASP.NET MVC 4 Internet 应用程序](whats-new-in-aspnet-mvc-4/_static/image2.png "新建 ASP.NET MVC 4 Internet 应用程序")

    *创建新 ASP.NET MVC 4 Internet 应用程序*

    > [!NOTE]
    > 在 ASP.NET MVC 3 中引入了 razor 语法。 其目标是字符和击键所需的文件中启用快速、 流畅编码工作流的数量降至最低。 Razor 利用现有 C# / VB （或其他） 语言技能，并提供可以实现令人惊叹的 HTML 构造工作流的模板标记语法。
4. 按**F5**以运行该解决方案和查看已续订的模板。 您可以签出了以下功能：

    **现代样式模板**

    模板已被续订，提供更多的新式样式。

    ![ASP.NET MVC 4 restyled 模板](whats-new-in-aspnet-mvc-4/_static/image3.png "restyled 模板的 MVC 4")

    *ASP.NET MVC 4 restyled 模板*

    ![新联系人页](whats-new-in-aspnet-mvc-4/_static/image4.png "新联系人页")

    *新联系人页*

    **自适应呈现**

    签出调整浏览器窗口，请注意，页面布局如何动态调整为新的窗口大小。 这些模板使用自适应呈现技术在没有任何自定义项的桌面和移动平台中正确呈现。

    ![在不同的浏览器大小中的 ASP.NET MVC 4 项目模板](whats-new-in-aspnet-mvc-4/_static/image5.png "中不同的浏览器大小的 ASP.NET MVC 4 项目模板")

    *在不同的浏览器大小中的 ASP.NET MVC 4 项目模板*

    **使用 JavaScript 更丰富的 UI**

    默认项目模板的另一个增强功能是使用 JavaScript 来提供更具交互性的 JavaScript。 在模板中使用的登录和注册链接将如何使用 jQuery 验证来验证从客户端的输入的字段。

    ![jQuery 验证](whats-new-in-aspnet-mvc-4/_static/image6.png)

    *jQuery 验证*

    > [!NOTE]
    > 请注意，这两个日志中的第一节中的部分，您可以记录中使用该站点中的注册帐户和可以使用另一个身份验证服务，如 google （默认情况下禁用） 的 altenativelly 登录的第二个部分。
5. 关闭浏览器以停止调试器并返回到 Visual Studio。
6. 打开文件**AuthConfig.cs**位于**应用\_启动**文件夹。
7. 从注册 Google 客户端的最后一行中删除注释*OAuth*身份验证。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > 请注意，可以轻松启用使用如 Facebook、 Twitter、 Microsoft 等任何 OpenID 或 OAuth 服务进行身份验证。
8. 按**F5**运行解决方案并导航到登录页。
9. 选择**Google**服务进行登录。

    ![在服务中选择日志](whats-new-in-aspnet-mvc-4/_static/image7.png)

    *在服务中选择日志*
10. 使用你的 Google 帐户登录。
11. 允许 Google 帐户中检索信息的站点 (localhost)。
12. 最后，您将必须在要将 Google 帐户相关联的站点中注册。

   ![将你的 Google 帐户相关联](whats-new-in-aspnet-mvc-4/_static/image8.png)

   *将你的 Google 帐户相关联*
13. 关闭浏览器以停止调试器并返回到 Visual Studio。
14. 立即浏览要查看由 ASP.NET MVC 4 项目模板中引入了一些其他新功能的解决方案。

   ![ASP.NET MVC 4 Internet 应用程序项目模板](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 Internet 应用程序项目模板")

   *ASP.NET MVC 4 Internet 应用程序项目模板*

   - **HTML 5 标记**

       浏览模板视图若要了解新的主题标记。

       ![使用 Razor 和 HTML5 标记 About.cshtml 新模板.](whats-new-in-aspnet-mvc-4/_static/image10.png "使用 Razor 和 HTML5 标记 About.cshtml 的新模板。")

       *新模板，使用 Razor 和 HTML5 标记 (About.cshtml)。*
   - **更新的 JavaScript 库**

       ASP.NET MVC 4 默认模板现在包括 KnockoutJS、 允许您创建丰富的 JavaScript MVVM 框架和高响应 web 应用程序使用 JavaScript 和 HTML。 如在 MVC3，jQuery 和 jQuery UI 库都还包含在 ASP.NET MVC 4。

     > [!NOTE]
     > 可以获取有关此链接中的 KnockOutJS 库的详细信息： [ [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/) ](http://learn.knockoutjs.com/)。 此外，了解有关 jQuery 和 jQuery UI 中[ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/)。

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a>任务 2-探索移动应用程序模板

ASP.NET MVC 4 便于网站适用于移动设备和平板电脑浏览器的开发。 此模板具有相同的应用程序结构为 Internet 应用程序模板 （请注意控制器代码，并几乎完全相同），但其样式进行了修改以便在基于触控的移动设备中正确呈现。

1. 选择**文件 |新 |项目**菜单命令。 在中**新的项目**对话框中，选择**Visual C# |Web**在左窗格中的模板树，并选择**ASP.NET MVC 4 Web 应用程序。** 将项目命名**PhotoGallery.Mobile**，选择一个位置 （或保留默认值），选择&quot;将添加到解决方案&quot;然后单击**确定**。
2. 在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Mobile 应用程序**项目模板，然后单击**确定**。 请确保已选择 Razor 作为视图引擎。

    ![创建新 ASP.NET MVC 4 移动应用程序](whats-new-in-aspnet-mvc-4/_static/image11.png "新建 ASP.NET MVC 4 移动应用程序")

    *创建新 ASP.NET MVC 4 移动应用程序*
3. 现在，你就能够了解解决方案，并查看一些引入移动的 ASP.NET MVC 4 解决方案模板的新功能：

    - **jQuery 移动库**

        移动应用程序项目模板包括 jQuery 移动库，它是移动浏览器兼容性的开源库。 jQuery Mobile 对支持 CSS 和 JavaScript 的移动浏览器应用渐进增强。 渐进式增强功能，所有浏览器显示网页的基本内容，同时仅使功能最强大的浏览器显示的丰富内容。 JavaScript 和 CSS 文件，包括 jQuery 移动样式在帮助移动浏览器以适应屏幕中的内容，而无需在页标记中进行任何更改。

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        *模板中包括 jQuery 移动库*
    - **基于 HTML5 标记**

        ![Mobile-application-template-using-HTML5-markup](whats-new-in-aspnet-mvc-4/_static/image13.png)

        *使用 HTML5 标记、 （Login.cshtml 和 index.cshtml） 的移动应用程序模板*
4. 按**F5**运行该解决方案。
5. 打开**Windows Phone 7 仿真程序**。
6. 在电话开始屏幕中，打开 Internet Explorer。 签出的桌面应用程序的起始位置的 URL 并通过手机浏览到该 URL (例如`http://localhost:[PortNumber]/`)。
7. 现在，你就能够输入的登录页或查看有关页面。 请注意到该网站的样式基于新美俏移动设备的应用程序。 ASP.NET MVC 4 项目模板正确显示移动设备，从而确保页面的所有元素都都可见且已启用。 请注意，在标头中的链接不够大，无法单击或点击。

    ![项目在移动设备中的模板页](whats-new-in-aspnet-mvc-4/_static/image14.png "项目在移动设备中的模板页")

    *在移动设备中的项目模板页*
8. 新模板还使用了**视区 meta 标记**。 大多数移动浏览器定义虚拟浏览器窗口的宽度或&quot;视区&quot;，这比移动设备的实际宽度。 这使得移动浏览器以显示整个 web 页内的虚拟显示器。 **视区 meta 标记**使 web 开发人员的移动设备上设置的宽度、 高度和小数位数为浏览器区域 **。** 移动应用程序的 ASP.NET MVC 4 模板将视区设置为设备宽 (&quot;宽度 = 设备宽度&quot;) 中的布局模板 (*views/shared\_Layout.cshtml*)，以便所有页面将具有其视区设置为设备屏幕宽度。 请注意，视区 meta 标记不会更改默认浏览器视图。
9. 打开 **\_Layout.cshtml**，它位于**视图 |共享**文件夹，并注释视区 meta 标记。 运行应用程序，如果不是已打开，并查看差异。


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

![注释视区 meta 标记后的站点](whats-new-in-aspnet-mvc-4/_static/image15.png "注释视区 meta 标记后的站点")

*注释视区 meta 标记后站点*
10. 在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。
11. 取消注释视区 meta 标记。


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a>任务 3-使用自适应呈现

在本任务中，您将学习另一种方法，而无需进行任何自定义同时呈现在移动设备和 Web 浏览器上正常网页。 你已具有类似用途使用视区 meta 标记。 现在就可以满足另一个功能强大的方法：*自适应呈现*。

自适应呈现是使用一种技术**CSS3 媒体查询**自定义应用于页面的样式。 媒体查询定义分组的特定条件下的 CSS 样式的样式表内的条件。 仅当条件为 true，则会将样式应用于已声明的对象。

提供的自适应呈现技术的灵活性使不同的设备上显示该站点进行任何自定义。 您可以定义任意多个样式所需的单一样式表上而无需编写逻辑代码选择样式。 因此，因为它可以减少重复的代码和用于呈现目的的逻辑的数量是调整页样式的一种非常巧妙方法。 但是，带宽消耗会增加，如 CSS 文件的大小会变得略微。

通过使用自适应呈现技术，站点将**正确显示，而不考虑浏览器。** 但是，应该考虑是否加载了额外的带宽是一个问题。

> [!NOTE]
> 媒体查询的基本格式： @media \[作用域： 所有 | 手持 | 打印 | 投影 | 屏幕\]([属性： 值]，然后...[属性： 值]）


媒体查询的示例： &gt;  <strong>@media所有和 (最大宽度： 1000 像素) 和 (最小宽度： 700px) {}:</strong>有关 700px 和 1000 像素之间的所有解决方法。

> <strong>@media 屏幕和 (最小宽度： 400px) 和 (最大宽度： 700px) {...}:</strong>仅对于屏幕。 解决方法必须介于 400 和 700px 之间。
> 
> <strong>@media 手持和 (最小宽度： 20em)，屏幕和 (最小宽度： 20em) {...}:</strong>手持设备 （移动设备和设备） 和屏幕。 最小宽度必须大于 20em。
> 
> 有关更多相关信息[W3C 站点](http://www.w3.org/TR/css3-mediaqueries/)。


您现在将探索自适应呈现的工作原理、 提高其可读性的 ASP.NET MVC 4 默认网站模板。

1. 打开**PhotoGallery.sln**解决方案已在任务 1 中创建并选择**PhotoGallery**项目。 按**F5**运行该解决方案。
2. 调整浏览器的宽度，设置 windows 到一半或小于其原始大小的四分之一。 请注意，在标头中的项会出现什么情况： 一些元素不会显示在标头的可见区域。
3. 打开<strong>Site.css</strong>文件从 Visual Studio 解决方案资源管理器，位于<strong>内容</strong>项目文件夹。 按<strong>CTRL + F</strong>若要打开 Visual Studio 集成的搜索，并写入<strong>@media</strong>查找<strong>CSS 媒体查询</strong>。

    此模板中定义的媒体查询条件的工作以这种方式： 当浏览器的窗口大小低于**850 px**，应用的 CSS 规则是在此媒体块内定义的。

    ![定位到该媒体查询](whats-new-in-aspnet-mvc-4/_static/image16.png "定位到该媒体查询")

    *定位到该媒体查询*
4. 850 中设置的最大宽度属性值替换为与 px **10px**，以便禁用自适应呈现，然后按**CTRL + S**以保存所做的更改。 返回到浏览器并按**CTRL + F5**若要刷新所做的更改与页面。 调整窗口的宽度时，请注意这两个页中的差异。

    ![在左侧，应用页@media省略样式，请在右侧，样式](whats-new-in-aspnet-mvc-4/_static/image17.png "左侧，在应用页@media省略样式，请在右侧，样式")

    <em>在左侧，应用页@media省略样式，请在右侧，样式</em>

    现在，我们来看下在移动设备上会发生什么情况：

    ![在左侧，应用页@media省略样式，请在右侧，样式](whats-new-in-aspnet-mvc-4/_static/image18.png "左侧，在应用页@media省略样式，请在右侧，样式")

    <em>在左侧，应用页@media省略样式，请在右侧，样式</em>

    尽管您会注意到，在 Web 浏览器中呈现页时不更改非常重要，使用移动设备时的差异变得更明显。 在左侧和右侧的图像，我们可以看到的自定义样式提高了可读性。

    可以在很多情况，从而更便于将条件设置到网站上的样式和解决常见的一种巧妙方法样式问题应用中使用自适应呈现。

    视区 meta 标记和 CSS 媒体查询不是特定于 ASP.NET MVC 4 中，因此您可以在任何 web 应用程序中充分利用这些功能。
5. 在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a>练习 2： 创建照片库 Web 应用程序

在此练习中，您将适用于显示照片的照片库应用程序。 ASP.NET MVC 4 项目模板，将开始，然后您将添加一项功能以从服务中检索照片并将其显示在主页页面中。

在以下练习中，你将更新此解决方案以增强移动设备显示的方式。

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a>任务 1-创建 Mock 照片服务

在本任务中，您将创建要检索的内容将显示在库中的照片服务的模拟。 若要执行此操作，将添加将只返回每张照片的数据的 JSON 文件的新控制器。

1. 打开**Visual Studio**如果尚未打开。
2. 选择**文件 |新 |项目**菜单命令。 在中**新的项目**对话框中，选择**Visual C# |Web**在左窗格中的模板树，并选择**ASP.NET MVC 4 Web 应用程序。** 将项目命名**PhotoGallery**，选择一个位置 （或保留默认值），单击**确定**。 或者，从现有的 ASP.NET MVC 4 继续工作**Internet 应用程序**从解决方案**练习 1**并跳过下一步。
3. 在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**项目模板，然后单击**确定**。 请确保具有 Razor 视图引擎为所选。
4. 在中**解决方案资源管理器**，右键单击**应用\_数据**文件夹的项目，然后选择**添加 |现有项**。 浏览到**Source\Assets\App\_数据**本实验的文件夹，并添加**Photos.json**文件。
5. 创建新的控制器名称**PhotoController**。 若要执行此操作，右键单击**控制器**文件夹中，转到**添加**，然后选择**控制器。** 完成该控制器的名称，将保留**空 MVC 控制器**模板，然后单击**添加**。

    ![添加 PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "添加 PhotoController")

    *添加 PhotoController*
6. 替换**索引**方法替换以下**库**操作，并返回内容时从您最近添加到项目的 JSON 文件。

    (代码段- *ASP.NET MVC 4 实验-Ex02-库操作*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. 按**F5**运行该解决方案，然后浏览到以下 URL 以测试模拟的照片服务： `http://localhost:[port]/photo/gallery` （已启动应用程序的当前端口上的 [端口] 值取决于）。 对此 URL 的请求应检索的内容**Photos.json**文件。

    ![测试模拟的照片服务](whats-new-in-aspnet-mvc-4/_static/image20.png "测试模拟的照片服务")

    *测试模拟的照片服务*

在实际实现可以使用[ASP.NET Web API](../../../../web-api/index.md)实现照片库服务。 ASP.NET Web API 是一种框架，可以轻松地构建 HTTP 服务访问范围广泛的客户端，包括浏览器和移动设备。 ASP.NET Web API 是用于在 .NET Framework 上生成 RESTful 应用程序的理想平台。

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a>任务 2-显示照片库

在本任务中，你将更新主页上要显示在照片库，请使用此练习中的第一个任务中创建的模拟的服务。 将添加模型文件并更新库视图。

1. 在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。
2. 创建**照片**类**模型**文件夹。 若要执行此操作，右键单击**模型**文件夹，选择**添加**然后单击**类**。 然后，将名称设置为**Photo.cs**然后单击**添加**。
3. 添加到以下成员**照片**类。

    (代码段- *ASP.NET MVC 4 实验-Ex02-照片模型*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. 从“控制器”文件夹打开 HomeController.cs 文件。
5. 添加下面的 using 语句。

    (代码段- *ASP.NET MVC 4 实验-Ex02-HomeController Using*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. 更新**索引**操作以使用**HttpClient**检索库数据，然后使用**JavaScriptSerializer**要反其序列化到视图模型。

    (代码段- *ASP.NET MVC 4 实验-Ex02-索引操作*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. 打开**Index.cshtml**下的文件**views/home**文件夹并将替换为以下代码的所有内容。

    此代码循环访问从服务检索的所有照片，并将它们显示为未排序列表。

    (代码段- *ASP.NET MVC 4 实验-Ex02-照片列表*)

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. 在中**解决方案资源管理器**，右键单击**内容**文件夹的项目，然后选择**添加 |现有项**。 浏览到**Source\Assets\Content**本实验的文件夹，并添加**Site.css**文件。 必须确认其替换。 如果有**Site.css**文件打开时，必须确认还重新加载该文件。
9. 打开文件资源管理器，并复制整个**照片**文件夹位于下**Source\Assets**此体验的解决方案资源管理器中的项目的根文件夹的文件夹。
10. 运行该应用程序。 现在应看到在库中显示照片的主页。

    ![照片库](whats-new-in-aspnet-mvc-4/_static/image21.png "照片库")

    *照片库*
11. 在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a>练习 3： 添加对移动设备的支持

一个 ASP.NET MVC 4 中的关键更新是适用于移动开发的支持。 在此练习中，您将通过扩展已在上一练习中创建的图片库解决方案浏览 ASP.NET MVC 4 移动应用程序的新功能。

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a>任务 1-ASP.NET MVC 4 应用程序的安装 jQuery Mobile

1. 打开**开始**解决方案位于**源/Ex3-MobileSupport/开始/** 文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 打开**程序包管理器控制台**通过单击**工具** > **NuGet 包管理器** > **包管理器控制台**菜单选项。

    ![打开 NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "打开 NuGet 包管理器控制台")

    *打开 NuGet 包管理器控制台*
3. 在包管理器控制台中运行以下命令以安装**jQuery.Mobile.MVC**包。

    jQuery Mobile 是一个开源库，用于构建触控优化的 web UI。 JQuery.Mobile.MVC NuGet 程序包包括帮助程序以使用 jQuery Mobile 与 ASP.NET MVC 4 应用程序。

    > [!NOTE]
    > 通过运行以下命令，你将下载 jQuery.Mobile.MVC 库从 Nuget。

    PM

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    此命令将安装 jQuery Mobile 和一些帮助器文件，其中包括：

    - **Views/Shared/\_Layout.Mobile.cshtml**： 是针对较小屏幕而优化的 jQuery Mobile 基于布局。 当网站收到请求时从移动浏览器时，它将替换原始布局 (\_Layout.cshtml) 替换为。
    - 视图切换器组件： 组成**Views/Shared/\_ViewSwitcher.cshtml**分部视图和**ViewSwitcherController.cs**控制器。 此组件将在移动浏览器以使用户能够切换到桌面版本的页面上显示的链接。  
        ![照片库项目与移动设备的支持](whats-new-in-aspnet-mvc-4/_static/image23.png "照片库项目与移动设备的支持")

        *照片库项目与移动设备的支持*
4. 注册的移动捆绑包。 若要执行此操作，打开**Global.asax.cs**文件，并添加以下行。

    (代码段- *ASP.NET MVC 4 实验室-Ex03-注册的移动捆绑*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. 运行使用桌面 web 浏览器的应用程序。
6. 打开**Windows Phone 7 仿真器**位于**开始菜单 |所有程序 |Windows Phone SDK 7.1 |Windows Phone 仿真程序。**
7. 在电话开始屏幕中，打开 Internet Explorer。 请查看应用程序的起始位置的 URL 并浏览到该 URL 与手机浏览器 (例如`http://localhost:[PortNumber]/`)。

    您将注意到如 jQuery.Mobile.MVC 具有显示针对移动设备优化的视图在项目中创建新的资产，看起来你的应用程序在 Windows Phone 模拟器中，不同。

    请注意，显示将切换到桌面视图的链接，手机顶部的消息。 此外，  **\_Layout.Mobile.cshtml**已创建的已安装的包的布局应用程序中包含不同的布局。

    > [!NOTE]
    > 到目前为止，没有链接以返回到移动视图。 它将包含在更高版本。

    ![照片库主页上的移动视图](whats-new-in-aspnet-mvc-4/_static/image24.png "照片库主页上的移动视图")

    *照片库主页上的移动视图*
8. 在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a>任务 2-创建移动视图

在此任务中，将改写，以便进行更好地 appareance 在移动设备中的内容创建索引视图的移动版本。

1. 复制**Views\Home\Index.cshtml**查看并将其创建副本、 重命名的新文件粘贴**Index.Mobile.cshtml**。
2. 打开新创建**Index.Mobile.cshtml**查看和替换现有&lt;ul&gt;标记，此代码。 通过执行此操作，你将更新&lt;ul&gt; jQuery 移动数据批注，以使用从 jQuery 移动主题的标记。

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > 请注意：
    > 
    > - **数据角色**属性设置为**listview**将呈现使用 listview 样式的列表。
    > 
    > - **数据嵌入**属性设置为 true 会显示带圆角的边框和边距的列表。
    > 
    > - **数据筛选器**属性设置为**true**将生成一个搜索框。
    > 
    > 您可以了解有关项目文档中的 jQuery 移动约定的详细信息： [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)
3. 按**CTRL + S**以保存所做的更改。
4. 切换到**Windows Phone 仿真程序**和刷新站点。 请注意，新的外观和感觉的库列表中，以及新的搜索框右上角。 然后，在搜索框中键入一个词 (例如， **Tulips**) 才能启动照片库中搜索。

    ![库使用筛选使用 listview 样式](whats-new-in-aspnet-mvc-4/_static/image25.png "库使用筛选使用 listview 样式")

    *使用筛选使用 listview 样式的库*

    总之，具有使用该视图可持续方案创建索引视图中处理的副本&quot;移动&quot;后缀。 此后缀指示到 ASP.NET MVC 4 移动设备生成的每个请求将使用此副本的索引。 此外，您已更新索引视图，以增强站点外观和感觉在移动设备中使用 jQuery Mobile 的移动的版本。
5. 返回到 Visual Studio 并打开**Site.Mobile.css**位于**内容**文件夹。
6. 修复照片标题，以使其显示在右侧的图像的位置。 若要执行此操作，以下代码添加到**Site.Mobile.css**文件。

    CSS

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. 按**CTRL + S**以保存所做的更改。
8. 切换回**Windows Phone 仿真程序**和刷新站点。 请注意，现在可恰当地定位照片标题。

    ![标题位于图像的右侧](whats-new-in-aspnet-mvc-4/_static/image26.png "定位在图像的右侧上的标题")

    *定位在图像的右侧上的标题*

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a>任务 3-jQuery Mobile 主题

每个布局和小组件中的 jQuery Mobile 被针对新的面向对象的 CSS 框架，利用它可以将完整统一的可视化设计主题应用到站点和应用程序。

jQuery Mobile 的默认主题包括 5 个样本指定字母 (a、 b、 c、 d、 e） 的快速参考。

在本任务中，你将更新要使用不同的主题，而不是默认的移动布局。

1. 切换回 Visual Studio。
2. 打开 **\_Layout.Mobile.cshtml**文件位于**views/shared**。
3. 数据角色设置为使用找到的 div 元素&quot;页上&quot;，并更新**数据主题**到&quot; **e**&quot;。

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. 按**CTRL + S**以保存所做的更改。
5. 刷新中的站点**Windows Phone 仿真程序**并留意新的颜色方案。

    ![使用不同的配色方案的移动布局](whats-new-in-aspnet-mvc-4/_static/image27.png "具有不同的配色方案的移动布局")

    *使用不同的配色方案的移动布局*

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a>任务 4-使用视图切换器组件和重写功能的浏览器

移动优化 web pages 的约定将添加其文本是如桌面视图或完整的站点模式，使用户切换到桌面版本的页面的链接。 JQuery.Mobile.MVC 包包括了示例**视图切换器**组件中使用此目的 **\_Layout.Mobile.cshtml**视图。

![若要切换到桌面视图链接](whats-new-in-aspnet-mvc-4/_static/image28.png "链接以切换到桌面视图")

*链接以切换到桌面视图*

视图切换器使用名为的新功能**浏览器重写**。 此功能允许将请求视为其视为来自其他浏览器 （用户代理） 比它们实际来自你的应用程序。

在此任务中，您将了解通过 jQuery.Mobile.MVC 和新浏览器中重写功能在 ASP.NET MVC 4 中添加的视图切换器的示例实现。

1. 切换回 Visual Studio。
2. 打开 **\_Layout.Mobile.cshtml**视图位于下**views/shared**文件夹，注意为分部视图所引用的视图切换器组件。

    ![使用视图切换器组件的移动布局](whats-new-in-aspnet-mvc-4/_static/image29.png "使用视图切换器组件的移动布局")

    *使用视图切换器组件的移动布局*
3. 打开 **\_ViewSwitcher.cshtml**分部视图。

    分部视图使用的新方法**ViewContext.HttpContext.GetOverriddenBrowser()** 来确定 web 请求的来源并显示相应的链接以切换到桌面或移动视图。

    **GetOverridenBrowser**方法将返回**HttpBrowserCapabilitiesBase**对应于当前设置为请求的用户代理的实例 （实际或重写）。 可以使用此值来获取属性，如**IsMobileDevice**。

    ![ViewSwitcher 分部视图](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 分部视图")

    *ViewSwitcher 分部视图*
4. 打开**ViewSwitcherController.cs**类位于**控制器**文件夹。 签出该 SwitchView 操作由 ViewSwitcher 组件中的链接，请注意，新的 HttpContext 方法。

    - **HttpContext.ClearOverridenBrowser()** 方法移除当前请求的任何重写的用户代理。
    - **HttpContext.SetOverridenBrowser()** 方法重写请求的实际用户代理值使用指定的用户代理。  
        ![ViewSwitcher 控制器](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 控制器")  
*ViewSwitcher 控制器*

        浏览器重写是一项核心功能的 ASP.NET MVC 4 中，即使不安装 jQuery.Mobile.MVC 包，这是也可用。 但是，此功能会影响视图、 布局和分部视图，并且它不影响任何依赖于 Request.Browser 对象的功能。

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a>任务 5-在桌面视图中添加视图切换器

在此任务中，你将更新以包括视图切换器的桌面布局。 这将允许移动用户返回到移动视图，浏览桌面视图时。

1. 刷新中的站点**Windows Phone 仿真程序**。
2. 单击**桌面视图**库顶部的链接。 请注意在桌面视图以便返回到移动视图中没有任何视图切换器。
3. 返回到 Visual Studio 并打开 **\_Layout.cshtml**视图。
4. 找到登录节，插入的调用来呈现 **\_ViewSwitcher**下面的分部视图 **\_LogOnPartial**分部视图。 然后，按**CTRL + S**以保存所做的更改。

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. 按**CTRL + S**以保存所做的更改。
6. Windows Phone 仿真程序中刷新页面，然后双击要放大的屏幕。 请注意，现在显示主页页面**移动视图**从移动视图切换到桌面视图的链接。

    ![查看切换器在桌面视图中呈现](whats-new-in-aspnet-mvc-4/_static/image32.png "桌面视图中呈现的视图切换器")

    *在桌面视图中呈现的视图切换器*
7. 再次切换到移动视图，然后浏览到<strong>有关</strong>页 (http://localhost[端口] / Home/有关)。 请注意，即使尚未创建 About.Mobile.cshtml 视图，关于页面将显示使用移动布局 (\_Layout.Mobile.cshtml)。

    ![有关页面](whats-new-in-aspnet-mvc-4/_static/image33.png "有关页面")

    *有关页*
8. 最后，桌面 Web 浏览器中打开的网站。 请注意，没有任何以前的更新具有影响桌面视图。

    ![图片库桌面视图](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery 桌面视图")

    *图片库桌面视图*

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a>任务 6-创建新的显示模式

新的显示模式功能，支持应用程序选择具体取决于生成请求的浏览器的视图。 例如，如果桌面浏览器主页发送请求，应用程序将返回**Views\Home\Index.cshtml**模板。 然后，如果在移动浏览器主页发送请求，应用程序将返回**Views\Home\Index.mobile.cshtml**模板。

在此任务中，您将创建适用于 iPhone 设备的自定义的布局和必须模拟从 iPhone 设备的请求。 若要执行此操作，可以使用任一 iPhone 仿真器/模拟器 (例如[电力移动模拟器](http://www.electricplum.com/)) 或修改用户代理的外接程序的浏览器。 有关如何在 Safari 浏览器中设置的用户代理字符串以模拟 iPhone 的说明，请参阅[如何让 Safari 模拟 IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)中 David Alison 的博文。

**请注意，此任务是可选的可以在整个实验室继续而不执行它。**

1. 在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。
2. 打开**Global.asax.cs**并添加以下 using 语句。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. 将以下突出显示的代码添加到应用程序\_Start 方法。

    (代码段- *ASP.NET MVC 4 实验室-Ex03-iPhone DisplayMode*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

已注册的新**名为为 DefaultDisplayMode &quot;iPhone&quot;** 中静态, **DisplayModeProvider.Instance.Modes**静态列表中，将针对匹配每个传入请求。 如果传入请求包含字符串&quot;iPhone&quot;，ASP.NET MVC 将查找其名称包含的视图&quot;iPhone&quot;后缀。 0 的参数指示如何特定是新的模式;例如，此视图是比常规更具体&quot;.mobile&quot;匹配请求从移动设备的规则。

此代码运行，iPhone 浏览器将生成请求后，将使用你的应用程序**views/shared\\_Layout.iPhone.cshtml**将在下一步骤中创建的布局。

> [!NOTE]
> 测试请求的 iPhone 简化出于演示目的，并且可能无法按预期的每个 iPhone 用户代理字符串 （对应于示例测试是区分大小写） 的这种方式。

4. 创建一份 **\_Layout.Mobile.cshtml**中的文件**views/shared**文件夹并将复制到重命名&quot;  **\_Layout.iPhone.csthml**&quot;.
5. 打开 **\_Layout.iPhone.csthml**在上一步中创建。
6. 数据角色属性设置为使用找到的 div 元素**页上**并将更改**数据主题**归于&quot; &quot;。


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

现在在 ASP.NET MVC 4 应用程序中有 3 个布局：

1. **\_Layout.cshtml**： 对于桌面浏览器所使用的默认布局。
2. **\_Layout.mobile.cshtml**： 为移动设备所使用的默认布局。
3. **\_Layout.iPhone.cshtml**： 适用于 iPhone 设备，使用不同的配色方案来区分从特定布局\_Layout.mobile.cshtml。
7. 按**F5**运行该应用程序和浏览中的站点**Windows Phone 仿真程序**。
8. 打开**iPhone 模拟器**(请参阅[附录 C](#AppendixC)有关如何安装和配置 iPhone 模拟器的说明)，并浏览到该网站太。 请注意，每个电话使用特定的模板。

    ![Using-different-views-for-each-mobile-device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    *对于每个移动设备使用不同的视图*

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a>练习 4： 使用异步控制器

Microsoft.NET Framework 4.5 引入了 C# 和 Visual Basic 中为.NET 编程中的异步功能提供新的基础的新语言功能。 此新基础使异步编程，类似于-和大约为-同步编程一样简单。 你现可使用在 ASP.NET MVC 4 中编写异步操作方法**AsyncController**类。 用于长时间运行的异步操作方法、 非 CPU 绑定的请求。 这样可避免阻止 Web 服务器在处理请求时执行工作。 AsyncController 类通常用于长时间运行的 Web 服务调用。

本练习中介绍了 ASP.NET MVC 4 中的异步操作的基础知识。 如果您希望更深入的了解，可以查看以下文章： [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a>任务 1-实现异步控制器

1. 打开**开始**解决方案位于**源/Ex4-Async/开始/** 文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 打开**HomeController.cs**类派生**控制器**文件夹。
3. 添加以下 using 语句。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. 更新**HomeController**类继承自**AsyncController**。 派生自 AsyncController 控制器使 ASP.NET 能够处理异步请求，并且它们仍可以服务同步操作方法。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. 添加**异步**关键字**索引**方法，并使其返回类型**任务&lt;ActionResult&gt;**。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > **异步**关键字是一个.NET Framework 4.5 提供了新的关键字; 它会告知编译器，此方法包含异步代码。 一个**任务**对象都表示可能在将来某个时刻完成的异步操作。
6. 替换为**客户端。GetAsync()** 调用与使用完整的异步版本，如下所示的 await 关键字。

    (代码段- *ASP.NET MVC 4 实验室-Ex04-GetAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > 在上一版本中，使用**结果**属性从**任务**对象来阻止线程，直到结果为返回 （同步版本）。
    > 
    > 添加**await**关键字告知编译器以异步方式等待方法调用返回的任务。 这意味着仅等待的方法完成后将为以回调形式执行代码的其余部分。 需要注意的另一件事情是您不需要更改的 try-catch 块，以实现此目的： 中背景或前景中发生的异常都仍被捕获，而无需使用处理程序框架提供的任何额外工作。
7. 更改代码以继续进行异步实现通过将行替换为对新代码，如下所示

    (代码段- *ASP.NET MVC 4 实验室-Ex04-ReadAsStringAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. 运行该应用程序。 你会注意到没有较大的变化，但你的代码不会阻止来自线程池使服务器资源的更好地使用并提高性能的线程。

    > [!NOTE]
    > 您可以了解有关在实验室中的新异步编程功能的详细信息&quot;**中使用 C# 和 Visual Basic.NET 4.5 的异步编程**&quot;包含在 Visual Studio 培训工具包。

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a>任务 2-取消标记的处理超时

异步操作方法的返回任务实例还可以支持超时。 在本任务中，将更新索引方法代码以处理超时方案使用取消标记。

1. 返回到 Visual Studio 并按**SHIFT + F5**以停止调试。
2. 添加以下 using 语句**HomeController.cs**文件。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. 更新索引操作，以便接收**CancellationToken**参数。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. 更新**GetAsync**调用即可传递的取消标记。

    (代码段- *CancellationToken 与 ASP.NET MVC 4 实验室-Ex04-SendAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. 修饰*索引*方法替换**AsyncTimeout**属性设置为 500 毫秒和一个**HandleError**属性配置为处理**TaskCanceledException**通过重定向到**TimedOut**视图。

    (代码段- *ASP.NET MVC 4 实验室-Ex04-属性*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. 打开**PhotoController**类和更新**库**方法来延迟执行 1000年毫秒 （1 秒），以模拟长时间运行的任务。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. 打开**Web.config**文件并添加以下元素，从而启用自定义错误。

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. 创建新视图中的**views/shared**名为**TimedOut** ，并使用默认布局。 在解决方案资源管理器，右键单击**views/shared**文件夹，然后选择**添加 |视图**。

    ![对于每个移动设备使用不同的视图](whats-new-in-aspnet-mvc-4/_static/image36.png "对于每个移动设备使用不同的视图")

    *对于每个移动设备使用不同的视图*
9. 更新**TimedOut**查看内容，如下所示。

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. 运行应用程序并导航到的根 URL。 随着您添加**Thread.Sleep**的 1000年毫秒，则会出现超时错误，由生成**AsyncTimeout**属性，来发现**HandleError**属性。

    ![处理超时异常](whats-new-in-aspnet-mvc-4/_static/image37.png "超时异常处理")

    *超时异常处理*

> [!NOTE]
> 此外，可以部署此应用程序到 Windows Azure Web Sites 以下[附录 d： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixD)。


<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>总结

在此动手实验，我们已观察到的一些新功能驻留在 ASP.NET MVC 4 中。 讨论了以下概念：

- 充分利用 ASP.NET MVC 项目模板包括新的移动应用程序项目模板的增强功能
- 使用 HTML5 视区属性和 CSS 媒体查询来改善在移动设备上显示
- 使用 jQuery Mobile 的渐进式增强功能和用于构建触控优化的 web UI
- 创建移动特定视图
- 使用视图切换器组件来移动和桌面应用程序中的视图之间切换
- 创建使用任务支持异步控制器

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>附录 a： 使用代码片段

使用代码段，可以轻松获得相关所需的所有代码。 实验室文档将告诉您完全何时可以使用它们，如下图中所示。

![使用 Visual Studio 代码段代码插入到你的项目](whats-new-in-aspnet-mvc-4/_static/image38.png "使用 Visual Studio 代码段代码插入到你的项目")

*使用 Visual Studio 代码段代码插入到你的项目*

***若要添加代码段使用键盘 (仅限 C#)***

1. 将光标置于要插入的代码。
2. 开始键入代码片段名称 （不带空格或连字符）。
3. 观看作为 IntelliSense 显示匹配的代码段的名称。
4. 选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。
5. 按 Tab 键两次，以在光标位置插入代码段。

![开始键入代码段名称](whats-new-in-aspnet-mvc-4/_static/image39.png "开始键入代码段名称")

*开始键入代码段名称*

![按 tab 键以选择突出显示代码段](whats-new-in-aspnet-mvc-4/_static/image40.png "按选项卡以选择突出显示代码段")

*按 tab 键以选择突出显示代码段*

![再次按 Tab 和代码段将 expand](whats-new-in-aspnet-mvc-4/_static/image41.png "再次按 Tab 和代码段将扩展")

*再次按 Tab 和代码段将扩展*

***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）***

1. 右键单击你想要插入的代码片段。
2. 选择**插入代码段**跟**我的代码片段**。
3. 通过单击选择列表中中的相关代码片段。

![右键单击你想要插入代码段和选择插入代码段](whats-new-in-aspnet-mvc-4/_static/image42.png "右键单击你想要插入代码段和选择插入代码段")

*右键单击你想要插入代码段和选择插入代码段*

![通过单击选择列表中中的相关代码片段](whats-new-in-aspnet-mvc-4/_static/image43.png "通过单击选择列表中中的相关代码片段")

*通过单击选择列表中中的相关代码片段*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>附录 b： 安装 Visual Studio Express 2012 for Web

你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** . 以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。

1. 转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。
2. 单击**立即安装**。 如果还没有**Web 平台安装程序**将重定向以下载并安装。
3. 一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。

    ![安装 Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，然后单击**我接受**以继续。

    ![接受许可条款](whats-new-in-aspnet-mvc-4/_static/image45.png)

    *接受许可条款*
5. 等待，直到下载和安装过程完成。

    ![安装进度](whats-new-in-aspnet-mvc-4/_static/image46.png)

    *安装进度*
6. 安装完成后，单击**完成**。

    ![安装已完成](whats-new-in-aspnet-mvc-4/_static/image47.png)

    *安装已完成*
7. 单击**退出**以关闭 Web 平台安装程序。
8. 若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。

    ![VS Express for Web 磁贴](whats-new-in-aspnet-mvc-4/_static/image48.png)

    *VS Express for Web 磁贴*

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a>附录 c： 安装 WebMatrix 2 和 iPhone 模拟器

若要模拟的 iPhone 设备中运行你的站点可以使用 WebMatrix 扩展&quot;适用于 iPhone 的电力移动模拟器&quot;。 此外，您可以配置相同的扩展名从 Visual Studio 2012 运行模拟器。

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a>任务 1-安装 WebMatrix 2

1. 转到[ [ https://go.microsoft.com/?linkid=9809776 ](https://go.microsoft.com/?linkid=9809776) ](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>WebMatrix 2</em>&quot;。
2. 单击**立即安装**。 如果还没有**Web 平台安装程序**将重定向以下载并安装。
3. 一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。

    ![安装 WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "安装 WebMatrix 2")

    *安装 WebMatrix 2*
4. 阅读所有产品的许可证和条款，然后单击**我接受**以继续。

    ![接受许可条款](whats-new-in-aspnet-mvc-4/_static/image50.png "接受许可条款")

    *接受许可条款*
5. 等待，直到下载和安装过程完成。

    ![安装进度](whats-new-in-aspnet-mvc-4/_static/image51.png "安装进度")

    *安装进度*
6. 安装完成后，单击**完成**。

    ![安装已完成](whats-new-in-aspnet-mvc-4/_static/image52.png "安装已完成")

    *安装已完成*
7. 单击**退出**以关闭 Web 平台安装程序。

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a>任务 2-安装在 iPhone 模拟器扩展

1. 运行**WebMatrix**和打开任何现有的网站或创建一个新。
2. 单击**运行**按钮从**主页**功能区，然后选择**添加新**。

    ![添加新的 WebMatrix 扩展](whats-new-in-aspnet-mvc-4/_static/image53.png "添加新的 WebMatrix 扩展插件")

    *添加新的 WebMatrix 扩展插件*
3. 选择**iPhone 模拟器**然后单击**安装**。

    ![浏览 WebMatrix 扩展](whats-new-in-aspnet-mvc-4/_static/image54.png "浏览 WebMatrix 扩展")

    *浏览 WebMatrix 扩展*
4. 在包的详细信息，请单击**安装**继续扩展安装。

    ![iPhone 模拟器扩展](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 模拟器扩展")

    *iPhone 模拟器扩展*
5. 阅读并接受最终用户许可协议的扩展。

    ![WebMatrix 扩展 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 扩展最终用户许可协议")

    *WebMatrix 扩展最终用户许可协议*
6. 现在，可以从 WebMatrix 中运行你的网站使用 iPhone 模拟器选项。

    ![运行使用 iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "运行使用 iPhone")

    *使用 iPhone 运行*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a>任务 3-配置 Visual Studio 2012 运行 iPhone 模拟器

1. 打开**Visual Studio 2012**和打开的任何网站或创建新的项目。
2. 单击从运行按钮的向下箭头，然后选择**浏览与**。

    ![使用浏览](whats-new-in-aspnet-mvc-4/_static/image58.png "浏览与")

    *浏览与*
3. 在中&quot;浏览方式&quot;对话框中，单击**添加**。
4. 在中&quot;添加程序&quot;对话框中，使用以下值：

   - <strong>程序</strong>: C:\Users\*{CurrentUser}<em>\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe * （相应地更新路径）</em>
   - **自变量**: &quot;1&quot;
   - **友好名称**: iPhone 模拟器

     ![添加程序](whats-new-in-aspnet-mvc-4/_static/image59.png "添加程序")

     *添加程序使用浏览*
5. 单击**确定**并关闭对话框。
6. 现在，已能够从 Visual Studio 2012 在 iPhone 模拟器中运行 Web 应用程序。

    ![浏览包含 iPhone 模拟器](whats-new-in-aspnet-mvc-4/_static/image60.png "浏览包含 iPhone 模拟器")

    *使用 iPhone 模拟器中浏览*

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附录 d： 发布 ASP.NET MVC 4 应用程序使用 Web 部署

本附录将演示如何从 Windows Azure 管理门户创建新的网站和发布应用程序获取按照本实验中，利用 Windows Azure 提供的 Web 部署发布功能。

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>任务 1-创建新的 Web 站点从 Windows Azure 门户

1. 转到[Windows Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。

    > [!NOTE]
    > 使用 Windows Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。 你可以注册[此处](http://aka.ms/aspnet-hol-azure)。

    ![登录到 Windows Azure 门户](whats-new-in-aspnet-mvc-4/_static/image61.png "登录到 Windows Azure 门户")

    *登录到 Windows Azure 管理门户*
2. 单击**新建**命令栏上。

    ![创建新的 Web 站点](whats-new-in-aspnet-mvc-4/_static/image62.png "创建新的 Web 站点")

    *创建新的 Web 站点*
3. 单击**计算** | **网站**。 然后选择**快速创建**选项。 为新网站提供可用的 URL，然后单击**创建网站**。

    > [!NOTE]
    > Windows Azure 网站是可以控制和管理在云中运行的 web 应用程序主机。 快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从门户外部的部署。 它不包括用于设置数据库的步骤。

    ![创建新的网站使用快速创建](whats-new-in-aspnet-mvc-4/_static/image63.png "创建新的网站使用快速创建")

    *创建新的网站使用快速创建*
4. 等到新**网站**创建。
5. 创建网站后，单击下面的链接**URL**列。 检查新的 Web 站点正常工作。

    ![浏览到新的 web 站点](whats-new-in-aspnet-mvc-4/_static/image64.png "浏览到新的 web 站点")

    *浏览到新的 web 站点*

    ![正在运行的网站](whats-new-in-aspnet-mvc-4/_static/image65.png "正在运行的网站")

    *正在运行的网站*
6. 返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。

    ![打开网站管理页](whats-new-in-aspnet-mvc-4/_static/image66.png "打开网站管理页")

    *打开网站管理页*
7. 在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。

    > [!NOTE]
    > *发布配置文件*包含所有发布到每个启用的发布方法的 Windows Azure 网站的 web 应用程序所需的信息。 发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。 **Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Windows Azure 网站。

    ![正在下载网站发布配置文件](whats-new-in-aspnet-mvc-4/_static/image67.png "下载网站发布配置文件")

    *正在下载网站发布配置文件*
8. 下载发布配置文件到已知位置。 进一步在此练习中将了解如何使用此文件从 Visual Studio 的 web 应用程序到 Windows Azure 网站发布。

    ![保存发布配置文件](whats-new-in-aspnet-mvc-4/_static/image68.png "保存发布配置文件")

    *保存发布配置文件*

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。 如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。

1. 用于存储应用程序数据库，将需要 SQL 数据库服务器。 可以从在 Windows Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。 如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。 请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。 不创建数据库，因为它将在后面的阶段中创建。

    ![SQL 数据库服务器仪表板](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database 服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。 若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png)按钮。

    ![添加客户端 IP 地址](whats-new-in-aspnet-mvc-4/_static/image71.png)

    *添加客户端 IP 地址*
3. 一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。

    ![确认更改](whats-new-in-aspnet-mvc-4/_static/image72.png)

    *确认更改*

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布

1. 返回到 ASP.NET MVC 4 解决方案。 在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。

    ![发布应用程序](whats-new-in-aspnet-mvc-4/_static/image73.png "发布应用程序")

    *发布此网站*
2. 导入发布配置文件保存在第一个任务。

    ![导入发布配置文件](whats-new-in-aspnet-mvc-4/_static/image74.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击**验证连接**。 验证完成后单击**下一步**。

    > [!NOTE]
    > 请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。

    ![验证连接](whats-new-in-aspnet-mvc-4/_static/image75.png "验证连接")

    *验证连接*
4. 在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。

    ![Web 部署配置](whats-new-in-aspnet-mvc-4/_static/image76.png "Web 部署配置")

    *Web 部署配置*
5. 配置数据库连接，如下所示：

   - 在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。
   - 在中**用户名**键入服务器管理员登录名。
   - 在中**密码**键入服务器管理员登录密码。
   - 键入新的数据库名称，例如： *MVC4SampleDB*。

     ![配置目标连接字符串](whats-new-in-aspnet-mvc-4/_static/image77.png "配置目标连接字符串")

     *配置目标连接字符串*
6. 然后单击“确定” 。 当系统提示你创建数据库时，单击**是**。

    ![创建数据库](whats-new-in-aspnet-mvc-4/_static/image78.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。 然后，单击 **“下一步”**。

    ![连接字符串指向 SQL 数据库](whats-new-in-aspnet-mvc-4/_static/image79.png "指向 SQL 数据库连接字符串")

    *连接字符串指向 SQL 数据库*
8. 在中**预览版**页上，单击**发布**。

    ![Web 应用程序发布](whats-new-in-aspnet-mvc-4/_static/image80.png "发布 web 应用程序")

    *Web 应用程序发布*
9. 在发布过程完成后，在默认浏览器将打开已发布的网站。

    ![应用程序发布到 Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "应用程序发布到 Windows Azure")

    *应用程序发布到 Windows Azure*
