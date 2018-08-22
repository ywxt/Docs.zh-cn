---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: 生成使用 ASP.NET Web API 的 RESTful Api |Microsoft Docs
author: rick-anderson
description: 近年来，它已成为清除 HTTP 不再仅仅用于提供 HTML 页面。 它也是一个强大的平台，用于构建 Web Api，使用一些 o...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 00304f67138873318b63c5e2ad0cd69aa7449521
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824657"
---
<a name="build-restful-apis-with-aspnet-web-api"></a>生成使用 ASP.NET Web API 的 RESTful Api
====================
通过[Web 训练营团队](https://twitter.com/webcamps)

> 近年来，它已成为清除 HTTP 不再仅仅用于提供 HTML 页面。 它也是一个强大的平台，用于构建 Web Api，使用少数几个动词 （GET、 POST 等） 以及几个简单的概念类似于*Uri*并*标头*。 ASP.NET Web API 是一组简化 HTTP 编程的组件。 因为它基于 ASP.NET MVC 运行时，Web API 将自动处理 HTTP 的低级别传输详细信息。 同时，Web API 自然会公开 HTTP 编程模型。 实际上，Web API 的一个目标是向*不*抽象出 HTTP 的现实。 因此，Web API 是灵活且易于扩展。 在本动手实验中，将使用 Web API 来构建一个简单的 REST API 为联系人管理器应用程序。 您还将生成客户端以使用 API。 REST 体系结构风格已被证明是利用 HTTP-的有效方法，尽管它并不是 HTTP 的唯一有效方法。 联系人管理器将公开用于列出、 添加和删除联系人，以及其他基于 Rest。 本实验需要基本了解 HTTP，其余部分，并假定你已基本了解 HTML、 JavaScript 和 jQuery。
> 
> > [!NOTE]
> > ASP.NET 网站上有一个专用于在 ASP.NET Web API 框架的区域[ https://asp.net/web-api ](https://asp.net/web-api)。 此站点将继续提供最新信息、 示例和新闻与 Web API，因此它请经常查看如果你想要深入了解创建可用于几乎任何设备或开发框架自定义 Web Api 的画面。
> > 
> > ASP.NET Web API，类似于 ASP.NET MVC 4 中，有很大的灵活性方面将服务层与允许您使用多个可用的依赖关系注入框架变得相当容易的控制器分离开来。 演示如何使用依赖关系注入在 ASP.NET Web API 项目中，你可以下载它从 Ninject 的 MSDN 中没有一个好的示例[此处](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)。
> 
> 
> 在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)。


<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验，您将学习如何：

- 实现 rest 样式 Web API
- 从 HTML 客户端调用 API

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

完成本动手实验需要以下：

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 B](#AppendixB)有关如何安装它的说明)。

<a id="Setup"></a>
### <a name="setup"></a>安装

**安装代码片段**

为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。 若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。

如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 a： 使用代码片段](#AppendixA)&quot;。

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [练习 1： 创建只读的 Web API](#Exercise1)
2. [练习 2： 创建读/写 Web API](#Exercise2)
3. [练习 3： 使用从 HTML 客户端 Web API](#Exercise3)

> [!NOTE]
> 每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。 如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。


估计的时间才能完成此实验： **60 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a>练习 1： 创建只读的 Web API

在此练习中，将为联系人管理器实现只读的 GET 方法。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a>任务 1-创建 API 项目

在本任务中，您将使用新的 ASP.NET web 项目模板创建 Web API web 应用程序。

1. 运行**Visual Studio 2012 Express for Web**，为此，请转到**启动**并键入**VS Express for Web**然后按**Enter**。
2. 从**文件**菜单中，选择**新项目**。 选择**Visual C# |Web**项目类型从项目类型树视图，然后选择**ASP.NET MVC 4 Web 应用程序**项目类型。 将项目的**名称**到*ContactManager*并**解决方案名称**到*开始*，然后单击**确定**.

    ![创建新的 ASP.NET MVC 4.0 Web 应用程序项目](build-restful-apis-with-aspnet-web-api/_static/image1.png "创建新的 ASP.NET MVC 4.0 Web 应用程序项目")

    *创建新的 ASP.NET MVC 4.0 Web 应用程序项目*
3. 在 ASP.NET MVC 4 项目类型对话框中，选择**Web API**项目类型。 单击 **“确定”**。

    ![指定 Web API 项目类型](build-restful-apis-with-aspnet-web-api/_static/image2.png "指定 Web API 项目类型")

    *指定 Web API 项目类型*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a>任务 2-创建联系人管理器 API 控制器

在本任务中，将创建 API 方法将驻留在其中的控制器类。

1. 删除名为的文件**ValuesController.cs**内**控制器**从项目的文件夹。
2. 右键单击**控制器**文件夹中该项目并选择**添加 |控制器**从上下文菜单。

    ![向项目添加新的控制器](build-restful-apis-with-aspnet-web-api/_static/image3.png "向项目添加新的控制器")

    *向项目添加新的控制器*
3. 在中**添加控制器**对话框中，选择**空 API 控制器**的模板菜单中。 控制器类命名**ContactController**。 然后，单击**添加。**

    ![使用添加控制器对话框创建新的 Web API 控制器](build-restful-apis-with-aspnet-web-api/_static/image4.png "使用添加控制器对话框创建新的 Web API 控制器")

    *使用添加控制器对话框创建新的 Web API 控制器*
4. 将以下代码添加到**ContactController**。

    (代码段- *Web API 实验-Ex01-获取 API 方法*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. 按**F5**调试应用程序。 Web API 项目的默认主页应显示。

    ![ASP.NET Web API 应用程序的默认主页](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 应用程序的默认主页")

    *ASP.NET Web API 应用程序的默认主页*
6. 在 Internet Explorer 窗口中，按**F12**键以打开**开发人员工具**窗口。 单击**网络**选项卡，然后依次**启动捕获**按钮开始到窗口中捕获网络流量。

    ![打开网络选项卡并启动网络捕获](build-restful-apis-with-aspnet-web-api/_static/image6.png "打开网络选项卡并启动网络捕获")

    *打开网络选项卡并启动网络捕获*
7. 追加与浏览器的地址栏中的 URL **/api/contact** ，然后按 enter。 传输的详细信息会在网络捕获窗口中显示。 请注意，响应的 MIME 类型是**应用程序 /json**。 此示例演示默认输出格式的 JSON 的方式。

    ![在网络视图中查看 Web API 请求的输出](build-restful-apis-with-aspnet-web-api/_static/image7.png "网络视图中查看 Web API 请求的输出")

    *在网络视图中查看 Web API 请求的输出*

    > [!NOTE]
    > Internet Explorer 10 的默认行为现在将询问如果用户想要保存或打开生成的 Web API 调用的流。 输出将包含 Web API URL 调用的 JSON 结果的文本文件。 若要查看通过开发人员工具窗口的响应的内容将不取消对话框。
8. 单击**转到详细视图**按钮以查看有关此 API 调用的响应的详细信息。

    ![切换到详细视图](build-restful-apis-with-aspnet-web-api/_static/image8.png "切换到详细信息视图")

    *切换到详细视图*
9. 单击**响应正文**选项卡以查看实际的 JSON 响应文本。

    ![查看 JSON 输出网络监视器中的文本](build-restful-apis-with-aspnet-web-api/_static/image9.png "查看 JSON 输出网络监视器中的文本")

    *在网络监视器中查看 JSON 输出文本*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a>任务 3-创建联系人的模型和增加为 Contact Controller

在本任务中，将创建 API 方法将驻留在其中的控制器类。

1. 右键单击**模型**文件夹，然后选择**添加 |类...** 从上下文菜单。

    ![向 web 应用程序中添加新模型](build-restful-apis-with-aspnet-web-api/_static/image10.png "向 web 应用程序中添加新模型")

    *向 web 应用程序中添加新模型*
2. 在中**添加新项**对话框中，将新文件命名**Contact.cs**单击**添加。**

    ![创建新的联系人类文件](build-restful-apis-with-aspnet-web-api/_static/image11.png "创建新的联系人类文件")

    *创建新的联系人类文件*
3. 将以下突出显示的代码添加到**联系人**类。

    (代码段- *Web API 实验-Ex01-Contact 类*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. 在**ContactController**类中，选择 word**字符串**中的方法定义**获取**方法，并键入单词*联系人*。 在键入的单词后, 指示器将出现在单词的开头**联系人**。 可以按住**Ctrl**键和按句点 （.） 键或单击使用鼠标打开在代码编辑器中，以自动填充帮助对话框图标**使用**指令的模型命名空间。

    ![对于命名空间声明中使用 Intellisense 协助](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    *对于命名空间声明中使用 Intellisense 协助*
5. 修改的代码**获取**方法，以便它返回联系人模型实例的数组。

    (代码段-*返回的联系人列表 Web API 实验-Ex01-*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. 按**F5**调试 web 应用程序在浏览器中的。 若要查看 API 的响应输出所做的更改，请执行以下步骤。

   1. 在浏览器打开后，按**F12**如果开发人员工具还不打开。
   2. 单击**网络**选项卡。
   3. 按**启动捕获**按钮。
   4. 添加 URL 后缀 **/api/contact**到的 URL 地址栏，然后按**Enter**密钥。
   5. 按**转到详细视图**按钮。
   6. 选择**响应正文**选项卡。应会看到表示联系人实例的数组的序列化的形式的 JSON 字符串。

      ![JSON 序列化复杂的 Web API 方法调用的输出](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON 序列化复杂的 Web API 方法调用的输出")

      *复杂的 Web API 方法调用的序列化的 JSON 输出*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a>任务 4-解压缩功能集成到服务层

此任务将演示如何功能提取到服务层，以方便开发人员可以将其服务的功能与控制器层，从而允许实际完成工作的服务的可重用性。

1. 在解决方案根目录中创建一个新文件夹并将其命名**Services**。 若要执行此操作，右键单击**ContactManager**项目，选择**添加** | **新文件夹**，其命名为*服务*。

    ![创建服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image14.png "创建服务文件夹")

    *正在创建服务文件夹*
2. 右键单击**Services**文件夹，然后选择**添加 |类...** 从上下文菜单。

    ![将新类添加到服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image15.png "将新类添加到服务文件夹")

    *将新类添加到服务文件夹*
3. 当**添加新项**对话框出现时，将新类命名**ContactRepository**然后单击**添加**。

    ![创建一个类文件以包含联系人存储库服务层的代码](build-restful-apis-with-aspnet-web-api/_static/image16.png "创建类文件以包含联系人存储库服务层的代码")

    *创建一个类文件以包含联系人存储库服务层的代码*
4. 添加 using 指令**ContactRepository.cs**文件以包括模型命名空间。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. 将以下突出显示的代码添加到**ContactRepository.cs**文件以实现 GetAllContacts 方法。

    (代码段- *Web API 实验-Ex01-联系人存储库*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. 打开**ContactController.cs**文件如果已打开。
7. 将以下代码添加到该文件的命名空间声明部分使用语句。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. 将以下突出显示的代码添加到**ContactController.cs**类添加一个私有字段来表示存储库的实例，以便成员可以产生的类的其余部分使用的服务实现。

    (代码段-*的 Web API 实验-Ex01-联系人控制器*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. 更改**获取**方法，以便它可以使用联系人存储库服务。

    (代码段-*通过存储库返回的联系人列表 Web API 实验-Ex01-*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. 放置一个断点**ContactController**的**获取**方法定义。

   ![将断点添加到联系人控制器](build-restful-apis-with-aspnet-web-api/_static/image17.png "将断点添加到联系人控制器")

   *将断点添加到联系人控制器*
11. 按 **F5** 运行该应用程序。
12. 在浏览器打开后，按**F12**打开开发人员工具。
13. 单击**网络**选项卡。
14. 单击**启动捕获**按钮。
15. 追加后缀的地址栏中的 URL **/api/contact**然后按**Enter**加载 API 控制器。
16. Visual Studio 2012 应中断一次**获取**方法开始执行。

   ![Get 方法中的重大](build-restful-apis-with-aspnet-web-api/_static/image18.png "Get 方法中的重大")

   *Get 方法中的重大*
17. 按 F5 继续。
18. 返回到 Internet Explorer 如果它尚未处于焦点模式。 请注意网络捕获窗口。

    ![网络中显示的 Web API 调用结果的 Internet 资源管理器视图](build-restful-apis-with-aspnet-web-api/_static/image19.png "网络中显示的 Web API 调用结果的 Internet 资源管理器视图")

    *在 Internet Explorer 中显示的 Web API 调用的结果的网络视图*
19. 单击**转到详细视图**按钮。
20. 单击**响应正文**选项卡。请注意 JSON 输出的 API 调用，以及它如何表示两个服务层来检索的联系人。

    ![在开发人员工具窗口中查看 Web API 的 JSON 输出](build-restful-apis-with-aspnet-web-api/_static/image20.png "开发人员工具窗口中查看 Web API 的 JSON 输出")

    *在开发人员工具窗口中查看 Web API 的 JSON 输出*

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a>练习 2： 创建读/写 Web API

在此练习中，将实现 POST 和 PUT 方法的联系人管理器中，若要启用与数据编辑功能。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a>任务 1-打开 Web API 项目

在本任务中，你将准备以增强，以便它可以接受用户输入在练习 1 中创建的 Web API 项目。

1. 运行**Visual Studio 2012 Express for Web**，为此，请转到**启动**并键入**VS Express for Web**然后按**Enter**。
2. 打开**开始**解决方案位于**源/Ex02-ReadWriteWebAPI/开始/** 文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
3. 打开**Services/ContactRepository.cs**文件。

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a>任务 2-将数据暂留功能添加到联系人存储库实现

在此任务中，您将扩展，以便它可以保存并接受用户输入和新联系人实例在练习 1 中创建的 Web API 项目的 ContactRepository 类。

1. 添加到下面的常量**ContactRepository**类来表示 web 服务器缓存项密钥名称的更高版本在此练习中的名称。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. 添加到构造函数**ContactRepository**包含下面的代码。

    (代码段- *Web API 实验-Ex02-联系人存储库构造函数*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. 修改的代码**GetAllContacts**方法如下所示。

    (代码段- *Web API 实验-Ex02-获取所有联系人*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > 此示例用于演示目的，并将使用 web 服务器的缓存作为存储介质，以便这些值将可供多个客户端同时，而不使用会话存储机制或请求存储生存期。 一个可以使用实体框架、 XML 存储或任何其他一种替代 web 服务器缓存。
4. 实现一个名为的新方法**SaveContact**到**ContactRepository**类执行的将联系人保存工作。 **SaveContact**方法应采用单个**联系人**参数和返回一个布尔值，该值指示成功或失败。

    (代码段- *Web API 实验-Ex02-实现 SaveContact 方法*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a>练习 3： 使用从 HTML 客户端 Web API

在此练习中，您将创建 HTML 客户端调用 Web API。 此客户端将使用 Web API 通过 JavaScript 促进数据交换，并将使用 HTML 标记的 web 浏览器中显示的结果。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a>任务 1-修改索引视图用于显示联系人提供 GUI

在本任务中，将修改 web 应用程序以支持在 HTML 浏览器中显示的现有联系人列表的要求的默认索引视图。

1. 打开**Visual Studio 2012 Express for Web**如果已打开。
2. 打开**开始**解决方案位于**源/Ex03-ConsumingWebAPI/开始/** 文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
3. 打开**Index.cshtml**文件位于**Views/Home**文件夹。
4. Div 元素中的 HTML 代码替换 id**正文**，以便它看起来像下面的代码。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. 要执行对 Web API 的 HTTP 请求的文件的底部添加以下 Javascript 代码。

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. 打开**ContactController.cs**文件如果已打开。
7. 上放置一个断点**获取**方法**ContactController**类。

    ![将断点放置在 API 控制器的 Get 方法](build-restful-apis-with-aspnet-web-api/_static/image21.png "将断点放置在 API 控制器的 Get 方法")

    *将断点放置在 API 控制器的 Get 方法*
8. 按**F5**以运行该项目。 在浏览器将加载 HTML 文档。

    > [!NOTE]
    > 请确保您浏览到你的应用程序的根 URL。
9. 在页面加载并执行 JavaScript，将命中断点和执行代码将暂停控制器中。

    ![使用 VS Express for Web 的 Web API 调用到调试](build-restful-apis-with-aspnet-web-api/_static/image22.png "调试到使用 VS Express for Web 的 Web API 调用")

    *使用 Visual Studio 2012 Express for Web 的 Web API 调用调试*
10. 删除该断点并按**F5**或调试工具栏上的**继续**按钮以继续加载在浏览器中的视图。 Web API 调用完成后应会看到从 Web API 返回在浏览器中调用显示为列表项的联系人。

    ![在浏览器中显示为列表项的 API 调用的结果](build-restful-apis-with-aspnet-web-api/_static/image23.png "API 调用在浏览器中显示为列表项的结果")

    *在浏览器中显示为列表项的 API 调用的结果*
11. 停止调试。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a>任务 2-修改索引视图创建联系人提供 GUI

在此任务中，将继续修改索引视图的 MVC 应用程序。 窗体将添加到 HTML 页面，将捕获用户输入并将其发送到 Web API 以创建新的联系人，并将创建新的 Web API 控制器方法以从图形用户界面收集日期。

1. 打开**ContactController.cs**文件。
2. 将新方法添加到名为的控制器类**Post**如下面的代码中所示。

    (代码段- *Web API 实验室-Ex03-Post 方法*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. 打开**Index.cshtml**文件在 Visual Studio 中，如果已打开。
4. 将以下 HTML 代码之后添加上一任务中的未排序列表添加到该文件。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. 在文档底部的脚本元素中，添加以下突出显示的代码以处理按钮单击事件，会将数据发布到 Web API 使用的 HTTP POST 调用。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. 在中**ContactController.cs**上, 放置一个断点**Post**方法。
7. 按**F5**在浏览器中运行应用程序。
8. 页面加载后在浏览器中，键入新的联系人名称和 Id，然后单击**保存**按钮。

    ![在浏览器中加载客户端 HTML 文档](build-restful-apis-with-aspnet-web-api/_static/image24.png "在浏览器中加载客户端 HTML 文档")

    *在浏览器中加载客户端 HTML 文档*
9. 当在调试器窗口的分页符**Post**方法，请查阅的属性**联系**参数。 值应匹配窗体中输入的数据。

    ![从客户端发送到 Web API 的联系人对象](build-restful-apis-with-aspnet-web-api/_static/image25.png "联系人对象从客户端发送到 Web API")

    *正在从客户端发送到 Web API 的联系人对象*
10. 单步执行之前在调试器中的方法**响应**创建变量。 在观察**局部变量**在调试器窗口中的，您将看到已设置的所有属性。

   ![在调试器中的创建之后的响应](build-restful-apis-with-aspnet-web-api/_static/image26.png "在调试器中的创建之后的响应")

   *在调试器中的创建之后响应*
11. 如果按下**F5**或单击**继续**请求将在调试器中完成。 新联系人后切换回浏览器时，已添加到联系人存储的列表**ContactRepository**实现。

   ![在浏览器反映成功创建新的联系人实例](build-restful-apis-with-aspnet-web-api/_static/image27.png "浏览器反映成功创建新的连接实例")

   *在浏览器反映成功创建新的连接实例*

> [!NOTE]
> 此外，您可以此应用程序部署到 Azure 的以下[附录 c： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixC)。


* * *

<a id="Summary"></a>
## <a name="summary"></a>总结

此实验介绍了可以使用新的 ASP.NET Web API 框架和使用框架的 RESTful Web Api 的实现。 在这里，您可以创建新的存储库可帮助数据暂留使用任意数量的机制并连接该服务而不是作为示例，请参见此体验中提供的简单一个。 Web API 支持很多其他功能，例如启用以支持 HTTP 和 JSON 或 XML 的任何语言编写的非 HTML 客户端的通信。 承载 Web API 是典型的 web 应用程序外部的能力也是可能的以及是创建您自己的序列化格式的功能。

ASP.NET 网站上有一个专用于在 ASP.NET Web API 框架的区域[ [ https://asp.net/web-api ](https://asp.net/web-api) ](https://asp.net/web-api)。 此站点将继续提供最新信息、 示例和新闻与 Web API，因此它请经常查看如果你想要深入了解创建可用于几乎任何设备或开发框架自定义 Web Api 的画面。

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>附录 a： 使用代码片段

使用代码段，可以轻松获得相关所需的所有代码。 实验室文档将告诉您完全何时可以使用它们，如下图中所示。

![使用 Visual Studio 代码段代码插入到你的项目](build-restful-apis-with-aspnet-web-api/_static/image28.png "使用 Visual Studio 代码段代码插入到你的项目")

*使用 Visual Studio 代码段代码插入到你的项目*

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a>若要添加代码段使用键盘 (仅限 C#)

1. 将光标置于要插入的代码。
2. 开始键入代码片段名称 （不带空格或连字符）。
3. 观看作为 IntelliSense 显示匹配的代码段的名称。
4. 选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。
5. 按 Tab 键两次，以在光标位置插入代码段。

    ![开始键入代码段名称](build-restful-apis-with-aspnet-web-api/_static/image29.png "开始键入代码段名称")

    *开始键入代码段名称*

    ![按 tab 键以选择突出显示代码段](build-restful-apis-with-aspnet-web-api/_static/image30.png "按选项卡以选择突出显示代码段")

    *按 tab 键以选择突出显示代码段*

    ![再次按 Tab 和代码段将 expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "再次按 Tab 和代码段将扩展")

    *再次按 Tab 和代码段将扩展*

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a>若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）

1. 右键单击你想要插入的代码片段。
2. 选择**插入代码段**跟**我的代码片段**。
3. 通过单击选择列表中中的相关代码片段。

    ![右键单击你想要插入代码段和选择插入代码段](build-restful-apis-with-aspnet-web-api/_static/image32.png "右键单击你想要插入代码段和选择插入代码段")

    *右键单击你想要插入代码段和选择插入代码段*

    ![通过单击选择列表中中的相关代码片段](build-restful-apis-with-aspnet-web-api/_static/image33.png "通过单击选择列表中中的相关代码片段")

    *通过单击选择列表中中的相关代码片段*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>附录 b： 安装 Visual Studio Express 2012 for Web

你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**. 以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。

1. 转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Azure SDK</em>&quot;。
2. 单击**立即安装**。 如果还没有**Web 平台安装程序**将重定向以下载并安装。
3. 一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。

    ![安装 Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，然后单击**我接受**以继续。

    ![接受许可条款](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    *接受许可条款*
5. 等待，直到下载和安装过程完成。

    ![安装进度](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    *安装进度*
6. 安装完成后，单击**完成**。

    ![安装已完成](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    *安装已完成*
7. 单击**退出**以关闭 Web 平台安装程序。
8. 若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。

    ![VS Express for Web 磁贴](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    *VS Express for Web 磁贴*

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附录 c： 发布 ASP.NET MVC 4 应用程序使用 Web 部署

本附录将演示如何从 Azure 门户创建新的网站和发布应用程序获取按照本实验中，利用 Azure 提供的 Web 部署发布功能。

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>任务 1-从 Azure 门户创建新的 Web 站点

1. 转到[Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。

    > [!NOTE]
    > 借助 Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。 你可以注册[此处](http://aka.ms/aspnet-hol-azure)。

    ![登录到 Windows Azure 门户](build-restful-apis-with-aspnet-web-api/_static/image39.png "登录到 Windows Azure 门户")

    *登录到门户*
2. 单击**新建**命令栏上。

    ![创建新的 Web 站点](build-restful-apis-with-aspnet-web-api/_static/image40.png "创建新的 Web 站点")

    *创建新的 Web 站点*
3. 单击**计算** | **网站**。 然后选择**快速创建**选项。 为新网站提供可用的 URL，然后单击**创建网站**。

    > [!NOTE]
    > Azure 是可以控制和管理在云中运行的 web 应用程序的主机。 快速创建选项，可部署到 Azure 门户外部的已完成的 web 应用程序。 它不包括用于设置数据库的步骤。

    ![创建新的网站使用快速创建](build-restful-apis-with-aspnet-web-api/_static/image41.png "创建新的网站使用快速创建")

    *创建新的网站使用快速创建*
4. 等到新**网站**创建。
5. 创建网站后，单击下面的链接**URL**列。 检查新的 Web 站点正常工作。

    ![浏览到新的 web 站点](build-restful-apis-with-aspnet-web-api/_static/image42.png "浏览到新的 web 站点")

    *浏览到新的 web 站点*

    ![正在运行的网站](build-restful-apis-with-aspnet-web-api/_static/image43.png "正在运行的网站")

    *正在运行的网站*
6. 返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。

    ![打开网站管理页](build-restful-apis-with-aspnet-web-api/_static/image44.png "打开网站管理页")

    *打开网站管理页*
7. 在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。

    > [!NOTE]
    > *发布配置文件*包含所有发布到 Azure 的每个启用的发布方法的 web 应用程序所需的信息。 发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。 **Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Azure。

    ![正在下载网站发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image45.png "下载网站发布配置文件")

    *正在下载网站发布配置文件*
8. 下载发布配置文件到已知位置。 进一步在此练习中将了解如何使用此文件发布到 Azure 的 web 应用程序从 Visual Studio。

    ![保存发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image46.png "保存发布配置文件")

    *保存发布配置文件*

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。 如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。

1. 用于存储应用程序数据库，将需要 SQL 数据库服务器。 可以从在 Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**. 如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。 请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。 不创建数据库，因为它将在后面的阶段中创建。

    ![SQL 数据库服务器仪表板](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database 服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。 若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png)按钮。

    ![添加客户端 IP 地址](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    *添加客户端 IP 地址*
3. 一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。

    ![确认更改](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    *确认更改*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布

1. 返回到 ASP.NET MVC 4 解决方案。 在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。

    ![发布应用程序](build-restful-apis-with-aspnet-web-api/_static/image51.png "发布应用程序")

    *发布此网站*
2. 导入发布配置文件保存在第一个任务。

    ![导入发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image52.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击**验证连接**。 验证完成后单击**下一步**。

    > [!NOTE]
    > 请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。

    ![验证连接](build-restful-apis-with-aspnet-web-api/_static/image53.png "验证连接")

    *验证连接*
4. 在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。

    ![Web 部署配置](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web 部署配置")

    *Web 部署配置*
5. 配置数据库连接，如下所示：

   - 在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。
   - 在中**用户名**键入服务器管理员登录名。
   - 在中**密码**键入服务器管理员登录密码。
   - 键入新的数据库名称，例如： *MVC4SampleDB*。

     ![配置目标连接字符串](build-restful-apis-with-aspnet-web-api/_static/image55.png "配置目标连接字符串")

     *配置目标连接字符串*
6. 然后单击“确定” 。 当系统提示你创建数据库时，单击**是**。

    ![创建数据库](build-restful-apis-with-aspnet-web-api/_static/image56.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。 然后，单击 **“下一步”**。

    ![连接字符串指向 SQL 数据库](build-restful-apis-with-aspnet-web-api/_static/image57.png "指向 SQL 数据库连接字符串")

    *连接字符串指向 SQL 数据库*
8. 在中**预览版**页上，单击**发布**。

    ![Web 应用程序发布](build-restful-apis-with-aspnet-web-api/_static/image58.png "发布 web 应用程序")

    *Web 应用程序发布*
9. 在发布过程完成后，在默认浏览器将打开已发布的网站。

    ![应用程序发布到 Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "应用程序发布到 Windows Azure")

    *应用程序发布到 Azure*
