---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: ASP.NET MVC 概述 |Microsoft Docs
author: microsoft
description: 了解有关 ASP.NET MVC 应用程序和 ASP.NET Web 窗体应用程序之间的差异。 了解如何决定何时生成的 ASP.NET MVC 应用程序。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: 61a7841ee238ec365b7d1909221bbe3d834faf84
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824754"
---
<a name="aspnet-mvc-overview"></a>ASP.NET MVC 概述
====================
by [Microsoft](https://github.com/microsoft)

> 了解有关 ASP.NET MVC 应用程序和 ASP.NET Web 窗体应用程序之间的差异。 了解如何决定何时生成的 ASP.NET MVC 应用程序。


模型-视图-控制器 (MVC) 体系结构模式将应用程序分成三个主要组件： 模型、 视图和控制器。 ASP.NET MVC 框架提供用于创建基于 MVC 的 Web 应用程序的 ASP.NET Web 窗体模式的替代方法。 ASP.NET MVC 框架是一个轻型、 高度可测试的演示框架，（如基于 Web 窗体的应用程序） 与现有的 ASP.NET 功能，如母版页和基于成员身份的身份验证集成。 MVC 框架中定义**System.Web.Mvc**命名空间和是基本的、 受支持的一部分**System.Web**命名空间。   
  
MVC 是许多开发人员都熟悉的标准设计模式。 某些类型的 Web 应用程序将受益于 MVC 框架。 其他人将继续使用基于 Web 窗体和回发的传统 ASP.NET 应用程序模式。 其他类型的 Web 应用程序将合并这两种方法;两种方法彼此互不。   
  
MVC 框架包括以下组件：


[![调用控制器操作所需的参数值](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**图 01**： 调用控制器操作所需的参数值 ([单击以查看实际尺寸的图像](asp-net-mvc-overview/_static/image2.png))


- **模型**。 模型对象是实现应用程序的数据域逻辑的应用程序部件。 通常情况下，模型对象检索，并将模型状态存储在数据库中。 例如，Product 对象可能会从数据库中检索信息、 操作它，然后更新将信息写回到 SQL Server 中的 Products 表。

在小型应用程序，该模型通常是而不是一个物理概念分离。 例如，如果应用程序仅读取数据集，并将其发送到视图，该应用程序没有物理模型层和相关的类。 在这种情况下，数据集将模型对象的角色。

- **视图**。 视图是显示应用程序的用户界面 (UI) 的组件。 通常，此 UI 被创建的模型数据。 示例将显示文本框、 下拉列表和基于产品对象的当前状态的复选框的产品表的编辑视图。

- **控制器**。 控制器是处理用户交互、 使用模型，并最终选择要呈现的视图显示 UI 的组件。 在 MVC 应用程序中，视图仅显示信息；控制器处理并响应用户输入和交互。 例如，控制器处理查询字符串值，并将这些值传递给模型，后者进而通过使用的值查询数据库。

MVC 模式可帮助您创建单独的应用程序 （输入的逻辑、 业务逻辑和 UI 逻辑），同时提供这些元素之间松散耦合的不同方面的应用程序。 该模式指定每种逻辑在应用程序中的位置。 UI 逻辑位于视图中。 输入逻辑位于控制器中。 业务逻辑位于模型中。 这种隔离有助于管理复杂性时生成应用程序，因为它使你能够专注于一次实现的一个方面。 例如，您可以集中精力而无需具体取决于业务逻辑的视图。   
  
除了管理复杂性，MVC 模式可以更轻松地测试基于 Web 窗体的 ASP.NET Web 应用程序比测试应用程序。 例如，在基于 Web 窗体的 ASP.NET Web 应用程序，同时显示输出并响应用户输入使用单个类。 编写自动化的测试的基于 Web 窗体的 ASP.NET 应用程序可能很复杂，因为若要测试单个页面，您必须实例化页类、 所有及其子控件和应用程序中的其他相关类。 这么多的类进行实例化，以运行该页，因为它可能难以编写专门侧重于应用程序的各个部分的测试。 因此可以更难实现都比 MVC 应用程序中的测试基于 Web 窗体的 ASP.NET 应用程序的测试。 而且，基于 Web 窗体的 ASP.NET 应用程序中的测试需要 Web 服务器。 MVC 框架可使组件分离并大量使用的接口，这样就可以测试各个组件中的框架的其余部分分开。   
  
MVC 应用程序的三个主要组件之间的松散耦合也可促进并行开发。 例如，一位开发人员可以从事视图、 第二个开发人员可以从事控制器逻辑和第三个开发人员可以专注于模型中的业务逻辑。

## <a name="deciding-when-to-create-an-mvc-application"></a>确定何时创建 MVC 应用程序

您必须仔细考虑是否使用 ASP.NET MVC 框架或 ASP.NET Web 窗体模型实现的 Web 应用程序。 MVC 框架未取代 Web 窗体模型中;为 Web 应用程序，可以使用任一框架。 （如果有现有的基于 Web 窗体的应用程序，这些继续工作方式与它们始终具有。）   
  
你决定为特定网站使用 MVC 框架或 Web 窗体模型之前，请权衡每种方法的优点。

### <a name="advantages-of-an-mvc-based-web-application"></a>基于 MVC 的 Web 应用程序的优点

ASP.NET MVC 框架具有以下优点：

- 它可以更轻松地将应用程序分为模型、 视图和控制器管理复杂性。
- 它不使用视图状态或基于服务器的窗体。 这使得 MVC 框架非常适合的开发人员希望完全控制对应用程序的行为。
- 它使用处理通过单一控制器的 Web 应用程序请求的前端控制器模式。 这使您可以设计支持丰富路由基础结构的应用程序。 有关详细信息，请参阅[前端控制器](https://go.microsoft.com/fwlink/?LinkId=106357 "前端控制器")MSDN 网站上。
- 它进行测试驱动开发 (TDD) 提供更好的支持。
- 它适用于 Web 应用程序支持的大型团队的开发人员和 Web 设计人员需要对应用程序行为的控件的高度。

### <a name="advantages-of-a-web-forms-based-web-application"></a>Web 窗体的基于 Web 应用程序的优点

基于 Web 窗体的框架具有以下优点：

- 它支持通过 HTTP，这有益于开发业务线 Web 应用程序保留状态的事件模型。 基于 Web 窗体的应用程序提供了许多支持数百个服务器控件中的事件。
- 它使用将功能添加到各个页面的页面控制器模式。 有关详细信息，请参阅[页面控制器](https://go.microsoft.com/fwlink/?LinkId=106359 "页面控制器")MSDN 网站上。
- 它使用视图状态或基于服务器的窗体，这可以使管理状态信息更容易。
- 它非常适合 Web 开发人员和设计人员想要利用大量组件可用于快速开发应用程序的小型团队。
- 一般情况下，它是不太复杂的应用程序开发，因为组件 (**页**类、 控件等) 紧密集成，并且通常需要比 MVC 模型更少的代码。

## <a name="features-of-the-aspnet-mvc-framework"></a>ASP.NET MVC Framework 的功能

ASP.NET MVC 框架提供了以下功能：

- 应用程序任务 （输入的逻辑、 业务逻辑和 UI 逻辑）、 可测试性，并且默认情况下的测试驱动开发 (TDD) 的分离。 MVC framework 中的所有核心协定都基于接口，并可以使用模拟对象，后者是模拟的对象，用于模拟应用程序中的实际对象的行为进行测试。 您可以进行单元测试应用程序而无需在 ASP.NET 进程中，这使得单元测试既快速又灵活运行控制器。 可以使用任何与.NET Framework 兼容的单元测试框架。
- 可扩展且可插入的框架。 ASP.NET MVC framework 的组件，以便它们可以轻松地替换或自定义设计。 您可以插入自己的视图引擎、 URL 路由策略、 操作方法参数序列化和其他组件。 ASP.NET MVC 框架还支持使用依赖关系注入 (DI) 和控制反转 (IOC) 容器模型。 DI，可将对象注入到类，而不是依靠类来创建对象本身。 IOC 指定，是否对象需要另一个对象，第一个对象应从配置文件之类的外部源获取第二个对象。 这使测试更加轻松。
- 一个功能强大的 URL 映射组件，用于生成具有易于理解和可搜索 Url 的应用程序。 Url 不需要包括文件扩展名和都设计为支持工作的 URL 命名模式非常适合搜索引擎优化 (SEO) 和具象状态传输 (REST) 寻址引擎。
- 支持使用现有的 ASP.NET 页面 （.aspx 文件）、 用户控件 （.ascx 文件） 和母版页 （.master 文件） 标记文件中的标记用作视图模板。 可以使用现有的 ASP.NET 功能与 ASP.NET MVC 框架，诸如嵌套母版页、 内联表达式 (&lt;%= %&gt;)，声明性服务器控件、 模板、 数据绑定、 本地化和等等。
- 对现有 ASP.NET 功能的支持。 ASP.NET MVC 允许您使用功能，例如窗体身份验证和 Windows 身份验证、 URL 授权、 成员资格和角色、 输出和数据缓存、 会话和配置文件状态管理、 运行状况监视、 配置系统和提供程序体系结构。
