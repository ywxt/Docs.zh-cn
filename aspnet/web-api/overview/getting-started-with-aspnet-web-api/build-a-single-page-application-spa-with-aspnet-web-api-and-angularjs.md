---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: 动手实验： 生成使用 ASP.NET Web API 和 Angular.js 的单页面应用程序 (SPA) |Microsoft Docs
author: rick-anderson
description: 在传统 web 应用程序，客户端 （浏览器） 可以启动与服务器之间的通信请求页面。 然后，在服务器处理请求...
ms.author: aspnetcontent
ms.date: 09/30/2015
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 8e9cc082d982aec0a4385a3cefecd118c937e641
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811515"
---
<a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a>动手实验： 生成使用 ASP.NET Web API 和 Angular.js 的单页面应用程序 (SPA)
====================
通过[Web 训练营团队](https://twitter.com/webcamps)

[下载 Web 训练营培训工具包](http://aka.ms/webcamps-training-kit)

> 在传统 web 应用程序，客户端 （浏览器） 可以启动与服务器之间的通信请求页面。 然后，在服务器处理请求，并将页面的 HTML 发送到客户端。 在后续页面 （例如用户导航到链接或提交的数据窗体） 交互的新请求发送到服务器，并且流将重新启动： 在服务器处理请求并将新页面发送到浏览器以响应新的操作请求ed 由客户端。
> 
> 在单页面应用程序 (Spa) 中整个页面已加载，在浏览器中后的初始请求，但通过 Ajax 请求发生后续交互。 这意味着浏览器具有更新仅已更改; 的页的一部分没有无需重新加载整个页面。 SPA 方法降低了应用程序以响应用户操作，从而导致更多的流畅体验所花费的时间。
> 
> SPA 的体系结构涉及传统 web 应用程序中不存在一些难题。 但是，新兴技术，如 ASP.NET Web API，JavaScript 框架类似 AngularJS 和 CSS3 提供的新样式功能使其十分轻松地设计和构建 Spa。
> 
> 在本动手实验，您将利用这些技术，以实现极客测验，基于 SPA 概念的琐碎内容网站。 首先将实现使用 ASP.NET Web API 公开所需的终结点检索测验问题并将存储答案的服务层。 然后，你将构建丰富且高度可响应用户界面使用 AngularJS 和 CSS3 转换效果。
> 
> 在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)。


## <a name="overview"></a>概述

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验，您将学习如何：

- 创建 ASP.NET Web API 服务，以发送和接收 JSON 数据
- 创建响应式 UI 使用 AngularJS
- 增强 CSS3 转换的 UI 体验

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

完成本动手实验需要以下：

- [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/)或更高版本

<a id="Setup"></a>
### <a name="setup"></a>安装

若要运行本动手实验中练习，需要先设置你的环境。

1. 打开 Windows 资源管理器并浏览到实验室**源**文件夹。
2. 右键单击**Setup.cmd** ，然后选择**以管理员身份运行**以启动将配置你的环境并安装本实验的 Visual Studio 代码段的安装过程。
3. 如果显示用户帐户控制对话框中，确认要继续执行的操作。

> [!NOTE]
> 请确保您运行安装程序之前已为此实验室的所有依赖项。


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>使用代码片段

在整个实验文档中，将指示您插入代码块。 为方便起见，此代码的大部分以 Visual Studio 代码段，可以在 Visual Studio 2013，为了避免必须手动添加访问从形式提供。

> [!NOTE]
> 每个练习均附带位于中的开始解决方案**开始**本练习，您可以按照独立于其他每个练习的文件夹。 请注意在练习期间添加的代码片段缺少这些开始解决方案中，并且可能无法工作，直到完成该练习。 在练习的源代码，您将发现**最终**包含具有无法完成相应练习中的步骤得到的代码的 Visual Studio 解决方案文件夹。 如果您在演练本动手实验需要更多帮助，可以使用这些解决方案作为指南。


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [创建 Web API](#Exercise1)
2. [创建 SPA 接口](#Exercise2)

估计的时间才能完成此实验： **60 分钟**

> [!NOTE]
> 在首次启动 Visual Studio，您必须选择一个预定义的设置集合。 每个预定义的集合旨在符合特定的开发风格，并确定窗口布局、 编辑器行为、 IntelliSense 代码段和对话框选项。 此实验中的过程描述了完成给定的任务在 Visual Studio 中使用时所需的操作**常规开发设置**集合。 如果您为您的开发环境选择不同的设置集合，可能会中应考虑到的步骤有所不同。


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a>练习 1： 创建 Web API

SPA 的关键部分之一是服务层。 它负责处理的 UI 和返回数据，以响应该调用发送的 Ajax 调用。 为了进行分析和使用的客户端计算机可读格式显示检索到的数据。

Web API 框架是 ASP.NET 堆栈的一部分，旨在更轻松地实现 HTTP 服务，通常发送和接收 JSON 或 XML 格式的数据通过 RESTful API。 在此练习中将创建 Web 站点以托管极客测验应用程序，然后实现后端服务公开和使用 ASP.NET Web API 将测验数据暂留。

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a>任务 1 – 创建初始项目适用于极客测验

在此任务将启动 ASP.NET Web API 基于为支持创建新的 ASP.NET MVC 项目**One ASP.NET**项目附带了 Visual Studio 的类型。 **一个 ASP.NET**统一所有 ASP.NET 技术并为您提供混合和匹配它们作为所需的选项。 然后，您将添加实体框架模型的类和数据库 initializator 插入测验问题。

1. 打开**Visual Studio Express 2013 for Web** ，然后选择**文件 |新建项目...** 启动一个新的解决方案。

    ![创建新的项目](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "创建新的项目")

    *创建新的项目*
2. 在中**新的项目**对话框中，选择**ASP.NET Web 应用程序**下**Visual C# |Web**选项卡。请确保 **.NET Framework 4.5**是所选，其命名*GeekQuiz*，选择**位置**然后单击**确定**。

    ![创建新的 ASP.NET Web 应用程序项目](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "创建新的 ASP.NET Web 应用程序项目")

    *创建新的 ASP.NET Web 应用程序项目*
3. 在中**新建 ASP.NET 项目**对话框中，选择**MVC**模板，然后选择**Web API**选项。 此外，请确保**身份验证**选项设置为**单个用户帐户**。 单击“确定”  继续。

    ![使用 MVC 模板，其中包括 Web API 组件创建新项目](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    *使用 MVC 模板，其中包括 Web API 组件创建新项目*
4. 在中**解决方案资源管理器**，右键单击**模型**文件夹**GeekQuiz**项目，然后选择**添加 |现有项...**.

    ![添加现有项目](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "添加现有项目")

    *添加现有项目*
5. 在中**添加现有项**对话框框中，导航到**源/资产/模型**文件夹，然后选择所有文件。 单击 **添加**。

    ![添加模型资产](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "添加模型资产")

    *添加模型资产*

    > [!NOTE]
    > 通过添加这些文件，将添加数据模型、 实体框架数据库上下文和极客测验应用程序的数据库初始值设定项。
    > 
    > **实体框架 (EF)** 是对象关系映射器 (ORM)，可用于创建使用而不是直接使用关系存储架构编程的概念应用程序模型编程数据访问应用程序。 您可以了解有关实体框架的详细信息[此处](../../../entity-framework.md)。
    > 
    > 下面是刚添加的类的说明：
    > 
    > - **TriviaOption:** 表示测验问题与关联的单个选项
    > - **TriviaQuestion:** 表示测验问题，并公开通过关联的选项**选项**属性
    > - **TriviaAnswer:** 表示测验问题响应用户选择的选项
    > - **TriviaContext:** 表示极客测验应用程序的实体框架数据库上下文。 此类派生自**DContext** ，并公开**DbSet**表示上面所述的实体集合的属性。
    > - **TriviaDatabaseInitializer:** 的实体框架初始值设定项的实现**TriviaContext**类，该类继承自**CreateDatabaseIfNotExists**。 此类的默认行为是创建数据库，仅当不存在，在插入实体指定**种子**方法。
6. 打开**Global.asax.cs**文件，并添加以下 using 语句。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. 在开头添加以下代码**应用程序\_启动**方法以设置**TriviaDatabaseInitializer**作为数据库初始值设定项。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. 修改**主页**控制器，以限制对访问进行身份验证的用户。 若要执行此操作，打开**HomeController.cs**文件内**控制器**文件夹，并添加**Authorize**归于**HomeController**类定义。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > **Authorize**筛选检查以确定用户进行身份验证。 如果用户未经过身份验证，则将返回 HTTP 状态代码 401 （未经授权），而无需调用该操作。 您可以应用筛选器全局范围内，在控制器级别，或在单个操作级别。
9. 现在，您将自定义 web 页和品牌的布局。 若要执行此操作，打开 **\_Layout.cshtml**文件内**视图 |共享**文件夹和更新的内容**&lt;标题&gt;** 通过替换元素*My ASP.NET Application*与*极客测验*.

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. 在同一文件中，通过删除更新的导航栏*有关*并*联系人*链接和重命名*主页*链接到*播放*。 此外，重命名*应用程序名称*链接到*极客测验*。 导航栏的 HTML 应如以下代码所示。

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. 通过替换来更新布局页的页脚*My ASP.NET Application*与*极客测验*。 若要执行此操作，请替换的内容**&lt;页脚&gt;** 具有以下突出显示的代码元素。

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a>任务 2 – 创建 TriviaController Web API

在上一任务中，创建极客测验 web 应用程序的初始结构。 现在，你将生成一个简单的 Web API 服务，它与测验数据模型进行交互并公开以下操作：

- **GET/api/琐碎内容**： 从要经过身份验证的用户可解答的测验列表中检索下一个问题。
- **POST/api/琐碎内容**： 存储测验答案已经过身份验证的用户指定的。

将使用 Visual Studio 提供的 ASP.NET 基架工具来创建 Web API 控制器类的基线。

1. 打开**WebApiConfig.cs**文件内**应用\_启动**文件夹。 此文件定义 Web API 服务，如路由映射到 Web API 控制器操作的方式的配置。
2. 添加以下 using 语句的文件的开头。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. 将以下突出显示的代码添加到**注册**全局配置用于 Web API 操作方法来检索 JSON 数据的格式化程序的方法。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > **CamelCasePropertyNamesContractResolver**会自动将转换到的属性名称*camel*情况，这就是 JavaScript 中的属性名称的常规约定。
4. 在中**解决方案资源管理器**，右键单击**控制器**文件夹**GeekQuiz**项目，然后选择**添加 |新的基架的项...**.

    ![创建新的基架的项](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "创建新的基架的项")

    *创建新的基架的项*
5. 在中**添加基架**对话框框中，请确保**常见**的左窗格中选择节点。 然后，选择**Web API 2 控制器-空**在中心窗格中单击模板**添加**。

    ![选择 Web API 2 控制器空模板](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "选择 Web API 2 控制器空模板")

    *选择 Web API 2 控制器空模板*

    > [!NOTE]
    > **ASP.NET 基架**是用于 ASP.NET Web 应用程序的代码生成框架。 Visual Studio 2013 包括 MVC 和 Web API 项目的预安装的代码生成器。 当你想要快速添加开发标准的数据操作所需的代码，以减少时间量与数据模型进行交互时，应在项目中使用基架。
    > 
    > 基架过程还可确保在项目中安装了所有必需的依赖项。 例如，如果您开始创建空的 ASP.NET 项目，然后使用基架添加 Web API 控制器，所需的 Web API NuGet 包和引用将自动添加到你的项目。
6. 在中**添加控制器**对话框中，键入*TriviaController*中**控制器名称**文本框中，然后单击**添加**。

    ![添加琐碎内容控制器](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "添加琐碎内容控制器")

    *添加琐碎内容控制器*
7. **TriviaController.cs**随后将文件添加到**控制器**文件夹**GeekQuiz**包含一个空项目**TriviaController**类。 添加以下 using 语句的文件的开头。

    (代码段- *AspNetWebApiSpa-Ex1-TriviaControllerUsings*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. 在开头添加以下代码**TriviaController**类来定义、 初始化和释放**TriviaContext**控制器中的实例。

    (代码段- *AspNetWebApiSpa-Ex1-TriviaControllerContext*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > **Dispose**方法**TriviaController**调用**释放**方法**TriviaContext**实例，它可确保所有释放上下文对象所使用的资源时**TriviaContext**实例已释放或垃圾回收。 这包括关闭所有打开的实体框架的数据库连接。
9. 在末尾添加以下帮助器方法**TriviaController**类。 此方法检索从数据库指定的用户必须回答以下测验问题。

    (代码段- *AspNetWebApiSpa-Ex1-TriviaControllerNextQuestion*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. 添加以下**获取**到操作方法**TriviaController**类。 此操作方法调用**NextQuestionAsync**检索下一个问题以经过身份验证的用户在上一步中定义的帮助器方法。

    (代码段- *AspNetWebApiSpa-Ex1-TriviaControllerGetAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. 在末尾添加以下帮助器方法**TriviaController**类。 此方法在数据库中存储指定的应答，并返回一个布尔值，该值指示这个答案正确。

    (代码段- *AspNetWebApiSpa-Ex1-TriviaControllerStoreAsync*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. 添加以下**Post**到操作方法**TriviaController**类。 此操作方法将相关联的身份验证的用户和调用的答案**StoreAsync**帮助器方法。 然后，它将响应发送由帮助器方法返回的布尔值。

    (代码段- *AspNetWebApiSpa-Ex1-TriviaControllerPostAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. 修改要添加将访问限于经过身份验证的用户的 Web API 控制器**Authorize**归于**TriviaController**类定义。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>任务 3 – 运行解决方案

在此任务将验证在上一任务中生成的 Web API 服务按预期工作。 将使用 Internet Explorer **F12 开发人员工具**捕获网络流量，以查看来自 Web API 服务的完整响应。

> [!NOTE]
> 请确保**Internet Explorer**中选择**启动**按钮位于 Visual Studio 工具栏上。
> 
> ![Internet Explorer 选项](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)


1. 按**F5**运行该解决方案。 **登录**页应显示在浏览器中。

    > [!NOTE]
    > 应用程序启动时，触发默认 MVC 路由，默认情况下映射到**索引**的操作**HomeController**类。 由于**HomeController**仅限于经过身份验证的用户 (请记住，修饰该类与**Authorize**练习 1 中的属性)，并且没有任何用户通过身份验证但应用程序原始请求重定向到登录页。

    ![运行解决方案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "运行解决方案")

    *运行解决方案*
2. 单击**注册**来创建新用户。

    ![注册一个新用户](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "注册一个新用户")

    *注册一个新用户*
3. 在中**注册**页上，输入**用户名**并**密码**，然后单击**注册**。

    ![注册页](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "注册页")

    *注册页*
4. 应用程序注册新帐户和用户进行身份验证和重定向回主页。

    ![用户进行身份验证](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "用户通过身份验证")

    *用户进行身份验证*
5. 在浏览器中，按**F12**以打开**开发人员工具**面板。 按**CTRL + 4**或单击**网络**图标，，然后单击绿色箭头按钮以开始捕获网络流量。

    ![启动 Web API 网络捕获](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "启动 Web API 网络捕获")

    *启动 Web API 网络捕获*
6. 追加**api/琐碎内容**到浏览器地址栏中的 URL。 现在将检查从响应的详细信息**获取**中的操作方法**TriviaController**。

    ![检索下一步的问题数据通过 Web API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "检索下一步的问题数据通过 Web API")

    *检索下一步的问题数据通过 Web API*

    > [!NOTE]
    > 下载完成后，系统会提示您提供下载的文件进行操作。 保持对话框的若要观看响应内容通过开发人员工具窗口将打开。
7. 现在将检查响应正文。 若要执行此操作，请单击**详细信息**选项卡，然后单击**响应正文**。 您可以检查下载的数据是具有属性的对象**选项**(这是一系列**TriviaOption**对象)， **id**和**标题**对应于**TriviaQuestion**类。

    ![查看 Web API 响应正文](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "查看 Web API 响应正文")

    *查看 Web API 响应正文*
8. 返回到 Visual Studio 并按**SHIFT + F5**以停止调试。

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a>练习 2： 创建 SPA 接口

在此练习中您将首先生成的极客测验，web 前端部分将重点放在单页面应用程序交互使用**AngularJS**。 然后将增强 CSS3 执行丰富的动画，并提供可视化效果的上下文切换到下一个问题从转换时的用户体验。

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a>任务 1 – 创建使用 AngularJS SPA 接口

在此任务将使用**AngularJS**实现极客测验应用程序的客户端。 **AngularJS**是一种开放源代码 JavaScript 框架，增加与基于浏览器的应用程序的内容*模型-视图-控制器*(MVC) 功能，促进这两个开发和测试。

首先，将通过从 Visual Studio 包管理器控制台安装 AngularJS。 然后，将创建控制器以提供极客测验应用和要呈现的测验问题和解答使用 AngularJS 模板引擎的视图的行为。

> [!NOTE]
> 有关 AngularJS 的详细信息，请参阅[ [ http://angularjs.org/ ](http://angularjs.org/) ](http://angularjs.org/)。


1. 打开**Visual Studio Express 2013 for Web** ，然后打开**GeekQuiz.sln**解决方案位于**源/Ex2-CreatingASPAInterface/开始**文件夹。 或者，继续使用该解决方案并获得前一练习中。
2. 打开**程序包管理器控制台**从**工具** | **库程序包管理器**。 键入以下命令以安装**AngularJS.Core** NuGet 包。

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. 在中**解决方案资源管理器**，右键单击**脚本**文件夹**GeekQuiz**项目，然后选择**添加 |新文件夹**。 将文件夹命名为**应用程序**然后按**Enter**。
4. 右键单击**应用程序**文件夹，只需创建并选择**添加 |JavaScript 文件**。

    ![创建新的 JavaScript 文件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    *创建新的 JavaScript 文件*
5. 在中**指定项名称**对话框中，键入*测验控制器*中**项名称**文本框中，然后单击**确定**。

    ![命名新的 JavaScript 文件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    *命名新的 JavaScript 文件*
6. 在中**测验 controller.js**文件中，添加以下代码以声明和初始化 AngularJS **QuizCtrl**控制器。

    (代码段- *AspNetWebApiSpa-Ex2-AngularQuizController*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > 构造函数**QuizCtrl**控制器需要一个名为注射参数 **$scope**。 作用域的初始状态应设置在构造函数通过将附加到的属性 **$scope**对象。 属性包含**视图模型**，并且控制器注册时将可访问的模板。
    > 
    > **QuizCtrl**控制器定义一个名为模块内**QuizApp**。 模块是工作的让您单位将应用程序分解为单独的组件。 使用模块的主要优势是代码更易于理解，便于进行单元测试、 可重用性和可维护性。
7. 若要从视图触发的事件做出反应，现在会将行为添加到作用域。 在末尾添加以下代码**QuizCtrl**控制器定义**nextQuestion**函数，在 **$scope**对象。

    (代码段- *AspNetWebApiSpa-Ex2-AngularQuizControllerNextQuestion*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > 此函数可检索从下一个问题**琐碎内容**Web API 在上一练习中创建并附加到的问题数据 **$scope**对象。
8. 在末尾插入以下代码**QuizCtrl**控制器定义**sendAnswer**函数，在 **$scope**对象。

    (代码段- *AspNetWebApiSpa-Ex2-AngularQuizControllerSendAnswer*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > 此函数将发送到用户所选的答案**琐碎内容**Web API，并将存储中的结果-即如果答案不正确，或未 – **$scope**对象。
    > 
    > **NextQuestion**并**sendAnswer**上面提供的函数使用 AngularJS **$http**对象进行抽象与 Web API 通过 XMLHttpRequest 的通信从浏览器的 JavaScript 对象。 AngularJS 支持带来了更高级别的抽象执行 CRUD 操作对通过 RESTful Api 的资源的另一个服务。 AngularJS **$resource**对象提供操作方法提供高级的行为，而无需与交互 **$http**对象。 请考虑使用 **$resource**方案 CRUD 模型所需的对象 (fore 信息，请参阅[$resource 文档](https://docs.angularjs.org/api/ngResource/service/$resource))。
9. 下一步是创建定义测验的视图的 AngularJS 模板。 若要执行此操作，打开**Index.cshtml**文件内**视图 |主页**文件夹并将替换为以下代码的内容。

    (代码段- *AspNetWebApiSpa-Ex2-GeekQuizView*)

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > AngularJS 模板是使用来自该模型和控制器的信息将转换为该用户将看到在浏览器中的动态视图的静态标记的声明性规范。 AngularJS 元素和元素属性，可在模板中的示例如下：
    > 
    > - **Ng 应用**指令指示 AngularJS 表示应用程序的根元素的 DOM 元素。
    > - **Ng 控制器**指令将一个控制器附加到 DOM 中声明该指令的位置的点处。
    > - 大括号表示法 **{{}}** 表示到控制器中定义的作用域属性的绑定。
    > - **Ng 单击**指令用于调用以响应用户单击作用域中定义的函数。
10. 打开**Site.css**文件内**内容**文件夹并在要提供的测验视图的外观和感觉的文件的末尾添加以下突出显示的样式。

    (代码段- *AspNetWebApiSpa-Ex2-GeekQuizStyles*)

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a>任务 2 – 运行解决方案

将执行此任务中使用新用户的解决方案的接口您使用 AngularJS 来回答一些测验问题生成。

1. 按**F5**运行该解决方案。
2. 注册新的用户帐户。 若要执行此操作，请在练习 1 中，任务 3 中所述的注册步骤。

    > [!NOTE]
    > 如果使用从上一练习解决方案，可以登录之前创建的用户帐户。
3. **主页**页应显示，其中显示测验的第一个问题。 通过单击某个选项来回答此问题。 这会触发**sendAnswer**之前，定义的函数，它将发送到所选的选项**琐碎内容**Web API。

    ![回答问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "回答问题")

    *回答问题*
4. 单击其中一个按钮后, 应显示答案。 单击**的下一个问题**显示下面的问题。 这会触发**nextQuestion**控制器中定义的函数。

    ![请求下一个问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "请求下一个问题")

    *请求下一个问题*
5. 应显示下一个问题。 继续根据需要多次回答的问题。 完成所有问题后，您应返回到第一个问题。

    ![另一个问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "另一个问题")

    *下一个问题*
6. 返回到 Visual Studio 并按**SHIFT + F5**以停止调试。

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a>任务 3 – 创建一个使用 CSS3 的翻转动画

在此任务将使用 CSS3 属性通过添加一个翻转效果时找到相关问题和检索下一个问题时执行丰富的动画。

1. 在中**解决方案资源管理器**，右键单击**内容**文件夹**GeekQuiz**项目，然后选择**添加 |现有项...**.

    ![将现有项添加到内容文件夹](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "的 Content 文件夹添加现有项目")

    *将现有项添加到内容的文件夹*
2. 在中**添加现有项**对话框框中，导航到**源/资产**文件夹，然后选择**Flip.css**。 单击 **添加**。

    ![从资产添加 Flip.css 文件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "从资产添加 Flip.css 文件")

    *从资产添加 Flip.css 文件*
3. 打开**Flip.css**文件您刚刚添加并查看其内容。
4. 找到**翻转转换**注释。 下面的注释样式使用 CSS**角度来看**和**rotateY**的转换，以生成&quot;卡翻转&quot;效果。

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. 找到**翻转期间隐藏窗格的背面**注释。 下面的注释样式隐藏的人脸在后端时它们通过设置面向向后翻转**隐面可见性**CSS 属性设置为*隐藏*。

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. 打开**BundleConfig.cs**文件内**应用\_启动**文件夹并添加对引用**Flip.css**文件**&quot;~/Content/css&quot;** 样式捆绑包

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. 按**F5**运行解决方案并使用你的凭据登录。
8. 通过单击某个选项来回答问题。 视图之间转换时，请注意翻转效果。

    ![回答问题具有翻转效果](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "回答问题具有翻转效果")

    *回答问题具有翻转效果*
9. 单击**的下一个问题**检索以下问题。 翻转效果应会再次出现。

    ![检索具有翻转效果的以下问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "检索翻转效果与下面的问题")

    *检索具有翻转效果下面的问题*

* * *

<a id="Summary"></a>
## <a name="summary"></a>总结

通过完成本动手实验介绍了如何：

- 创建 ASP.NET Web API 控制器使用 ASP.NET 基架
- 实现用于检索下一个测验问题的 Web API 获取操作
- 实现 Web API 后操作来存储测验答案
- 从 Visual Studio 包管理器控制台安装 AngularJS
- 实现 AngularJS 模板和控制器
- 使用 CSS3 过渡执行动画效果
