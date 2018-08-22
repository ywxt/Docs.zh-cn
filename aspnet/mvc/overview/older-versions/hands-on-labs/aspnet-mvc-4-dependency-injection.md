---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 依赖关系注入 |Microsoft Docs
author: rick-anderson
description: 注意： 此动手实验假定你具有的 ASP.NET MVC 和 ASP.NET MVC 4 的筛选器的基本知识。 如果您没有使用 ASP.NET MVC 4 筛选器之前，我们建议...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 3f9222c7b485f552da91f4875c882db7e03cdd0a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823546"
---
# <a name="aspnet-mvc-4-dependency-injection"></a>ASP.NET MVC 4 依赖关系注入

通过[Web 训练营团队](https://twitter.com/webcamps)

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

此动手实验假定你已了解的基础知识**ASP.NET MVC**并**ASP.NET MVC 4 筛选**。 如果您未使用过**ASP.NET MVC 4 筛选**之前，我们建议你超出**ASP.NET MVC 自定义操作筛选器**动手实验。

> [!NOTE]
> 在 Web 训练营培训工具包中，在可从包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。 特定于此实验室项目位于[ASP.NET MVC 4 依赖关系注入](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)。

在中**面向对象的编程**范例，对象协同工作的协作模型有 contributors （参与者） 和使用者。 正常情况下，此通信模型生成对象和组件，变得难以管理复杂性的不断提高时之间的依赖关系。

![类的依赖项和模型的复杂性](aspnet-mvc-4-dependency-injection/_static/image1.png "类依赖项和模型的复杂性")

*类依赖项和模型的复杂性*

可能听说**工厂模式**和之间的接口和使用服务，这些客户端对象位于通常负责服务位置的实现分离。

依赖关系注入模式是控制反转的特定实现。 **控制反转 (IoC)** 意味着对象不会创建它们依赖来完成其工作的其他对象。 相反，他们获得所需从外部源 （例如，xml 配置文件） 的对象。

**依赖关系注入 (DI)** 意味着这是通过对象干预，通常将构造函数参数传递的 framework 组件并设置属性。

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a>依赖关系注入 (DI) 设计模式

在高级别中，依赖关系注入的目标是，客户端类 (例如*选手*) 需要满足接口的某些内容 (例如*IClub*)。 它并不关心的具体类型是什么 (例如*WoodClub，IronClub，WedgeClub*或*PutterClub*)，它需要处理的其他人 (例如的合理*托盘*)。 ASP.NET MVC 中的依赖关系解析程序可以让你能够注册到其他位置您依赖关系的逻辑 (例如容器或*俱乐部包*)。

![依赖关系注入关系图](aspnet-mvc-4-dependency-injection/_static/image2.png "依赖关系注入图")

*依赖关系注入-高尔夫类比*

使用依赖关系注入模式和控制反转的优势如下所示：

- 减少了类耦合度
- 提高代码重用
- 改进了代码可维护性
- 改进了应用程序测试

> [!NOTE]
> 依赖关系注入有时与抽象工厂设计模式，但这两种方法之间的细微差异。 DI 具有背后努力解决依赖项通过调用工厂和注册的服务的框架。


现在，你已了解依赖关系注入模式，您将学习在此实验室中如何将其应用在 ASP.NET MVC 4 中。 首先，将使用中的依赖关系注入**控制器**包含数据库访问服务。 接下来，将应用到的依赖关系注入**视图**若要使用的服务，并显示信息。 最后，您将为 ASP.NET MVC 4 筛选器，将注入解决方案中的自定义操作筛选器扩展 DI。

在本动手实验中，你将了解如何：

- 将 ASP.NET MVC 4 与 Unity 集成实现使用 NuGet 包的依赖关系注入
- 使用依赖关系注入在 ASP.NET MVC 控制器
- 使用依赖关系注入在 ASP.NET MVC 视图
- 使用依赖关系注入在 ASP.NET MVC 操作筛选器

> [!NOTE]
> 此实验室使用 Unity.Mvc3 NuGet 包依赖关系解析，但可以调整为使用 ASP.NET MVC 4 的任何依赖关系注入框架。


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

此动手实验包含由以下练习：

1. [练习 1： 将注入控制器](#Exercise1)
2. [练习 2： 将注入视图](#Exercise2)
3. [练习 3： 将注入筛选器](#Exercise3)

> [!NOTE]
> 每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。 如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。


估计的时间才能完成此实验： **30 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a>练习 1： 将注入控制器

在此练习中，您将学习如何在 ASP.NET MVC 控制器中使用依赖关系注入，通过集成 Unity 使用 NuGet 包。 出于此原因，将单独从数据访问的逻辑将 MvcMusicStore 控制器到包括服务。 服务将在控制器构造函数，它将使用依赖关系注入的帮助解决中创建新的依赖项**Unity**。

此方法将演示如何生成不太耦合应用程序，即更灵活、 更易于维护和测试。 您将学习如何将 ASP.NET MVC 与 Unity 集成。

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a>有关 StoreManager 服务

MVC Music 商店现在提供开始解决方案中包括用于管理名为的存储控制器数据的服务**StoreService**。 下面介绍了存储区服务实现。 请注意，所有方法都返回模型的实体。

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

**StoreController**从开始新的解决方案现在消耗**StoreService**。 所有数据引用已都删除从**StoreController**，并修改当前的数据访问接口，而无需更改使用的任何方法现在可以**StoreService**。

将在下面查找**StoreController**实现具有的依赖项**StoreService**在类构造函数。

> [!NOTE]
> 在此练习中引入的依赖项与相关**控制反转**(IoC)。
> 
> **StoreController**类构造函数接收**IStoreService**至关重要，可执行从在类中的服务调用的类型参数。 但是， **StoreController**未实现默认构造函数 （不带任何参数） 的任何控制器必须能够使用 ASP.NET MVC。
> 
> 若要解决依赖关系，控制器必须创建的一个抽象工厂 （返回指定任何的类型对象的类）。


[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> 此类尝试创建 StoreController 而无需发送服务对象，如声明没有无参数构造函数时，将出现错误。


<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a>任务 1-运行应用程序

在本任务中，将运行 Begin 应用程序，包括服务插入应用程序逻辑分离开来数据访问的存储控制器。

运行程序时，你将收到一个异常，为控制器服务不默认情况下通过作为参数：

1. 打开**开始**解决方案位于**Source\Ex01 注入 Controller\Begin**。

   1. 需要先下载某些缺少的 NuGet 包然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 按**Ctrl + F5**不进行调试直接运行该应用程序。 你将收到错误消息&quot;**没有为此对象定义的无参数构造函数**&quot;:

    ![运行 ASP.NET MVC 开始应用程序时出错](aspnet-mvc-4-dependency-injection/_static/image3.png "运行 ASP.NET MVC 开始应用程序时出错")

    *运行 ASP.NET MVC 开始应用程序时出错*
3. 关闭浏览器。

以下步骤中你将适用于音乐应用商店解决方案将注入此控制器所需的依赖关系。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a>任务 2-到 MvcMusicStore 解决方案包括 Unity

在本任务中，将包括**Unity.Mvc3**到解决方案的 NuGet 包。

> [!NOTE]
> Unity.Mvc3 包专为 ASP.NET MVC 3，但与 ASP.NET MVC 4 完全兼容。
> 
> Unity 是轻量级的可扩展依赖关系注入容器并且还可以支持实例和类型拦截。 它是在任何类型的.NET 应用程序中使用的通用容器。 它提供了在依赖项注入机制包括中找到的所有常见功能： 创建对象，通过指定依赖项在运行时和大的灵活性，通过推迟到容器的组件配置要求的抽象。


1. 安装**Unity.Mvc3**中的 NuGet 包**MvcMusicStore**项目。 若要执行此操作，打开**程序包管理器控制台**从**视图** | **其他 Windows**。
2. 运行以下命令。

    PMC

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    ![安装 Unity.Mvc3 NuGet 包](aspnet-mvc-4-dependency-injection/_static/image4.png "安装 Unity.Mvc3 NuGet 包")

    *安装 Unity.Mvc3 NuGet 包*
3. 一次**Unity.Mvc3**安装包，请浏览的文件和文件夹会自动将其添加为了简化 Unity 配置。

    ![已安装的包 Unity.Mvc3](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 包安装")

    *Unity.Mvc3 包安装*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-applicationstart"></a>任务 3-在 Global.asax.cs 应用程序中注册 Unity\_开始

在本任务中，你将更新**应用程序\_启动**方法位于**Global.asax.cs**调用 Unity 引导程序初始值设定项，然后，更新引导程序文件注册服务和将用于依赖关系注入的控制器。

1. 现在，你将将挂接到引导程序是初始化 Unity 容器的文件和依赖关系解析程序。 若要执行此操作，打开**Global.asax.cs**并添加以下突出显示的代码内**应用程序\_启动**方法。

    (代码段- *ASP.NET 依赖关系注入实验-Ex01-初始化 Unity*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. 打开**Bootstrapper.cs**文件。
3. 包括以下命名空间： **MvcMusicStore.Services**并**MusicStore.Controllers**。

    (代码段- *ASP.NET 依赖关系注入实验-Ex01 的引导程序添加命名空间*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. 替换**BuildUnityContainer**方法的内容与注册存储控制器和存储服务的以下代码。

    (代码段- *ASP.NET 依赖关系注入实验-Ex01-注册存储控制器和服务*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在本任务中，将运行应用程序以验证它现在加载包括 Unity 之后。

1. 按**F5**若要运行该应用程序，该应用程序应立即加载而不显示任何错误消息。

    ![运行应用程序依赖关系注入](aspnet-mvc-4-dependency-injection/_static/image6.png "使用依赖关系注入运行应用程序")

    *使用依赖关系注入运行的应用程序*
2. 浏览到 **/存储**。 这会调用**StoreController**，其现已创建使用**Unity**。

    ![MVC Music 商店](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music 商店")

    *MVC Music 商店*
3. 关闭浏览器。

在以下练习中，您将学习如何扩展要在 ASP.NET MVC 视图和操作筛选器内部使用它的依赖关系注入作用域。

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a>练习 2： 将注入视图

在此练习中，您将学习如何使用依赖关系注入在 ASP.NET MVC 4 的新功能视图中为 Unity 集成。 为此，您将调用自定义服务应用商店浏览视图后，它将显示一条消息，如下图中。

然后，将与 Unity 集成项目并创建自定义依赖关系解析程序来注入依赖项。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a>任务 1-创建一个视图，它需要使用的服务

在本任务中，将创建一个视图，它执行服务调用，以生成新的依赖项。 该服务包含在此解决方案中包含的简单消息传送服务。

1. 打开**开始**解决方案位于**Source\Ex02 注入 View\Begin**文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
      > 
      > 有关详细信息，请参阅此文章： [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 包括**MessageService.cs**并**IMessageService.cs**类位于**源 \Assets**中的文件夹 **/服务**。 若要执行此操作，右键单击**Services**文件夹，然后选择**添加现有项**。 浏览到文件的位置，并将其包含。

    ![添加消息服务和服务接口](aspnet-mvc-4-dependency-injection/_static/image8.png "添加消息服务和服务接口")

    *添加消息服务和服务接口*

    > [!NOTE]
    > **IMessageService**接口定义两个属性由实现**MessageService**类。 这些属性-**消息**并**ImageUrl**-存储要显示的消息和图像的 URL。
3. 创建文件夹 **/pages**在项目的根文件夹，以及如何将现有类**MyBasePage.cs**从**Source\Assets**。 基本页将继承具有以下结构。

    ![页面文件夹](aspnet-mvc-4-dependency-injection/_static/image9.png "页面文件夹")

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. 打开**Browse.cshtml**从查看 **/视图/存储**文件夹，并使其继承**MyBasePage.cs**。

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. 在中**浏览**视图中，添加对的调用**MessageService**要显示的映像和服务来检索一条消息。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a>任务 2-包括自定义依赖关系解析程序和自定义视图页激活器

在上一任务中，您注入新的依赖项内执行其内部的服务调用的视图。 现在，将通过实现 ASP.NET MVC 依赖关系注入接口解析该依赖关系**IViewPageActivator**并**IDependencyResolver**。 你将在解决方案中包括的实现**IDependencyResolver** ，将使用 Unity 处理服务检索。 然后，将包括的另一个自定义实现**IViewPageActivator**将解决创建视图的接口。

> [!NOTE]
> 自 ASP.NET MVC 3 依赖关系注入的实现已简化用于注册服务的接口。 **IDependencyResolver**并**IViewPageActivator**依赖关系注入是 ASP.NET MVC 3 功能的一部分。
> 
> **-IDependencyResolver**界面替代了以前 IMvcServiceLocator。 IDependencyResolver 的实施者必须返回服务或服务集合的实例。
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> **-IViewPageActivator**接口提供了更加精细地控制如何通过依赖关系注入实例化视图页。 实现的类**IViewPageActivator**接口可以创建使用上下文信息的视图实例。
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]


1. 创建 /**工厂**项目的根文件夹中的文件夹。
2. 包括**CustomViewPageActivator.cs**到你的解决方案从 **/源/资产/** 到**工厂**文件夹。 为此，请右键单击 **/Factories**文件夹，选择**添加 |现有项**，然后选择**CustomViewPageActivator.cs**。 此类实现**IViewPageActivator**接口来保存 Unity 容器。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > **CustomViewPageActivator**负责管理通过使用 Unity 容器创建一个视图。
3. 包括**UnityDependencyResolver.cs**文件从 **/源/资产**到 **/Factories**文件夹。 为此，请右键单击 **/Factories**文件夹，选择**添加 |现有项**，然后选择**UnityDependencyResolver.cs**文件。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > **UnityDependencyResolver**类是 Unity 自定义 DependencyResolver。 当 Unity 容器中找不到服务时，被 invocated 基冲突解决程序。

在下面的任务将注册这两个实现以便了解服务和视图的位置的模型。

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a>任务 3-Unity 容器中注册的依赖关系注入

在此任务中，会将所有以前的内容在一起以进行工作的依赖关系注入。

到现在为止你的解决方案包含以下元素：

- 一个**浏览**视图继承自**MyBaseClass** ，并使用**MessageService**。
- 中间类-**MyBaseClass**-具有依赖关系注入的服务接口声明。
- 服务-a **MessageService** -及其界面**IMessageService**。
- Unity-自定义依赖关系解析程序**UnityDependencyResolver** -服务检索的处理。
- 视图页激活器- **CustomViewPageActivator** -创建页。

若要将注入**浏览**视图中，现在，您将注册的自定义依赖关系解析程序在 Unity 容器中。

1. 打开**Bootstrapper.cs**文件。
2. 注册的实例**MessageService**到 Unity 容器来初始化该服务：

    (代码段- *ASP.NET 依赖关系注入实验-Ex02-注册消息服务*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. 添加对的引用**MvcMusicStore.Factories**命名空间。

    (代码段- *ASP.NET 依赖关系注入实验-Ex02-工厂 Namespace*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. 注册**CustomViewPageActivator**到 Unity 容器视图页激活器为：

    (代码段- *ASP.NET 依赖关系注入实验-Ex02-注册 CustomViewPageActivator*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. ASP.NET MVC 4 默认依赖关系解析程序替换的实例**UnityDependencyResolver**。 若要执行此操作，请替换**Initialise**方法内容与以下代码：

    (代码段- *ASP.NET 依赖关系注入实验-Ex02-更新依赖关系解析程序*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > ASP.NET MVC 提供了一个默认依赖关系解析程序类。 若要与我们为 unity 创建的一个使用自定义依赖关系解析程序，此解析程序必须被替换。

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在本任务中，你将运行应用程序以验证存储浏览器使用该服务，并显示图像和检索到的消息：

1. 按 **F5** 运行该应用程序。
2. 单击**Rock**内流派菜单，请参阅如何**MessageService**被注入到视图和加载的欢迎消息和映像。 在此示例中，我们进入到&quot; **Rock**&quot;:

    ![MVC Music 商店的视图注入](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music 商店的视图注入")

    *MVC Music 商店的视图注入*
3. 关闭浏览器。

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a>练习 3： 将注入操作筛选器

在先前的动手**自定义操作筛选器**您曾经使用筛选器自定义和注入。 在此练习中，您将学习如何使用 Unity 容器使用依赖关系注入插入筛选器。 为此，将向解决方案中添加音乐应用商店将描摹站点的活动的自定义操作筛选器。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a>任务 1-在解决方案中包括跟踪筛选器

在本任务中，您将包括在音乐应用商店中自定义操作筛选器与跟踪事件。 为自定义操作筛选器的概念已中处理的上一个实验室&quot;自定义操作筛选器&quot;，您将只包括此实验中，从资产文件夹的筛选器类，然后创建用于 Unity 的筛选器提供程序：

1. 打开**开始**解决方案位于**Source\Ex03-注入操作 Filter\Begin**文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
      > 
      > 有关详细信息，请参阅此文章： [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 包括**TraceActionFilter.cs**文件从 **/源/资产**到 **/筛选**文件夹。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > 此自定义操作筛选器执行 ASP.NET 跟踪。 你可以检查&quot;ASP.NET MVC 4 本地和动态操作筛选器&quot;实验室进行更多参考。
3. 添加空的类**FilterProvider.cs**文件夹中的项目到  **/筛选器。**
4. 添加**System.Web.Mvc**并**Microsoft.Practices.Unity**中的命名空间**FilterProvider.cs**。

    (代码段- *ASP.NET 依赖关系注入实验室-Ex03-筛选器提供程序添加命名空间*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. 使类继承自**IFilterProvider**接口。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. 添加**IUnityContainer**属性中的**FilterProvider**类，然后创建一个类构造函数来分配容器。

    (代码段- *ASP.NET 依赖关系注入实验室-Ex03-筛选器提供程序构造函数*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > 不创建筛选器提供程序类构造函数**新**对象内。 作为参数传递容器，并通过 Unity 解决依赖项。
7. 在中**FilterProvider**类中，实现方法**GetFilters**从**IFilterProvider**接口。

    (代码段- *ASP.NET 依赖关系注入实验室-Ex03-筛选器提供程序 GetFilters*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a>任务 2-注册和启用该筛选器

在本任务中，将启用站点跟踪。 为此，请将注册中的筛选器**Bootstrapper.cs BuildUnityContainer**方法以启动跟踪：

1. 打开**Web.config**位于项目根目录和 System.Web 组启用跟踪跟踪。

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. 打开**Bootstrapper.cs**项目根目录。
3. 添加对的引用**MvcMusicStore.Filters**命名空间。

    (代码段- *ASP.NET 依赖关系注入实验室-Ex03 的引导程序添加命名空间*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. 选择**BuildUnityContainer**方法，并注册 Unity 容器中的筛选器。 你将需要注册筛选器提供程序，以及操作筛选器。

    (代码段- *ASP.NET 依赖关系注入实验室-Ex03-注册 FilterProvider 和 ActionFilter*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在此任务中，您将运行该应用程序和测试自定义操作筛选器跟踪活动：

1. 按 **F5** 运行该应用程序。
2. 单击**Rock**流派菜单中。 如果需要，可以浏览到多个流派。

    ![音乐应用商店](aspnet-mvc-4-dependency-injection/_static/image11.png "音乐应用商店")

    *Music 商店*
3. 浏览到 **/Trace.axd**若要查看应用程序跟踪页上，然后依次**查看详细信息**。

    ![应用程序跟踪日志](aspnet-mvc-4-dependency-injection/_static/image12.png "应用程序跟踪日志")

    *应用程序跟踪日志*

    ![应用程序跟踪的请求详细信息](aspnet-mvc-4-dependency-injection/_static/image13.png "跟踪应用程序的请求的详细信息")

    *应用程序跟踪的请求详细信息*
4. 关闭浏览器。

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>总结

通过完成本动手实验介绍了如何在 ASP.NET MVC 4 中使用依赖关系注入，通过集成 Unity 使用 NuGet 包。 若要实现此目的，你已在控制器、 视图和操作筛选器内使用依赖关系注入。

介绍了以下概念：

- ASP.NET MVC 4 依赖关系注入功能
- Unity 集成使用 Unity.Mvc3 NuGet 包
- 控制器中的依赖关系注入
- 在视图中的依赖关系注入
- 操作筛选器的依赖关系注入

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 a： 安装 Visual Studio Express 2012 for Web

你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**. 以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。

1. 转到[ [ https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。
2. 单击**立即安装**。 如果还没有**Web 平台安装程序**将重定向以下载并安装。
3. 一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，然后单击**我接受**以继续。

    ![接受许可条款](aspnet-mvc-4-dependency-injection/_static/image15.png)

    *接受许可条款*
5. 等待，直到下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-dependency-injection/_static/image16.png)

    *安装进度*
6. 安装完成后，单击**完成**。

    ![安装已完成](aspnet-mvc-4-dependency-injection/_static/image17.png)

    *安装已完成*
7. 单击**退出**以关闭 Web 平台安装程序。
8. 若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-dependency-injection/_static/image18.png)

    *VS Express for Web 磁贴*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>附录 b： 使用代码片段

使用代码段，可以轻松获得相关所需的所有代码。 实验室文档将告诉您完全何时可以使用它们，如下图中所示。

![使用 Visual Studio 代码段代码插入到你的项目](aspnet-mvc-4-dependency-injection/_static/image19.png "使用 Visual Studio 代码段代码插入到你的项目")

*使用 Visual Studio 代码段代码插入到你的项目*

***若要添加代码段使用键盘 (仅限 C#)***

1. 将光标置于要插入的代码。
2. 开始键入代码片段名称 （不带空格或连字符）。
3. 观看作为 IntelliSense 显示匹配的代码段的名称。
4. 选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。
5. 按 Tab 键两次，以在光标位置插入代码段。

![开始键入代码段名称](aspnet-mvc-4-dependency-injection/_static/image20.png "开始键入代码段名称")

*开始键入代码段名称*

![按 tab 键以选择突出显示代码段](aspnet-mvc-4-dependency-injection/_static/image21.png "按选项卡以选择突出显示代码段")

*按 tab 键以选择突出显示代码段*

![再次按 Tab 和代码段将 expand](aspnet-mvc-4-dependency-injection/_static/image22.png "再次按 Tab 和代码段将扩展")

*再次按 Tab 和代码段将扩展*

***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。 右键单击你想要插入的代码片段。

1. 选择**插入代码段**跟**我的代码片段**。
2. 通过单击选择列表中中的相关代码片段。

![右键单击你想要插入代码段和选择插入代码段](aspnet-mvc-4-dependency-injection/_static/image23.png "右键单击你想要插入代码段和选择插入代码段")

*右键单击你想要插入代码段和选择插入代码段*

![通过单击选择列表中中的相关代码片段](aspnet-mvc-4-dependency-injection/_static/image24.png "通过单击选择列表中中的相关代码片段")

*通过单击选择列表中中的相关代码片段*
