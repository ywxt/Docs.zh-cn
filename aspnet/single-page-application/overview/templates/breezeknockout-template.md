---
uid: single-page-application/overview/templates/breezeknockout-template
title: Breeze/Knockout 模版 |Microsoft Docs
author: madskristensen
description: Breeze/Knockout 单页面应用程序模板
ms.author: aspnetcontent
ms.date: 01/30/2013
ms.assetid: 3bd94827-3c59-448f-abc3-36e6df4858db
msc.legacyurl: /single-page-application/overview/templates/breezeknockout-template
msc.type: authoredcontent
ms.openlocfilehash: f816563b77aaeae0ef79b31ddb4e066c9764bb51
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37813479"
---
<a name="breezeknockout-template"></a>Breeze/Knockout 模版
====================
通过[Mads Kristensen](https://github.com/madskristensen)

> Breeze/Knockout MVC 模板是编写的 Ward Bell
> 
> [下载 Breeze/Knockout MVC 模板](https://go.microsoft.com/fwlink/?LinkId=282649)


您听说过"单页面应用程序"(SPA) 并想知道它是什么。 虽然无法了解它，而不是与它自己。 但谁还有时间来下载示例？ 如果您有 Visual Studio，将包含最多的示例 SPA 和 ASP.NET mvc 4"Breeze/Knockout 单页面应用程序"模板运行在不会早于 60 秒。

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

## <a name="what-is-the-breezeknockout-spa-template"></a>什么是 Breeze/Knockout SPA 模板？

大多数项目模板生成应用程序框架。 通过添加你的代码置于这些基本加点料和最终交付的工作应用程序。 Breeze/Knockout SPA 模板是不同的。 它会生成示例应用程序，以便研究。 它演示了 SPA 应用程序设计和许多用于构建 SPA 的技术。

Breeze/Knockout 模版上是一种变体[KnockoutJS SPA 模板](../introduction/knockoutjs-template.md)包含在 ASP.NET 和 Web Tools 2012.2 更新。 Breeze SPA 模板生成具有相同的用户体验的应用程序，但它具有不同的实现，使用数据管理变得轻而易举。

KnockoutJS SPA 模板，可使用原始 jQuery AJAX 中，服务请求足以满足简单的应用程序。 但更复杂的应用具有满足更加严苛的数据管理要求。 例如，大多数应用程序：

- 查询和扩展的用户会话期间重新查询服务器。
- 添加查询筛选器、 排序和分页。
- 在多个屏幕之间共享相同的数据。
- 累积更改向很多对象，然后将其保存为一个事务。
- 验证在客户端上的更改，因此，用户可以将更改提交到数据库之前更正错误。

BreezeJS 库处理这些繁琐的事务，使你能开发最重要的应用程序逻辑和用户体验。

[**Breeze** ](http://www.breezejs.com/?utm_source=ms-spa)是用于构建丰富的数据应用程序中 JavaScript 和 HTML 的以前已作为独立桌面应用程序传递的应用类型的开放源代码库。

Breeze/Knockout 模板可帮助你执行向更可靠的数据管理基础结构的第一个关键步骤。 它将生成与 KnockoutJS SPA 模板表面上是相同的示例待办事项应用程序。 在内部，它替换 Breeze 的 AJAX 数据层，以便可以比较两个方法，通过并行。 当然，它几乎不能涉及到 Breeze 应用程序的可能性。 但您会看到 Breeze 的工作原理和如何稍有需要进行这种转换。

让我们开始吧。

## <a name="create-a-breezeknockout-template-project"></a>创建一个 Breeze/Knockout 模板项目

下载并安装该模板通过单击上面的下载按钮。 该模板打包为 Visual Studio 扩展 (VSIX) 文件。 您可能需要重启 Visual Studio。

在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。 下**Visual C#**，选择**Web**。 在项目模板列表中选择**ASP.NET MVC 4 Web 应用程序**。 命名项目，然后单击**确定**。

在中**新的项目**向导中，选择**Breeze Knockout SPA**。

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeKOSpaTemplate.png)

按 Ctrl-F5 生成并运行应用程序而不进行调试，或按 f5 边运行边调试。

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

当首次运行该应用程序时，它显示登录屏幕。 单击"注册"链接，一个新页面种到视图中，您可以在其中输入用户名和密码。 （登录名和注册页使用构建 ASP.NET MVC。）当您提交注册表单时，服务器会生成 TodoList 以下两个项为您的帐户。 其呈现给你在上一个黄色的注释。

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

现在，已在 SPA 土地。 所有内容您看到和体验时操作 Todo 呈现和管理的 Knockout 和 Breeze 帮助客户端上。 以用户身份浏览应用程序... 但与开发人员的关注。 在浏览器中使用的开发人员工具来捕获网络流量。 (在 Internet Explorer： 按 f12 键，选择**网络**选项卡，然后单击**开始捕获**。)现在请尝试以下方法：

- 添加新的 Todo 项。
- 单击标签和编辑 Todo 项标题
- 选中复选框以将标记项已完成。 请注意，文本框被禁用，因此是不再可编辑的标题。
- 单击右侧的标签的 x。 项目将消失，并从数据库删除。
- 选择另一个项，并清除其标题。 您将有标题是必需的验证错误。 短暂暂停之后还原上一个标题。
- 键入可笑长标题中。 你将收到不同的验证错误的标题是太长。
- 单击"添加待办事项列表"按钮。 上一列表的左侧将显示新列表。
- 播放使用触发其所需的 TodoList 标题和长度验证。
- 单击以清除错误消息的标题文本框中。
- 单击右上角以删除任务列表和其 todo 圆圈中的"x"。

验证逻辑是通过 Breeze 的执行的客户端。 服务器模型类上的验证特性是传播到客户端，并自动执行之前客户端与服务器联系。

查看网络流量。 请注意，Breeze 检测到错误时，已连接到服务器的任何调用。 每个有效的更改时为"/ api/Todo/SaveChanges"的 POST 请求。 Breeze 捆绑包所做的更改并将其发送到一起以单个请求到 Web API 控制器`SaveChanges`方法。 这就是不同于 KockoutJS SPA 模板，这使得 PUT、 POST 和 DELETE 分别为每个项的请求。

## <a name="peek-inside"></a>在查看

此应用程序具有一个客户端和服务器端。 客户端堆栈组成一个小的 HTML 和应用程序 JavaScript 模块 （在"应用"文件夹中） 的组合以及第三方 JavaScript 库 （在"脚本"文件夹中）。

![](http://www.breezejs.com/sites/all/images/spa-template/ClientArchitecture.png)

如果您研究 KnockoutJS SPA 模板，这应该很熟悉。 重点放在蓝色框。 UI 体系结构是视图的模型-视图-视图模型 (MVVM)，其中的 HTML 小组件视图的完全分隔从视图模型中支持的演示文稿代码。 数据绑定系统 (Knockout 在此情况下) 协调的视图和视图模型，这样，每个可以执行其作业而无需其他精通。

模型封装 Todo 数据。 模型中的实体都由构造通过 Breeze Knockout 可观察量属性，以便它们可以直接绑定到视图中的小组件。 视图模型要求数据上下文来获取和保存模型实体。 数据上下文委托的大部分 breeze 工作。

一些开发人员代码和三个原则.NET 库的服务器端堆栈组成： Web API、 实体框架和 Breeze.NET:

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

KockoutJS SPA 模板相同的基本体系结构。 但是，实现是要简单得多： Dto 已删除，并且已到 Breeze.NET 委派大多数实体框架的详细信息。

## <a name="next-steps"></a>后续步骤

我们建议您浏览代码，由引导[广泛的讨论](http://www.breezejs.com/spa-template?utm_source=ms-spa)的客户端和服务器堆栈 Breeze 网站上的。

您可以尝试播放使用 Breeze 客户端的查询的灵活性。添加一些筛选器和排序。 你可以添加多个模型的属性和多个实体以更好地了解端到端 SPA 开发的。 当你确信该设计的时你可以断开 Todo 功能并替换为您自己。

很快您就可以大的下一步： 添加客户端屏幕并在它们之间导航。 将留下此 SPA 模板和转向更完整的 SPA 堆栈，如[John Papa 热总是随身携带毛巾](https://github.com/johnpapa/HotTowel#readme "热总是随身携带毛巾")，从而将 Durandal 添加到 Breeze 和 Knockout 组合。
