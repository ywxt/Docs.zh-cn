---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: 向模型添加验证 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 4c7867587ba0610f0f1c23d9a0b9fbdc4040de7c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823584"
---
<a name="adding-validation-to-the-model"></a>向模型添加验证
====================
通过[Scott Hanselman](https://github.com/shanselman)

> 这是介绍 ASP.NET MVC 的基础知识初学者教程。 将创建一个简单的 web 应用程序读取和写入数据库中。 请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。


在本部分中我们要实现启用我们的应用程序中的输入的验证所需的支持。 我们将确保我们的数据库内容始终是正确的并且它们尝试并输入电影数据无效时向最终用户提供有用的错误消息。 我们将开始将少量验证逻辑添加到电影类。

右键单击模型文件夹并选择添加类。 命名您的类的电影。

当我们在前面创建的电影实体模型时，IDE 将创建 Movie 类。 事实上，可以在一个文件，将在另一部分是电影类的一部分。 这被称为一个分部类。 我们将从另一个文件扩展 Movie 类。

我们将使用将验证提示给系统一些属性，指向"合作者类"创建部分 movie 类。 我们将标记的 Title 和价格为必需的并还坚持的价格为某范围内。 右键单击 Models 文件夹，然后选择添加类。 命名您的类的电影，然后单击确定按钮。 下面是我们部分的 Movie 类如下所示的内容。

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

重新运行你的应用程序并尝试输入的电影价格超过 100。 已提交表单后，将会出错。 错误捕获在服务器端和发送窗体后发生。 请注意如何 ASP.NET MVC 内置 HTML 帮助程序已不够智能，无法显示错误消息和维护为我们在文本框中元素的值：

[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)

这非常有用，但如果我们可以告诉用户在客户端立即获取涉及服务器之前很好。

让我们来启用 JavaScript 与某些客户端验证。

## <a name="adding-client-side-validation"></a>添加客户端验证

由于我们的 Movie 类已具有一些验证特性，我们将只需将几个 JavaScript 文件添加到我们 Create.aspx 视图模板和添加一行代码以启用客户端验证，才能开始。

从内部 VWD 转我们的电影视图/文件夹并打开 Create.aspx。

打开解决方案资源管理器中的脚本文件夹并拖动到中的以下三个脚本&lt;head&gt;标记。

- MicrosoftAjax.js
- MicrosoftMvcValidation.js

你想要按此顺序显示这些脚本文件。

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

此外，添加上述 Html.BeginForm 这一行：

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

下面是在 IDE 中所示的代码。

[![电影-Microsoft Visual Web Developer 2010 速成版 (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)

运行应用程序并再次，访问 /Movies/Create 并单击创建而无需输入任何数据。 错误消息会立即显示没有页面闪存，我们将与相关联发送数据的情况下按原路返回到服务器。 这是因为 ASP.NET MVC 现在验证的输入上 （使用 JavaScript） 的客户端和服务器上。

[![创建的 Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)

这看起来不错 ！ 现在让我们添加一个附加列到数据库。

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part6.md)
> [下一页](getting-started-with-mvc-part8.md)
