---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: 添加视图 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: e3b923aa5572781261c5a75546700faf223703d4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37834499"
---
<a name="adding-a-view"></a>添加视图
====================
通过[Scott Hanselman](https://github.com/shanselman)

> 这是介绍 ASP.NET MVC 的基础知识初学者教程。 将创建一个简单的 web 应用程序读取和写入数据库中。 请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。


在本部分中我们要看看如何可以让我们使用视图模板文件来完全封装生成 HTML 响应返回给客户端的 HelloWorldController 类。

让我们首先我们 Index 方法中使用视图模板。 我们的方法称为索引，处于 HelloWorldController。 当前我们 index （） 方法返回具有一条消息，是控制器类中的进行硬编码的字符串。

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

让我们现在更改 Index 方法，以改为如下所示：

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

现在让我们添加一个视图模板对项目，我们可以使用我们的 index （） 方法。 若要执行此操作，使用某处的中间索引方法鼠标右键单击，然后单击添加视图...

![图像](getting-started-with-mvc-part3/_static/image1.png)

这将显示"添加视图"对话框，这为我们提供了一些我们想要创建可由我们 Index 方法的视图模板的选项。 现在，不更改任何内容，并只需单击添加按钮。

[![添加视图对话框](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)

单击添加后，新的文件夹和一个新文件将显示在解决方案文件夹中，如下所示。 我现在有在该文件夹的视图和 Index.aspx 文件下的 HelloWorld 文件夹。

[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)

新索引文件也是已打开并可供编辑。 添加一些文本下第一个&lt;h2&gt;索引&lt;/h2&gt;像"Hello World"。

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

运行应用程序并访问[ `http://localhost:xx/HelloWorld` ](http://localhostxx)再次在浏览器中。 在此示例中我们控制器中的索引方法不执行任何操作，但未调用"返回 View()"，这表示我们想要使用视图模板文件来呈现响应返回给客户端。 因为我们未显式指定要使用的视图模板文件的名称，ASP.NET MVC 默认使用 \Views\HelloWorld 文件夹中的 Index.aspx 视图文件。 现在我们看到我们硬编码在视图中的字符串。

[![索引的 Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)

看起来相当棒。 但是，请注意，浏览器的标题显示"Index"，并在页上的大标题显示"我 MVC 应用程序。" 让我们将这些更改。

### <a name="changing-views-and-master-pages"></a>更改视图和母版页

首先，让我们来更改文本"我 MVC 应用程序。" 该文本共享，并显示在每一页。 它实际显示只能在一个位置，在代码中，即使它是在我们的应用程序中每一页上。 转到解决方案资源管理器中的 /Views/Shared 文件夹并打开 Site.Master 文件。 此文件称为母版页，它是共享的"shell"，使用它我们其他所有页。

请注意在此文件中，显示 ContentPlaceholder"主要内容"一些文本。

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

该占位符是其中创建的所有页会都显示，"包装"在母版页中。 请尝试更改标题，然后运行您的应用程序并访问多个页面。 您会发现一次更改会出现在多个页面。

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

现在，每个页面将使用的主标题-这就是 H1-"我的 MVC 影片应用程序。" 用于处理在那里共享跨所有页面顶部的白色文本。

下面是 Site.Master 中完整地与我们更改了标题：

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

现在，让我们来更改索引页面的标题。

打开 /HelloWorld/Index.aspx。 没有两个位置更改。 首先，标题中显示的浏览器中，然后辅助标头的也是 H2 的标题。 我将它们分别略有不同，以便你可以查看哪一段代码将更改应用程序的哪个部分。

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

运行你的应用并访问 /Movies。 请注意，浏览器标题、 主标题和辅助标题已更改。 很容易地对视图使用较小的更改在应用程序进行重大更改。

[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)

我们这一点点"数据"（在此情况下的"Hello World"！ 消息） 是硬编码不过。 我们有 V （视图），我们有 C （控制器），但尚无的 M （模型）。 我们稍后将演示如何创建数据库并从它检索模型数据。

## <a name="passing-a-viewmodel"></a>传递 ViewModel

我们转到数据库，并讨论模型之前，不过，我们首先讨论一下"Viewmodel"。 这些是代表要呈现的 HTML 响应返回给客户端的视图模板需要的对象。 它们通常会创建并由控制器类传递给视图模板，并且应只包含视图模板所需的数据而没有更。

以前我们 HelloWorld 示例中，我们 Welcome() 操作方法花费了名称和 numTimes 参数，其输出到浏览器。 而不是必须继续直接将此响应呈现的控制器，而是让一个小型类来存放该数据，并将它给用于呈现回 HTML 响应使用它的视图模板。 这样控制器涉及到一件事和查看模板另一个 – 使我们能够保持干净"关注点分离"我们的应用程序中。

返回到 HelloWorldController.cs 文件并添加一个新的"WelcomeViewModel"类并更改你的控制器内的欢迎使用方法。 下面是完整的 HelloWorldController.cs 使用同一个文件中的新类。

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

即使是在多个行，我们欢迎方法实际上是只有两个代码语句。 第一条语句设置到的 ViewModel 对象，并在第二个阶段的两个参数打包到视图上生成的对象。

现在，我们需要 Welcome 视图模板 ！ 在欢迎使用方法中右键单击并选择添加视图。 这一次，我们将检查"创建强类型视图"，并从下拉列表中选择我们 WelcomeViewModel 类。 此新视图将只知道 WelcomeViewModels 和任何其他类型的对象。

> *注意： 需要将已编译的添加为你 WelcomeViewModel 才会显示在下拉列表中后，一次。*


下面是添加视图对话框应如下所示。 单击添加按钮。 ![添加视图标有圆圈](getting-started-with-mvc-part3/_static/image10.png)

下添加此代码&lt;h2&gt;新 Welcome.aspx 中。 我们将进行循环，并根据用户所说我们应多次说 Hello ！

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

另请注意，虽然你输入这些内容因为我们告诉过这有关 WelcomeViewModel 视图 （已婚，记得吗？） 我们获取有帮助的 Intellisense 每次我们引用我们在下面的屏幕截图中显示的模型对象：

[![NumTime 源代码](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)

运行应用程序并访问`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`试。 现在，我们将数据从该 URL，它自动传递到我们的控制器、 控制器打包到 ViewModel 数据并将传递到视图上的该对象。 不是以 HTML 的形式向用户显示数据视图。

[![欢迎-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)

当然，这是一种类型的"M"的模型，但不是数据库类。 我们来看，我们已了解并创建一个电影数据库。

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part2.md)
> [下一页](getting-started-with-mvc-part4.md)
