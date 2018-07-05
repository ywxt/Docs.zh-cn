---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 基础知识 |Microsoft Docs
author: rick-anderson
description: 此动手实验室基于 MVC （模型视图控制器） 音乐应用商店，介绍，并说明如何使用 ASP.NET MV 分步的教程应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 3a282d02ba929eb86571e92f190550614962524d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386570"
---
# <a name="aspnet-mvc-4-fundamentals"></a>ASP.NET MVC 4 基础知识

通过[Web 训练营团队](https://twitter.com/webcamps)

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

此动手实验室基于 MVC （模型视图控制器） 音乐应用商店，介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 分步的教程应用程序。 在实验室中，您将了解简单起见，尚未使用这些技术在一起的电源。 将开始使用简单的应用程序时，将生成它，直到你具有完全正常运行 ASP.NET MVC 4 Web 应用程序。

此实验室可与 ASP.NET MVC 4。

如果你想要浏览的教程应用程序的 ASP.NET MVC 3 版本，您可以找到它在[MVC Music 商店](https://github.com/evilDave/MVC-Music-Store)。

此动手实验假定开发人员在 HTML 和 JavaScript 等 Web 开发技术可以体验。

> [!NOTE]
> 在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。 特定于此实验室项目位于[ASP.NET MVC 4 基础知识](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)。

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a>音乐应用商店应用程序

将生成在本实验的音乐应用商店 web 应用程序包含三个主要部分： 购物、 结帐和管理。 访问者将能够按流派浏览唱片集、 将唱片集添加到购物车、 检查其所做的选择和最后继续签出以登录并完成订单。 此外，存储管理员将能够管理可用的唱片集，以及它们的主要属性。

![音乐应用商店屏幕](aspnet-mvc-4-fundamentals/_static/image1.png "音乐应用商店屏幕")

*音乐应用商店的屏幕*

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a>ASP.NET MVC 4 Essentials

音乐应用商店应用程序将使用构建**模型视图控制器 (MVC)**，体系结构模式，将应用程序分成三个主要组件：

- **模型**： 模型对象是实现域逻辑的应用程序部件。 通常情况下，模型对象还会检索并将模型状态存储在数据库中。
- **视图：** 视图是显示应用程序的用户界面 (UI) 的组件。 通常，此 UI 被创建的模型数据。 示例将显示文本框和下拉列表根据唱片集对象的当前状态的唱片集的编辑视图。
- **控制器：** 控制器是处理用户交互、 处理模型，并最终选择的视图来呈现的 UI 的组件。 在 MVC 应用程序中，视图仅显示信息；控制器处理并响应用户输入和交互。

MVC 模式有助于创建单独的应用程序 （输入的逻辑、 业务逻辑和 UI 逻辑），同时提供这些元素之间松散耦合的不同方面的应用程序。 这种隔离有助于管理复杂性时生成应用程序，因为这样你就可以专注于一次实现的一个方面。 此外，MVC 模式可以轻松地测试应用程序，还鼓励使用测试驱动开发 (TDD) 用于创建应用程序。

**ASP.NET MVC** framework 提供了用于创建基于 ASP.NET MVC 的 Web 应用程序的 ASP.NET Web 窗体模式的替代方法。 **ASP.NET MVC** framework 是一个轻型、 高度可测试的演示框架，（如基于 Web 窗体应用程序） 与现有的 ASP.NET 功能，如母版页和基于成员资格的集成身份验证，以便获取核心.NET framework 的所有功能。 这是如果你已了解如何使用 ASP.NET Web 窗体因为所有已使用的库都可在 ASP.NET MVC 4 中也很有用。

此外，MVC 应用程序的三个主要组件之间的松散耦合也可促进并行开发。 例如，一位开发人员可以从事视图、 第二个开发人员可以从事控制器逻辑和第三个开发人员可以专注于模型中的业务逻辑。

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，你将了解如何：

- 基于音乐应用商店应用程序教程从头开始创建 ASP.NET MVC 应用程序
- 添加控制器来处理到网站和用于浏览其主要功能的主页 Url
- 添加自定义其样式以及显示的内容的视图
- 添加模型类来包含和管理数据和域逻辑
- 使用视图模型模式来将信息从控制器操作传递到视图模板
- 浏览 internet 应用程序的 ASP.NET MVC 4 新模板

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

必须具有要完成本实验的以下项：

- [Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (读取[附录 A](#AppendixA)有关如何安装它的说明)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>安装

**安装代码片段**

为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。 若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。

如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 c： 使用代码片段](#AppendixC)&quot;。

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

此动手实验包含由以下练习：

1. [练习 1： 创建 MusicStore ASP.NET MVC Web 应用程序项目](#Exercise1)
2. [练习 2： 创建控制器](#Exercise2)
3. [练习 3： 将参数传递到控制器](#Exercise3)
4. [练习 4： 创建视图](#Exercise4)
5. [练习 5： 创建视图模型](#Exercise5)
6. [练习 6： 在视图中使用参数](#Exercise6)
7. [练习 7： 了解 ASP.NET MVC 4 新模板](#Exercise7)

> [!NOTE]
> 每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。 如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。


估计的时间才能完成此实验： **60 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a>练习 1： 创建 MusicStore ASP.NET MVC Web 应用程序项目

在此练习中，您将学习如何为 Web，以及其主文件夹组织在 Visual Studio 2012 Express 中创建 ASP.NET MVC 应用程序。 此外，您将学习如何添加新的控制器并使其在应用程序的主页中显示一个简单的字符串。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a>任务 1-创建 ASP.NET MVC Web 应用程序项目

1. 在本任务中，将创建一个空的 ASP.NET MVC 应用程序项目使用 MVC 的 Visual Studio 模板。 启动**VS Express for Web**。
2. 在“文件”菜单上，单击“新建项目”。
3. 在中**新的项目**对话框中，选择**ASP.NET MVC 4 Web 应用程序**项目类型，位于**Visual C#** **Web**模板列表。
4. 更改**名称**到*MvcMusicStore*。
5. 设置在新解决方案的位置**开始**在此练习中的源文件夹中，例如文件夹 **[YOUR-h o L-PATH] \Source\Ex01-CreatingMusicStoreProject\Begin**。 单击 **“确定”**。

    ![创建新建项目对话框](aspnet-mvc-4-fundamentals/_static/image2.png "创建新建项目对话框")

    *创建新项目对话框*
6. 在中**新的 ASP.NET MVC 4 项目**对话框中，选择**基本**模板并确保选中**视图引擎**所选**Razor**。 单击 **“确定”**。

    ![新建 ASP.NET MVC 4 项目对话框](aspnet-mvc-4-fundamentals/_static/image3.png "新建 ASP.NET MVC 4 项目对话框")

    *新建 ASP.NET MVC 4 项目对话框*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a>任务 2-探索的解决方案结构

ASP.NET MVC 框架包括可帮助您创建支持 MVC 模式的 Web 应用程序的 Visual Studio 项目模板。 此模板创建新的 ASP.NET MVC Web 应用程序使用所需的文件夹、 项模板和配置文件条目。

在此任务中，将检查该解决方案结构，以了解所涉及的元素和它们之间的关系。 以下文件夹包含在所有 ASP.NET MVC 应用程序，因为默认情况下，ASP.NET MVC framework 使用&quot;惯例优先于配置&quot;方法，并简化了一些默认假设基于命名文件夹约定。

1. 在创建项目后，查看已在右侧的解决方案资源管理器中创建的文件夹结构：

    ![在解决方案资源管理器中的 ASP.NET MVC 文件夹结构](aspnet-mvc-4-fundamentals/_static/image4.png "解决方案资源管理器中的 ASP.NET MVC 文件夹结构")

    *在解决方案资源管理器中的 ASP.NET MVC 文件夹结构*

   1. **控制器**。 此文件夹将包含在控制器类。 在基于 MVC 应用程序，控制器负责处理最终用户交互，操作模型，并最终选择要呈现的 UI 的视图。

       > [!NOTE]
       > MVC framework 要求所有控制器的名称以结尾&quot;控制器&quot;-例如，HomeController、 LoginController 或 ProductController。
   2. **模型**。 表示 MVC Web 应用程序的应用程序模型的类，提供此文件夹。 这通常包括定义对象和用于与数据存储进行交互的逻辑的代码。 通常情况下，实际模型对象将位于单独的类库。 但是，在创建新的应用程序时，可能包括类，然后在开发周期中将其移动到单独的类库，请在以后。
   3. **视图**。 此文件夹是视图，负责显示应用程序的用户界面组件的建议的位置。 视图使用.aspx、.ascx、.cshtml 和.master 文件，除了与呈现视图相关的任何其他文件。 视图文件夹包含文件夹，用于每个控制器;该文件夹以控制器名称前缀命名。 例如，如果您有一个名为控制器**HomeController**，Views 文件夹将包含名为 Home 的文件夹。 默认情况下，当 ASP.NET MVC 框架加载视图时，它查找具有 Views\controllerName 文件夹中的请求的视图名称的.aspx 文件 (**视图 [ControllerName] [Action].aspx**) 或 (**视图 [ControllerName][Action].cshtml**) 的 Razor 视图。

      > [!NOTE]
      > 除了前面列出的文件夹，MVC Web 应用程序使用**Global.asax**文件以设置全局 URL 路由默认值，并使用**Web.config**文件来配置应用程序。

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a>任务 3-添加一个 HomeController

在不使用 MVC framework 的 ASP.NET 应用程序，用户交互被组织的页面，左右引发和处理这些页面中的事件。 与此相反，用户与 ASP.NET MVC 应用程序的交互是围绕控制器和其操作方法进行组织。

但是，ASP.NET MVC 框架将 Url 映射到称为控制器的类。 控制器处理传入请求，处理用户输入和交互、 执行相应的应用程序逻辑并确定要发送回客户端的响应 （显示 HTML，下载的文件，将重定向到不同的 URL，等等。）。 对于显示 HTML，控制器类通常会调用单独的视图组件来生成 HTML 标记的请求。 在 MVC 应用程序中，视图仅显示信息；控制器处理并响应用户输入和交互。

在本任务中，您将添加将句柄的音乐应用商店网站主页上的 Url 的控制器类。

1. 右键单击**控制器**在解决方案资源管理器，选择文件夹**添加**，然后**控制器**命令：

    ![添加控制器命令](aspnet-mvc-4-fundamentals/_static/image5.png "添加控制器命令")

    *添加控制器命令*
2. **添加控制器**此时将显示对话框。 将控制器命名*HomeController*然后按**添加**。

    ![添加控制器对话框](aspnet-mvc-4-fundamentals/_static/image6.png "添加控制器对话框")

    *添加控制器对话框*
3. 该文件**HomeController.cs**中创建**控制器**文件夹。 为了获得**HomeController**其索引操作上返回一个字符串，将为**索引**方法使用以下代码：

    (代码段- *ASP.NET MVC 4 基础知识--Ex1 HomeController 索引*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在本任务中，您将试用 web 浏览器中的应用程序。

1. 按**F5**运行该应用程序。 编译项目并在本地 IIS Web 服务器启动。 本地 IIS Web 服务器会自动打开 web 浏览器指向的 Web 服务器的 URL。

    ![在 web 浏览器中运行的应用程序](aspnet-mvc-4-fundamentals/_static/image7.png "web 浏览器中运行的应用程序")

    *在 web 浏览器中运行的应用程序*

    > [!NOTE]
    > 本地 IIS Web 服务器将运行该网站上的随机空闲端口号。 在上图中，该站点运行在`http://localhost:50103/`，因此它正在使用端口 50103。 端口号可能会有所不同。
2. 关闭浏览器。

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a>练习 2： 创建控制器

在此练习中，您将了解如何更新控制器以实现简单音乐应用商店应用程序的功能。 该控制器将定义要处理的每个以下的特定请求的操作方法：

- 在音乐应用商店音乐流派列表页
- 列出所有特定流派音乐 album 的浏览页面
- 显示有关特定音乐唱片集信息的详细信息页

为此练习的作用域，这些操作将只是现在返回的字符串。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a>任务 1-添加新的 StoreController 类

在本任务中，您将添加一个新的控制器。

1. 如果尚未打开，启动**VS Express for Web 2012**。
2. 在中**文件**菜单中，选择**打开项目**。 在打开项目对话框中，浏览到**Source\Ex02 CreatingAController\Begin**，选择**Begin.sln**然后单击**打开**。 或者，您也可以继续使用该解决方案完成上一练习后获得。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
3. 添加新控制器。 若要执行此操作，右键单击**控制器**在解决方案资源管理器，选择文件夹**添加**，然后**控制器**命令。 更改**控制器名称**到*StoreController*，然后单击**添加**。

    ![添加控制器对话框](aspnet-mvc-4-fundamentals/_static/image8.png "添加控制器对话框")

    *添加控制器对话框*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a>任务 2-修改 StoreController 的操作

在本任务中，您将修改控制器方法调用**操作**。 操作是负责处理 URL 请求并决定应发送回浏览器或调用 URL 的用户的内容。

1. **StoreController**的类已经拥有**索引**方法。 您将其更高版本在此实验室中用于实现页面，其中列出了音乐应用商店的所有内容类型。 现在，只需替换**索引**方法返回一个字符串的以下代码替换&quot;Hello from Store.Index()&quot;:

    (代码段- *ASP.NET MVC 4 基础知识--Ex2 StoreController 索引*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. 添加**浏览**并**详细信息**方法。 若要执行此操作，以下代码添加到**StoreController**:

    (代码段- *ASP.NET MVC 4 基础知识--Ex2 StoreController BrowseAndDetails*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在本任务中，您将试用 web 浏览器中的应用程序。

1. 按**F5**运行该应用程序。
2. 在项目启动**主页**页。 更改 URL 以验证每个操作的实现。

    1. **/ 存储**。 你将看到 **&quot;Hello from Store.Index()&quot;**。
    2. **/ Store/浏览**。 你将看到 **&quot;Hello from Store.Browse()&quot;**。
    3. **/ 存储/详细信息**。 你将看到 **&quot;Hello from Store.Details()&quot;**。

        ![浏览 StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "浏览 StoreBrowse")

        *浏览 /Store/Browse*
3. 关闭浏览器。

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a>练习 3： 将参数传递到控制器

到目前为止，你有已返回的常量字符串从控制器。 在此练习中，您将了解如何将参数传递到控制器使用的 URL 以及查询字符串，然后再进行文本在浏览器对响应的方法操作。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a>任务 1-添加到 StoreController Genre 参数

在本任务中，您将使用**querystring**发送到的参数**浏览**中的操作方法**StoreController**。

1. 如果尚未打开，启动**VS Express for Web**。
2. 在中**文件**菜单中，选择**打开项目**。 在打开项目对话框中，浏览到**Source\Ex03 PassingParametersToAController\Begin**，选择**Begin.sln**然后单击**打开**。 或者，您也可以继续使用该解决方案完成上一练习后获得。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
3. 打开**StoreController**类。 若要执行此操作，在**解决方案资源管理器**，展开**控制器**文件夹，然后双击**StoreController.cs**。
4. 更改**浏览**方法中，添加一个字符串参数来请求提供针对特定流派。 ASP.NET MVC 将自动传递任何查询字符串或窗体发布参数名为**流派**时调用此操作方法。 若要执行此操作，请替换**浏览**方法使用以下代码：

    (代码段- *ASP.NET MVC 4 基础知识--Ex3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> 正在使用**HttpUtility.HtmlEncode**到实用程序方法会阻止用户使用形式的链接将 Javascript 注入到视图  **/Store/浏览？Genre =&lt;脚本&gt;window.location = '[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**。
> 
> 有关更多说明，请访问[此 msdn 文章](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>任务 2-运行应用程序

在此任务中，你将试用 web 浏览器中的应用程序并使用**流派**参数。

1. 按**F5**运行该应用程序。
2. 在项目启动**主页**页。 将 URL 更改为  */存储/浏览？Genre = Disco*以验证该操作接收的 genre 参数。

    ![浏览 StoreBrowseGenre = Disco](aspnet-mvc-4-fundamentals/_static/image10.png "浏览 StoreBrowseGenre = Disco")

    *浏览 /Store/Browse？Genre = Disco*
3. 关闭浏览器。

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a>任务 3-添加在 URL 中嵌入一个 Id 参数

在本任务中，您将使用**URL**传递**Id**参数**详细信息**的操作方法**StoreController**。 ASP.NET MVC 的默认路由约定是将 URL 段作为名为的参数处理在操作方法名称后面**Id**。如果操作方法具有名为 Id 参数，则 ASP.NET MVC 将自动 URL 段对您作为参数传递。 在 URL 中**应用商店/详细信息/5**， **Id**将被解释为**5**。

1. 更改**详细信息**方法**StoreController**、 添加**int**参数调用**id**。若要执行此操作，请替换**详细信息**方法使用以下代码：

    (代码段- *ASP.NET MVC 4 基础知识--Ex3 StoreController DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在此任务中，你将试用 web 浏览器中的应用程序并使用**Id**参数。

1. 按**F5**运行该应用程序。
2. 在项目启动**主页**页。 将 URL 更改为 */Store/Details/5*以验证该操作接收的 id 参数。

    ![浏览 StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "浏览 StoreDetails5")

    *浏览 /Store/Details/5*

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a>练习 4： 创建视图

到目前为止您具有的控制器操作返回的字符串。 虽然这是了解控制器的工作方式的有效方法，但并不如何实际的 Web 应用程序构建。 视图是提供更好的方法以返回到浏览器，使用模板文件中生成 HTML 的组件。

在此练习中将了解如何添加布局的母版页来设置用于常见 HTML 内容，以增强站点和最后一个视图模板以启用 HomeController 返回 HTML 的外观的样式表的模板。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-layoutcshtml"></a>任务 1-修改文件\_layout.cshtml

该文件 **~/Views/Shared/\_layout.cshtml** ，可设置用于在整个网站中使用的常见 HTML 的模板。 在本任务中会将布局母版页与带有链接的常见标头添加到主页和存储区域。

1. 如果尚未打开，启动**VS Express for Web**。
2. 在中**文件**菜单中，选择**打开项目**。 在打开项目对话框中，浏览到**Source\Ex04 CreatingAView\Begin**，选择**Begin.sln**然后单击**打开**。 或者，您也可以继续使用该解决方案完成上一练习后获得。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
3. 该文件 <strong>\_layout.cshtml</strong>包含在站点上的所有页面的 HTML 容器布局。 它包括<strong>&lt;html&gt;</strong>元素的 HTML 响应中，并将<strong>&lt;头&gt;</strong>并<strong>&lt;正文&gt;</strong>元素。 <strong>@RenderBody（)</strong>在 HTML 正文标识区域模板将能够使用动态内容填充该视图。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. 将具有链接的常见标头添加到站点中的所有页面上的主页上和应用商店区域。 为此，添加以下代码&lt;正文&gt;语句。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. 包括一个 div 来呈现每个页的正文部分。 替换 <strong>@RenderBody（)</strong>以下 higlighted 代码: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > 你知道吗？ Visual Studio 2012 提供代码片段，轻松地将常用的代码添加 HTML、 代码文件等 ！ 尝试通过键入**&lt;div&gt;** ，然后按**选项卡**两次，插入一个完整**div**标记。

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a>任务 2-添加 CSS 样式表

空项目模板包含一个非常简化的 CSS 文件只包括用来显示基本窗体和验证消息的样式。 将使用其他 CSS 和图像 （可能由设计器），以便增强站点的外观。

在本任务中，您将添加定义站点的样式的 CSS 样式表。

1. 中包含的 CSS 文件和映像**Source\Assets\Content**本实验的文件夹。 若要将它们添加到应用程序，将从其内容**Windows 资源管理器**到窗口**解决方案资源管理器**在 Visual Studio Express for Web，如下所示：

    ![拖动样式内容](aspnet-mvc-4-fundamentals/_static/image12.png "拖动样式内容")

    *拖动样式内容*
2. 警告将显示一个对话框，询问是否确定要替换**Site.css**文件和某些现有的映像。 检查**应用于所有项**然后单击**是**。

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a>任务 3-添加视图模板

在此任务中，您将添加一个视图模板来生成 HTML 响应将使用布局母版页和 CSS 添加在本练习中。

1. 若要浏览网站的主页上时，请使用视图模板，您将首先需要而不是返回一个字符串，则指示**HomeController 索引**方法将返回**视图**。 打开**HomeController**类，并更改其**索引**方法以返回**ActionResult**，并使其返回**View()**。

    (代码段- *ASP.NET MVC 4 基础知识--Ex4 HomeController 索引*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. 现在，您需要添加适当的视图模板。 若要执行此操作，**右击**内**索引**操作方法，然后选择**添加视图**。 此时会弹出**添加视图**对话框。

    ![将从视图中 Index 方法添加](aspnet-mvc-4-fundamentals/_static/image13.png "添加中 Index 方法中的视图")

    *添加从索引方法中的视图*
3. **添加视图**对话框会出现，生成的视图模板文件。 默认情况下，此对话框预填充视图模板的名称，使其匹配将使用它的操作方法。 因为您使用了**添加视图**内的上下文菜单**索引**HomeController 中的操作方法**添加视图**对话框具有作为默认视图名称的索引。 单击 **添加**。

    ![添加视图对话框](aspnet-mvc-4-fundamentals/_static/image14.png "添加视图对话框")

    *添加视图对话框*
4. Visual Studio 将生成**Index.cshtml**内的视图模板**views/home**文件夹，然后打开它。

    ![主页创建的索引视图](aspnet-mvc-4-fundamentals/_static/image15.png "主页索引视图创建")

    *创建主索引视图*

    > [!NOTE]
    > 名称和位置**Index.cshtml**文件是相关的并遵循的默认 ASP.NET MVC 命名约定。
    > 
    > 文件夹 \Views\**主页** 与控制器名称匹配 (**主页**控制器)。 视图模板名称 (**索引**)，匹配将显示该视图的控制器操作方法。
    > 
    > 这样一来，避免了 ASP.NET MVC，无需显式指定的名称或视图模板的位置时使用此命名约定可以返回视图。
5. 生成的视图模板为基础 **\_layout.cshtml**前面定义的模板。 更新到 ViewBag.Title 属性**主页**，并将更改到的主要内容**这是主页上**，如下面的代码中所示：

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. 选择**MvcMusicStore**项目的解决方案资源管理器和按**F5**运行该应用程序。

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a>任务 4： 验证

若要验证已正确执行所有步骤前一练习中，请继续操作，如下所示：

在浏览器中打开应用程序中，您应该注意的：

1. 找到并显示了 HomeController 的索引操作方法**\Views\Home\Index.cshtml**查看模板，即使调用的代码**返回 View()**，因为视图模板，然后标准命名约定。
2. 主页上显示欢迎使用中定义的消息**\Views\Home\Index.cshtml**视图模板。
3. 使用主页页面 **\_layout.cshtml**模板，因此，欢迎使用消息包含在标准站点 HTML 布局。

    ![主索引视图使用定义 LayoutPage 和样式](aspnet-mvc-4-fundamentals/_static/image16.png "主页使用定义 LayoutPage 和样式的索引视图")

    *使用定义 LayoutPage 和样式的主索引视图*

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a>练习 5： 创建视图模型

到目前为止，进行硬编码 HTML，显示你的视图，但若要创建动态 web 应用程序，视图模板应从控制器接收的信息。 一个要用于此目的的常用技术是**ViewModel**模式，允许控制器打包生成相应的 HTML 响应所需的所有信息。

在此练习中，您将学习如何创建 ViewModel 类并添加所需的属性： 在应用商店和这些影片类型列表中的流派的数。 你还将更新 StoreController 用于创建的 ViewModel，并最后，将创建新的视图模板将显示在页中所述的属性。

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a>任务 1-创建 ViewModel 类

在此任务中，您将创建一个 ViewModel 类，可以将实现存储流派列表方案。

1. 如果尚未打开，启动**VS Express for Web**。
2. 在中**文件**菜单中，选择**打开项目**。 在打开项目对话框中，浏览到**Source\Ex05 CreatingAViewModel\Begin**，选择**Begin.sln**然后单击**打开**。 或者，您也可以继续使用该解决方案完成上一练习后获得。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
3. 创建**Viewmodel**文件夹来保存 ViewModel。 若要执行此操作，右键单击顶级**MvcMusicStore**项目，选择**添加**，然后**新文件夹**。

    ![添加一个新的文件夹](aspnet-mvc-4-fundamentals/_static/image17.png "添加一个新的文件夹")

    *添加一个新的文件夹*
4. 将文件夹命名为*Viewmodel*。

    ![在解决方案资源管理器中的 ViewModels 文件夹](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels 文件夹在解决方案资源管理器")

    *在解决方案资源管理器中的 ViewModels 文件夹*
5. 创建**ViewModel**类。 若要执行此操作，右键单击**Viewmodel**文件夹最近创建的选择**添加**，然后**新项**。 下**代码**，选择**类**项，然后将文件命名*StoreIndexViewModel.cs*，然后单击**添加**。

    ![添加新类](aspnet-mvc-4-fundamentals/_static/image19.png "添加一个新类")

    *添加新类*

    ![创建 StoreIndexViewModel 类](aspnet-mvc-4-fundamentals/_static/image20.png "创建 StoreIndexViewModel 类")

    *创建 StoreIndexViewModel 类*

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a>任务 2-将属性添加到 ViewModel 类

有两个参数以从传递 StoreController 到视图模板以生成预期的 HTML 响应： 在应用商店和这些影片类型列表中的流派的数。

在本任务中，您将添加到这些 2 属性**StoreIndexViewModel**类： **NumberOfGenres** （整数） 和**流派**（字符串列表）。

1. 添加**NumberOfGenres**并**流派**属性设置为**StoreIndexViewModel**类。 若要执行此操作，请向类定义添加下面两行代码：

    (代码段- *ASP.NET MVC 4 基础知识--Ex5 StoreIndexViewModel 属性*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> **{Get; 设置;}** 表示法利用了 C# 的自动实现的属性功能。 它提供一个属性的优点而无需我们声明支持字段。

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a>任务 3-更新 StoreController 使用 StoreIndexViewModel

**StoreIndexViewModel**类将从传递所需的信息进行封装**StoreController**的**索引**视图模板以生成响应的方法.

在本任务中，你将更新**StoreController**若要使用**StoreIndexViewModel**。

1. 打开**StoreController**类。

    ![打开 StoreController 类](aspnet-mvc-4-fundamentals/_static/image21.png "打开 StoreController 类")

    *打开 StoreController 类*
2. 若要使用**StoreIndexViewModel**类派生**StoreController**，在顶部添加以下命名空间**StoreController**代码：

    (代码段- *ASP.NET MVC 4 基础知识-使用 Viewmodel Ex5 StoreIndexViewModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. 更改**StoreController**的**索引**操作方法，以便它创建并填充**StoreIndexViewModel**对象，然后将其传递到视图模板生成 HTML 响应与之。

    > [!NOTE]
    > 在实验室&quot;ASP.NET MVC 模型和数据访问&quot;将编写代码，从数据库中检索的存储类型列表。 在下面的代码，您将创建**列表**的虚拟数据类型，将填充**StoreIndexViewModel**。
    > 
    > 创建和设置后**StoreIndexViewModel**对象，它将作为参数传递**视图**方法。 这表示在视图模板将使用该对象来生成 HTML 响应与之。
4. 替换**索引**方法使用以下代码：

    (代码段- *ASP.NET MVC 4 基础知识--Ex5 StoreController Index 方法*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> 如果您熟悉 C#，您可能会假定使用**var**意味着**viewModel**变量是后期绑定。 这不正确-C# 编译器所使用类型推理基于分配给该变量用于确定是否**viewModel**属于类型**StoreIndexViewModel**。 此外，通过编译本地**viewModel**变量作为**StoreIndexViewModel** get 编译时检查和 Visual Studio 代码编辑器支持类型。

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a>任务 4-创建使用 StoreIndexViewModel 的视图模板

在本任务中，将创建将使用从控制器传递的 StoreIndexViewModel 对象来显示影片类型列表的视图模板。

1. 然后再创建新的视图模板，让我们来生成项目，以便**添加视图对话框**知道**StoreIndexViewModel**类。 通过选择生成项目**构建**菜单项，然后**生成 MvcMusicStore**。

    ![生成项目](aspnet-mvc-4-fundamentals/_static/image22.png "生成项目")

    *生成项目*
2. 创建新的视图模板。 为此，请右键单击内**索引**方法，然后选择**添加视图**。

    ![添加视图](aspnet-mvc-4-fundamentals/_static/image23.png "添加视图")

    *添加视图*
3. 因为**添加视图对话框**从调用**StoreController**，它会将视图模板添加默认情况下**\Views\Store\Index.cshtml**文件。 检查**创建强类型化的视图**复选框，然后选择**StoreIndexViewModel**作为**模型类**。 此外，请确保选择的视图引擎是**Razor**。 单击 **添加**。

    ![添加视图对话框](aspnet-mvc-4-fundamentals/_static/image24.png "添加视图对话框")

    *添加视图对话框*

    **\Views\Store\Index.cshtml**创建视图模板文件并将其打开。 根据提供的信息**添加视图**中的最后一步，模板将预期的视图的对话框**StoreIndexViewModel**实例标记为要用于生成 HTML 响应的数据。 你会注意到模板继承`ViewPage<musicstore.viewmodels.storeindexviewmodel>`C# 中。

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a>任务 5-正在更新视图模板

在本任务中，你将更新中检索的类型和其名称在页面内的最后一个任务创建的视图模板。

> [!NOTE]
> 将使用语法 @ (通常称为&quot;代码片段&quot;) 执行视图模板中的代码。

1. 在**Index.cshtml**文件内,**存储区**文件夹中，其代码替换为以下代码：

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. 循环访问中的流派列表**StoreIndexViewModel**并创建一个 HTML **&lt;u l&gt;** 列出使用**foreach**循环。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. 按**F5**运行该应用程序和浏览 **/存储**。 您将看到传入的流派列表**StoreIndexViewModel**对象从**StoreController**到视图模板。

    ![视图显示影片类型列表](aspnet-mvc-4-fundamentals/_static/image26.png "视图，用于显示影片类型列表")

    *视图显示影片类型列表*
4. 关闭浏览器。

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a>练习 6： 在视图中使用参数

练习 3 介绍了如何将参数传递到控制器。 在此练习中，您将学习如何在视图模板中使用这些参数。 为此，将向你介绍首次将帮助你管理你的数据和域逻辑的模型类。 此外，您将学习如何创建 ASP.NET MVC 应用程序内的页面的链接而无需担心的事情，如编码的 URL 路径。

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a>任务 1-添加模型类

与 Viewmodel，创建只是为了将信息从控制器传递给视图，不同模型的类用于包含和管理数据和域逻辑。 在此任务中，您将添加两个模型类来表示这些概念：**流派**并**唱片集**。

1. 如果尚未打开，启动**VS Express for Web**
2. 在中**文件**菜单中，选择**打开项目**。 在打开项目对话框中，浏览到**Source\Ex06 UsingParametersInView\Begin**，选择**Begin.sln**然后单击**打开**。 或者，您也可以继续使用该解决方案完成上一练习后获得。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
3. 添加**流派**的模型。 若要执行此操作，右键单击**模型**中的文件夹**解决方案资源管理器**，选择**添加**，然后**新项**选项。 下**代码**，选择**类**项，然后将文件命名*Genre.cs*，然后单击**添加**。

    ![添加类](aspnet-mvc-4-fundamentals/_static/image27.png "添加类")

    *添加新项*

    ![添加流派模型类](aspnet-mvc-4-fundamentals/_static/image28.png "添加流派 Model 类")

    *添加流派 Model 类*
4. 添加**名称**流派类的属性。 若要执行此操作，添加以下代码：

    (代码段- *ASP.NET MVC 4 基础知识--Ex6 流派*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. 按照与前面一样，相同的步骤添加**唱片集**类。 若要执行此操作，右键单击**模型**中的文件夹**解决方案资源管理器**，选择**添加**，然后**新项**选项。 下**代码**，选择**类**项，然后将文件命名*Album.cs*，然后单击**添加**。
6. 将两个属性添加到唱片集类：**流派**并**标题**。 若要执行此操作，添加以下代码：

    (代码段- *ASP.NET MVC 4 基础知识--Ex6 唱片集*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a>任务 2-添加 StoreBrowseViewModel

一个**StoreBrowseViewModel**将在本任务中使用以显示匹配所选的流派唱片集。 在此任务中，您将创建此类，然后添加两个属性，以处理**流派**并将其**唱片集**的列表。

1. 添加**StoreBrowseViewModel**类。 若要执行此操作，右键单击**Viewmodel**中的文件夹**解决方案资源管理器**，选择**添加**，然后**新项**选项。 下**代码**，选择**类**项，然后将文件命名*StoreBrowseViewModel.cs*，然后单击**添加**。
2. 添加对中的模型的引用**StoreBrowseViewModel**类。 若要执行此操作，添加以下使用命名空间：

    (代码段- *ASP.NET MVC 4 基础知识--Ex6 UsingModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. 添加到两个属性**StoreBrowseViewModel**类：**流派**并**相册**。 若要执行此操作，添加以下代码：

    (代码段- *ASP.NET MVC 4 基础知识--Ex6 ModelProperties*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> 什么是**列表&lt;唱片集&gt;** ？: 使用此定义**列表&lt;T&gt;** 类型，其中**T**约束向此元素的类型**列表**属于，在这种情况下**唱片集**（或其任何子代）。
> 
> 若要设计类和方法的类或方法声明并实例化由客户端代码是 C# 语言的一个功能之前延迟的一个或多个类型的规范，此功能称为**泛型**。
> 
> **列表&lt;T&gt;** 泛型等效于**ArrayList**键入和现已推出**System.Collections.Generic**命名空间。 使用的好处之一**泛型**是，由于指定的类型，不需要处理的类型检查操作，例如强制转换到的元素**唱片集**需要像一样**ArrayList**。

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a>任务 3-在 StoreController 中使用新的 ViewModel

在本任务中，您将修改**StoreController**的**浏览**并**详细信息**操作方法为使用新**StoreBrowseViewModel**.

1. 添加对模型文件夹中的引用**StoreController**类。 若要执行此操作，请展开**控制器**中的文件夹**解决方案资源管理器**，然后打开**StoreController**类。 然后添加以下代码：

    (代码段- *ASP.NET MVC 4 基础知识--Ex6 UsingModelInController*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. 替换**浏览**要使用的操作方法**StoreViewBrowseController**类。 您将使用虚拟数据创建一种流派和两个新的唱片集对象 （在下一步的动手实验室中您将使用数据库中的实际数据）。 若要执行此操作，请替换**浏览**方法使用以下代码：

    (代码段- *ASP.NET MVC 4 基础知识--Ex6 BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. 替换**详细信息**要使用的操作方法**StoreViewBrowseController**类。 您将创建一个新**唱片集**对象返回给**视图**。 若要执行此操作，请替换**详细信息**方法使用以下代码：

    (代码段- *ASP.NET MVC 4 基础知识--Ex6 DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a>任务 4-添加浏览视图模板

在本任务中，您将添加**浏览**视图以显示找到的特定流派唱片集。

1. 在创建新的视图模板之前, 应先生成项目，以便**添加视图**对话框知道**ViewModel**类使用。 通过选择生成项目**构建**菜单项，然后**生成 MvcMusicStore**。
2. 添加**浏览**视图。 若要执行此操作，右键单击**浏览**的操作方法**StoreController**然后单击**添加视图**。
3. 在中**添加视图**对话框框中，验证是否视图名称**浏览**。 检查**创建强类型化视图**复选框，然后选择**StoreBrowseViewModel**从**模型类**下拉列表。 其他字段保留为其默认值。 然后单击 **“添加”**。

    ![添加浏览视图](aspnet-mvc-4-fundamentals/_static/image29.png "添加浏览视图")

    *添加浏览视图*
4. 修改**Browse.cshtml**以显示类型的信息，请访问**StoreBrowseViewModel**传递给视图模板对象。 若要执行此操作，将内容替换为以下代码: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，将测试**浏览**方法检索从相册**浏览**方法操作。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为  **/存储/浏览？Genre = Disco**以验证操作返回两个唱片集。

    ![浏览应用商店 Disco 相册](aspnet-mvc-4-fundamentals/_static/image30.png "浏览应用商店 Disco 相册")

    *浏览应用商店 Disco 相册*

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a>任务 6-显示有关特定唱片集的信息

在本任务中，您将实现**商店/详细信息**视图以显示有关特定唱片集信息。 在此动手实验中，将显示有关唱片集的所有内容已包含在**视图**模板。 是的而不是创建**StoreDetailsViewModel**类，您将使用当前**StoreBrowseViewModel**将唱片集传递给它的模板。

1. 关闭浏览器，如果需要以返回到 Visual Studio 窗口。 添加一个新**详细信息**查看**StoreController**的**详细信息**操作方法。 若要执行此操作，右键单击**详细信息**中的方法**StoreController**类，并单击**添加视图**。
2. 在中**添加视图**对话框中，确认**视图名称**是**详细信息**。 检查**创建强类型化视图**复选框，然后选择**唱片集**从**模型类**下拉列表。 其他字段保留为其默认值。 然后单击 **“添加”**。 这将创建并打开**\Views\Store\Details.cshtml**文件。

    ![添加详细信息视图](aspnet-mvc-4-fundamentals/_static/image31.png "添加详细信息视图")

    *添加详细信息视图*
3. 修改**Details.cshtml**文件以显示唱片集的信息，请访问**唱片集**传递给视图模板对象。 若要执行此操作，将内容替换为以下代码: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>任务 7-运行应用程序

在此任务中，将测试**详细信息**视图检索中的唱片集的信息**详细介绍了操作**方法。

1. 按**F5**运行该应用程序。
2. 在项目启动**主页**页。 将 URL 更改为 **/Store/Details/5**验证唱片集的信息。

    ![浏览唱片集详细信息](aspnet-mvc-4-fundamentals/_static/image32.png "浏览唱片集详细信息")

    *浏览唱片集的详细信息*

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a>任务 8-添加页之间的链接

在本任务中，您将添加要为相应的每个流派名称中具有一个链接的存储区视图中的链接 **/Store/浏览**URL。 这样一来，例如单击某个类型时**Disco**，它将导航到 **/Store/浏览？ genre = Disco** URL。

1. 关闭浏览器，如果需要以返回到 Visual Studio 窗口。 更新**索引**页，将添加到链接**浏览**页。 若要执行此操作，在**解决方案资源管理器**展开**视图**文件夹，然后**应用商店**文件夹，然后双击**Index.cshtml**页。
2. 将链接添加到所选流派，该值指示浏览视图。 若要执行此操作，将以下突出显示的代码内**&lt;li&gt;** 标记: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > 另一种方法会将链接直接到页上，使用如下所示的代码：
   > 
   > &lt;a =&quot;/Store/浏览？ genre =@genreName&quot;&gt;@genreName &lt; /a&gt;
   > 
   > 尽管这种方法有效，但它依赖于硬编码的字符串。 如果您更高版本重命名控制器，您将必须手动更改此指令。 更好的替代方法是使用**的 HTML 帮助器**方法。 ASP.NET MVC 包括一个 HTML 帮助器方法，可用于此类任务。 **Html.ActionLink()** 帮助器方法，可轻松构建 HTML **&lt;&gt;** 链接，以确保 URL 路径为正确编码的 URL。
   > 
   > Htlm.ActionLink 有多个重载。 在此练习将使用一个采用三个参数：
   > 
   > 1. 链接文本，将显示类型名称
   > 2. 控制器操作名称 (**浏览**)
   > 3. 路由参数值，指定这两个名称 (**流派**) 和值 (**流派名称**)

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a>任务 9-运行应用程序

在本任务中，您将测试，其中包含指向相应显示每个流派 **/Store/浏览**URL。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为 **/存储**以验证每个流派链接到相应 **/Store/浏览**URL。

    ![浏览页面的链接进行浏览流派](aspnet-mvc-4-fundamentals/_static/image33.png "浏览流派链接浏览页面")

    *浏览页面的链接进行浏览类型*

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a>任务 10-使用动态 ViewModel 集合以将值传递

在本任务中，您将学习的简单而强大的方法而无需进行任何更改在模型中的控制器和视图之间传递值。 ASP.NET MVC 4 提供的集合&quot;ViewModel&quot;，这可以分配给任何动态值和控制器和视图也内部访问。

您现在将使用 ViewBag 动态集合的列表传递给&quot;**带有星标流派**&quot;从到视图控制器。 存储索引视图将权**ViewModel**和显示的信息。

1. 关闭浏览器，如果需要以返回到 Visual Studio 窗口。 打开**StoreController.cs**并修改**索引**方法来创建一系列带有流派星标到 ViewModel 集合：

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > 此外可以使用语法**ViewBag [&quot;Starred&quot;]** 访问的属性。
2. 星形图标**&quot;starred.png&quot;** 中包含**Source\Assets\Images**本实验的文件夹。 若要将其添加到应用程序，将从其内容**Windows 资源管理器**到窗口**解决方案资源管理器**Visual Web Developer 速成版中，如下所示：

    ![向解决方案添加星形图像](aspnet-mvc-4-fundamentals/_static/image34.png "添加到解决方案的星形图像")

    *向解决方案添加星形图像*
3. 打开视图**Store/Index.cshtml**并修改的内容。 将读取&quot;带有星标&quot;属性中的**ViewBag**集合，并要求当前的类型名称是否在列表中。 在这种情况下将显示从右到流派链接星形图标。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a>任务 11-运行应用程序

在本任务中，您将测试带星号的流派显示星形图标。

1. 按**F5**运行该应用程序。
2. 在项目启动**主页**页。 将 URL 更改为 **/存储**以验证每个特色的风格有 respecting 标签：

    ![与带星号的元素浏览流派](aspnet-mvc-4-fundamentals/_static/image35.png "浏览与带星号的元素的类型")

    *浏览与带星号的元素的类型*

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a>练习 7： 了解 ASP.NET MVC 4 新模板

在此练习中，您将了解 ASP.NET MVC 4 项目模板的增强功能使新模板的最相关功能的介绍。

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a>任务 1： 浏览 ASP.NET MVC 4 Internet 应用程序模板

1. 如果尚未打开，启动**VS Express for Web**
2. 选择**文件 |新 |项目**菜单命令。 在中**新的项目**对话框中，选择**Visual C# |Web**在左窗格中的模板树，然后选择**ASP.NET MVC 4 Web 应用程序**。 **名称**项目*MusicStore* ，并更新**解决方案名称**到*开始*，然后选择一个位置 （或保留默认值），单击**确定**.

    ![创建新的 ASP.NET MVC 4 项目](aspnet-mvc-4-fundamentals/_static/image36.png "创建新的 ASP.NET MVC 4 项目")

    *创建新的 ASP.NET MVC 4 项目*
3. 在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**项目模板，然后单击**确定**。 请注意，您可以选择 Razor 或 ASPX 作为视图引擎。

    ![创建新 ASP.NET MVC 4 Internet 应用程序](aspnet-mvc-4-fundamentals/_static/image37.png "新建 ASP.NET MVC 4 Internet 应用程序")

    *创建新 ASP.NET MVC 4 Internet 应用程序*

    > [!NOTE]
    > 在 ASP.NET MVC 3 中引入了 razor 语法。 其目标是字符和击键所需的文件中启用快速、 流畅编码工作流的数量降至最低。 Razor 利用现有 C# /VB （或其他） 语言技能，并提供可以实现令人惊叹的 HTML 构造工作流的模板标记语法。
4. 按**F5**以运行该解决方案并查看已续订的模板。 您可以签出了以下功能：

    1. **现代样式模板**

        模板已被续订，提供更多的新式样式。

        ![ASP.NET MVC 4 restyled 模板](aspnet-mvc-4-fundamentals/_static/image38.png "restyled 模板的 ASP.NET MVC 4")

        *ASP.NET MVC 4 restyled 模板*
    2. **自适应呈现**

        签出调整浏览器窗口，请注意，页面布局如何动态调整为新的窗口大小。 这些模板使用自适应呈现技术在没有任何自定义项的桌面和移动平台中正确呈现。

        ![在不同的浏览器大小中的 ASP.NET MVC 4 项目模板](aspnet-mvc-4-fundamentals/_static/image39.png "中不同的浏览器大小的 ASP.NET MVC 4 项目模板")

        *在不同的浏览器大小中的 ASP.NET MVC 4 项目模板*
5. 关闭浏览器以停止调试器并返回到 Visual Studio。
6. 现在，已能够了解解决方案，并查看一些 ASP.NET MVC 4 项目模板中引入的新功能。

    ![ASP.NET MVC4-internet 的应用程序的项目的模板](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 Internet 应用程序项目模板")

    *ASP.NET MVC 4 Internet 应用程序项目模板*

   1. **HTML5 标记**

       浏览模板视图若要了解新主题的标记，例如打开**About.cshtml**内查看**主页**文件夹。

       ![使用 Razor 和 HTML5 标记的新模板](aspnet-mvc-4-fundamentals/_static/image41.png "使用 Razor 和 HTML5 标记的新模板")

       *使用 Razor 和 HTML5 标记的新模板*
   2. **包含的 JavaScript 库**

      1. **jQuery**: jQuery 简化了 HTML 文档遍历、 事件处理、 进行动画处理，和 Ajax 交互。
      2. **jQuery UI**： 此库提供用于低级别交互和动画，高级效果和受主题影响小组件，基于 jQuery JavaScript 库抽象。

         > [!NOTE]
         > 您可以了解 jQuery 和 jQuery UI 中[ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/)。
      3. **KnockoutJS**: ASP.NET MVC 4 默认模板现在包括**KnockoutJS**，可以创建使用 JavaScript 和 HTML 的丰富和高响应 web 应用程序的 JavaScript MVVM 框架。 像在 ASP.NET MVC 3 中，jQuery 和 jQuery UI 库还包含在 ASP.NET MVC 4。

          > [!NOTE]
          > 可以获取有关此链接中的 KnockOutJS 库的详细信息： [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/)。
      4. **Modernizr**： 此库将自动运行，使您的网站与较旧的浏览器兼容，当使用 HTML5 和 CSS3 的技术。

          > [!NOTE]
          > 可以获取有关此链接中的 Modernizr 库的详细信息： [ http://www.modernizr.com/ ](http://www.modernizr.com/)。
   3. **Simplemembership 一起包含在解决方案中**

       Simplemembership 一起旨在以替换先前的 ASP.NET 角色和成员资格提供程序系统。 它具有许多新功能，它更轻松地进行安全的 web 页面开发人员以更灵活的方式。

       Internet 模板已设置了一些将 simplemembership 一起进行集成，例如，AccountController 已准备好使用 OAuthWebSecurity （适用于 OAuth 帐户注册、 登录、 管理等） 和 Web 的安全。

       ![解决方案中包含 SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "simplemembership 一起包含在解决方案中")

       *Simplemembership 一起包含在解决方案中*

       > [!NOTE]
       > 查找有关的详细信息[OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) MSDN 中。

> [!NOTE]
> 此外，可以部署此应用程序到 Windows Azure Web Sites 以下[附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixB)。


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>总结

通过完成本动手实验介绍了 ASP.NET MVC 的基础知识：

- MVC 应用程序和它们的交互方式的核心元素
- 如何创建 ASP.NET MVC 应用程序
- 如何添加和配置控制器来处理参数传递的 URL 和查询字符串
- 如何添加布局的母版页来设置用于常见 HTML 内容，以增强外观和感觉和视图模板，以显示 HTML 内容的样式表的模板
- 如何使用视图模型的模式，将属性传递给视图模板来显示动态信息
- 如何使用传递到控制器视图模板中的参数
- 如何将链接添加到 ASP.NET MVC 应用程序内的页面
- 如何添加和使用视图中的动态属性
- ASP.NET MVC 4 项目模板中的增强功能

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 a： 安装 Visual Studio Express 2012 for Web

你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**. 以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。

1. 转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。
2. 单击**立即安装**。 如果还没有**Web 平台安装程序**将重定向以下载并安装。
3. 一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，然后单击**我接受**以继续。

    ![接受许可条款](aspnet-mvc-4-fundamentals/_static/image44.png)

    *接受许可条款*
5. 等待，直到下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-fundamentals/_static/image45.png)

    *安装进度*
6. 安装完成后，单击**完成**。

    ![安装已完成](aspnet-mvc-4-fundamentals/_static/image46.png)

    *安装已完成*
7. 单击**退出**以关闭 Web 平台安装程序。
8. 若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-fundamentals/_static/image47.png)

    *VS Express for Web 磁贴*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署

本附录将演示如何从 Windows Azure 管理门户创建新的网站和发布应用程序获取按照本实验中，利用 Windows Azure 提供的 Web 部署发布功能。

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>任务 1-创建新的 Web 站点从 Windows Azure 门户

1. 转到[Windows Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。

    > [!NOTE]
    > 使用 Windows Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。 你可以注册[此处](http://aka.ms/aspnet-hol-azure)。

    ![登录到 Windows Azure 门户](aspnet-mvc-4-fundamentals/_static/image48.png "登录到 Windows Azure 门户")

    *登录到 Windows Azure 管理门户*
2. 单击**新建**命令栏上。

    ![创建新的 Web 站点](aspnet-mvc-4-fundamentals/_static/image49.png "创建新的 Web 站点")

    *创建新的 Web 站点*
3. 单击**计算** | **网站**。 然后选择**快速创建**选项。 为新网站提供可用的 URL，然后单击**创建网站**。

    > [!NOTE]
    > Windows Azure 网站是可以控制和管理在云中运行的 web 应用程序主机。 快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从门户外部的部署。 它不包括用于设置数据库的步骤。

    ![创建新的网站使用快速创建](aspnet-mvc-4-fundamentals/_static/image50.png "创建新的网站使用快速创建")

    *创建新的网站使用快速创建*
4. 等到新**网站**创建。
5. 创建网站后，单击下面的链接**URL**列。 检查新的 Web 站点正常工作。

    ![浏览到新的 web 站点](aspnet-mvc-4-fundamentals/_static/image51.png "浏览到新的 web 站点")

    *浏览到新的 web 站点*

    ![正在运行的网站](aspnet-mvc-4-fundamentals/_static/image52.png "正在运行的网站")

    *正在运行的网站*
6. 返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。

    ![打开网站管理页](aspnet-mvc-4-fundamentals/_static/image53.png "打开网站管理页")

    *打开网站管理页*
7. 在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。

    > [!NOTE]
    > *发布配置文件*包含所有发布到每个启用的发布方法的 Windows Azure 网站的 web 应用程序所需的信息。 发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。 **Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Windows Azure 网站。

    ![正在下载网站发布配置文件](aspnet-mvc-4-fundamentals/_static/image54.png "下载网站发布配置文件")

    *正在下载网站发布配置文件*
8. 下载发布配置文件到已知位置。 进一步在此练习中将了解如何使用此文件从 Visual Studio 的 web 应用程序到 Windows Azure 网站发布。

    ![保存发布配置文件](aspnet-mvc-4-fundamentals/_static/image55.png "保存发布配置文件")

    *保存发布配置文件*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。 如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。

1. 用于存储应用程序数据库，将需要 SQL 数据库服务器。 可以从在 Windows Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。 如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。 请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。 不创建数据库，因为它将在后面的阶段中创建。

    ![SQL 数据库服务器仪表板](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database 服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。 若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png)按钮。

    ![添加客户端 IP 地址](aspnet-mvc-4-fundamentals/_static/image58.png)

    *添加客户端 IP 地址*
3. 一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。

    ![确认更改](aspnet-mvc-4-fundamentals/_static/image59.png)

    *确认更改*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布

1. 返回到 ASP.NET MVC 4 解决方案。 在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。

    ![发布应用程序](aspnet-mvc-4-fundamentals/_static/image60.png "发布应用程序")

    *发布此网站*
2. 导入发布配置文件保存在第一个任务。

    ![导入发布配置文件](aspnet-mvc-4-fundamentals/_static/image61.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击**验证连接**。 验证完成后单击**下一步**。

    > [!NOTE]
    > 请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。

    ![验证连接](aspnet-mvc-4-fundamentals/_static/image62.png "验证连接")

    *验证连接*
4. 在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。

    ![Web 部署配置](aspnet-mvc-4-fundamentals/_static/image63.png "Web 部署配置")

    *Web 部署配置*
5. 配置数据库连接，如下所示：

   - 在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。
   - 在中**用户名**键入服务器管理员登录名。
   - 在中**密码**键入服务器管理员登录密码。
   - 键入新的数据库名称，例如： *MVC4SampleDB*。

     ![配置目标连接字符串](aspnet-mvc-4-fundamentals/_static/image64.png "配置目标连接字符串")

     *配置目标连接字符串*
6. 然后单击“确定” 。 当系统提示你创建数据库时，单击**是**。

    ![创建数据库](aspnet-mvc-4-fundamentals/_static/image65.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。 然后，单击 **“下一步”**。

    ![连接字符串指向 SQL 数据库](aspnet-mvc-4-fundamentals/_static/image66.png "指向 SQL 数据库连接字符串")

    *连接字符串指向 SQL 数据库*
8. 在中**预览版**页上，单击**发布**。

    ![Web 应用程序发布](aspnet-mvc-4-fundamentals/_static/image67.png "发布 web 应用程序")

    *Web 应用程序发布*
9. 在发布过程完成后，在默认浏览器将打开已发布的网站。

    ![应用程序发布到 Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "应用程序发布到 Windows Azure")

    *应用程序发布到 Windows Azure*

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附录 c： 使用代码片段

使用代码段，可以轻松获得相关所需的所有代码。 实验室文档将告诉您完全何时可以使用它们，如下图中所示。

![使用 Visual Studio 代码段代码插入到你的项目](aspnet-mvc-4-fundamentals/_static/image69.png "使用 Visual Studio 代码段代码插入到你的项目")

*使用 Visual Studio 代码段代码插入到你的项目*

***若要添加代码段使用键盘 (仅限 C#)***

1. 将光标置于要插入的代码。
2. 开始键入代码片段名称 （不带空格或连字符）。
3. 观看作为 IntelliSense 显示匹配的代码段的名称。
4. 选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。
5. 按 Tab 键两次，以在光标位置插入代码段。

![开始键入代码段名称](aspnet-mvc-4-fundamentals/_static/image70.png "开始键入代码段名称")

*开始键入代码段名称*

![按 tab 键以选择突出显示代码段](aspnet-mvc-4-fundamentals/_static/image71.png "按选项卡以选择突出显示代码段")

*按 tab 键以选择突出显示代码段*

![再次按 Tab 和代码段将 expand](aspnet-mvc-4-fundamentals/_static/image72.png "再次按 Tab 和代码段将扩展")

*再次按 Tab 和代码段将扩展*

***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。 右键单击你想要插入的代码片段。

1. 选择**插入代码段**跟**我的代码片段**。
2. 通过单击选择列表中中的相关代码片段。

![右键单击你想要插入代码段和选择插入代码段](aspnet-mvc-4-fundamentals/_static/image73.png "右键单击你想要插入代码段和选择插入代码段")

*右键单击你想要插入代码段和选择插入代码段*

![通过单击选择列表中中的相关代码片段](aspnet-mvc-4-fundamentals/_static/image74.png "通过单击选择列表中中的相关代码片段")

*通过单击选择列表中中的相关代码片段*
