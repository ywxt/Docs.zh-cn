---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 自定义操作筛选器 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 提供了用于执行筛选逻辑之前或之后调用操作方法的操作筛选器。 操作筛选器是自定义特性 tha...
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: c435fef624d526ceb01dbc370c5df52e2a1e8350
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807930"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a>ASP.NET MVC 4 自定义操作筛选器

通过[Web 训练营团队](https://twitter.com/webcamps)

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 提供了用于执行筛选逻辑之前或之后调用操作方法的操作筛选器。 操作筛选器是提供声明性方法将操作前和操作后行为添加到控制器的操作方法的自定义属性。

在本动手实验将到 MvcMusicStore 解决方案来捕获控制器的请求并记录到数据库表的站点的活动创建自定义操作筛选器属性。 你将能够通过注入的日志记录筛选器添加到任何控制器或操作。 最后，您将看到显示的访问者的列表在日志视图。

此动手实验假定你已了解的基础知识**ASP.NET MVC**。 如果您未使用过**ASP.NET MVC**之前，我们建议你超出**ASP.NET MVC 4 基础知识**动手实验。

> [!NOTE]
> 在 Web 训练营培训工具包中，在可从包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。 特定于此实验室项目位于[ASP.NET MVC 4 自定义操作筛选器](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)。

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，你将了解如何：

- 创建要扩展的筛选功能的自定义操作筛选器属性
- 通过为特定级别的注入应用自定义筛选器属性
- 全局注册自定义操作筛选器

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

如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 c： 使用代码片段](#AppendixC)&quot;。

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

此动手实验包含由以下练习：

1. [练习 1： 日志记录操作](#Exercise1)
2. [练习 2： 管理多个操作筛选器](#Exercise2)

估计的时间才能完成此实验： **30 分钟**。

> [!NOTE]
> 每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。 如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。


<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a>练习 1： 日志记录操作

在此练习中，您将学习如何使用 ASP.NET MVC 4 筛选器提供程序创建自定义操作日志筛选器。 为此您将应用于 MusicStore 站点，以将所选的控制器中记录所有活动日志记录筛选器。

将筛选器，从而扩大**ActionFilterAttributeClass**并重写**OnActionExecuting**方法来捕获每个请求，然后执行日志记录操作。 有关 HTTP 请求的上下文信息，执行方法、 结果和参数将由 ASP.NET MVC 提供**ActionExecutingContext**类 **。**

> [!NOTE]
> ASP.NET MVC 4 也有默认筛选器提供程序可以使用而无需创建自定义筛选器。 ASP.NET MVC 4 提供了以下类型的筛选器：
> 
> - **授权**筛选，从而安全决定是否要执行的操作方法，如执行身份验证或验证请求的属性。
> - **操作**筛选器，用于包装操作方法执行。 此筛选器可以执行其他处理，如提供给操作方法的额外数据、 检查返回值，或取消执行的操作方法
> - **结果**筛选器，用于包装的 ActionResult 对象执行。 此筛选器可以执行其他处理的结果，如修改 HTTP 响应。
> - **异常**筛选器，如果没有在操作方法中，使用授权筛选器开始和结束与结果执行的某个位置引发未处理的异常，则执行。 异常筛选器可用于任务，例如日志记录或显示错误页。
> 
> 有关筛选器提供程序的详细信息，请访问此 MSDN 链接: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx))。


<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a>有关 MVC 音乐应用商店应用程序日志记录功能

此音乐应用商店解决方案具有站点日志记录的新数据模型表**ActionLog**，包含以下字段： 接收请求，调用操作、 客户端 IP 和时间戳的控制器的名称。

![数据模型。ActionLog 表。](aspnet-mvc-4-custom-action-filters/_static/image1.png "数据模型。ActionLog 表。")

*数据模型-ActionLog 表*

该解决方案提供了 ASP.NET MVC 视图，为操作日志，请参阅**MvcMusicStores/视图/ActionLog**:

![操作日志视图](aspnet-mvc-4-custom-action-filters/_static/image2.png "操作日志视图")

*操作日志视图*

与此假设结构，将中断控制器的请求和执行日志记录通过使用自定义筛选集中的所有工作。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a>任务 1-创建自定义筛选器来捕获控制器的请求

在此任务将创建一个将包含日志记录逻辑的自定义筛选器属性类。 为此，您将扩展 ASP.NET MVC **ActionFilterAttribute**类和实现该接口**IActionFilter**。

> [!NOTE]
> **ActionFilterAttribute**是所有属性筛选器的基类。 它提供了以下方法后且在执行控制器操作之前执行特定的逻辑：
> 
> - **OnActionExecuting**(ActionExecutingContext filterContext): 操作之前，只需调用方法。
> - **OnActionExecuted**(ActionExecutedContext filterContext): 调用操作方法之后之前 （在之前视图呈现） 执行的结果。
> - **OnResultExecuting**(ResultExecutingContext filterContext): 只需之前 （在之前视图呈现） 执行的结果。
> - **OnResultExecuted**(ResultExecutedContext filterContext): （在呈现视图时） 后执行的结果后。
> 
> 通过到派生类中替代任何一种方法，可以执行筛选的代码。


1. 打开**开始**解决方案位于**\Source\Ex01-LoggingActions\Begin**文件夹。

   1. 你将需要下载某些缺少的 NuGet 包，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
      > 
      > 有关详细信息，请参阅此文章： [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 添加一个新 C# 类到**筛选器**文件夹并将其命名*CustomActionFilter.cs*。 此文件夹将存储的自定义筛选器。
3. 打开**CustomActionFilter.cs**并添加对引用**System.Web.Mvc**并**MvcMusicStore.Models**命名空间：

    (代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex1 CustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. 继承**CustomActionFilter**类派生**ActionFilterAttribute** ，然后进行**CustomActionFilter**类实现**是 IActionFilter**接口。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. 请**CustomActionFilter**类重写方法**OnActionExecuting**并添加必要的逻辑来记录筛选器的执行。 若要执行此操作，添加以下突出显示的代码内**CustomActionFilter**类。

    (代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex1 LoggingActions*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > **OnActionExecuting**的方法使用**Entity Framework**添加新的 ActionLog 注册。 它会创建并填充新的实体实例的上下文信息**filterContext**。
    > 
    > 可以阅读更多有关**ControllerContext**类在[msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a>任务 2-将代码拦截器注入到应用商店控制器类

在此任务将通过将其注入到所有控制器类并将记录的控制器操作添加自定义筛选器。 本练习的目的存储控制器类将具有一个日志。

该方法**OnActionExecuting**从**ActionLogFilterAttribute**调用插入的元素时，在运行自定义筛选器。

还有可能以截获特定控制器方法。

1. 打开**StoreController**处**MvcMusicStore\Controllers**并添加对引用**筛选器**命名空间：

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. 注入自定义筛选器**CustomActionFilter**成**StoreController**类通过添加 **[CustomActionFilter]** 属性的类声明之前。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > 当筛选器注入到控制器类时，所有操作也都注入。 如果你想要应用筛选器仅对一组操作，必须将注入 **[CustomActionFilter]** 到每个之一：
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在本任务中，您将测试的日志记录筛选器正常工作。 将启动应用程序并访问应用商店，，然后您将检查记录的活动。

1. 按 **F5** 运行该应用程序。
2. 浏览到 **/ActionLog**若要查看日志视图初始状态：

    ![记录页活动之前的跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image3.png "记录页活动之前的跟踪器状态")

    *页活动之前的日志跟踪程序状态*

   > [!NOTE]
   > 默认情况下，它将始终显示检索现有流派菜单时，将生成的一项。
   > 
   > 为简单起见我们正在清理**ActionLog**表每次应用程序运行时以便只显示每个特定任务的验证的日志。
   > 
   > 可能需要删除中的以下代码**会话\_启动**方法 (在**Global.asax**类)，以便保存在存储区中执行的所有操作的历史日志控制器。
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. 单击其中一个**流派**菜单中，并执行某些操作，例如浏览可用的唱片集。
4. 浏览到 **/ActionLog**且日志为空按**F5**刷新页面。 检查未跟踪您的访问：

    ![操作日志记录活动与](aspnet-mvc-4-custom-action-filters/_static/image4.png "活动记录具有操作日志")

    *使用活动记录的操作日志*

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a>练习 2： 管理多个操作筛选器

在此练习中将将第二个自定义操作筛选器添加到 StoreController 类并定义将在其中执行两个筛选器的特定顺序。 然后将更新代码以注册全局筛选器。

有不同的方法定义的筛选器的执行顺序时需要考虑。 例如，Order 属性和筛选器的作用域：

您可以定义**作用域**对于每个筛选器，例如，可将范围限定的所有操作筛选器中运行**控制器都范围**，和所有授权筛选器中运行**全局作用都域**. 作用域具有定义的执行顺序。

此外，每个操作筛选器有一个顺序属性，用于确定筛选器的作用域中的执行顺序。

有关自定义操作筛选器执行顺序的详细信息，请访问此 MSDN 文章: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx))。

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a>任务 1： 创建新的自定义操作筛选器

在此任务中，您将创建新的自定义操作筛选器可将注入到 StoreController 类中，学习如何管理筛选器的执行顺序。

1. 打开**开始**解决方案位于**\Source\Ex02-ManagingMultipleActionFilters\Begin**文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

    1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
    2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
    3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

        > [!NOTE]
        > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
        > 
        > 有关详细信息，请参阅此文章： [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 添加一个新 C# 类到**筛选器**文件夹并将其命名*MyNewCustomActionFilter.cs*
3. 打开**MyNewCustomActionFilter.cs**并添加对引用**System.Web.Mvc**并**MvcMusicStore.Models**命名空间：

    (代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex2-MyNewCustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. 默认类声明替换为以下代码。

    (代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex2-MyNewCustomActionFilterClass*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > 此自定义操作筛选器是几乎比你在上一练习中创建相同的。 主要区别是，它有*&quot;记录由&quot;* 更新与此新类的名称以标识针对筛选器属性已注册的日志。

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a>任务 2： 将新代码拦截器注入到 StoreController 类

在此任务中，会将新的自定义筛选器添加到 StoreController 类，并运行解决方案，以验证这两种筛选器协同工作。

1. 打开**StoreController**类位于**MvcMusicStore\Controllers** ，并插入新的自定义筛选器**MyNewCustomActionFilter**到**StoreController**类，如下所示的以下代码。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. 现在，运行应用程序，以便了解这些两个自定义操作筛选器的工作方式。 若要执行此操作，按**F5**并等待，直到应用程序启动。
3. 浏览到 **/ActionLog**若要查看日志视图初始状态。

    ![记录页活动之前的跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image5.png "记录页活动之前的跟踪器状态")

    *页活动之前的日志跟踪程序状态*
4. 单击其中一个**流派**菜单中，并执行某些操作，例如浏览可用的唱片集。
5. 检查这一次;两次跟踪您的访问： 你在为每个自定义操作筛选器的添加后**StorageController**类。

    ![操作日志记录活动与](aspnet-mvc-4-custom-action-filters/_static/image6.png "活动记录具有操作日志")

    *使用活动记录的操作日志*
6. 关闭浏览器。

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a>任务 3： 管理筛选器排序

在本任务中，您将学习如何使用顺序属性设置管理筛选器的执行顺序。

1. 打开**StoreController**类位于**MvcMusicStore\Controllers**并指定**顺序**喜欢这两个筛选器中的属性如下所示。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. 现在，验证根据其顺序属性的值执行筛选器的方式。 您会发现具有最小的顺序值的筛选器 (**CustomActionFilter**) 是执行的第一个。 按**F5**并等待，直到应用程序启动。
3. 浏览到 **/ActionLog**若要查看日志视图初始状态。

    ![记录页活动之前的跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image7.png "记录页活动之前的跟踪器状态")

    *页活动之前的日志跟踪程序状态*
4. 单击其中一个**流派**菜单中，并执行某些操作，例如浏览可用的唱片集。
5. 检查这一次，您的访问未跟踪的筛选器的顺序值按排序： **CustomActionFilter**日志的第一个。

    ![操作日志记录活动与](aspnet-mvc-4-custom-action-filters/_static/image8.png "活动记录具有操作日志")

    *使用活动记录的操作日志*
6. 现在，将更新的筛选器的顺序值，并验证日志记录顺序如何变化。 在中**StoreController**类中，更新类似的筛选器的顺序值如下所示。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. 再次运行该应用程序，通过按**F5**。
8. 单击其中一个**流派**菜单中，并执行某些操作，例如浏览可用的唱片集。
9. 检查这一次，日志是否创建由**MyNewCustomActionFilter**筛选器显示在最前面。

    ![操作日志记录活动与](aspnet-mvc-4-custom-action-filters/_static/image9.png "活动记录具有操作日志")

    *使用活动记录的操作日志*

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a>任务 4： 注册全局筛选器

在此任务中，将更新解决方案，以注册新的筛选器 (**MyNewCustomActionFilter**) 作为全局筛选器。 通过执行此操作，将会触发的所有操作执行应用程序中，而不仅限 StoreController 的如在上一任务中所示。

1. 在中**StoreController**类中，删除 **[MyNewCustomActionFilter]** 属性和 order 属性从 **[CustomActionFilter]**。 其外观应如下所示：

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. 打开**Global.asax**文件，找到**应用程序\_启动**方法。 请注意，每次应用程序启动时它正在注册全局筛选器，通过调用**RegisterGlobalFilters**方法内的**FilterConfig**类。

    ![在 Global.asax 中注册全局筛选器](aspnet-mvc-4-custom-action-filters/_static/image10.png "在 Global.asax 中注册全局筛选器")

    *在 Global.asax 中注册全局筛选器*
3. 打开**FilterConfig.cs**文件内**应用\_启动**文件夹。
4. 添加对使用 System.Web.Mvc; 的引用使用 MvcMusicStore.Filters;命名空间。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. 更新**RegisterGlobalFilters**方法添加自定义筛选器。 若要执行此操作，添加突出显示的代码：

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. 运行应用程序通过按**F5**。
7. 单击其中一个**流派**菜单中，并执行某些操作，例如浏览可用的唱片集。
8. 检查现在 **[MyNewCustomActionFilter]** 太 HomeController 和 ActionLogController 中注入。

    ![操作日志记录活动与](aspnet-mvc-4-custom-action-filters/_static/image11.png "活动记录具有操作日志")

    *使用全局活动记录的操作日志*

> [!NOTE]
> 此外，可以部署此应用程序到 Windows Azure Web Sites 以下[附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixB)。


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>总结

通过完成本动手实验介绍了如何扩展操作筛选器来执行自定义操作。 您还学习了如何将注入到页面控制器的任何筛选器。 使用以下概念：

- 如何使用 ASP.NET MVC ActionFilterAttribute 类创建自定义操作筛选器
- 如何将筛选器注入到 ASP.NET MVC 控制器
- 如何管理使用 Order 属性筛选器排序
- 如何注册全局筛选器

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 a： 安装 Visual Studio Express 2012 for Web

你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**. 以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。

1. 转到[ [ https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。
2. 单击**立即安装**。 如果还没有**Web 平台安装程序**将重定向以下载并安装。
3. 一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，然后单击**我接受**以继续。

    ![接受许可条款](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    *接受许可条款*
5. 等待，直到下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    *安装进度*
6. 安装完成后，单击**完成**。

    ![安装已完成](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    *安装已完成*
7. 单击**退出**以关闭 Web 平台安装程序。
8. 若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-custom-action-filters/_static/image16.png)

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

    ![登录到 Windows Azure 门户](aspnet-mvc-4-custom-action-filters/_static/image17.png "登录到 Windows Azure 门户")

    *登录到 Windows Azure 管理门户*
2. 单击**新建**命令栏上。

    ![创建新的 Web 站点](aspnet-mvc-4-custom-action-filters/_static/image18.png "创建新的 Web 站点")

    *创建新的 Web 站点*
3. 单击**计算** | **网站**。 然后选择**快速创建**选项。 为新网站提供可用的 URL，然后单击**创建网站**。

    > [!NOTE]
    > Windows Azure 网站是可以控制和管理在云中运行的 web 应用程序主机。 快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从门户外部的部署。 它不包括用于设置数据库的步骤。

    ![创建新的网站使用快速创建](aspnet-mvc-4-custom-action-filters/_static/image19.png "创建新的网站使用快速创建")

    *创建新的网站使用快速创建*
4. 等到新**网站**创建。
5. 创建网站后，单击下面的链接**URL**列。 检查新的 Web 站点正常工作。

    ![浏览到新的 web 站点](aspnet-mvc-4-custom-action-filters/_static/image20.png "浏览到新的 web 站点")

    *浏览到新的 web 站点*

    ![正在运行的网站](aspnet-mvc-4-custom-action-filters/_static/image21.png "正在运行的网站")

    *正在运行的网站*
6. 返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。

    ![打开网站管理页](aspnet-mvc-4-custom-action-filters/_static/image22.png "打开网站管理页")

    *打开网站管理页*
7. 在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。

    > [!NOTE]
    > *发布配置文件*包含所有发布到每个启用的发布方法的 Windows Azure 网站的 web 应用程序所需的信息。 发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。 **Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Windows Azure 网站。

    ![正在下载网站发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image23.png "下载网站发布配置文件")

    *正在下载网站发布配置文件*
8. 下载发布配置文件到已知位置。 进一步在此练习中将了解如何使用此文件从 Visual Studio 的 web 应用程序到 Windows Azure 网站发布。

    ![保存发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image24.png "保存发布配置文件")

    *保存发布配置文件*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。 如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。

1. 用于存储应用程序数据库，将需要 SQL 数据库服务器。 可以从在 Windows Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。 如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。 请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。 不创建数据库，因为它将在后面的阶段中创建。

    ![SQL 数据库服务器仪表板](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database 服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。 若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png)按钮。

    ![添加客户端 IP 地址](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    *添加客户端 IP 地址*
3. 一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。

    ![确认更改](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    *确认更改*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布

1. 返回到 ASP.NET MVC 4 解决方案。 在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。

    ![发布应用程序](aspnet-mvc-4-custom-action-filters/_static/image29.png "发布应用程序")

    *发布此网站*
2. 导入发布配置文件保存在第一个任务。

    ![导入发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image30.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击**验证连接**。 验证完成后单击**下一步**。

    > [!NOTE]
    > 请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。

    ![验证连接](aspnet-mvc-4-custom-action-filters/_static/image31.png "验证连接")

    *验证连接*
4. 在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。

    ![Web 部署配置](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web 部署配置")

    *Web 部署配置*
5. 配置数据库连接，如下所示：

   - 在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。
   - 在中**用户名**键入服务器管理员登录名。
   - 在中**密码**键入服务器管理员登录密码。
   - 键入新的数据库名称。

     ![配置目标连接字符串](aspnet-mvc-4-custom-action-filters/_static/image33.png "配置目标连接字符串")

     *配置目标连接字符串*
6. 然后单击“确定” 。 当系统提示你创建数据库时，单击**是**。

    ![创建数据库](aspnet-mvc-4-custom-action-filters/_static/image34.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。 然后，单击 **“下一步”**。

    ![连接字符串指向 SQL 数据库](aspnet-mvc-4-custom-action-filters/_static/image35.png "指向 SQL 数据库连接字符串")

    *连接字符串指向 SQL 数据库*
8. 在中**预览版**页上，单击**发布**。

    ![Web 应用程序发布](aspnet-mvc-4-custom-action-filters/_static/image36.png "发布 web 应用程序")

    *Web 应用程序发布*
9. 在发布过程完成后，在默认浏览器将打开已发布的网站。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附录 c： 使用代码片段

使用代码段，可以轻松获得相关所需的所有代码。 实验室文档将告诉您完全何时可以使用它们，如下图中所示。

![使用 Visual Studio 代码段代码插入到你的项目](aspnet-mvc-4-custom-action-filters/_static/image37.png "使用 Visual Studio 代码段代码插入到你的项目")

*使用 Visual Studio 代码段代码插入到你的项目*

***若要添加代码段使用键盘 (仅限 C#)***

1. 将光标置于要插入的代码。
2. 开始键入代码片段名称 （不带空格或连字符）。
3. 观看作为 IntelliSense 显示匹配的代码段的名称。
4. 选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。
5. 按 Tab 键两次，以在光标位置插入代码段。

![开始键入代码段名称](aspnet-mvc-4-custom-action-filters/_static/image38.png "开始键入代码段名称")

*开始键入代码段名称*

![按 tab 键以选择突出显示代码段](aspnet-mvc-4-custom-action-filters/_static/image39.png "按选项卡以选择突出显示代码段")

*按 tab 键以选择突出显示代码段*

![再次按 Tab 和代码段将 expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "再次按 Tab 和代码段将扩展")

*再次按 Tab 和代码段将扩展*

***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。 右键单击你想要插入的代码片段。

1. 选择**插入代码段**跟**我的代码片段**。
2. 通过单击选择列表中中的相关代码片段。

![右键单击你想要插入代码段和选择插入代码段](aspnet-mvc-4-custom-action-filters/_static/image41.png "右键单击你想要插入代码段和选择插入代码段")

*右键单击你想要插入代码段和选择插入代码段*

![通过单击选择列表中中的相关代码片段](aspnet-mvc-4-custom-action-filters/_static/image42.png "通过单击选择列表中中的相关代码片段")

*通过单击选择列表中中的相关代码片段*
