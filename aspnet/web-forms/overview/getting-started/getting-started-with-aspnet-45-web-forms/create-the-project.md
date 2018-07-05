---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
title: 创建项目 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 2ce36f78-8ecb-4ab1-b748-6d0ab633ea3f
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
msc.type: authoredcontent
ms.openlocfilehash: e5d6fa312ce0375eee5ca456aaea9f088d806cfc
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384483"
---
<a name="create-the-project"></a>创建项目
====================
通过[Erik Reitan](https://github.com/Erikre)

[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。 Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。


在本教程中将创建、 查看，并运行 Visual Studio 中，这将允许您以熟悉的 ASP.NET 功能中的默认项目。 此外，您将查看 Visual Studio 环境。

## <a name="what-youll-learn"></a>你将学习：

- 如何创建一个新的 Web 窗体项目。
- Web 窗体项目文件结构。
- 如何在 Visual Studio 中运行项目。
- 默认 Web 窗体应用程序的不同功能。
- 有关如何使用 Visual Studio 环境的一些基础知识。

## <a name="creating-the-project"></a>创建项目

1. 打开 Visual Studio。
2. 选择**新的项目**从**文件**Visual Studio 菜单中的。 

    ![创建新项目的菜单项的项目-](create-the-project/_static/image1.png)
3. 选择**模板** - &gt; **Visual C#**  - &gt; **Web**在左侧的模板组。
4. 选择**ASP.NET Web 应用程序**在中心列中的模板。  
 本系列教程使用.NET Framework 4.5.2。
5. 将项目命名*WingtipToys* ，然后选择**确定**按钮。 

    ![创建项目的新建项目对话框](create-the-project/_static/image2.png)

    > [!NOTE]
    > 在本教程系列中的项目的名称是**WingtipToys**。 建议使用此*确切*项目名称，以便按预期运行整个系列教程提供的代码。

6. 单击**更改身份验证**按钮。 选择**单个用户帐户**然后单击**确定**按钮。

7. 选择**Web 窗体**模板，然后单击**确定**按钮。

    ![创建新的项目模板的项目-](create-the-project/_static/image3.png)

项目将需要一些时间来创建。 准备就绪后，打开**Default.aspx**页。

![创建新的项目模板的项目-](create-the-project/_static/image4.png)

您可以切换**设计**视图和**源**视图中选择中心窗口底部的选项。 **设计**视图显示 ASP.NET 网页、 母版页、 内容页面、 HTML 页面和用户控制是否使用附近所见即所得视图。 **源**视图显示在 Web 页上，可以编辑的 HTML 标记。

> [!TIP] 
> 
> **了解 ASP.NET 框架**
> 
> ASP.NET Web 窗体，可以使用熟悉的拖放、 事件驱动模型生成动态网站。 设计图面和数百个控件和组件可以快速生成复杂且功能强大的 UI 驱动站点具有数据访问权限。 Wingtip Toy 存储基于 ASP.NET Web 窗体，但许多在本系列教程中了解的概念都适用于所有 ASP.NET。
> 
> ASP.NET 提供了四个主要开发框架：
> 
> - [ASP.NET Web 窗体](../../../index.md)  
>  Web 窗体框架以开发人员更喜欢声明性和基于控件的编程中，例如 Microsoft Windows 窗体 (WinForms) 和 WPF/XAML/Silverlight 为目标。 因此，开发人员寻找用于 web 开发的快速应用程序开发 (RAD) 环境与受欢迎，它提供所见即所得设计器驱动的开发模型。 如果不熟悉 web 编程和熟悉的传统的 Microsoft RAD 客户端开发工具 （例如，对于 Visual Basic 和 Visual C# 中），您可以快速生成 web 应用程序，而无需在 HTML 和 JavaScript 中的体验。
> - [ASP.NET MVC](../../../../mvc/index.md)  
>  ASP.NET MVC 面向以下开发人员感兴趣的模式和原则，例如测试驱动开发、 关注点分离、 反转控制 (IoC) 和依赖关系注入 (DI)。 此框架鼓励将分离其表示层提供的 web 应用程序的业务逻辑层。
> - [ASP.NET 网页](../../../../web-pages/index.md)  
>  ASP.NET 网页以简单的 web 开发情景，按一系列 PHP 开发人员为目标。 在 Web 页面模型中，创建 HTML 页，然后将基于服务器的代码添加到页以便动态控制该标记的呈现方式。 网页专门为一款轻量级框架，且它是 asp.net 的人员知道 HTML，但不可能具有广泛的编程体验-例如，学生或爱好者的最简单入口点。 它也是 web 开发人员了解 PHP 或类似框架开始使用 ASP.NET 的好方法。
> - [ASP.NET 单页面应用程序](../../../../single-page-application/index.md)  
>  ASP.NET 单页面应用程序 (SPA) 帮助您生成包含大量使用 HTML、 CSS 3 和 JavaScript 的客户端进行交互的应用程序。 ASP.NET 和 Web Tools 2012.2 更新附带了用于构建使用 knockout.js 和 ASP.NET Web API 的单页应用程序的新模板。 除了新 SPA 模板社区创建的新 SPA 模板也已可供下载。
> 
> 除四个主要开发框架，ASP.NET 还提供其他技术，它们是必须要注意的和熟悉，但不是包括在本系列教程中：
> 
> - [ASP.NET Web API](../../../../web-api/index.md) -一个框架，用于构建 HTTP 服务的访问范围广泛的客户端，包括浏览器和移动设备。
> - [ASP.NET SignalR](../../../../signalr/index.md) -轻松开发实时 web 功能的库。


### <a name="reviewing-the-project"></a>查看项目

在 Visual Studio 中，**解决方案资源管理器**窗口允许您管理的项目文件。 让我们看看已添加到你的应用程序中的文件夹**解决方案资源管理器**。 Web 应用程序模板中添加基本的文件夹结构：

![创建项目的解决方案资源管理器](create-the-project/_static/image5.png)

Visual Studio 创建一些初始文件夹和文件为你的项目。 您将使用在本教程后面的第一个文件如下所示：

| **文件** | **目的** |
| --- | --- |
| *Default.aspx* | 通常第一页的浏览器中运行应用程序时显示。 |
| *Site.Master* | 允许你在应用程序中创建一致布局并使用标准的行为的页面的页面。 |
| *Global.asax* | 一个包含对应用程序级别和会话级别由 ASP.NET 或 HTTP 模块引发的事件作出响应的代码的可选文件。 |
| *Web.config* | 应用程序的配置数据。 |

### <a name="running-the-default-web-application"></a>运行默认的 Web 应用程序

默认 Web 应用程序提供了丰富的体验基于内置功能和支持。 无需更改任何默认 Web 窗体项目，该应用程序已准备好在本地 Web 浏览器上运行。

1. 按***F5***时 Visual Studio 中的键。   
 应用程序将生成并显示在 Web 浏览器中。  

    ![创建项目-默认页](create-the-project/_static/image6.png)
2. 已完成的评审正在运行应用程序后，关闭浏览器窗口。

此默认 Web 应用程序中有三个主要页面： *Default.aspx* （主文件夹）， *About.aspx*，并*Contact.aspx*。 每个这些页可从顶部导航栏访问。 也有两个帐户文件夹中包含的其他页、 Register.aspx 页面和 Login.aspx 页面。 这两页，可使用 ASP.NET 成员资格功能来创建、 存储和验证用户凭据。

## <a name="aspnet-web-forms-background"></a>ASP.NET Web 窗体背景

ASP.NET Web 窗体是基于 Microsoft ASP.NET 技术，在其中动态在服务器运行的代码生成网页输出到浏览器或客户端设备的页面。 ASP.NET Web 窗体页自动呈现功能，例如样式、 布局和等等的正确符合浏览器的 HTML。 Web 窗体都支持.NET 公共语言运行时，如 Microsoft Visual Basic 和 Microsoft Visual C# 的任何语言与兼容。 此外，基于 Web 窗体[Microsoft.NET Framework](https://msdn.microsoft.com/vstudio/aa496123)，其中提供了托管的环境中，类型安全性和继承等好处。

ASP.NET Web 窗体页运行时，此页将经历生命周期中将执行一系列处理步骤。 这些步骤包括初始化，实例化控件、 还原和维护状态、 运行事件处理程序代码，以及进行呈现。 随着你变得更熟悉的 ASP.NET Web 窗体强大功能，是您必须了解[ASP.NET 页面生命周期](https://msdn.microsoft.com/library/ms178472(v=vs.100).aspx)，以便可以在适当的生命周期阶段的预期的效果编写代码。

Web 服务器收到页请求时，它发现页，对其进行处理，将其发送到浏览器中，然后将放弃所有页的信息。 如果用户再次请求相同的页面，服务器会重复整个过程，重新处理从零开始的页。 将另一种方法，在服务器具有它有处理页的页没有内存是无状态。 ASP.NET 页框架会自动处理维护您的页面和其控件的状态的任务并为您提供显式方式维护状态的特定于应用程序的信息。

> [!TIP] 
> 
> **在 Web 窗体应用程序模板中的 web 应用程序功能**
> 
> ASP.NET Web 窗体应用程序模板提供了一套丰富的内置功能。 它不仅提供了与您*Home.aspx*页上， *About.aspx*页上， *Contact.aspx*页上，但还包括注册用户，并将保存的成员资格功能其凭据，以便他们可以登录到你的网站。 此概述提供了有关的一些功能包含在 ASP.NET Web 窗体应用程序模板和如何在 Wingtip Toys 应用程序中使用的详细信息。
> 
> **成员身份**
> 
> [ASP.NET](https://msdn.microsoft.com/library/yh26yfzy.aspx)标识将用户的凭据存储在应用程序创建的数据库。 你的用户登录时，应用程序通过读取数据库验证其凭据。 你的项目*帐户*文件夹包含用于实现成员资格的各个部分的文件： 注册、 登录、 更改密码，和授予的访问权限。 此外，ASP.NET Web 窗体支持 OAuth 和 OpenID。 这些身份验证增强功能使用户能够登录到你的站点使用此类为 Facebook、 Twitter、 Windows Live 和 Google 帐户中的现有凭据。
> 
> ![创建项目的解决方案资源管理器 （ASP.NET 标识）](create-the-project/_static/image7.png)
> 
> 默认情况下，该模板创建成员资格数据库的 SQL Server Express LocalDB，附带 Visual Studio Express 2013 for Web 开发数据库服务器实例上使用默认数据库名称。
> 
> **SQL Server Express LocalDB**
> 
> [SQL Server Express LocalDB](https://technet.microsoft.com/library/hh510202.aspx)是具有许多可编程性功能的 SQL Server 数据库的 SQL Server 的轻量版本。 SQL Server Express LocalDB 在用户模式下运行，并具有快速的零配置安装具有一个安装必备组件的简短列表。 Microsoft SQL Server、 任何数据库或 TRANSACT-SQL 代码中可以从移动 SQL Server Express LocalDB 到 SQL Server 和 SQL Azure 无需执行任何升级步骤。 因此，可以面向所有版本的 SQL Server 的应用程序作为开发人员环境使用 SQL Server Express LocalDB。 SQL Server Express LocalDB 使在 SQL Server Compact 中不可用的存储的过程、 用户定义的函数和聚合，.NET Framework 集成、 空间类型和其他人等功能。
> 
> **母版页**
> 
> [ASP.NET 母版页](https://msdn.microsoft.com/library/wtxbf3hh.aspx)在应用程序中定义一致的外观和行为的所有页面。 主控页的布局将与单个内容页面以生成用户看到的最后一页中的内容合并。 在 Wingtip Toys 应用程序，您将修改*Site.master*母版页，以便在 Wingtip Toys 网站中的所有页面都共享相同的独特徽标和导航栏。
> 
> **HTML5**
> 
> ASP.NET Web 窗体应用程序模板支持[HTML5](http://www.w3schools.com/html/html5_intro.asp)，这是最新版本的 HTML 标记语言。 HTML5 支持新的元素和功能，使其更轻松地创建网站。
> 
> **Modernizr**
> 
> 对于不支持 HTML5 的浏览器，可以使用[Modernizr](http://www.modernizr.com/)。 Modernizr 是开放源代码 JavaScript 库，可以检测是否支持 HTML5 功能，以及如果不启用它们的浏览器。 在 ASP.NET Web 窗体应用程序模板，Modernizr 会安装 NuGet 包。
> 
> **Bootstrap**
> 
> 使用 Visual Studio 2013 项目模板[Bootstrap](http://getbootstrap.com/)，创建的 Twitter 的布局和主题框架。 Bootstrap 使用 CSS3 提供响应式设计，这意味着布局可以动态地适应不同的浏览器窗口大小。 Bootstrap 的主题功能还可用于轻松地影响应用程序的外观和行为的更改。 默认情况下，Visual Studio 2013 中的 ASP.NET Web 应用程序模板包括 Bootstrap 作为 NuGet 包。
> 
> **NuGet 包**
> 
> ASP.NET Web 窗体应用程序模板包括一套[NuGet](http://www.nuget.org/)包。 这些包提供开放源代码库和工具的窗体中的组件化的功能。 还有各种可帮助您创建和测试应用程序的包。 Visual Studio 就可轻松添加、 删除和更新 NuGet 包。 开发人员可以创建并同时将包添加到 NuGet。
> 
> ![创建项目的 NuGet 对话框](create-the-project/_static/image8.png)
> 
> 在安装包时，NuGet 将文件复制到你的解决方案，并自动使所需的任何更改，例如添加引用，以及更改与 Web 应用程序关联的配置。 如果您决定在库中删除，NuGet 将删除文件，并反转任何它所做的更改在项目中，以便不保留任何混乱。 NuGet 是可从**工具**Visual Studio 菜单中的。
> 
> **jQuery**
> 
> [jQuery](http://jquery.com/)是一个快速且简洁的 JavaScript 库，简化了 HTML 文档遍历、 事件处理、 进行动画处理，并快速 web 开发的 Ajax 交互。 JQuery JavaScript 库作为 NuGet 包包含 ASP.NET Web 窗体应用程序模板中。
> 
> **非介入式验证**
> 
> 内置的验证程序控件已配置为将非介入式 JavaScript 用于客户端验证逻辑。 这大大减少了呈现页面标记中的内联 JavaScript 并减少整体的页面大小。 非介入式验证全局添加到 ASP.NET Web 窗体应用程序模板中的设置基于&lt;appSettings&gt;的元素*Web.config*根目录下的应用程序的文件。
> 
> **实体框架代码优先**
> 
> Wingtip Toys 应用程序使用 ASP.NET Web 窗体应用程序模板中的功能，除了[Entity Framework Code First](https://weblogs.asp.net/scottgu/archive/2010/12/08/announcing-entity-framework-code-first-ctp5-release.aspx)，这是一个 NuGet 库，当您使用数据时，代码为中心的开发。 简单地说，它会创建你的应用程序可以根据您编写的代码的数据库部分。 使用实体框架，检索和操作数据作为强类型化对象。 此，您专注于业务逻辑中你的应用程序而不是如何访问数据的详细信息。
> 
> 有关已安装的库和包 ASP.NET Web 窗体模板中包含的其他信息，请参阅安装 NuGet 包的列表。 若要执行此操作，在 Visual Studio 中创建一个新的 Web 窗体项目，选择**工具** - &gt; **库程序包管理器** - &gt; **管理解决方案的 NuGet 包**，然后选择**已安装的包**中**管理 NuGet 包**对话框。


### <a name="touring-visual-studio"></a>Touring Visual Studio

Visual Studio 中的主窗口包括**解决方案资源管理器**，则**服务器资源管理器**(**数据库资源管理器**Express 中)，则**属性窗口**，则**工具箱**，则**工具栏**，并且**文档窗口**。

![创建项目的 NuGet 对话框](create-the-project/_static/image9.png)

有关 Visual Studio 的详细信息，请参阅[可视化指南 Visual Web Developer](https://msdn.microsoft.com/library/ee410104.aspx)。

## <a name="summary"></a>总结

在本教程中已创建、 查看并运行默认的 Web 窗体应用程序。 在您阅读的不同功能的默认 Web 窗体应用程序并了解有关如何使用 Visual Studio 环境的一些基础知识。 在以下教程将创建数据访问层。

## <a name="additional-resources"></a>其他资源

[选择适当的编程模型](../../../videos/how-do-i/choosing-the-right-programming-model.md)   
[与网站项目的 web 应用程序项目](https://msdn.microsoft.com/library/dd547590.aspx)   
[ASP.NET Web 窗体页概述](https://msdn.microsoft.com/library/428509ah.aspx)

> [!div class="step-by-step"]
> [上一页](introduction-and-overview.md)
> [下一页](create_the_data_access_layer.md)
