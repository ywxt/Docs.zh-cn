---
uid: single-page-application/overview/introduction/knockoutjs-template
title: 单页面应用程序： KnockoutJS 模板 |Microsoft Docs
author: MikeWasson
description: Knockout 模板
ms.author: aspnetcontent
ms.date: 01/30/2013
ms.assetid: f9c07af0-4b20-4b08-af8f-47fc3df169a2
msc.legacyurl: /single-page-application/overview/introduction/knockoutjs-template
msc.type: authoredcontent
ms.openlocfilehash: 9e48c7033cefe8b6e4c456577b7a6448f9815d0b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37832524"
---
<a name="single-page-application-knockoutjs-template"></a>单页面应用程序： KnockoutJS 模板
====================
通过[Mike Wasson](https://github.com/MikeWasson)

> Knockout MVC 模板是 ASP.NET 和 Web Tools 2012.2 的一部分
> 
> [下载 ASP.NET 和 Web 工具 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650)


ASP.NET 和 Web Tools 2012.2 更新包括用于 ASP.NET MVC 4 的单页面应用程序 (SPA) 模板。 此模板旨在帮助你开始快速构建交互式客户端的 web 应用。

"单页面应用程序"(SPA) 是加载单个 HTML 页面，然后页面动态更新，而不是加载新页面的 web 应用程序的常规术语。 初始页面加载后 SPA 通过 AJAX 请求与服务器通信。

![](knockoutjs-template/_static/image1.png)

AJAX 是什么新鲜事物，但如今有更加轻松地构建和维护大型复杂的 SPA 应用程序的 JavaScript 框架。 此外，html5 和 CSS3 轻松地创建丰富的 Ui。

若要开始，SPA 模板创建一个示例"待办事项列表"应用程序。 在本教程中，我们将该模板的指导的教程。 首先，我们将看看待办事项列表应用程序本身，然后检查使其适用的技术力量。

## <a name="create-a-new-spa-template-project"></a>创建一个新的 SPA 模板项目

要求：

- Visual Studio 2012 或 Visual Studio Express 2012 for Web
- ASP.NET Web 工具 2012.2 更新。 可以安装更新[此处](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)。

启动 Visual Studio 并选择**新的项目**从起始页。 或者，从**文件**菜单中，选择**新建**，然后**项目**。

在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。 下**Visual C#**，选择**Web**。 在项目模板列表中选择**ASP.NET MVC 4 Web 应用程序**。 命名项目，然后单击**确定**。

![](knockoutjs-template/_static/image2.png)

在中**新的项目**向导中，选择**单页面应用程序**。

![](knockoutjs-template/_static/image3.png)

按 F5 生成并运行该应用程序。 当首次运行该应用程序时，它显示登录屏幕。

![](knockoutjs-template/_static/image4.png)

单击&quot;注册&quot;链接并创建一个新用户。

![](knockoutjs-template/_static/image5.png)

登录后，应用程序将创建包含两个项的默认待办事项列表。 可以单击"添加待办事项列表"以添加新列表。

![](knockoutjs-template/_static/image6.png)

重命名列表中，将项添加到列表中，并选中它们。 您还可以删除项或删除整个列表。 所做的更改自动保存到服务器上的数据库 (实际上 LocalDB 在此情况下，由于本地运行应用程序)。

![](knockoutjs-template/_static/image7.png)

## <a name="architecture-of-the-spa-template"></a>SPA 模板的体系结构

下图显示了应用程序的主要构建基块。

![](knockoutjs-template/_static/image8.png)

在服务器端 ASP.NET MVC 提供 HTML，同时也处理基于窗体的身份验证。

ASP.NET Web API 处理与 ToDoLists 和 Todoitem，包括获取、 创建、 更新和删除相关的所有请求。 客户端交换使用的 Web API 以 JSON 格式的数据。

实体框架 (EF) 是 O/RM 层。 将处理 ASP.NET 的面向对象的世界和基础数据库之间。 数据库使用 LocalDB，但您可以在 Web.config 文件中更改此。 通常你会使用 LocalDB 进行本地开发并随后部署到 SQL 数据库的服务器上，使用 EF 代码优先迁移。

在客户端，Knockout.js 库可处理从 AJAX 请求的页面更新。 Knockout 使用数据绑定与最新的数据同步页。 这样一来，您无需编写任何代码，它将指导完成的 JSON 数据并更新 DOM 相反中指示如何显示数据的 Knockout 的 HTML, 将声明性属性。

此体系结构的一大优势是它将表示层与应用程序逻辑分开。 您可以创建的 Web API 部分，而无需了解任何有关您的网页的外观。 在客户端上创建"视图模型"到表示这些数据，并在视图模型使用 Knockout 将绑定到 HTML。 这样，您可以轻松地更改而无需更改视图模型的 HTML。 （我们将介绍 Knockout 有点更高版本。）

## <a name="models"></a>模型

在 Visual Studio 项目中，模型文件夹包含在服务器端使用的模型。 （客户端上还有模型; 我们会谈到那些。）

![](knockoutjs-template/_static/image9.png)

**TodoItem TodoList**

这些是用于 Entity Framework Code First 的数据库模型。 请注意，这些模型有指向彼此的属性。 `ToDoList` 包含一系列的 Todoitem，并且每个`ToDoItem`已返回到其父级 ToDoList 的引用。 这些属性称为导航属性，以及它们所表示的一对多关系待办事项列表和其待办事项。

`ToDoItem`类还使用 **[ForeignKey]** 属性指定`ToDoListId`是外的键到`ToDoList`表。 这将告知 EF 将 foreign key 约束添加到数据库。

[!code-csharp[Main](knockoutjs-template/samples/sample1.cs)]

**TodoItemDto TodoListDto**

这些类定义将发送到客户端的数据。 "DTO"代表"数据传输对象"。 DTO 定义如何将实体序列化为 JSON。 一般情况下，有几个使用 Dto 的原因：

- 若要控制序列化的属性。 DTO 可包含从域模型属性的子集。 出于安全原因 （若要隐藏敏感数据） 或只是可能会执行此操作以减少发送的数据量。
- 若要更改形状的数据，例如若要平展更复杂的数据结构。
- 若要使任何业务逻辑从 DTO （关注点分离）。
- 如果出于某种原因，不能序列化您的域模型。 例如，循环引用可能会导致问题时有将对象序列化处理 Web API 中的此问题的方法 (请参阅[处理循环对象引用](../../../web-api/overview/formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)); 但使用 DTO 仅完全避免此问题。

在 SPA 模板中，Dto 包含域模型相同的数据。 但是，它们非常仍然有用，因为它们避免循环引用导航属性，它们说明了常规的 DTO 模式。

**AccountModels.cs**

此文件包含站点成员身份的模型。 `UserProfile`类定义成员资格数据库中的用户配置文件的架构。 （在这种情况下，唯一信息是用户 ID 和用户名称。）此文件中的其他模型类用于创建用户注册和登录窗体。

## <a name="entity-framework"></a>Entity Framework

SPA 模板使用 EF Code First。 在 Code First 开发中，你定义模型首先在代码中，并 EF 使用模型来创建数据库。 此外可以使用现有的数据库使用 EF ([Database First](https://msdn.microsoft.com/data/jj206878.aspx))。

`TodoItemContext`模型文件夹中的类派生自**DbContext**。 此类提供的模型和 EF 之间的"粘合"。 `TodoItemContext`持有`ToDoItem`集合和一个`TodoList`集合。 若要查询数据库，只需编写针对这些集合的 LINQ 查询。 例如，下面是如何选择所有用户"Alice"待办事项列表：

[!code-csharp[Main](knockoutjs-template/samples/sample2.cs)]

您可以向集合添加新项、 更新项，或从集合中删除项和保留对数据库的更改。

## <a name="aspnet-web-api-controllers"></a>ASP.NET Web API 控制器

在 ASP.NET Web API 中，控制器是处理 HTTP 请求的对象。 如前文所述，SPA 模板将使用 Web API 上启用 CRUD 操作`ToDoList`和`ToDoItem`实例。 控制器位于解决方案的 Controllers 文件夹中。

![](knockoutjs-template/_static/image10.png)

- `TodoController`： 处理待办事项的 HTTP 的请求
- `TodoListController`： 处理待办事项列表的 HTTP 的请求。

这些名称是很重要，因为 Web API 与控制器名称的 URI 路径相匹配。 (若要了解 Web API 将 HTTP 请求路由到控制器的方式，请参阅[ASP.NET Web API 中的路由](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)。)

让我们看看`ToDoListController`类。 它包含单个数据成员：

[!code-csharp[Main](knockoutjs-template/samples/sample3.cs)]

`TodoItemContext`用于与通信 EF，如前面所述。 在控制器上的方法实现 CRUD 操作。 Web API 将映射到控制器方法中，从客户端的 HTTP 请求，如下所示：

| HTTP 请求 | 控制器方法 | 描述 |
| --- | --- | --- |
| GET /api/todo | `GetTodoLists` | 获取待办事项列表的集合。 |
| GET/api/todo/*id* | `GetTodoList` | 获取按 ID 待办事项列表 |
| PUT/api/todo/*id* | `PutTodoList` | 更新待办事项列表。 |
| POST /api/todo | `PostTodoList` | 创建新的待办事项列表。 |
| 删除/api/todo/*id* | `DeleteTodoList` | 删除待办事项列表。 |

请注意，对于某些操作的 Uri，包含的 ID 值的占位符。 例如，若要删除到-列表 id 为 42，URI 是`/api/todo/42`。

若要了解有关使用 Web API 的 CRUD 操作的详细信息，请参阅[创建支持 CRUD 操作的 Web API](../../../web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations.md)。 此控制器的代码是非常简单。 下面是一些有趣的要点：

- `GetTodoLists`方法使用 LINQ 查询来登录的用户的 id 对结果进行筛选。 这样一来，用户只能看到属于他或她的数据。 此外，请注意，Select 语句用于将转换`ToDoList`实例转换`TodoListDto`实例。
- PUT 和 POST 方法修改数据库之前检查模型状态。 如果**ModelState.IsValid**为 false，这些方法将返回 HTTP 400 错误的请求。 阅读有关在 Web API 中的模型验证的详细信息[模型验证](../../../web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api.md)。
- 控制器类还使用修饰 **[Authorize]** 属性。 此属性检查 HTTP 请求进行身份验证。 如果请求未经过身份验证，客户端收到 HTTP 401 未授权。 阅读有关在进行身份验证的详细信息[身份验证和 ASP.NET Web API 中的授权](../../../web-api/overview/security/authentication-and-authorization-in-aspnet-web-api.md)。

`TodoController`类是非常类似于`TodoListController`。 最大的区别是它不定义任何 GET 方法，因为客户端将获取待办事项，以及每个待办事项列表。

## <a name="mvc-controllers-and-views"></a>MVC 控制器和视图

MVC 控制器也位于解决方案的 Controllers 文件夹。 `HomeController` 应用程序的主 HTML 呈现。 Views/Home/Index.cshtml 中定义了主控制器的视图。 主页视图呈现不同的内容，具体取决于用户登录：

[!code-cshtml[Main](knockoutjs-template/samples/sample4.cshtml)]

当用户登录时，他们将看到的主要用户界面。 否则，他们将看到登录面板。 请注意此条件呈现发生在服务器端。 永远不会尝试隐藏客户端上的敏感内容和发送 HTTP 响应中的 #8212anything 可见的人正在监视的原始 HTTP 消息。

## <a name="client-side-javascript-and-knockoutjs"></a>客户端的 JavaScript 和 Knockout.js

现在我们可以开始从服务器端到客户端应用程序。 SPA 模板使用 jQuery 和 Knockout.js 的组合来创建平滑的交互式用户界面。 Knockout.js 是一个 JavaScript 库，它可以更轻松地将 HTML 绑定到数据。 Knockout.js 使用称为"模型-视图-视图模型。"的模式

- 该模型是域数据 （ToDo 列表和 ToDo 项）。
- 该视图是 HTML 文档。
- 视图模型是用于保存模型数据的 JavaScript 对象。 视图模型是在 ui 的代码抽象。 它并不知道 HTML 表示形式。 相反，它表示抽象视图，例如"待办事项列表"的功能。

该视图是数据绑定到视图模型。 向视图模型的更新会自动反映在视图中。 绑定处理其他的方向。 （例如单击） 在 DOM 中的事件是数据绑定到函数视图模型上触发 AJAX 调用。

SPA 模板将客户端 JavaScript 组织到三个层：

- todo.datacontext.js： 发送 AJAX 请求。
- todo.model.js： 定义模型。
- todo.viewmodel.js： 定义视图模型。

![](knockoutjs-template/_static/image11.png)

这些脚本文件位于解决方案的脚本/应用程序文件夹中。

![](knockoutjs-template/_static/image12.png)

**todo.datacontext**处理对 Web API 控制器的所有 AJAX 调用。 （在中记录日志的 AJAX 调用在其他位置中, 定义 ajaxlogin.js。）

**todo.model.js**定义待办事项列表客户端 （浏览器） 模型。 有两个模型类： todoItem 和 todoList。

许多中的模型类的属性属于类型"ko.observable"。 可观察量是 Knockout 原理神奇之处。 从[Knockout 文档](http://knockoutjs.com/documentation/introduction.html)： 可观察量是"JavaScript 对象，它可以通知有关更改的订阅服务器。" 可观察量的值更改时，Knockout 会更新绑定到这些可观察量的任何 HTML 元素。 例如，todoItem 具有标题和执行属性的可观察量：

[!code-javascript[Main](knockoutjs-template/samples/sample5.js)]

您还可以订阅在代码中的可观测对象。 例如，"执行"和"标题"属性中的更改订阅的 todoItem 类：

[!code-javascript[Main](knockoutjs-template/samples/sample6.js)]

**视图模型**

视图模型 todo.viewmodel.js 中定义。 视图模型是应用程序将 HTML 页面元素绑定到域数据的位置的中心点。 在 SPA 模板中，视图模型包含 todoLists 可观察量数组。 视图模型中的以下代码告知 Knockout 中应用这些绑定：

[!code-javascript[Main](knockoutjs-template/samples/sample7.js)]

## <a name="html-and-data-binding"></a>HTML 和数据绑定

该页面的主 HTML Views/Home/Index.cshtml 中定义。 由于我们使用的数据绑定，HTML 只是一个模板用于什么实际获取呈现。 使用 knockout*声明性*绑定。 通过将"数据绑定"属性添加到该元素将页面元素绑定到数据。 下面是一个非常简单的示例，取自 Knockout 文档：

[!code-html[Main](knockoutjs-template/samples/sample8.html)]

在此示例中，Knockout 会更新的内容**&lt;跨越&gt;** 元素的值与`myItems.count()`。 当此值发生更改时，Knockout 将更新的文档。

Knockout 提供了多种不同的绑定类型。 下面是一些在 SPA 模板中使用的绑定：

- **foreach**： 可以循环访问一个循环并将相同的标记应用于列表中的每个项。 这用于呈现的待办事项列表和待办事项。 内**foreach**，绑定应用于列表的元素。
- **可见**： 用于切换可见性。 隐藏标记时集合为空，或使可见的错误消息。
- **值**： 用来填充窗体值。
- **单击**： 将单击事件绑定到视图模型上的函数。

## <a name="anti-csrf-protection"></a>反 CSRF 保护

跨站点请求伪造 (CSRF) 是一种攻击，恶意站点发送请求到易受攻击的站点在当前登录用户。 为了帮助防止 CSRF 攻击，ASP.NET MVC 将使用*防伪令牌*，也称为请求验证令牌。 其思路是，服务器将随机生成的令牌放入网页。 当客户端提交到服务器的数据时，它必须在请求消息中包括此值。

防伪标记起作用，因为恶意页面无法读取用户的令牌，由同域策略引起。 （同域策略阻止访问彼此的内容的两个不同的站点上托管的文档。）

ASP.NET MVC 通过防伪标记提供内置支持[防伪](https://msdn.microsoft.com/library/system.web.helpers.antiforgery.aspx)类和[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute.aspx)属性。 目前，此功能不是内置 Web API。 但是，SPA 模板包含 Web API 的自定义实现。 此代码中定义`ValidateHttpAntiForgeryTokenAttribute`类，该类位于解决方案的筛选器文件夹中。 若要了解有关 Web API 中的反 CSRF 的详细信息，请参阅[防止跨站点请求伪造 (CSRF) 攻击](../../../web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks.md)。

## <a name="conclusion"></a>结束语

SPA 模板是为帮助你开始快速编写现代、 交互式的 web 应用程序而设计的。 它使用 Knockout.js 库来区分表示形式 （HTML 标记） 和数据和应用程序逻辑。 但 Knockout 不是唯一可用于创建 SPA 的 JavaScript 库。 如果你想要了解一些其他选项，看一看[社区创建 SPA 模板](../templates/index.md)。
