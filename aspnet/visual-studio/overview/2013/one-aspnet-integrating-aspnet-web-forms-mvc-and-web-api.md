---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 动手实验： One ASP.NET： 集成 ASP.NET Web 窗体、 MVC 和 Web API |Microsoft Docs
author: rick-anderson
description: ASP.NET 是一个用于构建网站、 应用和服务使用专用的技术，如 MVC、 Web API 以及其他框架。 与展开 ASP.NET h...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: b6ac0dca92ab3d75eb871099882dcea549264354
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824643"
---
<a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a>动手实验： One ASP.NET： 集成 ASP.NET Web 窗体、 MVC 和 Web API
====================
通过[Web 训练营团队](https://twitter.com/webcamps)

[下载 Web 训练营培训工具包](http://aka.ms/webcamps-training-kit)

> ASP.NET 是一个用于构建网站、 应用和服务使用专用的技术，如 MVC、 Web API 以及其他框架。 ASP.NET 自创建以来看到与展开并表示需要具有集成这些技术，在向工作已最新的工作**One ASP.NET**。
> 
> Visual Studio 2013 引入了新的统一的项目系统可让您构建的应用程序和一个项目中使用所有的 ASP.NET 技术。 此功能消除了需要的项目并坚持，开始时选择一种技术，而是鼓励使用一个项目中的多个 ASP.NET 框架。
> 
> 在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)。


<a id="Overview"></a>
## <a name="overview"></a>概述

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验，您将学习如何：

- 创建基于网站**One ASP.NET**项目类型
- 使用不同**ASP.NET**框架喜欢**MVC**并**Web API**同一项目中
- 标识的主要组成部分**ASP.NET**应用程序
- 充分利用**ASP.NET 基架**框架自动创建控制器和视图执行 CRUD 操作基于模型类
- 公开一组相同的计算机和可读的格式为每个作业使用合适的工具中的信息

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

完成本动手实验需要以下：

- [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/)或更高版本
- [Visual Studio 2013 Update 1](https://go.microsoft.com/fwlink/?LinkId=301714)

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

1. [创建一个新的 Web 窗体项目](#Exercise1)
2. [创建使用基架 MVC 控制器](#Exercise2)
3. [创建使用基架 Web API 控制器](#Exercise3)

估计的时间才能完成此实验： **60 分钟**

> [!NOTE]
> 在首次启动 Visual Studio，您必须选择一个预定义的设置集合。 每个预定义的集合旨在符合特定的开发风格，并确定窗口布局、 编辑器行为、 IntelliSense 代码段和对话框选项。 此实验中的过程描述了完成给定的任务在 Visual Studio 中使用时所需的操作**常规开发设置**集合。 如果您为您的开发环境选择不同的设置集合，可能会中应考虑到的步骤有所不同。


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a>练习 1： 创建一个新的 Web 窗体项目

在本练习将创建新的 Web 窗体站点中使用 Visual Studio 2013 **One ASP.NET**统一的项目体验，这样就可以轻松地将相同的应用程序中的 Web 窗体、 MVC 和 Web API 组件进行集成。 然后将浏览生成的解决方案，并标识其部件，并最后您会看到操作中的 Web 站点。

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a>任务 1 – 创建新站点使用一个 ASP.NET 体验

在本任务中将开始在 Visual Studio 中创建新的 Web 站点基于**One ASP.NET**项目类型。 **一个 ASP.NET**统一所有 ASP.NET 技术并为您提供混合和匹配它们作为所需的选项。 然后将应用程序中并排显示识别实时 Web 窗体、 MVC 和 Web API 的不同的组件。

1. 打开**Visual Studio Express 2013 for Web** ，然后选择**文件 |新建项目...** 启动一个新的解决方案。

    ![创建新项目](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    *创建新的项目*
2. 在中**新的项目**对话框中，选择**ASP.NET Web 应用程序**下**Visual C# |Web**选项卡，并确保 **.NET Framework 4.5**处于选中状态。 将项目命名*MyHybridSite*，选择**位置**然后单击**确定**。

    ![新的 ASP.NET Web 应用程序项目](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    *创建新的 ASP.NET Web 应用程序项目*
3. 在中**新建 ASP.NET 项目**对话框中，选择**Web 窗体**模板，然后选择**MVC**并**Web API**选项。 此外，请确保**身份验证**选项设置为**单个用户帐户**。 单击“确定”  继续。

    ![使用 Web 窗体模板，其中包括 Web API 和 MVC 组件创建新项目](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    *使用 Web 窗体模板，其中包括 Web API 和 MVC 组件创建新项目*
4. 你现在可以浏览生成的解决方案的结构。

    ![探索生成的解决方案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    *探索生成的解决方案*

    1. **帐户：** 此文件夹包含要注册、 登录和管理应用程序的用户帐户的 Web 窗体页。 此文件夹添加何时**单个用户帐户**在 Web 窗体项目模板的配置过程中选择身份验证选项。
    2. **模型：** 此文件夹将包含表示应用程序数据的类。
    3. **控制器**并**视图**： 这些文件夹所需的**ASP.NET MVC**并**ASP.NET Web API**组件。 您将了解在下一步练习中的 MVC 和 Web API 的技术。
    4. **Default.aspx**， **Contact.aspx**并**About.aspx**文件都可以使用作为起点来生成特定于页面的预定义的 Web 窗体页你应用程序。 这些文件的编程逻辑驻留在单独的文件称为&quot;代码隐藏&quot;文件，其中具有&quot;。 aspx.vb&quot;或&quot;。 aspx.cs&quot;扩展 (具体取决于使用语言）。 代码隐藏逻辑在服务器上运行，并动态地生成您的页面的 HTML 输出。
    5. **Site.Master**并**Site.Mobile.Master**页面在应用程序中定义外观和感觉和所有页面的标准行为。
5. 双击**Default.aspx**文件浏览页的内容。

    ![探索 Default.aspx 页](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    *探索 Default.aspx 页*

    > [!NOTE]
    > **页**指令在文件顶部定义 Web 窗体页的属性。 例如， **MasterPageFile**属性指定到主路径页-在这种情况下， *Site.Master*页-并**Inherits**属性定义页后，可以继承的代码隐藏类。 此类位于由文件中**代码隐藏**属性。
    > 
    > **Asp: Content**控制保存页面 （文本、 标记和控件） 的实际内容和映射到**asp: ContentPlaceHolder**在母版页上的控件。 在这种情况下，将在呈现页内容*MainContent*中定义的控件*Site.Master*页。
6. 展开**应用程序\_启动**文件夹，注意**WebApiConfig.cs**文件。 Visual Studio 中生成的解决方案包括该文件，因为使用 One ASP.NET 模板配置你的项目时包括 Web API。
7. 打开**WebApiConfig.cs**文件。 在中*WebApiConfig*类将查找与配置关联的 Web API，它映射 HTTP 将路由到**Web API 控制器**。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. 打开**RouteConfig.cs**文件。 内部*RegisterRoutes*方法将查找与 MVC 中，它映射到 HTTP 路由关联的配置**MVC 控制器**。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a>任务 2 – 运行解决方案

在此任务将运行生成的解决方案，了解应用程序和它的某些功能，例如 URL 重写和内置身份验证。

1. 若要运行解决方案，按**F5**或单击**启动**按钮位于工具栏上。 该应用程序主页应在浏览器中打开。

    ![运行解决方案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. 验证正在调用的 Web 窗体页。 若要执行此操作，将附加 **/contact.aspx**到的 URL 地址栏，然后按**Enter**。

    ![友好的 Url](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    *友好的 Url*

    > [!NOTE]
    > 正如您所看到的该 URL 将变为 **/联系**。 从开始**ASP.NET 4**，已添加到 Web 窗体的 URL 路由功能，因此，可将 Url 等*[ http://www.mysite.com/products/software ](http://www.mysite.com/products/software)* 而不是 *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*. 有关详细信息，请参阅[URL 路由](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)。
3. 现在，您将了解到应用程序集成的身份验证流。 若要执行此操作，请单击**注册**页面的右上角中。

    ![注册一个新用户](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    *注册一个新用户*
4. 在中**注册**页上，输入**用户名**并**密码**，然后单击**注册**。

    ![注册页](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    *注册页*
5. 应用程序注册新帐户，并对用户身份验证。

    ![用户通过身份验证](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    *用户通过身份验证*
6. 返回到 Visual Studio 并按**SHIFT + F5**以停止调试。

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a>练习 2： 创建使用基架 MVC 控制器

在此练习中将充分利用 Visual Studio 创建 ASP.NET MVC 5 控制器包含操作和 Razor 视图，而无需编写一行代码执行 CRUD 操作，提供的 ASP.NET 基架框架。 基架过程将使用 Entity Framework Code First 在 SQL 数据库中生成的数据上下文和数据库架构。

**关于 Entity Framework 代码优先**

实体框架 (EF) 是一对象关系映射程序 (ORM)，可通过编程使用而不是直接使用关系存储架构编程概念应用程序模型创建数据访问应用程序。

Entity Framework Code First 建模工作流，可使用您自己的域类来表示执行查询时，EF 将依赖于该模型更改跟踪和更新函数。 使用 Code First 开发工作流，你不需要首先创建数据库或指定架构，你的应用程序。 相反，您可以编写定义用于应用程序中，最合适的域模型对象的标准.NET 类，实体框架将为您创建数据库。

> [!NOTE]
> 您可以了解有关实体框架的详细信息[此处](../../../entity-framework.md)。


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a>任务 1 – 创建新模型

现在，你将定义**人员**类，该类将基架过程用于创建 MVC 控制器和视图的模型。 将首先创建**人员**model 类，在控制器中的 CRUD 操作将自动创建和使用基架功能。

1. 打开**Visual Studio Express 2013 for Web**并**MyHybridSite.sln**解决方案位于**源/Ex2-MvcScaffolding/开始**文件夹。 或者，继续使用该解决方案并获得前一练习中。
2. 在中**解决方案资源管理器**，右键单击**模型**文件夹**MyHybridSite**项目，然后选择**添加 |类...**.

    ![添加人员 model 类](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    *添加人员 model 类*
3. 在中**添加新项**对话框中，将文件命名*Person.cs*然后单击**添加**。

    ![创建 Person 模型类](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    *创建 Person 模型类*
4. 替换的内容**Person.cs**用下面的代码文件。 按**CTRL + S**以保存所做的更改。

    (代码段- *BringingTogetherOneAspNet-Ex2-PersonClass*)

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. 在中**解决方案资源管理器**，右键单击**MyHybridSite**项目，然后选择**生成**，或按**CTRL + SHIFT + B**以生成项目。

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a>任务 2 – 创建一个 MVC 控制器

既然**Person**创建模型，将使用与实体框架的 ASP.NET MVC 基架创建的 CRUD 控制器操作和视图**人员**。

1. 在中**解决方案资源管理器**，右键单击**控制器**文件夹**MyHybridSite**项目，然后选择**添加 |新的基架的项...**.

    ![创建新的基架生成的控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    *创建新的基架控制器*
2. 在中**添加基架**对话框中，选择**包含的 MVC 5 控制器视图，使用实体框架**，然后单击**添加。**

    ![选择使用视图和 Entity Framework 的 MVC 5 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    *选择使用视图和 Entity Framework 的 MVC 5 控制器*
3. 设置*MvcPersonController*作为**控制器名称**，选择**使用异步控制器操作**选项，然后选择**人员 (MyHybridSite.Models)** 作为**模型类**。

    ![添加基架 MVC 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    *添加基架 MVC 控制器*
4. 下**数据上下文类**，单击**新建数据上下文...**.

    ![创建新的数据上下文](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    *创建新的数据上下文*
5. 在中**新建数据上下文**对话框中，名称新建数据上下文*PersonContext*然后单击**添加**。

    ![创建新 PersonContext](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    *创建新的 PersonContext 类型*
6. 单击**外**若要创建的新控制器**人员**使用基架。 控制器操作、 Person 数据上下文和 Razor 视图，然后将生成 visual Studio。

    ![之后使用基架创建 MVC 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    *之后使用基架创建 MVC 控制器*
7. 打开**MvcPersonController.cs**中的文件**控制器**文件夹。 请注意，自动生成 CRUD 操作方法。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > 通过选择**使用异步控制器操作**通过基架的复选框选项前面步骤中，Visual Studio 生成涉及到人员的数据上下文的访问的所有操作的异步操作方法。 建议的异步操作方法用于长时间运行、 非 CPU 绑定的请求，以避免阻止 Web 服务器在处理请求时执行工作。

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a>任务 3 – 运行解决方案

在本任务中，你将运行解决方案以验证的视图**人员**按预期方式工作。 将添加新人员若要验证已成功保存到数据库。

1. 按**F5**运行该解决方案。
2. 导航到 **/MvcPerson**。 应显示已搭建基架显示的人员列表的视图。
3. 单击**创建新**以添加新人员。

    ![导航到已搭建基架 MVC 视图](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    *导航到已搭建基架 MVC 视图*
4. 在中**创建**视图中，提供**名称**和一个**年龄**人，然后单击**创建**。

    ![添加新人员](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    *添加新人员*
5. 新用户添加到列表。 在元素列表中，单击**详细信息**以显示人员的详细信息视图。 然后，在**详细信息**视图中，单击**回列表**以返回到列表视图。

    ![人的详细信息视图](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    *人的详细信息视图*
6. 单击**删除**链接以删除用户。 在中**删除**视图中，单击**删除**来确认操作。

    ![删除用户](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    *删除用户*
7. 返回到 Visual Studio 并按**SHIFT + F5**以停止调试。

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a>练习 3： 创建使用基架 Web API 控制器

Web API 框架是 ASP.NET 堆栈的一部分，旨在使实现 HTTP 服务更容易，但通常发送和接收 JSON 或 XML 格式的数据通过 RESTful API。

在此练习中，您将再次使用 ASP.NET 基架生成的 Web API 控制器。 您将使用相同**Person**并**PersonContext**从上一练习，以提供相同的个人数据以 JSON 格式的类。 你将看到相同的 ASP.NET 应用程序中以不同方式，您就可以公开相同的资源。

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a>任务 1 – 创建一个 Web API 控制器

在本任务中会创建一个新**Web API 控制器**，将公开机器能够识别格式应类似于 JSON 中的个人数据。

1. 如果尚未打开，打开**Visual Studio Express 2013 for Web** ，然后打开**MyHybridSite.sln**解决方案位于**源/Ex3-WebAPI/开始**文件夹。 或者，继续使用该解决方案并获得前一练习中。

    > [!NOTE]
    > 如果你将开始从练习 3 开始解决方案，请按**CTRL + SHIFT + B**以生成解决方案。
2. 在中**解决方案资源管理器**，右键单击**控制器**文件夹**MyHybridSite**项目，然后选择**添加 |新的基架的项...**.

    ![创建新的基架生成的控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    *创建新的基架生成的控制器*
3. 在中**添加基架**对话框中，选择**Web API**左窗格中，然后**包含 Web API 2 控制器操作，使用实体框架**在中间窗格中，然后单击**添加。**

    ![选择包含操作和实体框架的 Web API 2 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "选择使用操作和 Entity Framework Web API 2 控制器")

    *选择 Web API 2 控制器包含操作和实体框架*
4. 设置*ApiPersonController*作为**控制器名称**，选择**使用异步控制器操作**选项，然后选择**人员 (MyHybridSite.Models)** 并**PersonContext (MyHybridSite.Models)** 作为**模型**并**数据上下文**分别是类。 然后单击 **“添加”**。

    ![添加 Web API 控制器使用基架](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "添加使用基架 Web API 控制器")

    *添加使用基架 Web API 控制器*
5. 然后，visual Studio 将生成**ApiPersonController**四个的 CRUD 操作，可用于处理数据的类。

    ![之后使用基架创建的 Web API 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "后使用基架创建的 Web API 控制器")

    *之后使用基架创建的 Web API 控制器*
6. 打开**ApiPersonController.cs**文件，并检查*GetPeople*操作方法。 此方法将查询的数据库字段**PersonContext**类型，才能获取数据的人员。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. 请注意，上面的方法定义的注释。 它提供了公开此操作将在下一个任务中使用的 URI。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > 默认情况下，Web API 配置为捕获到的查询 */api*路径，以避免与 MVC 控制器的碰撞。 如果需要更改此设置，请参阅[ASP.NET Web API 中的路由](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)。

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a>任务 2 – 运行解决方案

在此任务将使用 Internet Explorer **F12 开发人员工具**检查来自 Web API 控制器的完整响应。 你将看到如何可以捕获网络流量，以获取更详细地了解应用程序数据。

> [!NOTE]
> 请确保**Internet Explorer**中选择**启动**按钮位于 Visual Studio 工具栏上。
> 
> ![Internet Explorer 选项](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> **F12 开发人员工具**具有众多此动手实验中未涉及的功能。 如果你想要了解有关它的详细信息，请参阅[使用 F12 开发人员工具](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))。


1. 按**F5**运行该解决方案。

    > [!NOTE]
    > 若要正确理解此任务，你的应用程序需要具有的数据。 如果你的数据库为空，可以返回到在练习 2 中的任务 3 和如何创建使用 MVC 视图的新用户在执行的步骤。
2. 在浏览器中，按**F12**以打开**开发人员工具**面板。 按**CTRL** + **4** ，或单击**网络**图标，，然后单击绿色箭头按钮以开始捕获网络流量。

    ![启动 Web API 网络捕获](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "启动 Web API 网络捕获")

    *启动 Web API 网络捕获*
3. 追加**api/ApiPerson**到浏览器地址栏中的 URL。 现在将检查从响应的详细信息**ApiPersonController**。

    ![检索通过 Web API 的个人数据](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "检索通过 Web API 的个人数据")

    *通过 Web API 中检索用户数据*

    > [!NOTE]
    > 下载完成后，系统会提示您提供下载的文件进行操作。 保持对话框的若要观看响应内容通过开发人员工具窗口将打开。
4. 现在将检查响应正文。 若要执行此操作，请单击**详细信息**选项卡，然后单击**响应正文**。 可以检查，下载的数据是具有属性的对象的列表**Id**，**名称**并**年龄**对应于**人员**类。

    ![查看 Web API 响应正文](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "查看 Web API 响应正文")

    *查看 Web API 响应正文*

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a>任务 3 – 添加 Web API 帮助页

在创建 Web API 时，它可用于创建，以便其他开发人员知道如何调用你的 API 帮助页。 您可以创建并文档页手动更新，但最好是自动生成它们可以避免不得不执行维护工作。 在此任务将使用 Nuget 包来自动生成到解决方案的 Web API 帮助页。

1. 从**工具**在 Visual Studio 中，选择菜单**库程序包管理器**，然后单击**程序包管理器控制台**。
2. 在中**程序包管理器控制台**窗口中，执行以下命令：

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > **Microsoft.AspNet.WebApi.HelpPage**包安装必要的程序集并在添加 MVC 视图下的帮助页**领域/HelpPage**文件夹。

    ![HelpPage 区域](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 区域")

    *HelpPage 区域*
3. 默认情况下，帮助页具有占位符字符串的文档。 XML 文档注释可用于创建文档。 若要启用此功能，请打开**HelpPageConfig.cs**文件位于**应用程序的区域/HelpPage\_启动**文件夹，然后取消注释以下行：

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. 在中**解决方案资源管理器**，右键单击该项目**MyHybridSite**，选择**属性**然后单击**生成**选项卡。

    ![生成选项卡](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "生成部分")

    *生成选项卡*
5. 下**输出**，选择**XML 文档文件**。 在编辑框中，键入**应用程序\_Data/XmlDocument.xml**。

    ![输出中生成选项卡的部分](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "输出中生成选项卡的部分")

    *生成选项卡中的输出部分*
6. 按**CTRL** + **S**以保存所做的更改。
7. 打开**ApiPersonController.cs**文件从**控制器**文件夹。
8. 输入新的一行之间*GetPeople*方法签名并 */ / 获取 api/ApiPerson*注释，，然后键入三个正斜杠。

    > [!NOTE]
    > Visual Studio 会自动插入的 XML 元素定义方法文档。
9. 添加摘要文本和返回值*GetPeople*方法。 它应如以下所示。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. 按**F5**运行该解决方案。
11. 追加 **/help**到地址栏中的 URL 浏览到帮助页。

    ![ASP.NET Web API 帮助页](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API 帮助页")

    *ASP.NET Web API 帮助页*

    > [!NOTE]
    > 页面的主要内容是 Api，由控制器进行分组的表。 表项动态生成的使用**IApiExplorer**接口。 如果添加或更新的 API 控制器时，表将自动更新下一次生成应用程序。
    > 
    > **API**列列出了 HTTP 方法和相对 URI。 **说明**列包含已从该方法的文档中提取的信息。
12. 请注意，在说明列中显示您在前面的方法定义添加的说明。

    ![API 方法描述](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API 方法说明")

    *API 方法说明*
13. 单击其中一个 API 方法来导航到包含更多详细信息，包括示例响应正文的页面。

    ![详细信息页](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "详细信息页")

    *详细的信息页*

* * *

<a id="Summary"></a>
## <a name="summary"></a>总结

通过完成本动手实验介绍了如何：

- 创建 Visual Studio 2013 中使用一个 ASP.NET 体验的新 Web 应用程序
- 将多个 ASP.NET 技术集成到一个单个项目
- 从使用 ASP.NET 基架在模型类生成 MVC 控制器和视图
- 生成 Web API 控制器，使用异步编程和通过 Entity Framework 数据访问等功能
- 为你的控制器中自动生成 Web API 帮助页
