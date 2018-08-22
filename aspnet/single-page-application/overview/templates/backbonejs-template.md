---
uid: single-page-application/overview/templates/backbonejs-template
title: Backbone 模板 |Microsoft Docs
author: madskristensen
description: Backbone.js SPA 模板
ms.author: riande
ms.date: 04/04/2013
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 325c4f5370340b2e223521fada77cf0e78a67b5b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825063"
---
<a name="backbone-template"></a>Backbone 模板
====================
通过[Mads Kristensen](https://github.com/madskristensen)

> 是由 Kazi Manzur Rashid 编写的主干 SPA 模板
> 
> [下载 Backbone.js SPA 模板](https://go.microsoft.com/fwlink/?LinkId=293631)


Backbone.js SPA 模板旨在帮助你开始快速构建交互式客户端的 web 应用使用[Backbone.js。](http://backbonejs.org/)

该模板用于开发 ASP.NET MVC 中的 Backbone.js 应用程序提供初始的主干。 在初始状态下，它提供基本的用户登录功能，包括用户注册、 登录、 密码重置，并使用基本电子邮件模板的用户确认。

要求：

- [ASP.NET 和 Web Tools 2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a>创建一个主干模板项目

下载并安装该模板通过单击上面的下载按钮。 该模板打包为 Visual Studio 扩展 (VSIX) 文件。 您可能需要重启 Visual Studio。

在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。 下**Visual C#**，选择**Web**。 在项目模板列表中选择**ASP.NET MVC 4 Web 应用程序**。 命名项目，然后单击**确定**。

![](backbonejs-template/_static/image1.png)

在中**新的项目**向导，选择 Backbone.js SPA 项目。

![](backbonejs-template/_static/image2.png)

按 Ctrl-F5 生成并运行应用程序而不进行调试，或按 f5 边运行边调试。

![](backbonejs-template/_static/image3.png)

单击"我的帐户"将显示登录页：

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a>演练： 客户端代码

让我们开始在客户端。 客户端应用程序脚本位于 ~/Scripts/application 文件夹中。 编写的应用程序[TypeScript](http://www.typescriptlang.org/) （.ts 文件） 进行编译为 JavaScript （.js 文件）。

**应用程序**

`Application` application.ts 中定义。 此对象初始化应用程序，并且可作为根命名空间。 例如，用户已登录，它维护在该应用程序之间共享的配置和状态信息。

`application.start`方法创建模式的视图，并将附加事件处理程序应用程序级事件，例如用户登录。 接下来，它将创建默认路由器，并检查是否指定了任何客户端的 URL。 如果不是，它将重定向到默认 url (# ！ /)。

**事件**

当开发松散耦合组件时，事件始终是非常重要。 通常，应用程序以响应用户操作执行多个操作。 主干提供内置事件与组件，如模型、 集合和视图。 而不是创建这些组件间的相互依赖关系，该模板使用"发布/订阅"模式： `events` events.ts 中, 定义的对象充当用于发布和订阅的应用程序事件的事件中心。 `events`对象是单一实例。 下面的代码演示如何订阅事件，然后触发该事件：

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

**路由器**

在 Backbone.js，路由器提供路由客户端的页面并将其连接到操作和事件的方法。 该模板定义中 router.ts 单一路由器。 路由器创建 activable 视图，并切换视图时维护状态。 （下一节描述了 activable 视图）。最初，该项目包含两个虚拟视图，家庭和有关。 它还具有找不到视图，如果不知道路由，则显示。

**视图**

~/Scripts/application/视图中定义这些视图。 有两种类型的视图、 activable 视图和模式对话框视图。 由路由器调用 activable 视图。 Activable 视图显示时，所有其他 activable 视图变为非活动状态。 若要创建 activable 视图，扩展视图提供`Activable`对象：

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

使用扩展`Activable`将两个新方法添加到视图中，`activate`和`deactivate`。 路由器调用这些方法来激活和停用仍视图。

作为实现模式视图[Twitter Bootstrap](http://twitter.github.com/bootstrap/)模式对话框。 `Membership`和`Profile`视图是模式视图。 模型视图可由任何应用程序事件调用。 例如，在`Navigation`视图中，单击"我的帐户"链接显示任一`Membership`视图或`Profile`视图中的，具体取决于用户已登录。 `Navigation`附加 click 事件处理程序的具有任何子元素`data-command`属性。 以下是 HTML 标记：

[!code-html[Main](backbonejs-template/samples/sample3.html)]

此处是 navigation.ts 要挂钩到事件中的代码：

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

**模型**

模型 ~/Scripts/application/模型中进行定义。 所有模型都具有三个基本操作： 默认属性、 验证规则和服务器端的终结点。 下面是一个典型示例：

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

**插件**

~/Scripts/application/lib 文件夹包含一些便利的 jQuery 插件。Form.ts 文件定义的插件使用窗体数据。 通常，您需要进行序列化或反序列化窗体数据和显示的任何模型验证错误。 插件 form.ts 有方法，如`serializeFields`， `deserializeFields`，和`showFieldErrors`。 下面的示例演示如何序列化模型的窗体。

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

插件 flashbar.ts 分配给用户的各种类型的反馈消息。 方法是`$.showSuccessbar`，`$.showErrorbar`和`$.showInfobar`。 在后台，它使用 Twitter Bootstrap 警报显示可以很好地经过动画处理的消息。

插件 confirm.ts 替换浏览器的确认对话框中，尽管该 API 是略有不同：

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a>演练： 服务器代码

现在让我们看一下在服务器端。

**控制器**

在单页面应用程序中，服务器播放用户界面中只有很小的作用。 通常情况下，服务器将呈现的初始页面，然后发送和接收 JSON 数据。

该模板具有两个 MVC 控制器：`HomeController`呈现的初始页，并`SupportsController`用于确认新的用户帐户和重置密码。 在模板中的所有其他控制器是 ASP.NET Web API 控制器，发送和接收 JSON 数据。 默认情况下，控制器都使用新`WebSecurity`类来执行与用户相关的任务。 但是，它们还具有可选的构造函数，让你将传递委托中对这些任务。 这简化了测试，并让您替换`WebSecurity`与其他事情，请使用 IoC 容器。 下面是一个示例：

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a>视图

设计视图为模块化： 页面的每个部分都有自己专用的视图。 单页面应用程序中很常见包括不具有任何相应的控制器的视图。 可以通过调用包括一个视图`@Html.Partial('myView')`，但是这会变得枯燥乏味。 若要简化此过程，该模板定义一个帮助器方法， `IncludeClientViews`，呈现的所有指定的文件夹视图：

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

如果未指定文件夹名称，默认文件夹名称是"ClientViews"。 如果客户端视图也使用分部视图，名称以下划线字符的分部视图 (例如， `_SignUp`)。 `IncludeClientViews`方法不包括其名称以下划线开头的任何视图。 若要包括在客户端视图的分部视图，请调用`Html.ClientView('SignUp')`而不是`Html.Partial('_SignUp')`。

**发送电子邮件**

若要发送电子邮件，该模板，请使用[邮政](http://aboutcode.net/postal)。 邮政抽象的与代码的其余部分，但是，`IMailer`接口，所以您可以轻松地将其替换为另一个实现。 电子邮件模板位于视图/电子邮件文件夹中。 发件人的电子邮件地址中，在 web.config 文件中，指定`sender.email`的关键**appSettings**部分。 此外，当`debug="true"`在 web.config 中，应用程序不需要用户电子邮件确认可加速开发。

## <a name="github"></a>GitHub

您还可以在找到 Backbone.js SPA 模板[GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)。
