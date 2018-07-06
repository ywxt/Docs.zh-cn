---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: 添加控制器 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: aspnetcontent
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: b9ba4336b2239d835b648b82674bd4cfa8ca43dc
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809029"
---
<a name="adding-a-controller"></a>添加控制器
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。


MVC 代表*模型-视图-控制器*。 MVC 是一种模式用于开发应用程序也设计、 可测试且易于维护。 基于 MVC 的应用程序包含：

- **M**模式： 类，表示数据的应用程序和使用验证逻辑以强制实施针对这些数据的业务规则。
- **V**视图： 应用程序使用动态生成 HTML 响应的模板文件。
- **C**控制器： 处理传入的浏览器请求的类中检索模型数据，然后指定将响应返回到浏览器的视图模板。

我们将进行介绍本系列教程中的所有这些概念并说明如何使用它们来构建应用程序。

让我们首先创建一个控制器类。 在中**解决方案资源管理器**，右键单击*控制器*文件夹，然后选择**添加控制器**。

![](adding-a-controller/_static/image1.png)

新控制器命名&quot;HelloWorldController&quot;。 将保留为默认模板**空 MVC 控制器**然后单击**添加**。

![添加控制器](adding-a-controller/_static/image2.png)

请注意，在**解决方案资源管理器**的一个新的文件具有已创建的名为*HelloWorldController.cs*。 该文件是在 IDE 中打开。

![](adding-a-controller/_static/image3.png)

将以下代码替换为该文件的内容。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

控制器方法将返回 HTML 的字符串作为示例。 控制器被命名为`HelloWorldController`和更高版本的第一个方法命名为`Index`。 让我们从浏览器调用它。 运行应用程序 （按 F5 或 Ctrl + F5）。 在浏览器中，追加&quot;HelloWorld&quot;到地址栏中的路径。 (例如，在图中，其下方的`http://localhost:1234/HelloWorld.`) 在浏览器中的页将类似于以下屏幕截图。 在上述方法中，代码直接返回一个字符串。 你告诉系统只返回一些 HTML，并确实执行此操作 ！

![](adding-a-controller/_static/image4.png)

ASP.NET MVC 调用不同的控制器类 （和其中不同的操作方法），具体取决于传入的 URL。 使用 ASP.NET MVC 的默认 URL 路由逻辑使用如下格式来确定哪些代码以调用：

`/[Controller]/[ActionName]/[Parameters]`

URL 的第一个部分确定要执行的控制器类。 因此 */HelloWorld*映射到`HelloWorldController`类。 URL 的第二部分确定要执行的类上的操作方法。 因此 */HelloWorld/索引*会导致`Index`方法的`HelloWorldController`类来执行。 请注意，我们只需要浏览到 */HelloWorld*和`Index`默认情况下使用了方法。 这是因为方法命名为`Index`是如果有一个未显式指定调用在控制器的默认方法。

浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。 `Welcome`方法运行并返回字符串&quot;这是 Welcome 操作方法...&quot;. 默认 MVC 映射`/[Controller]/[ActionName]/[Parameters]`。 对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。 目前尚未使用 URL 的 `[Parameters]` 部分。

![](adding-a-controller/_static/image5.png)

让我们这样可以将一些参数信息从 URL 传递给控制器稍微修改一下该示例 (例如， */HelloWorld/欢迎？ 名称 = Scott&amp;numtimes = 4*)。 更改你`Welcome`方法以包括两个参数，如下所示。 请注意，代码使用 C# 可选参数功能指示`numTimes`参数应默认为 1，如果为该参数不传递任何值。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

运行应用程序并浏览到示例 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。 你可以尝试不同的值`name`和`numtimes`在 URL 中。 [ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)会自动将映射到方法中的参数将命名的参数从地址栏中的查询字符串。

![](adding-a-controller/_static/image6.png)

在这些示例中这两个控制器始终执行&quot;VC&quot;的 MVC 部分 — 即，视图和控制器工作。 控制器将直接返回 HTML。 通常，您不希望控制器直接返回 HTML，因为这会变得非常麻烦的代码。 而是我们通常将使用单独的视图模板文件来帮助生成 HTML 响应。 让我们看如何实现这在下一步。

> [!div class="step-by-step"]
> [上一页](intro-to-aspnet-mvc-4.md)
> [下一页](adding-a-view.md)
