---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: 介绍如何调试 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: Rick-Anderson
description: 调试是查找并修复错误的代码页中的过程。 本章展示一些工具和技术可用于调试和分析...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: e5302492f01cbd507e0b0fd995f21621bf6f04c8
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021308"
---
<a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a>介绍如何调试 ASP.NET Web Pages (Razor) 站点
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 此文章介绍了调试 ASP.NET Web Pages (Razor) 网站的网页中的各种方法。 调试是查找并修复错误的代码页中的过程。
>
> **你将学习：**
>
> - 如何显示信息，可帮助分析和调试页。
> - 如何使用调试工具在 Visual Studio 中。
>
>
> 下面是在本文中引入的 ASP.NET 功能：
>
> - `ServerInfo`帮助器。
> - `ObjectInfo` 帮助器。
>
>
> ## <a name="software-versions"></a>软件版本
>
>
> - ASP.NET 网页 (Razor) 3
> - Visual Studio 2013
>
>
> 本教程还适用于 ASP.NET Web Pages 2。 可以使用 WebMatrix 3，但不是支持集成的调试器。


错误和代码中的问题故障排除的一个重要方面是在第一时间避免它们。 您可以通过将放有可能导致错误代码的部分实现`try/catch`块。 详细信息，请参阅部分中的错误处理[ASP.NET Web 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=202890)。

`ServerInfo`帮助器是一个诊断工具，可提供有关承载您的页面的 web 服务器环境的信息的概述。 它还显示当请求页面时浏览器发送的 HTTP 请求信息。 `ServerInfo`帮助器将显示当前用户标识，发出请求，浏览器的类型，等等。 此类信息可以帮助您解决常见的问题。

1. 创建一个名为的新 web 页*ServerInfo.cshtml*。
2. 在页面的结束时，只需在关闭前`</body>`标记中，添加`@ServerInfo.GetHtml()`:

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    您可以添加`ServerInfo`代码页中的任意位置。 但将其添加结束时将保留其输出独立于其他页面内容，因此可以轻松地读取。

    > [!NOTE]
    >
    > **重要**网页移到生产服务器之前，您应该从您的 web 页面删除诊断的任何代码。 这适用于`ServerInfo`帮助程序，以及这篇文章涉及将代码添加到页面的其他诊断技术。 因为此类型的信息可能具有恶意企图的人员很有用，您不希望您的网站访问者，以在服务器和类似详细信息，查看有关服务器名称、 用户名、 路径信息。
