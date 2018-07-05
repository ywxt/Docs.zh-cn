---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: 添加控制器 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: be8b21b4b8db60b1a67918d2df8779e729243fc8
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374667"
---
<a name="adding-a-controller"></a>添加控制器
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE [Tutorial Note](sample/code-location.md)]

MVC 代表*模型-视图-控制器*。 MVC 是一种模式用于开发应用程序也设计、 可测试且易于维护。 基于 MVC 的应用程序包含：

- **M**模式： 类，表示数据的应用程序和使用验证逻辑以强制实施针对这些数据的业务规则。
- **V**视图： 应用程序使用动态生成 HTML 响应的模板文件。
- **C**控制器： 处理传入的浏览器请求的类中检索模型数据，然后指定将响应返回到浏览器的视图模板。

我们将进行介绍本系列教程中的所有这些概念并说明如何使用它们来构建应用程序。

> [!NOTE]
> 在上一步默认 MVC 模板被选中。 这将创建主文件夹、 帐户和默认情况下管理控制器。

让我们首先创建一个控制器类。 在中**解决方案资源管理器**，右键单击*控制器*文件夹，然后单击**添加**，然后**控制器**。


![](adding-a-controller/_static/image1.png)

在中**添加基架**对话框中，单击**MVC 5 控制器-空**，然后单击**添加**。

![](adding-a-controller/_static/image2.png)  
 

新控制器命名为"HelloWorldController"，然后单击**添加**。

![添加控制器](adding-a-controller/_static/image3.png)

请注意，在**解决方案资源管理器**的一个新的文件具有已创建的名为*HelloWorldController.cs*和 new folder *Views\HelloWorld*。 控制器已在 IDE 中打开。

![](adding-a-controller/_static/image4.png)

将以下代码替换为该文件的内容。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

控制器方法将返回 HTML 的字符串作为示例。 控制器被命名为`HelloWorldController`和第一种方法名为`Index`。 让我们从浏览器调用它。 运行应用程序 （按 F5 或 Ctrl + F5）。 在浏览器中，追加&quot;HelloWorld&quot;到地址栏中的路径。 (例如，在图中，其下方的`http://localhost:1234/HelloWorld.`) 在浏览器中的页将类似于以下屏幕截图。 在上述方法中，代码直接返回一个字符串。 你告诉系统只返回一些 HTML，并确实执行此操作 ！

![](adding-a-controller/_static/image5.png)

ASP.NET MVC 调用不同的控制器类 （和其中不同的操作方法），具体取决于传入的 URL。 使用 ASP.NET MVC 的默认 URL 路由逻辑使用如下格式来确定哪些代码以调用：

`/[Controller]/[ActionName]/[Parameters]`

设置中的路由的格式*应用程序\_Start/RouteConfig.cs*文件。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

运行应用程序并不提供任何 URL 段，则默认为"Home"控制器，并在上面的代码的 defaults 节中指定"的索引"操作方法。

URL 的第一个部分确定要执行的控制器类。 因此 */HelloWorld*映射到`HelloWorldController`类。 URL 的第二部分确定要执行的类上的操作方法。 因此 */HelloWorld/索引*会导致`Index`方法的`HelloWorldController`类来执行。 请注意，我们只需要浏览到 */HelloWorld*和`Index`默认情况下使用了方法。 这是因为方法命名为`Index`是如果有一个未显式指定调用在控制器的默认方法。 URL 段的第三部分 (`Parameters`) 针对的是路由数据。 在本教程中，我们将更高版本上看到路由数据。

浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。 `Welcome`方法运行并返回字符串&quot;这是 Welcome 操作方法...&quot;. 默认 MVC 映射`/[Controller]/[ActionName]/[Parameters]`。 对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。 目前尚未使用 URL 的 `[Parameters]` 部分。

![](adding-a-controller/_static/image6.png)

让我们这样可以将一些参数信息从 URL 传递给控制器稍微修改一下该示例 (例如， */HelloWorld/欢迎？ 名称 = Scott&amp;numtimes = 4*)。 更改你`Welcome`方法以包括两个参数，如下所示。 请注意，代码使用 C# 可选参数功能指示`numTimes`参数应默认为 1，如果为该参数不传递任何值。

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> 安全说明： 使用上面的代码[HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx)以防止恶意输入 (即 JavaScript) 的应用程序。 有关详细信息请参阅[如何： 保护对脚本攻击在 Web 应用程序通过应用 HTML 编码为字符串](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)。


 运行应用程序并浏览到示例 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`)。 你可以尝试不同的值`name`和`numtimes`在 URL 中。 [ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)会自动将映射到方法中的参数将命名的参数从地址栏中的查询字符串。

![](adding-a-controller/_static/image7.png)

在上面的 URL 段示例 ( `Parameters`) 未使用，则`name`并`numTimes`作为参数传递[查询字符串](http://en.wikipedia.org/wiki/Query_string)。 ?  （问号） 在上述 URL 中为分隔符，并后接查询字符串。 &amp; 字符用于分隔查询字符串。

欢迎使用方法替换为以下代码：

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

运行应用程序并输入以下 URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`

![](adding-a-controller/_static/image8.png)

这一次第三个 URL 段匹配路由参数`ID.``Welcome`操作方法包含一个参数 (`ID`) 的匹配中的 URL 规范`RegisterRoutes`方法。

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

在 ASP.NET MVC 应用程序，它是更常见的做法在作为路由数据 （例如，我们使用上述 ID 所做的那样） 比将其作为查询字符串中传递的参数中传递。 您还可以添加一个路由，同时传递`name`和`numtimes`参数作为 URL 中的路由数据中。 在中*应用程序\_Start\RouteConfig.cs*文件中，添加"Hello"路由：

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

运行应用程序，并浏览到`/localhost:XXX/HelloWorld/Welcome/Scott/3`。

![](adding-a-controller/_static/image9.png)

对于许多 MVC 应用程序的默认路由工作正常。 你将了解在本教程中使用模型联编程序，数据传递更高版本，无需为此，修改默认路由。

在这些示例控制器始终执行&quot;VC&quot;的 MVC 部分 — 即，视图和控制器工作。 控制器将直接返回 HTML。 通常，您不希望控制器直接返回 HTML，因为这会变得非常麻烦的代码。 而是我们通常将使用单独的视图模板文件来帮助生成 HTML 响应。 让我们看如何实现这在下一步。

> [!div class="step-by-step"]
> [上一页](getting-started.md)
> [下一页](adding-a-view.md)
