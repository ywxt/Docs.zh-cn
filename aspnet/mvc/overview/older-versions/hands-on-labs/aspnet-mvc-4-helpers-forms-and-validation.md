---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 帮助程序、 窗体和验证 |Microsoft Docs
author: rick-anderson
description: 在 ASP.NET MVC 4 模型和数据访问的动手实验中，你已加载并显示数据库中的数据。 在本动手实验中，您将添加到...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: f2eb624e72d6f52d1694b5753ee2b1f8117c2851
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376732"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a>ASP.NET MVC 4 帮助程序、 窗体和验证

通过[Web 训练营团队](https://twitter.com/webcamps)

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

在中**ASP.NET MVC 4 模型和数据访问**动手实验中，您已被加载和显示数据库中的数据。 在本动手实验中，您将添加到**音乐应用商店**应用程序编辑该数据的能力。

记住这一目标，将首先创建将支持唱片集的创建、 读取、 更新和删除 (CRUD) 操作的控制器。 将生成利用 ASP.NET MVC 基架功能，以显示 HTML 表中的唱片集的属性的索引视图模板。 若要增强该视图，您将添加的自定义 HTML 帮助程序将截断长说明。

然后，您将添加编辑和创建视图，你会更改在数据库中，从下拉列表等窗体元素的帮助唱片集。

最后，您就可以让用户删除唱片集，并还会从输入错误的数据通过验证其输入阻止它们。

此动手实验假定你已了解的基础知识**ASP.NET MVC**。 如果您未使用过**ASP.NET MVC**之前，我们建议你超出**ASP.NET MVC 基础知识**动手实验。

此实验室将引导你通过前面所述通过将细微的更改应用于源文件夹中提供的示例 Web 应用的新功能和增强功能。

> [!NOTE]
> 在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。 特定于此实验室项目位于[ASP.NET MVC 4 帮助器、 窗体和验证](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)。

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，你将了解如何：

- 创建控制器支持 CRUD 操作
- 生成的索引视图以显示 HTML 表中的实体属性
- 添加自定义 HTML 帮助器
- 创建和自定义编辑视图
- 区分响应 HTTP GET 或 HTTP POST 调用的操作方法
- 添加和自定义创建视图
- 处理实体的删除
- 验证用户输入

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

必须具有要完成本实验的以下项：

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>安装

**安装代码片段**

为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。 若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。

如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 b： 使用代码片段](#AppendixB)&quot;。

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

以下练习构成本动手实验：

1. [创建存储管理器控制器和其索引视图](#Exercise1)
2. [添加 HTML 帮助器](#Exercise2)
3. [创建编辑视图](#Exercise3)
4. [添加创建视图](#Exercise4)
5. [处理删除](#Exercise5)
6. [添加验证](#Exercise6)
7. [在客户端使用非介入式 jQuery](#Exercise7)

> [!NOTE]
> 每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。 如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。


估计的时间才能完成此实验： **60 分钟**

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a>练习 1： 创建存储管理器控制器和其索引视图

在此练习中，您将学习如何创建新的控制器，以支持 CRUD 操作，自定义其 Index 操作方法，以从数据库和最后生成利用 ASP.NET MVC 基架的索引视图模板返回的唱片集列表若要显示 HTML 表中的唱片集的属性的功能。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a>任务 1-创建 StoreManagerController

在本任务中，您将创建名为的新控制器**StoreManagerController**以支持 CRUD 操作。

1. 打开**开始**解决方案位于**源/Ex1-CreatingTheStoreManagerController/开始/** 文件夹。

   1. 需要先下载某些缺少的 NuGet 包然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 添加新的控制器。 若要执行此操作，右键单击**控制器**在解决方案资源管理器，选择文件夹**添加**，然后**控制器**命令。 更改**控制器****名称**到**StoreManagerController** ，并确保选择**包含空读/写操作的MVC控制器**处于选中状态。 单击 **添加**。

    ![添加控制器对话框](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "添加控制器对话框")

    *添加控制器对话框*

    生成新的控制器类。 指示若要添加操作的读/写，存根 （stub） 方法，因为使用 TODO 注释填充，并提示您包括应用程序特定逻辑创建常见 CRUD 操作。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a>任务 2-自定义 StoreManager 索引

在此任务中，将自定义 StoreManager Index 操作方法，以从数据库中返回的唱片集的列表视图。

1. 在 StoreManagerController 类中，添加以下*使用*指令。

    (代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex1 使用 MvcMusicStore*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. 将字段添加到**StoreManagerController**以保存的实例**MusicStoreEntities。**

    (代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex1 MusicStoreEntities*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. 实现 StoreManagerController 索引操作可以返回的唱片集的列表视图。

    控制器操作逻辑将非常类似于前面编写的 StoreController 的索引操作。 使用 LINQ 检索所有唱片集，包括流派和艺术家信息显示。

    (代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex1 StoreManagerController 索引*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a>任务 3-创建索引视图

在本任务中，您将创建索引视图模板要显示的唱片集返回的列表**StoreManager**控制器。

1. 在创建新的视图模板之前, 应先生成项目，以便**添加视图对话框**知道**唱片集**类使用。 选择**生成 |生成 MvcMusicStore**以生成项目。
2. 内右击**索引**操作方法，然后选择**添加视图**。 此时会弹出**添加视图**对话框。

    ![添加视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "添加视图")

    *添加从索引方法中的视图*
3. 在添加视图对话框中，验证是否视图名称是**索引**。 选择**创建强类型化视图**选项，然后选择**唱片集 (MvcMusicStore.Models)** 从**模型类**下拉列表。 选择**列表**从**基架模板**下拉列表。 将保留**视图引擎**到**Razor**和其他字段具有其默认值，然后单击**添加**。

    ![添加索引视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "添加索引视图")

    *添加索引视图*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a>任务 4-自定义索引视图的基架

在此任务中，将调整与 ASP.NET MVC 基架功能，使其显示所需的字段创建的简单视图模板。

> [!NOTE]
> **基架**支持在 ASP.NET MVC 中的生成一个简单的视图模板，其中列出了唱片集模型中的所有字段。 **基架**，可以快速开始对强类型化视图： 而不是无需手动编写视图模板，快速基架生成的默认模板，然后，可以修改生成的代码。


1. 查看创建的代码。 生成的字段列表将属于以下 HTML 表**基架**使用用于显示表格数据。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. 替换**&lt;表&gt;** 以下代码，以仅显示代码**流派**，**艺术家**，**唱片集标题**，并**价格**字段。 这会删除**AlbumId**并**唱片集画面 URL**列。 此外，它更改 GenreId 和 ArtistId 要显示的及其链接的类属性的列**Artist.Name**并**Genre.Name**，并删除**详细信息**链接。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. 更改以下说明。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，将测试**StoreManager** **索引**视图模板显示根据前面的步骤的设计的唱片集的列表。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为 **/StoreManager**若要验证是否显示唱片集的列表，显示其**标题**，**艺术家**并**流派**。

    ![浏览唱片集的列表](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "浏览唱片集的列表")

    *浏览唱片集的列表*

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a>练习 2： 添加 HTML 帮助器

StoreManager 索引页都有一个潜在的问题： 标题和艺术家姓名属性可以同时为足够长，以引发关闭表格的格式。 在此练习中将了解如何添加自定义的 HTML 帮助器来截断该文本。

在下图中，可以看到如何格式时所使用的小型浏览器大小修改由于文本的长度。

![浏览与唱片集的列表不截断的文本](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "浏览与唱片集的列表不截断的文本")

*浏览与唱片集的列表不截断的文本*

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a>任务 1-扩展的 HTML 帮助器

在本任务中，您将添加一个新方法**Truncate**到**HTML** ASP.NET MVC 视图中公开的对象。 若要执行此操作，将实现**扩展方法**到内置**System.Web.Mvc.HtmlHelper**类提供的 ASP.NET MVC。

> [!NOTE]
> 若要详细了解**扩展方法**，请访问此 msdn 文章。 [https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx)。


1. 打开**开始**解决方案位于**源/Ex2-AddingAnHTMLHelper/开始/** 文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 打开 StoreManager 的索引视图。 若要执行此操作，在解决方案资源管理器中展开**视图**文件夹，然后**StoreManager** ，然后打开**Index.cshtml**文件。
3. 添加以下代码<strong>@model</strong>指令来定义<strong>Truncate</strong>帮助器方法。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a>任务 2-在页中截断的文本

在本任务中，您将使用**Truncate**方法来截断视图模板中的文本。

1. 打开 StoreManager 的索引视图。 若要执行此操作，在解决方案资源管理器中展开**视图**文件夹，然后**StoreManager** ，然后打开**Index.cshtml**文件。
2. 替换显示的线条**艺术家姓名**和唱片集的**标题**。 若要执行此操作，将以下行。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在此任务中，将测试**StoreManager** **索引**视图模板将截断的唱片集标题和艺术家姓名。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为 **/StoreManager**以验证该长时间中的文本**标题**并**艺术家**列将被截断。

    ![截断的标题和艺术家姓名](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "截断标题和艺术家名称")

    *截断的标题和艺术家姓名*

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a>练习 3： 创建编辑视图

在此练习中，您将学习如何创建一个窗体以允许存储管理器编辑唱片集。 在将浏览 **/StoreManager/Edit/id** URL (**id**正在编辑的唱片集的唯一 id)，从而使对服务器的 HTTP GET 调用。

控制器编辑操作方法将从数据库中检索相应的唱片集，创建**StoreManagerViewModel**对象封装 （以及的艺术家和流派列表），然后将其传递给为视图模板向用户呈现的 HTML 页。 此页将包含**&lt;窗体&gt;** 使用文本框和下拉列表以进行编辑的唱片集属性的元素。

一旦用户更新唱片集的表单值并单击**保存**按钮，将更改提交通过 HTTP POST 回叫 **/StoreManager/Edit/id**。尽管 URL 将保留与最后一次调用中的相同，但 ASP.NET MVC 标识，这次它是 HTTP POST，因此执行不同的编辑操作方法 (一个使用修饰 **[HttpPost]**)。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a>任务 1-实现 HTTP GET 编辑操作方法

在此任务中，您将实现要检索从数据库中的相应唱片集的编辑操作方法的 HTTP GET 版本以及所有流派和艺术家的列表。 它将此数据打包成**StoreManagerViewModel**的最后一步，然后将传递到用于呈现具有响应的视图模板中定义的对象。

1. 打开**开始**解决方案位于**源/Ex3-CreatingTheEditView/开始/** 文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 打开**StoreManagerController**类。 若要执行此操作，请展开**控制器**文件夹，然后双击**StoreManagerController.cs**。
3. 替换**HTTP GET 编辑**使用以下代码来检索相应的操作方法**唱片集**并将**流派**和**艺术家**列出了。

    (代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex3 StoreManagerController HTTP GET 编辑操作*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > 正在使用**System.Web.Mvc** **SelectList**艺术家和而不是流派**System.Collections.Generic**列表。
    > 
    > **SelectList**是更简洁的方式来填充 HTML 下拉列表和管理当前所选内容等内容。 实例化和更高版本设置中的控制器操作这些 ViewModel 对象将使编辑窗体方案更简洁。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a>任务 2-创建编辑视图

在本任务中，将创建更高版本将显示的唱片集属性的编辑视图模板。

1. 创建编辑视图。 若要执行此操作，右键单击内**编辑**操作方法，然后选择**添加视图**。
2. 在添加视图对话框中，验证是否视图名称是**编辑**。 检查**创建强类型化视图**复选框，然后选择**唱片集 (MvcMusicStore.Models)** 从**查看数据类**下拉列表。 选择**编辑**从**基架模板**下拉列表。 其他字段保留为其默认值，然后单击**添加**。

    ![添加编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "添加 Edit 视图")

    *添加 Edit 视图*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在此任务中，将测试**StoreManager** **编辑**视图页会显示作为参数传递的唱片集的属性的值。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为 **/StoreManager/Edit/1**以验证是否显示了传递的唱片集的属性的值。

    ![浏览唱片集的编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "浏览唱片集的编辑视图")

    *浏览唱片集的编辑视图*

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a>任务 4-实现唱片集编辑器模板上的下拉列表

在此任务中，你将在最后一个任务中，创建视图模板添加下拉列表，以便用户可以选择从一系列艺术家和流派。

1. 将替换所有**唱片集**fieldset 以下代码：

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > **Html.DropDownList**已添加帮助器来呈现下拉列表选择艺术家和流派。 参数传递给**Html.DropDownList**是：
    > 
    > 1. 窗体字段的名称 (**&quot;ArtistId&quot;**)。
    > 2. **SelectList**的值的下拉列表。

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，将测试**StoreManager** **编辑**视图页显示而不是艺术家和类型 ID 文本字段的下拉列表。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为 **/StoreManager/Edit/1**以验证它显示而不是艺术家和类型 ID 文本字段的下拉列表。

    ![浏览具有下拉列表确定的唱片集的编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "浏览唱片集的相应下拉列表编辑视图")

    *浏览唱片集的编辑视图，这次使用下拉列表*

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a>任务 6-实现 HTTP POST 编辑操作方法

现在，编辑视图显示按预期方式，您需要实现 HTTP POST 编辑操作方法以保存到相册所做的更改。

1. 关闭浏览器，如果需要以返回到 Visual Studio 窗口。 打开**StoreManagerController**从**控制器**文件夹。
2. 替换**HTTP POST 编辑**操作方法与以下的代码 （请注意，必须将其替换的方法是接收两个参数的重载的版本）：

    (代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex3 StoreManagerController HTTP POST 编辑操作*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > 将执行此方法，当用户单击**保存**视图的按钮，并执行 HTTP POST 回发到服务器的表单值将其保留在数据库中。 修饰器 **[HttpPost]** 指示应这些 HTTP POST 方案使用的方法。 该方法采用**唱片集**对象。 ASP.NET MVC 将自动创建的唱片集对象从已发布&lt;窗体&gt;值。
    > 
    > 该方法将执行以下步骤：
    > 
    > 1. 如果模型是有效的：
    > 
    >     1. 更新要将其标记为已修改对象的上下文中的唱片集条目。
    >     2. 保存所做的更改和重定向到索引视图。
    > 2. 如果模型不是有效的它将会填充使用 ViewBag **GenreId**并**ArtistId**，则会返回接收到的唱片集对象，以允许用户与视图执行任何所需的更新。

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>任务 7-运行应用程序

在此任务中，将测试**StoreManager 编辑**视图页实际上将更新后的唱片集数据保存在数据库中。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为 **/StoreManager/Edit/1**。 将唱片集标题改为**负载**，然后单击**保存**。 验证在列表中的唱片集实际更改唱片集的标题。

    ![正在更新相册](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "更新唱片集")

    *正在更新唱片集*

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a>练习 4： 添加创建视图

既然**StoreManagerController**支持**编辑**功能，在此练习中将了解如何添加创建视图模板，以便存储管理器将新的唱片集添加到应用程序。

编辑功能与您处理，将实现使用中的两个不同方法的创建方案**StoreManagerController**类：

1. 存储管理器第一次访问时，一种操作方法将显示一个空窗体 **/StoreManager/创建**URL。
2. 第二个操作方法将处理方案当单击 store manager**保存**中的窗体按钮，然后提交值回 **/StoreManager/创建**作为 HTTP POST 的 URL。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a>任务 1-实现创建 HTTP GET 操作方法

在此任务中，您将实现的 Create 操作方法来检索所有流派和艺术家的列表，此数据打包到 HTTP GET 版本**StoreManagerViewModel**对象，然后将传递给视图模板。

1. 打开**开始**解决方案位于**源/Ex4-AddingACreateView/开始/** 文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 打开**StoreManagerController**类。 若要执行此操作，请展开**控制器**文件夹，然后双击**StoreManagerController.cs**。
3. 替换**创建**以下操作方法代码：

    (代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex4 StoreManagerController HTTP GET 创建操作*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a>任务 2-添加 Create 视图

在本任务中，您将添加将显示一个新的 （空） 唱片集窗体创建视图模板。

1. 内右击**创建**操作方法，然后选择**添加视图**。 这将显示添加视图对话框。
2. 在添加视图对话框中，验证是否视图名称是**创建**。 选择**创建强类型化视图**选项，然后选择**唱片集 (MvcMusicStore.Models)** 从**模型类**下拉列表和**创建**从**基架模板**下拉列表。 其他字段保留为其默认值，然后单击**添加**。

    ![添加 create 视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "添加-a-创建-view.png")

    *添加 Create 视图*
3. 更新**GenreId**并**ArtistId**字段使用下拉列表，如下所示：

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在此任务中，将测试**StoreManager** **创建**视图页将显示一个空的唱片集窗体。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为**StoreManager/创建**。 验证用于填充新的唱片集属性显示一个空窗体。

    ![使用一个空窗体创建视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "创建一个空窗体视图")

    *使用一个空窗体创建视图*

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a>任务 4-实现 HTTP POST 创建操作方法

在此任务中，您将实现将在用户单击时调用的创建操作方法的 HTTP POST 版本**保存**按钮。 该方法应在数据库中保存新唱片集。

1. 关闭浏览器，如果需要以返回到 Visual Studio 窗口。 打开**StoreManagerController**类。 若要执行此操作，请展开**控制器**文件夹，然后双击**StoreManagerController.cs**。
2. 替换**HTTP POST 创建**以下操作方法代码：

    (代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex4 StoreManagerController HTTP-POST 创建操作*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > 创建操作非常类似于上一个编辑操作方法，但而不是将对象设置为已修改，它将被添加到上下文。

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，将测试**StoreManager 创建**视图页，可以创建新的唱片集，然后重定向到 StoreManager 索引视图。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为**StoreManager/创建**。 所有窗体字段用数据填充新的唱片集，如图所示：

    ![创建相册](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "创建相册")

    *创建相册*
3. 验证会重定向到 StoreManager 索引视图，其中包括刚刚创建的新唱片集。

    ![创建新相册](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "创建新相册")

    *创建新相册*

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a>练习 5： 处理删除

若要删除唱片集的功能尚未实现。 这是本练习中将对。 像之前那样将实现使用两个不同方法中的删除方案**StoreManagerController**类：

1. 一种操作方法将显示确认窗体
2. 第二个操作方法将处理窗体提交

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a>任务 1-实现 HTTP GET Delete 操作方法

在此任务中，您将实现要检索的唱片集信息的删除操作方法的 HTTP GET 版本。

1. 打开**开始**解决方案位于**源/Ex5-HandlingDeletion/开始/** 文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 打开**StoreManagerController**类。 若要执行此操作，请展开**控制器**文件夹，然后双击**StoreManagerController.cs**。
3. 删除控制器操作正是与上一存储详细信息控制器操作相同： 它会查询**唱片集**对象从数据库中使用**id**提供 URL，并返回适当**视图**。 若要执行此操作，将为 HTTP GET**删除**以下操作方法代码：

    (代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex5 处理删除 HTTP GET Delete 操作*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. 内右击**删除**操作方法，然后选择**添加视图**。 这将显示添加视图对话框。
5. 在添加视图对话框中，验证是否视图名称是**删除**。 选择**创建强类型化视图**选项，然后选择**唱片集 (MvcMusicStore.Models)** 从**模型类**下拉列表。 选择**删除**从**基架模板**下拉列表。 其他字段保留为其默认值，然后单击**添加**。

    ![添加 Delete 视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "添加 Delete 视图")

    *添加 Delete 视图*
6. 删除模板显示模型中的所有字段。 将显示仅唱片集的标题。 若要执行此操作，请将视图的内容替换为以下代码：

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>任务 2-运行应用程序

在此任务中，将测试**StoreManager** **删除**视图页显示确认删除窗体。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为 **/StoreManager**。 选择要删除通过单击一个相册**删除**并验证是否已上载新视图。

    ![删除 Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "删除 Album")

    *删除 Album*

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a>任务 3-实现 HTTP POST Delete 操作方法

在此任务中，您将实现将在用户单击时调用的 Delete 操作方法的 HTTP POST 版本**删除**按钮。 该方法应在删除数据库中的唱片集。

1. 关闭浏览器，如果需要以返回到 Visual Studio 窗口。 打开**StoreManagerController**类。 若要执行此操作，请展开**控制器**文件夹，然后双击**StoreManagerController.cs**。
2. 替换**HTTP POST Delete**以下操作方法代码：

    (代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex5 处理删除 HTTP POST Delete 操作*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在此任务中，将测试**StoreManager 删除**视图页可让您删除唱片集，然后重定向到 StoreManager 索引视图。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为 **/StoreManager**。 选择要删除通过单击一个相册**删除。** 通过单击确认删除**删除**按钮：

    ![删除 Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "删除 Album")

    *删除 Album*
3. 验证是否删除唱片集，因为它不会出现在**索引**页。

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a>练习 6： 添加验证

目前，您所具有的创建和编辑窗体不执行任何类型的验证。 如果用户离开价格字段中的所需的字段留空或键入字母，会向您的第一个错误将从数据库中。

通过将数据批注添加到 model 类，可以向应用程序添加验证。 描述所需的规则应用于您的模型属性，可以利用数据批注和 ASP.NET MVC 将负责强制执行和向用户显示相应的消息。

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a>任务 1-添加数据批注

在此任务中，您将添加到将使创建和编辑页面的唱片集模型的数据注释显示验证消息在适当的时候。

对于简单的模型类，添加数据批注只需添加处理**使用**语句**System.ComponentModel.DataAnnotation**，然后将放到 **[必需]** 上相应的属性的属性。 下面的示例将使**名称**属性在视图中的必填字段。

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

这是稍微复杂一些类似于此应用程序的情况下在其中生成实体数据模型。 如果你的数据批注直接添加到模型类，它们将被覆盖如果从数据库对模型进行更新。 相反，您可使用元数据部分类将是为了容纳批注并与模型相关联的类使用 **[MetadataType]** 属性。

1. 打开**开始**解决方案位于**源/Ex6-AddingValidation/开始/** 文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 打开**Album.cs**从**模型**文件夹。
3. 替换**Album.cs**内容与突出显示的代码，以便它看起来如下所示：

    > [!NOTE]
    > 在行 **[DisplayFormat(ConvertEmptyStringToNull=false)]** 指示数据源中更新数据字段时，将不会从模型的空字符串转换为 null。 实体框架将 null 值分配给该模型之前数据批注验证字段时，此设置会避免异常。

    (代码段- *ASP.NET MVC 4 帮助程序和窗体和验证-Ex6 唱片集的元数据部分类*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > 这**唱片集**分部类具有**MetadataType**属性，用于指向**AlbumMetaData**数据批注的类。 以下是一些用于批注的唱片集模型的数据批注属性：
    > 
    > - 需要-指示该属性是必填的字段
    > - DisplayName-定义要使用窗体字段并验证消息的文本
    > - DisplayFormat-指定如何显示和格式化数据字段。
    > - StringLength-定义字符串字段的最大长度
    > - 范围-最大和最小值为数值字段
    > - ScaffoldColumn-允许隐藏编辑器窗体中的字段

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>任务 2-运行应用程序

在本任务中，您将测试创建和编辑页面验证字段，使用上一个任务中选择的显示名称。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为**StoreManager/创建**。 验证是否显示名称匹配的分部类中的 (如**唱片集画面 URL**而不是**AlbumArtUrl**)
3. 单击**创建**，而不填充窗体。 验证获取相应的验证消息。

    ![验证创建页中的字段](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "验证创建页中的字段")

    *在创建页中的已验证的字段*
4. 你可以验证相同出现**编辑**页。 将 URL 更改为 **/StoreManager/Edit/1**并验证是否显示名称与在分部类中的匹配 (如**唱片集画面 URL**而不是**AlbumArtUrl**)。 空**标题**并**价格**字段，然后单击**保存**。 验证获取相应的验证消息。

    ![在编辑页中的已验证的字段](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    *在编辑页中的已验证的字段*

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a>练习 7： 在客户端使用非介入式 jQuery

在此练习中，您将学习如何启用客户端的 MVC 4 非介入式 jQuery 验证。

> [!NOTE]
> 非介入式 jQuery 使用数据 ajax 前缀 JavaScript 来调用操作方法在服务器而不是干扰的方式发出的内联客户端脚本。


<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a>任务 1-运行之前启用非介入式 jQuery 在应用程序

在本任务中，将运行之前要比较这两种验证模型包括 jQuery 在应用程序。

1. 打开**开始**解决方案位于**源/Ex7-UnobtrusivejQueryValidation/开始/** 文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 按 **F5** 运行该应用程序。
3. 在主页页面中启动项目。 浏览 **/StoreManager/创建**然后单击**创建**而不填充该窗体以验证你收到验证消息：

    ![客户端验证已禁用](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "禁用客户端验证")

    *禁用客户端验证*
4. 在浏览器中打开的 HTML 源代码：

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a>任务 2-启用非介入式客户端验证

在本任务中，将启用 jQuery**非介入式客户端验证**从**Web.config**文件，它是默认情况下所有新的 ASP.NET MVC 4 项目中设置为 false。 此外，您将添加所需的脚本引用，以使 jQuery 非介入式客户端验证工作。

1. 打开**Web.Config**文件在项目根目录位置，并确保选中**ClientValidationEnabled**并**UnobtrusiveJavaScriptEnabled**密钥值设置为 **，则返回 true**。

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > 此外可以通过在 Global.asax.cs 以获得相同的结果的代码来启用客户端验证：
    > 
    > **HtmlHelper.ClientValidationEnabled = true;**
    > 
    > 此外，可以将 ClientValidationEnabled 属性分配到任何控制器具有自定义行为。
2. 打开**Create.cshtml**处**Views\StoreManager**。
3. 以下脚本文件，请确保**jquery.validate**并**jquery.validate.unobtrusive**，查看站点中引用&quot; **~/bundles/jqueryval**&quot;捆绑包。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > 所有这些 jQuery 库包含在新的 MVC 4 项目。 您可以找到更多库中的 **/脚本**您项目的文件夹。
    > 
    > 为了使此验证库的工作原理，您需要添加对 jQuery 框架库的引用。 由于已在添加此引用 **\_Layout.cshtml**文件，您不需要在此特定视图中添加它。

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a>任务 3-运行应用程序使用非介入式 jQuery 验证

在此任务中，将测试**StoreManager**创建视图模板执行用户创建新的唱片集时使用 jQuery 库的客户端验证。

1. 按 **F5** 运行该应用程序。
2. 在主页页面中启动项目。 浏览 **/StoreManager/创建**然后单击**创建**而不填充该窗体以验证你收到验证消息：

    ![使用 jQuery 启用客户端验证](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "使用 jQuery 启用客户端验证")

    *使用 jQuery 启用客户端验证*
3. 在浏览器中，打开创建视图的源代码:

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > 对于每个客户端验证规则，非介入式 jQuery 将添加一个特性，其数据-val-*rulename*=&quot;*消息*&quot;。 下面是一系列标记该 Unobtrusive jQuery 插入 html 输入字段来执行客户端验证：
   > 
   > - 数据值
   > - 数据 val 编号
   > - 数据值范围
   > - 数据值的范围最小/最大数据值范围
   > - -Val 的所需的数据
   > - 数据值长度
   > - 数据值的长度最大/最小数据 val 长度
   > 
   > 所有数据值将都填入模型**数据批注**。 然后，可以在客户端运行在服务器端工作的所有逻辑。 例如，价格属性具有以下数据注释在模型中：
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > 在使用非介入式 jQuery 后, 生成的代码是：
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>总结

通过完成本动手实验介绍了如何使用户能够更改与使用以下数据库中存储的数据：

- 控制器的操作，例如索引、 创建、 编辑、 删除
- ASP.NET MVC 基架功能用于 HTML 表中显示属性
- 自定义 HTML 帮助程序来提高用户体验
- 对 HTTP GET 或 HTTP POST 调用做出响应的操作方法
- 有关类似视图模板，如创建和编辑共享的编辑器模板
- 窗体元素，如下拉列表
- 数据注释进行模型验证
- 使用 jQuery 非介入式库的客户端验证

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 a： 安装 Visual Studio Express 2012 for Web

你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**. 以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。

1. 转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。
2. 单击**立即安装**。 如果还没有**Web 平台安装程序**将重定向以下载并安装。
3. 一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，然后单击**我接受**以继续。

    ![接受许可条款](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    *接受许可条款*
5. 等待，直到下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    *安装进度*
6. 安装完成后，单击**完成**。

    ![安装已完成](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    *安装已完成*
7. 单击**退出**以关闭 Web 平台安装程序。
8. 若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    *VS Express for Web 磁贴*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>附录 b： 使用代码片段

使用代码段，可以轻松获得相关所需的所有代码。 实验室文档将告诉您完全何时可以使用它们，如下图中所示。

![使用 Visual Studio 代码段代码插入到你的项目](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "使用 Visual Studio 代码段代码插入到你的项目")

*使用 Visual Studio 代码段代码插入到你的项目*

***若要添加代码段使用键盘 (仅限 C#)***

1. 将光标置于要插入的代码。
2. 开始键入代码片段名称 （不带空格或连字符）。
3. 观看作为 IntelliSense 显示匹配的代码段的名称。
4. 选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。
5. 按 Tab 键两次，以在光标位置插入代码段。

![开始键入代码段名称](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "开始键入代码段名称")

*开始键入代码段名称*

![按 tab 键以选择突出显示代码段](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "按选项卡以选择突出显示代码段")

*按 tab 键以选择突出显示代码段*

![再次按 Tab 和代码段将 expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "再次按 Tab 和代码段将扩展")

*再次按 Tab 和代码段将扩展*

***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。 右键单击你想要插入的代码片段。

1. 选择**插入代码段**跟**我的代码片段**。
2. 通过单击选择列表中中的相关代码片段。

![右键单击你想要插入代码段和选择插入代码段](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "右键单击你想要插入代码段和选择插入代码段")

*右键单击你想要插入代码段和选择插入代码段*

![通过单击选择列表中中的相关代码片段](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "通过单击选择列表中中的相关代码片段")

*通过单击选择列表中中的相关代码片段*
