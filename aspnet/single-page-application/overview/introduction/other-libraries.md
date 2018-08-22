---
uid: single-page-application/overview/introduction/other-libraries
title: 了解 Knockout 之外的库？ | Microsoft Docs
author: madskristensen
description: 了解 Knockout 之外的库？
ms.author: riande
ms.date: 02/05/2013
ms.assetid: a8367c6d-ef94-4dff-a010-5eff9e6eea96
msc.legacyurl: /single-page-application/overview/introduction/other-libraries
msc.type: authoredcontent
ms.openlocfilehash: 53c97580b45bb40a6c3256c8038ec5c8b861b69f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830089"
---
<a name="know-a-library-other-than-knockout"></a>了解 Knockout 之外的库？
====================
通过[Mads Kristensen](https://github.com/madskristensen)

[单页面应用程序 (SPA) 模板](knockoutjs-template.md)是若要开始编写单页面应用程序的好方法。 该模板使用[KnockoutJS](http://knockoutjs.com/)若要将应用程序数据绑定到 DOM 元素。

但 Knockout 不是用于创建丰富的客户端应用程序的唯一 JavaScript 库。 其他库以不同方式解决类似的难题。 因此我们几个社区创建的模板可供下载，您可能希望通过另一个库。 每个模板使用各种不同的客户端 JavaScript 库。

若要安装模板社区创建的请访问的模板页下面列出，并单击下载按钮。 这些模板作为 VSIX 文件提供。

## <a name="backbonejs"></a>BackboneJS

[Backbone.js SPA 模板](../templates/backbonejs-template.md)。 此模板提供用于开发的初始主干[Backbone.js](http://backbonejs.org/)在 ASP.NET MVC 应用程序。 在初始状态下，它提供基本的用户登录功能，包括用户注册、 登录、 密码重置，并使用基本电子邮件模板的用户确认。

## <a name="breezejs"></a>BreezeJS

[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)是开放源代码库来管理中的 JavaScript 客户端的丰富数据。 Breeze 将处理查询、 缓存、 更改跟踪、 验证和的详细信息。 两个模板功能变得轻而易举：

- [Breeze/Knockout](../templates/breezeknockout-template.md)模板扩展了 Knockout SPA 模板，显示可以生成的单页面应用程序使用 Breeze 适用于数据管理和 KnockoutJS 数据绑定的轻松程度。
- [Breeze/Angular](../templates/breezeangular-template.md)模板，还扩展了使用 Breeze，但使用 Knockout SPA 模板[AngularJS](http://angularjs.org)进行数据绑定、 依赖关系注入和屏幕管理的库。

此外，[热总是随身携带毛巾 SPA 模板](../templates/hottowel-template.md)使用 BreezeJS。

## <a name="emberjs"></a>EmberJS

[EmberJS SPA 模板](../templates/emberjs-template.md)。 此模板使用[Ember](http://emberjs.com/)，一个功能强大的 MVC JavaScript 库，可解决了很多用于构建丰富的客户端应用程序的挑战。

Ember SPA 模板是使用 EmberJS 和 Handlebars 模板化的 Knockout SPA 模板重新实现。

## <a name="hot-towel"></a>热总是随身携带毛巾

[热总是随身携带毛巾 SPA 模板](../templates/hottowel-template.md)。 此模板会为在多个 JavaScript 库，包括 Breeze 和 Knockout、 RequireJS 和 Twitter Bootstrap。

与此处列出的其他模板相比，热总是随身携带毛巾 teample 提供从中您可以构建你自己的更完整的应用程序。 有多个概念需要注意的但一旦您了解它们，此模板可能只是要查找的内容。 如果你想要生成 SPA，但不能决定要开始，请使用热总是随身携带毛巾，以秒为单位，您将得到一个 SPA 和所有工具则需要在其上进行构建。

## <a name="feature-table"></a>功能表

下面是每个 SPA 模板提供的功能：


|                        | ASP.NET SPA | 主干 | Breeze/Angular | Breeze/KO |  Ember   | 热总是随身携带毛巾 |
|------------------------|-------------|----------|----------------|-----------|----------|-----------|
|      待办事项示例       |  &#10003;   |          |    &#10003;    | &#10003;  | &#10003; |           |
|     裸机模板      |             | &#10003; |                |           |          | &#10003;  |
| 导航和历史记录 |             | &#10003; |    &#10003;    |           | &#10003; | &#10003;  |
|        库        |             |          |                |           |          |           |
|        Angular         |             |          |    &#10003;    |           |          |           |
|    &#8195;Backbone     |             | &#10003; |                |           |          |           |
|         Breeze         |             |          |    &#10003;    | &#10003;  |          | &#10003;  |
|        Durandal        |             |          |                |           |          | &#10003;  |
|         Ember          |             |          |                |           | &#10003; |           |
|        Knockout        |  &#10003;   |          |                | &#10003;  |          | &#10003;  |

