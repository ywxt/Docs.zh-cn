---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: 创建 JavaScript 客户端 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 4967e21190c34f698e9c28fd9b921f07bef2ffaf
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834947"
---
<a name="create-the-javascript-client"></a>创建 JavaScript 客户端
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](https://github.com/MikeWasson/BookService)

在本部分中，您将创建使用 HTML、 JavaScript 的客户端应用程序，并[Knockout.js](http://knockoutjs.com/)库。 我们将分阶段构建客户端应用程序：

- 显示书籍的列表。
- 显示某个通讯簿的详细信息。
- 添加新书籍。

Knockout 库使用模型-视图-视图模型 (MVVM) 模式：

- **模型**（在我们的用例、 书籍和作者） 的业务域中的数据的服务器端表示形式。
- **视图**是表示层 (HTML)。
- **视图模型**是用于保存模型的 JavaScript 对象。 视图模型是在 ui 的代码抽象。 它并不知道 HTML 表示形式。 相反，它表示抽象功能的视图，如&quot;书籍列表&quot;。

该视图是数据绑定到视图模型。 向视图模型的更新会自动反映在视图中。 视图模型还获取事件从视图中，如按钮单击。

![](part-6/_static/image1.png)

这种方法轻松更改布局和 UI 的应用，因为您可以更改绑定，无需重新编写任何代码。 例如，可能显示的项作为列表`<ul>`，然后稍后将其更改为一个表。

## <a name="add-the-knockout-library"></a>添加 Knockout 库

在 Visual Studio 中，从**工具**菜单中，选择**库程序包管理器**。 然后选择**程序包管理器控制台**。 在包管理器控制台窗口中，输入以下命令：

[!code-console[Main](part-6/samples/sample1.cmd)]

此命令将 Knockout 文件添加到脚本文件夹中。

## <a name="create-the-view-model"></a>创建视图模型

添加名为脚本文件夹的 app.js 的 JavaScript 文件。 (在解决方案资源管理器中右键单击脚本文件夹中，选择**外**，然后选择**JavaScript 文件**。)粘贴以下代码：

[!code-javascript[Main](part-6/samples/sample2.js)]

在 Knockout，`observable`类使数据绑定。 当一个可观测对象的内容发生变化时，可观察对象以便他们能够更新本身通知的所有数据绑定控件。 (`observableArray`类是数组新版*可观察量*。)开始时，我们的视图模型具有两个可观察量：

- `books` 保存书籍列表。
- `error` 如果 AJAX 调用失败，则包含一条错误消息。

`getAllBooks`方法通过 AJAX 调用来获取的书籍列表。 然后它会将推送到结果`books`数组。

`ko.applyBindings`方法是 Knockout 库的一部分。 它将作为参数的视图模型，并设置数据绑定。

## <a name="add-a-script-bundle"></a>添加脚本捆绑包

捆绑是一项功能 ASP.NET 4.5，轻松地组合或多个文件捆绑到一个文件中。 绑定可以请求数减少到服务器，这可以提高页面加载时间。

打开文件应用\_Start/BundleConfig.cs。 将以下代码添加到 RegisterBundles 方法。

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> [上一页](part-5.md)
> [下一页](part-7.md)
