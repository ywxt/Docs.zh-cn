---
uid: single-page-application/overview/templates/breezeangular-template
title: Breeze/Angular 模板 |Microsoft Docs
author: madskristensen
description: Breeze/Angular 单页面应用程序模板
ms.author: aspnetcontent
ms.date: 03/08/2013
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 3799c891625b28312b54ed33628748dcc1b74925
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811745"
---
<a name="breezeangular-template"></a>Breeze/Angular 模板
====================
通过[Mads Kristensen](https://github.com/madskristensen)

> Breeze/Angular MVC 模板是编写的 Ward Bell
> 
> [下载 Breeze/Angular 的 MVC 模板](https://go.microsoft.com/fwlink/?LinkId=286437)


[AngularJS](http://angularjs.org)是来自 Google 的开放源代码库，用于构建单页面应用程序 (Spa)。 它提供数据绑定、 依赖关系注入和屏幕管理。 将其与结合[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)，为数据建模和数据管理和您的另一个开放源代码库具有出色的 HTML/JavaScript 客户端应用程序的基本组成部分。

Breeze/Angular SPA 模板上是一种变体[KnockoutJS SPA 模板](../introduction/knockoutjs-template.md)包含在 ASP.NET 和 Web Tools 2012.2 更新。 如果您有 Visual Studio，则必须示例 SPA 启动并运行在 60 秒内。

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

表面上是，应用程序看起来非常相似 KnockoutJS SPA 模板。 但实质上大不相同。 KnockoutJS 模板使用 Knockout 数据绑定和数据访问的原始 AJAX。 Breeze/Angular 模板使用 Angular 进行数据绑定和 Breeze 进行数据访问。 这些库启用其他功能，包括页面导航和历史记录。

下面是应用程序的关于页面：

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

当前用户会话期间，此页显示正在运行的日志的事件包括：

- 分页。 请注意在 #2 和 #7 Todo 控制器创建。
- 远程查询 (#3) 和本地缓存查询 (#7)。
- 新保存 （#5，6） 和修改 (#4) 的实体。
- 客户端上验证 (#9)，以便用户可以提交更改之前更正错误到数据库的更改。

有很多东西要浏览此模板中包括：

- 动态加载的 HTML 视图模板。
- 通过 Angular"指令。"的自定义数据绑定
- 模块性和依赖关系注入。
- 查询筛选器、 排序、 分页、 投影和包含的相关实体。
- 在多个屏幕之间共享数据。
- 作为单个事务中保存多个更改。
- 验证规则自动从服务器传播到 JavaScript 客户端。

让我们开始吧。

## <a name="create-a-breezeangular-template-project"></a>创建一个 Breeze/Angular 模板项目

下载并安装该模板通过单击上面的下载按钮。 该模板打包为 Visual Studio 扩展 (VSIX) 文件。 您可能需要重启 Visual Studio。

在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。 下**Visual C#**，选择**Web**。 在项目模板列表中选择**ASP.NET MVC 4 Web 应用程序**。 命名项目，然后单击**确定**。

在中**新的项目**向导中，选择**Breeze Angular SPA**。

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

按 Ctrl-F5 生成并运行应用程序而不进行调试，或按 f5 边运行边调试。

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

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
- 单击以查看这些活动的日志的右上角的"关于"链接。

验证逻辑是通过 Breeze 的执行的客户端。 服务器模型类上的验证特性是传播到客户端，并自动执行之前客户端与服务器联系。

查看网络流量。 请注意，Breeze 检测到错误时，已连接到服务器的任何调用。 每个有效的更改时为"/ api/Todo/SaveChanges"的 POST 请求。 Breeze 捆绑包所做的更改并将其发送到一起以单个请求到 Web API 控制器`SaveChanges`方法。 这就是不同于 KockoutJS SPA 模板，这使得 PUT、 POST 和 DELETE 分别为每个项的请求。

此外，请注意没有任何网络流量时切换之间任务列表和有关页。 这是因为查询被限定到本地缓存中变得轻而易举。

## <a name="peek-inside"></a>在查看

此应用程序具有一个客户端和服务器端。 客户端堆栈组成一个小的 HTML 和应用程序 JavaScript 模块 （在"应用"文件夹中） 的组合以及第三方 JavaScript 库 （在"脚本"文件夹中）。

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

UI 体系结构支持在控制器中的演示文稿代码区分开来的视图的 HTML 小组件。 这样，每个可以执行其作业而无需精通另，Angular 的数据绑定系统协调视图和控制器。

控制器会询问要获取和保存模型实体的数据上下文。 数据上下文委托的大部分工作 breeze，构造 JSON 查询结果中的自跟踪模型对象。

一些开发人员代码和三个原则.NET 库的服务器端堆栈组成： Web API、 实体框架和 Breeze.NET:

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

KockoutJS SPA 模板相同的基本体系结构。 但是，实现是要简单得多： Dto 已删除，并且已到 Breeze.NET 委派大多数实体框架的详细信息。

## <a name="next-steps"></a>后续步骤

我们建议您浏览代码，由引导[广泛的讨论](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa)的客户端和服务器堆栈 Breeze 网站上的。

您可以尝试播放使用 Breeze 客户端的查询的灵活性。添加一些筛选器和排序。 你可以添加多个模型的属性和多个实体以更好地了解端到端 SPA 开发的。 当你确信该设计的时你可以断开 Todo 功能并替换为您自己。

祝你编码愉快！
