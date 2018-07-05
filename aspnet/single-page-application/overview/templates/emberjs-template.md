---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS 模板 |Microsoft Docs
author: xqiu
description: EmberJS 模板
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/30/2013
ms.topic: article
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
ms.technology: ''
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1f5b005180fed15c51b36417cdcd6acc98123c9a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374161"
---
<a name="emberjs-template"></a>EmberJS 模板
====================
通过[Xinyang Qiu](https://github.com/xqiu)

> EmberJS MVC 模板是由 Nathan Totten、 Thiago Santos 和 Xinyang Qiu 编写的。
> 
> [下载 EmberJS MVC 模板](https://go.microsoft.com/fwlink/?LinkId=282647)


EmberJS SPA 模板是为帮助你开始快速构建交互式客户端的 web 应用使用 EmberJS 而设计的。

"单页面应用程序"(SPA) 是加载单个 HTML 页面，然后页面动态更新，而不是加载新页面的 web 应用程序的常规术语。 初始页面加载后 SPA 通过 AJAX 请求与服务器通信。

![](emberjs-template/_static/image1.png)

AJAX 是什么新鲜事物，但如今有更加轻松地构建和维护大型复杂的 SPA 应用程序的 JavaScript 框架。 此外，html5 和 CSS3 轻松地创建丰富的 Ui。

EmberJS SPA 模板使用[Ember](http://emberjs.com/) JavaScript 库来处理从 AJAX 请求的页面更新。 Ember.js 使用数据绑定与最新的数据同步页。 这样一来，您无需编写任何代码，它将指导完成的 JSON 数据并更新 DOM 相反，你可以声明性属性置于告诉 Ember.js 如何呈现数据的 HTML。

在服务器端 EmberJS 模板是几乎完全相同[KnockoutJS SPA 模板](../introduction/knockoutjs-template.md)。 它使用 ASP.NET MVC 为 HTML 文档和 ASP.NET Web API，以处理来自客户端 AJAX 请求提供服务。 有关模板的这些方面的详细信息，请参阅[KnockoutJS 模板](../introduction/knockoutjs-template.md)文档。 本主题重点介绍 Knockout 模板和 EmberJS 模板之间的差异。

## <a name="create-an-emberjs-spa-template-project"></a>创建 EmberJS SPA 模板项目

下载并安装该模板通过单击上面的下载按钮。 您可能需要重启 Visual Studio。

在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。 下**Visual C#**，选择**Web**。 在项目模板列表中选择**ASP.NET MVC 4 Web 应用程序**。 命名项目，然后单击**确定**。

![](emberjs-template/_static/image2.png)

在中**新的项目**向导中，选择**Ember.js SPA 项目**。

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a>EmberJS SPA 模板概述

EmberJS 模板使用 jQuery、 Ember.js、 Handlebars.js 创建平滑的交互式用户界面的组合。

Ember.js 是一个 JavaScript 库，使用客户端的 MVC 模式。

- 一个*模板*、 书面 Handlebars 模板化语言，描述的应用程序用户界面。 在发布模式下[Handlebars 编译器](https://github.com/Myslik/csharp-ember-handlebars)用于捆绑包和编译 handlebars 模板。
- 一个*模型*将它从服务器 （待办事项列表和 ToDo 项） 中获取的应用程序数据存储。
- 一个*控制器*存储应用程序状态。 控制器通常存在模型数据复制到相应的模板。
- 一个*视图*将转换应用程序中的基元事件，并将传递给控制器。
- 一个*路由器*管理应用程序状态，保持 Url 和模板的同步。

此外，Ember 数据库可用于同步 （通过 RESTful API 从服务器获取） 的 JSON 对象和客户端模型。

EmberJS SPA 模板将脚本组织到八个层：

- webapi\_adapter.js、 webapi\_serializer.js： 扩展了 Ember 数据库以使用 ASP.NET Web API。
- Scripts/helpers.js： 定义新的 Ember Handlebars 帮助器。
- Scripts/app.js： 创建应用程序，并配置适配器和序列化程序。
- 脚本/应用/模型/\*.js： 定义模型。
- 脚本/应用/视图/\*.js： 定义的视图。
- 脚本/应用/控制器/\*.js： 定义控制器。
- 脚本/应用/routes、 Scripts/app/router.js： 定义了路由。
- 模板 /\*.hbs： 定义 handlebars 模板。

让我们看一些更详细地这些脚本。

## <a name="models"></a>模型

模型进行定义的脚本/应用/models 文件夹中。 有两个模型文件： 将 todoitem.js 文件和 todoList.js。

**todo.model.js**定义待办事项列表客户端 （浏览器） 模型。 有两个模型类： todoItem 和 todoList。 在 Ember 中，模型是 DS 子类。模型。 一个模型可以有属性具有属性：

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

模型可以与其他模型定义的关系：

[!code-css[Main](emberjs-template/samples/sample2.css)]

模型可以计算出绑定到其他属性的属性：

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

模型可以具有一个观察到的属性更改时调用的观察者函数：

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a>视图

在脚本/app/views 文件夹中定义这些视图。 视图将转换应用程序 UI 中的事件。 事件处理程序可以调用返回控制器的功能，或只需直接调用数据上下文。

例如，以下代码是从 views/TodoItemEditView.js。 它定义的事件处理为输入的文本字段。

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a>控制器

控制器定义的脚本/应用/controllers 文件夹中。 若要表示单个模型，扩展`Ember.ObjectController`:

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

在控制器还可以通过扩展表示的模型集合`Ember.ArrayController`。 例如，TodoListController 表示数组的`todoList`对象。 控制器按 todoList ID 以降序进行排序：

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

控制器定义了一个名为函数`addTodoList`，它创建新的 todoList 并将其添加到数组。 若要查看如何调用此函数，请打开名为 todoListTemplate.html，在模板文件夹中的模板文件。 以下模板代码绑定到按钮`addTodoList`函数：

[!code-html[Main](emberjs-template/samples/sample8.html)]

该控制器还包含`error`属性，其中包含一条错误消息。 下面是用于显示错误消息 （也在 todoListTemplate.html) 的模板代码：

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a>路由

Router.js 定义的路由和默认模板，以显示，还设置了应用程序状态，并与 Url 匹配的路由：

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

TodoListRoute.js 加载通过重写 setupController 函数 TodoListRoute 的数据：

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

Ember 使用命名约定来匹配 Url、 路由名称、 控制器和模板。 有关详细信息，请参阅[ http://emberjs.com/guides/routing/defining-your-routes/ ](http://emberjs.com/guides/routing/defining-your-routes/) EmberJS 文档。

## <a name="templates"></a>模板

模板文件夹包含四个模板：

- application.hbs： 启动应用程序时呈现的默认模板。
- about.hbs:"/ 关于"路由模板。
- index.hbs： 根模板"/"的路由。
- todoList.hbs： 的模板"/ todo"路由。
- \_navbar.hbs: 模板定义导航菜单。

应用程序模板的作用类似于主页面。 它包含一个标头、 页脚和"{{outlet}}"要插入的路由中的其他模板。 有关在 Ember 中的应用程序模板的详细信息，请参阅[ http://guides.emberjs.com/v1.10.0/templates/the-application-template// ](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)。

"/ TodoList"模板包含两个循环表达式。 外部循环是`{{#each controller}}`，并内部循环是`{{#each todos}}`。 以下代码显示了内置`Ember.Checkbox`查看，以自定义`App.TodoItemEditView`，并使用链接`deleteTodo`操作。

[!code-html[Main](emberjs-template/samples/sample12.html)]

`HtmlHelperExtensions` Controllers/HtmlHelperExensions.cs 中, 定义的类定义一个帮助程序函数来缓存，并插入模板文件时**调试**设置为**true** Web.config 文件中。 从 Views/Home/App.cshtml 中定义的 ASP.NET MVC 视图文件调用此函数：

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

调用不带任何参数，该函数将呈现的所有模板文件的模板文件夹中。 此外可以指定一个子文件夹或特定的模板文件。

当**调试**是**false**在 Web.config 中，该应用程序包括绑定项"~/bundles/templates"。 此捆绑包项将添加在 BundleConfig.cs，使用 Handlebars 编译器库：

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
