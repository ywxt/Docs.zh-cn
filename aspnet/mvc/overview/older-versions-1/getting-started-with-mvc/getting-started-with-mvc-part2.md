---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 添加控制器 |Microsoft Docs
author: shanselman
description: 如果本教程是此处使用 Visual Studio 2013 提供更新的版本。 新教程使用 ASP.NET MVC 5，可获得许多改进通过 t...
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: 9a8ecac5203234c140783bbe3a518d35f6a57675
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48910773"
---
<a name="adding-a-controller"></a>添加控制器
====================
通过[Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > 如果本教程中可用的更新的版本[这里](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)。 新教程使用 ASP.NET MVC 5，通过本教程提供了许多改进。
>
>
> 这是介绍 ASP.NET MVC 的基础知识初学者教程。 将创建一个简单的 web 应用程序读取和写入数据库中。 请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。


MVC 代表模型、 视图、 控制器。 MVC 是一种模式用于开发应用程序，从而使每个部分具有不同于另一个是责任。

- 数据的应用程序模型：
- 视图： 应用程序将使用动态生成 HTML 响应模板文件。
- 控制器： 处理应用程序，传入 URL 请求的类中检索模型数据，然后指定将响应返回给客户端呈现的视图模板

我们将在本教程中介绍所有这些概念并说明如何使用它们来构建应用程序。

右键单击解决方案资源管理器中的 controllers 文件夹并选择添加控制器，让我们创建一个新的控制器。

[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)

新控制器"HelloWorldController"命名，并单击添加。

[![添加控制器对话框](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)

请注意，在解决方案资源管理器中，已为您调用 HelloWorldController.cs 创建一个新文件并在现在打开该文件在右侧**IDE**。

[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)

创建在您的新公共类 HelloWorldController 如下所示的两个新方法。 作为示例，我们将直接从控制器返回 HTML 的字符串。

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

将控制器命名为 HelloWorldController 和新方法调用索引。 在再次运行应用程序，可以像以前一样 （单击播放按钮或按 f5 键以执行此操作）。 一旦你的浏览器已启动，更改到的地址栏中的路径`http://localhost:xx/HelloWorld`其中 xx 是任何数字在计算机已选。 现在你的浏览器应如下面的屏幕截图所示。 我们在上面我们方法返回的字符串传递到一个名为"内容"。 方法 我们告诉过系统只返回一些 HTML，并确实执行此操作 ！

ASP.NET MVC 调用不同的控制器类 （和其中不同的操作方法），具体取决于传入的 URL。 使用 ASP.NET MVC 的默认映射逻辑使用如下格式来控制运行的代码：

/[Controller]/[ActionName]/[Parameters]

URL 的第一个部分确定要执行的控制器类。 因此 /HelloWorld 将映射到 HelloWorldController 类。 URL 的第二部分确定要执行的类上的操作方法。 /HelloWorld/Index 时会导致 HelloWorldcontroller 类执行的 index （） 方法。 请注意，我们只需要访问上述 /HelloWorld 和表示为索引的方法。 这是因为名为"Index"的方法是如果有一个未显式指定调用在控制器的默认方法。

[![这是我的默认操作](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)

现在，我们来访问`http://localhost:xx/HelloWorld/Welcome.`现在我们的欢迎使用方法已执行并返回其 HTML 字符串。

同样，/ [Controller] / [ActionName] / [参数]，因此控制器是 HelloWorld，欢迎在这种情况下是该方法。 我们还没有这样的参数。

[![这是 Welcome 操作方法](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)

让我们这样我们可以将中的一些信息从 URL 中传递给我们的控制器，例如如下稍微修改一下我们的示例: / HelloWorld/欢迎？ 名称 = Scott&amp;numtimes = 4。 更改欢迎使用方法，以包括两个参数和与下面类似的更新。 请注意，我们已使用 C# 可选参数功能指示是否它未传入参数 numTimes 应默认为 1。

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

运行应用程序并访问`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`根据需要更改名称和 numtimes 的值。 系统会自动映射到方法中的参数将命名的参数从查询字符串的地址栏中。

在这些示例中这两个控制器已执行所有操作，并具有已直接返回 HTML。 通常我们不希望我们控制器直接-返回 HTML，因为结束的代码非常繁琐。 而是我们通常将使用单独的视图模板文件来帮助生成 HTML 响应。 让我们看看如何我们可以执行此操作。 关闭浏览器并返回到 IDE。

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part1.md)
> [下一页](getting-started-with-mvc-part3.md)
