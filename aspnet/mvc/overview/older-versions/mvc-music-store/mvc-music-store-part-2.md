---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 第 2 部分： 控制器 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 2 部分介绍了控制器。
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 8824d5d2f5670aee2df6dc6e74767e4a851dd4ae
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37841090"
---
<a name="part-2-controllers"></a>第 2 部分： 控制器
====================
通过[Jon Galloway](https://github.com/jongalloway)

> MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。  
>   
> MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。  
>   
> 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 2 部分介绍了控制器。


与传统的 web 框架，传入的 Url 通常映射到磁盘上的文件中。 例如： 所示的请求 url"/ Products.aspx"或"/ Products.php"可能会处理由"Products.aspx"或"Products.php"文件。

基于 web 的 MVC 框架将 Url 映射到服务器代码中以略有不同的方式。 而不是将传入 Url 映射到文件，它们而是将 Url 映射到类上的方法。 这些类称为"控制器"和要负责处理传入的 HTTP 请求，处理用户输入、 检索和保存数据，并确定要发送的响应返回给客户端 （显示 HTML、 下载文件，将重定向到不同URL 等）。

## <a name="adding-a-homecontroller"></a>添加一个 HomeController

我们将首先我们 MVC Music 商店的应用程序添加到我们的站点的主页将处理 Url 的控制器类。 我们将遵循 ASP.NET MVC 的默认命名约定，并调用其 HomeController。

右键单击解决方案资源管理器中的"控制器"文件夹，然后选择"添加"，然后单击"控制器..."命令：

![](mvc-music-store-part-2/_static/image1.jpg)

这将显示"添加控制器"对话框。 控制器"HomeController"命名，然后按添加按钮。

![](mvc-music-store-part-2/_static/image1.png)

这将创建一个新文件，HomeController.cs 中，使用以下代码：

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

若要启动尽可能简单地，让我们来替换 Index 方法仅返回字符串的简单方法。 我们将执行两项更改：

- 更改此方法返回一个字符串而不是 ActionResult
- 更改要返回"Hello 从主页"的返回语句

该方法现在应如下所示：

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a>运行应用程序

现在让我们运行该站点。 我们可以开始我们的 web 服务器并尝试使用任何以下站点::

- 选择调试 ⇨ 启动调试菜单项
- 单击工具栏中的绿色箭头按钮 ![](mvc-music-store-part-2/_static/image2.jpg)
- 使用键盘快捷方式，F5。

使用任何上述步骤将编译我们的项目，并引起是内置于 Visual Web Developer 启动 ASP.NET 开发服务器。 通知会在以指示 ASP.NET Development Server 已启动，屏幕的底部角中，将显示的端口号下运行。

![](mvc-music-store-part-2/_static/image2.png)

Visual Web Developer 会自动打开浏览器窗口中的 URL 指向我们的 web 服务器。 这将使我们可以快速试用我们的 web 应用程序：

![](mvc-music-store-part-2/_static/image3.png)

嗯，这是很快捷 – 我们创建一个新网站，添加三个行函数，并且我们在浏览器中有文本。 不特别复杂，但它是一个开始。

*注意： Visual Web Developer 包括 ASP.NET 开发服务器，这将在一个随机免费"端口"号上运行你的网站。在上面的屏幕截图中的网站运行在`http://localhost:26641/`，因此它正在使用端口 26641。端口号将不同。当我们谈及 URL 的 like /Store/Browse 本教程中时，，将投入的端口号。假设 26641 端口号，浏览到/Store/浏览将意味着浏览到`http://localhost:26641/Store/Browse`。*

## <a name="adding-a-storecontroller"></a>添加 StoreController

我们添加了一个简单的 HomeController 实现我们的站点的主页。 现在让我们添加另一个控制器，我们将使用实现我们音乐应用商店的浏览功能。 存储控制器将支持三种方案：

- 在我们的音乐应用商店音乐流派列表页
- 列出所有特定流派音乐 album 的浏览页面
- 显示有关特定音乐唱片集信息的详细信息页

我们将首先添加一个新的 StoreController 类... 如果尚未安装，请停止正在运行的应用程序或者通过关闭浏览器选择调试 ⇨ 停止调试菜单项。

现在，添加新 StoreController。 就像我们一样 HomeController，我们将执行此操作通过右键单击解决方案资源管理器中的"控制器"文件夹，然后选择添加-&gt;控制器菜单项

![](mvc-music-store-part-2/_static/image4.png)

我们新 StoreController 已具有一个"索引"方法。 我们将使用此"Index"方法来实现我们列出了我们在音乐应用商店中的所有类型的列表页面。 我们还将添加两个其他的方法来实现两种情况下我们想要以处理我们 StoreController： 浏览和详细信息。

我们的控制器中的这些方法 （索引、 浏览和详细信息） 称为"控制器操作"，如您所见与 HomeController.Index （） 操作方法，它们的作用是响应 URL 请求，并 （通常情况下） 确定哪些内容应发送回浏览器或调用 URL 的用户。

我们通过更改 theIndex() 方法以返回字符串"Hello 从 Store.Index()"启动我们 StoreController 的实现，并且我们将为 browse （） 和 Details() 添加类似的方法：

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

再次运行该项目，并浏览以下 Url:

- / 存储
- / Store/浏览
- / 存储/详细信息

访问这些 Url 将调用我们的控制器内的操作方法并返回字符串响应：

![](mvc-music-store-part-2/_static/image5.png)

那太好了，但它们是只是常量字符串。 让我们来使这些动态的因此它们从 URL 中获取信息并将其显示在页面输出中。

首先，我们将更改浏览操作方法来检索该 URL 的查询字符串值。 我们可以通过将"genre"参数添加到我们的操作方法来执行此操作。 当我们执行此操作 ASP.NET MVC 将自动传递名为"genre"到我们的操作方法，在调用时任何查询字符串或窗体 post 参数。

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

*注意： 我们使用 HttpUtility.HtmlEncode 实用程序方法来清理用户输入。这可以防止用户与 /Store/Browse 形式的链接将 Javascript 注入到视图？Genre =&lt;脚本&gt;window.location = 'http://hackersite.com'&lt;/script&gt;。*

现在让我们浏览到/Store/浏览？Genre = Disco

![](mvc-music-store-part-2/_static/image6.png)

让我们下一次更改要读取并显示输入的参数的详细信息操作名为 id。 与我们前面的方法，我们不会为嵌入的 ID 值作为查询字符串参数。 而是我们会将其嵌入直接在 URL 本身中。 例如： /Store/Details/5。

ASP.NET MVC 可以让我们轻松执行此操作而无需进行任何配置。 ASP.NET MVC 的默认路由约定是操作方法名称后的 URL 的段视为名为"ID"的参数。 如果你操作的方法有一个名为 ID 参数则 ASP.NET MVC 将自动传递 URL 段向你作为参数。

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

运行应用程序并浏览到 /Store/Details/5:

![](mvc-music-store-part-2/_static/image7.png)

让我们回顾一下到目前为止我们所做:

- 我们已在 Visual Web Developer 中创建新的 ASP.NET MVC 项目
- 我们已经讨论了 ASP.NET MVC 应用程序的基本文件夹结构
- 我们已了解如何运行我们的网站使用 ASP.NET 开发服务器
- 我们已经创建了两个控制器类： 一个 HomeController 和 StoreController
- 我们为我们控制器的响应 URL 请求并返回到浏览器的文本添加了操作方法


> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-1.md)
> [下一页](mvc-music-store-part-3.md)