3. 保存页面，并在浏览器中运行它。

    ![调试-1](introduction-to-debugging/_static/image1.jpg)

    `ServerInfo`帮助程序在页中显示的信息的四个表：

   - 服务器配置。 本部分提供有关在托管的 web 服务器，包括计算机名称、 正在运行的 ASP.NET、 域名和服务器时间的版本信息。
   - ASP.NET 服务器变量。 本部分提供了有关多个 HTTP 协议详细信息 （称为 HTTP 变量） 的详细信息和值是每个网页请求的一部分。
   - HTTP 运行时信息。 本部分提供有关该版本的 Microsoft.NET Framework 下运行您的网页、 路径、 缓存等有关的详细信息的详细信息。 (正如在获知[ASP.NET Web 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=202890)、 ASP.NET Web Pages 使用的 Razor 语法基于 Microsoft 的 ASP.NET web 服务器技术，它本身基于更大的软件开发库中名为.NET Framework。）
   - 环境变量。 本部分提供 web 服务器上的所有本地环境变量及其值的列表。

     所有服务器和请求信息的完整说明不在本文的范围内，但您可以看到，`ServerInfo`帮助程序返回很多诊断信息。 有关详细信息的值的`ServerInfo`返回时，请参阅[识别环境变量](https://technet.microsoft.com/library/dd560744(WS.10).aspx)Microsoft TechNet 网站上并[IIS 服务器变量](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)MSDN 网站上。

## <a name="embedding-output-expressions-to-display-page-values"></a>嵌入输出表达式，以显示页的值

若要查看你的代码中发生的情况的另一种方法是在页面中嵌入输出表达式。 如您所知，可以通过添加类似于直接输出变量的值`@myVariable`或`@(subTotal * 12)`到页。 对于调试，您可以在代码中，在战略点处放置这些输出表达式。 这使您可以在页面运行时查看关键变量或计算结果的值。 完成后调试，可以删除的表达式或它们注释掉。此过程说明了使用嵌入式的表达式来帮助调试页面的典型方式。

1. 创建名为的新 WebMatrix 页*OutputExpression.cshtml*。
2. 将为页面提供以下内容：

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    该示例使用`switch`用于检查的值的语句`weekday`变量，然后显示它是根据一周中的哪一天的不同的输出消息。 在示例中，`if`中第一个代码块的块任意更改通过将一天添加到当前周日期值的日期是星期几。 这是为了便于说明引入了一个错误。
3. 保存页面，并在浏览器中运行它。

    页显示为错误日期是星期几的消息。 任何日期是星期几它实际上是，将看到更高版本的一天内的消息。 尽管这种情况下您知道原因的消息是关闭 （因为代码有意设置不正确的日期值），实际上通常很难知道操作会在代码中的错误。 若要调试，您需要找出发生了什么情况的主要对象和变量的值如`weekday`。
4. 添加输出表达式的方法是插入`@weekday`两个位置由代码中的注释中所示。 这些输出表达式将显示变量的值在该点在执行代码。

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. 保存并运行在浏览器中的页。

    页面显示实际日期是星期几第一次，然后将结果从一天，然后从生成的消息中添加的更新日期是星期几`switch`语句。 两个变量表达式的输出 (`@weekday`) 具有天之间没有空格，因为您没有添加任何 HTML`<p>`到输出; 标记的表达式是仅用于测试。

    ![调试 2](introduction-to-debugging/_static/image2.jpg)

    现在，可以看到错误的位置。 当你首次显示`weekday`变量在代码中，它显示正确的天。 显示时其第二次之后,`if`块在代码中，一天处于关闭状态的一个。 因此，您知道工作日变量的第一个和第二个外观之间发生了一些事情。 如果这是一个真正的 bug，这种方法可帮助你缩小问题的原因的代码的位置。
6. 删除你添加的两个输出表达式以及删除更改日期是星期几的代码页中修复代码。 剩余的完整的代码块如以下示例所示：

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. 在浏览器中运行页。 此时会显示正确的消息显示实际日期是星期几。

## <a name="using-the-objectinfo-helper-to-display-object-values"></a>使用 ObjectInfo 帮助器来显示对象的值

`ObjectInfo`帮助器显示类型和每个对象将传递给它的值。 可用来在代码中 （例如，您使用在前面的示例输出表达式所做的那样），查看变量和对象的值加上可以看到的数据类型有关对象的信息。

1. 打开名为的文件*OutputExpression.cshtml*之前创建。
2. 页面中的所有代码都替换为以下代码块：

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. 保存并运行在浏览器中的页。

    ![调试 4](introduction-to-debugging/_static/image3.jpg)

    在此示例中，`ObjectInfo`帮助器将显示两个项：

   - 类型。 对于第一个变量，该类型是`DayOfWeek`。 对于第二个变量，该类型是`String`。
   - 值。 在这种情况下，你已在页中显示的问候语变量的值，因为值再次显示时将传递到变量`ObjectInfo`。

     对于更复杂的对象，`ObjectInfo`帮助器可以显示详细信息&#8212;基本上，它可以显示的类型和所有对象的属性的值。

## <a name="using-debugging-tools-in-visual-studio"></a>使用 Visual Studio 中调试工具

对于更全面的调试体验，使用[Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。 使用 Visual Studio 中，可以在代码中你想要检查的代码行处设置断点。

![设置断点](introduction-to-debugging/_static/image1.png)

测试网站时，正在执行的代码都将在断点处暂停。

![到达断点](introduction-to-debugging/_static/image2.png)

您可以检查变量和单步执行代码--逐行的当前值。

![请参阅值](introduction-to-debugging/_static/image3.png)

有关使用 Visual Studio 中集成的调试器来调试 ASP.NET Razor 页的信息，请参阅[编程 ASP.NET Web Pages (Razor) 使用 Visual Studio](https://go.microsoft.com/fwlink/?LinkId=205854)。

## <a name="additional-resources"></a>其他资源

- [编程使用 Visual Studio 的 ASP.NET Web Pages (Razor)](https://go.microsoft.com/fwlink/?LinkId=205854)
- [IIS 服务器变量](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)(MSDN)
- [识别环境变量](https://technet.microsoft.com/library/dd560744(WS.10).aspx)(TechNet)
