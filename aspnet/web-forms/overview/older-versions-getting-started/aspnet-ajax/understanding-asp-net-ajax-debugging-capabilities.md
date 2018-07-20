---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
title: 了解 ASP.NET AJAX 调试功能 |Microsoft Docs
author: scottcate
description: 调试代码的能力是每个开发人员应具有其无论他们使用的技术库中的一项技能。 虽然许多开发人员...
ms.author: aspnetcontent
ms.date: 03/28/2008
ms.assetid: 7f9380c6-19f7-4c82-a019-916ec6dffc9c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
msc.type: authoredcontent
ms.openlocfilehash: 9d420a41f50d06541d04a1dd3cb78a2e6beaaa9a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37813823"
---
<a name="understanding-aspnet-ajax-debugging-capabilities"></a>了解 ASP.NET AJAX 调试功能
====================
通过[Scott Cate](https://github.com/scottcate)

[下载 PDF](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial06_Debugging_MS_Ajax_Applications_cs.pdf)

> 调试代码的能力是每个开发人员应具有其无论他们使用的技术库中的一项技能。 尽管许多开发人员习惯于使用 Visual Studio.NET 或 Web Developer 速成版来调试使用 VB.NET 或 C# 代码的 ASP.NET 应用程序，一些不知道它还是对于调试 JavaScript 之类的客户端的代码非常有用。 此外可以对启用了 AJAX 的应用程序和更多专门的 ASP.NET AJAX 应用程序应用相同类型的用于调试.NET 应用程序的技术。


## <a name="debugging-aspnet-ajax-applications"></a>调试 ASP.NET AJAX 应用程序

Dan Wahlin

调试代码的能力是每个开发人员应具有其无论他们使用的技术库中的一项技能。 不用说了解可用的不同调试选项可保存时间在很大程度上一个项目，并甚至可能是几个方面的麻烦问题。 尽管许多开发人员习惯于使用 Visual Studio.NET 或 Web Developer 速成版来调试使用 VB.NET 或 C# 代码的 ASP.NET 应用程序，一些不知道它还是对于调试 JavaScript 之类的客户端的代码非常有用。 此外可以对启用了 AJAX 的应用程序和更多专门的 ASP.NET AJAX 应用程序应用相同类型的用于调试.NET 应用程序的技术。

在本文中将了解如何使用 Visual Studio 2008 和多种其他工具来调试 ASP.NET AJAX 应用程序来快速查找 bug 和其他问题。 这一讨论将包括有关启用 Internet Explorer 6 或更高的调试、 使用 Visual Studio 2008 和脚本资源管理器来单步执行代码，以及使用其他免费工具，如 Web Development Helper 的信息。 此外将了解如何调试 ASP.NET AJAX 应用程序在 Firefox 中使用扩展名为 Firebug 这样逐句通过直接在浏览器而无需任何其他工具中的 JavaScript 代码。 最后，将向你介绍，可帮助各种调试任务，如跟踪和代码断言语句与 ASP.NET AJAX 库中的类。

在尝试调试在 Internet Explorer 中查看的页之前有几个基本步骤都需要执行以启用调试。 让我们看看需要为开始执行一些基本安装程序要求。

## <a name="configuring-internet-explorer-for-debugging"></a>为调试配置 Internet 资源管理器

大多数人不感兴趣使用 Internet Explorer 查看网站上遇到 JavaScript 问题存在。 事实上，一般用户并不知道要执行的操作如果他们看到一条错误消息。 因此，默认情况下，在浏览器中的关闭状态是调试选项。 但是，它是非常简单，要启用调试，并将其用于开发新的 AJAX 应用程序。

若要启用调试功能，请转到 Internet 资源管理器菜单上的工具 Internet 选项并选择高级选项卡。内的浏览部分中，请确保各项是未选中状态：

- 禁用脚本调试 (Internet Explorer)
- 禁用脚本调试 （其他）

尽管不是必需的如果想要调试的应用程序，你可能想要立即为可见和明显的页中的任何 JavaScript 错误。 您可以强制所有错误都以一个消息框显示的"显示关于每个脚本错误的通知"复选框。 虽然这是一个很好的选项，若要在开发应用程序时启用，它可以很快就会令人讨厌如果由于遇到 JavaScript 错误的可能性是相当好只需仔细阅读其他网站。

已针对调试正确配置后，应查看图 1 显示了哪些 Internet Explorer 高级对话框。


[![为调试配置 Internet Explorer。](understanding-asp-net-ajax-debugging-capabilities/_static/image2.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image1.png)

**图 1**： 适用于调试配置 Internet Explorer。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-debugging-capabilities/_static/image3.png))


调试具有已启用后，您将看到显示在名为脚本调试器视图菜单中的新菜单项。 在下一条语句，它具有两个选项可包括打开和中断。 打开所选时将提示您若要调试 Visual Studio 2008 （请注意，Visual Web Developer 速成版还可用于调试） 中的页。 如果当前运行 Visual Studio.NET，则可以选择使用该实例或创建新实例。 选择下一个语句处中断时将提示您若要执行的 JavaScript 代码时调试页。 如果在页面的 onLoad 事件中执行的 JavaScript 代码可以刷新页面以触发调试会话。 如果在单击按钮之后运行的 JavaScript 代码然后单击该按钮后立即时，调试器将运行。

> *> [!NOTE] 如果运行 Windows Vista 与用户访问控制 (UAC) 启用，并且必须设置为以管理员身份运行 Visual Studio 2008，Visual Studio 将无法附加到进程，当系统提示要附加。若要解决此问题，首先，启动 Visual Studio，并使用该实例来调试。*


已打开的页和你想要更全面检查时，尽管在下一节将演示如何调试 ASP.NET AJAX 页面直接从 Visual Studio 2008 中的，使用 Internet Explorer 脚本调试器选项非常有用。

## <a name="debugging-with-visual-studio-2008"></a>使用 Visual Studio 2008 进行调试

Visual Studio 2008 提供了世界各地的开发人员依赖于每天为调试.NET 应用程序的调试功能。 内置调试器可以单步执行代码，对象数据，对于特定变量，请观看监视调用堆栈以及其他更多的视图。 除了调试 VB.NET 或 C# 代码时，调试器也会有所帮助，用于调试 ASP.NET AJAX 应用程序，并将允许您通过 JavaScript 代码逐行单步。 按照焦点可用于调试客户端脚本文件，而不是无需提供的调试使用 Visual Studio 2008 的应用程序的完整过程论文的技术详细信息。

可以通过多种方法启动的调试 Visual Studio 2008 中的页的过程。 首先，您可以使用在上一部分中所述的 Internet 资源管理器脚本调试程序选项。 这适用于已在浏览器中加载页面并想要开始调试它。 或者，可以右键单击解决方案资源管理器中的.aspx 页，并从菜单中选择设为起始页。 如果您习惯于调试 ASP.NET 页然后您以前可能编写过此。 按 F5 后可以调试页面。 但是，通常可以任意位置设置断点时您希望在 VB.NET 或 C# 代码中，并不总是与 JavaScript 的情况正如您看到下一步。

*与外部脚本嵌入*

Visual Studio 2008 调试器将 JavaScript 嵌入在页不同于外部 JavaScript 文件中。 使用外部脚本文件，可以打开文件并在您选择的任意行上设置断点。 可以通过单击代码编辑器窗口左侧的灰色栏区域中设置断点。 当 JavaScript 嵌入直接到页使用`<script>`不会选择使用标记，通过单击灰色的送纸器区域中设置断点。 尝试在嵌入的脚本行上设置断点将导致警告:"这不是断点的有效位置"。

可以通过将代码移到外部.js 文件并引用它使用的 src 属性来避开此问题&lt;脚本&gt;标记：


[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample1.html)]

如果将代码移到外部文件不会选择或需要比它更多的工作是值得？ 尽管无法设置断点使用编辑器，可以添加直接在你想要开始调试的代码的调试器语句。 您还可以使用 ASP.NET AJAX 库中 Sys.Debug 类可强制调试启动。 您将了解有关本文中稍后介绍的 Sys.Debug 类的详细信息。

使用的示例`debugger`关键字在列表 1 中所示。 此示例将强制使调试器中断正确进行对 update 函数的调用之前。

**代码清单 1。使用调试器关键字来强制 Visual Studio.NET 调试器中断。**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample2.js)]

只要点击该调试程序语句，将提示您调试使用 Visual Studio.NET 的页面，可以开始单步执行代码。 执行此，你可能会遇到访问 ASP.NET AJAX 库脚本文件，因此，让我们使用的页中出现问题时看一看使用 Visual Studio。NET 的脚本资源管理器。

## <a name="using-visual-studio-net-windows-to-debug"></a>使用 Visual Studio.NET Windows 调试

一旦启动调试会话并开始通过使用默认 F11 键代码的每个步骤，可能会遇到中显示的错误对话框请参见图 2，除非所有页中使用的脚本文件都是开放和可用于调试。


[![可用于调试没有源代码时显示错误对话框。](understanding-asp-net-ajax-debugging-capabilities/_static/image5.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image4.png)

**图 2**： 可用于调试没有源代码时显示错误对话框。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-debugging-capabilities/_static/image6.png))


此对话框会显示，因为 Visual Studio.NET 不确定如何获取对某些由页面引用的脚本的源代码。 虽然这可能是非常令人沮丧首先，没有简单的修复。 启动调试会话并命中断点后，请转到调试 Windows 脚本资源管理器窗口上的 Visual Studio 2008 菜单或使用 Ctrl + Alt + N 热键。

> *> [!NOTE] 如果看不到列出的脚本资源管理器菜单，请转到工具**自定义* *Visual Studio.NET 菜单上的命令。在类别部分中找到调试条目并单击它以显示所有可用的菜单项。在命令列表中，向下滚动到脚本资源管理器，然后将它拖到调试* *Windows 菜单中的前面所述。执行此操作也将脚本资源管理器菜单项提供每次运行 Visual Studio.NET。*


脚本资源管理器可以用于查看在页面中使用的所有脚本和在代码编辑器中打开它们。 脚本资源管理器打开后，双击当前正在调试在代码编辑器窗口中打开它的.aspx 页。 为所有其他脚本资源管理器中所示的脚本执行相同操作。 一旦所有脚本都是将其打开，可以在代码窗口中按 F11 （和使用其他调试热键） 来单步执行代码。 图 3 显示了脚本资源管理器的示例。 它列出正在调试的当前文件 (Demo.aspx) 以及两个自定义脚本和动态注入由 ASP.NET AJAX ScriptManager 的页面的两个脚本。


[![脚本资源管理器可轻松访问页面中使用的脚本。](understanding-asp-net-ajax-debugging-capabilities/_static/image8.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image7.png)

**图 3**。 脚本资源管理器可轻松访问页面中使用的脚本。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-debugging-capabilities/_static/image9.png))


其他几个 windows 还可用于单步执行代码页中提供的有用信息。 例如，可以使用局部变量窗口以查看不同页上，即时窗口来评估特定的变量或条件，并查看输出中所用的变量的值。 输出窗口还可用于查看写出使用 Sys.Debug.trace 函数 （它将在本文后面介绍） 或 Internet Explorer 的 Debug.writeln 函数跟踪语句。

逐句通过代码使用调试程序可以将鼠标放在代码中以查看它们所分配的值的变量。 但是，脚本调试程序有时不会显示任何内容根据鼠标悬停在给定的 JavaScript 变量上。 若要查看的值，突出显示的语句或想要在代码编辑器窗口中看到，然后将鼠标悬停其上的变量。 尽管在每种情况下，此方法不起作用，但很多时候您将能够看到的值，而无需在不同的调试窗口，如局部变量窗口中查看。

可以在查看演示此处讨论的功能的一些视频教程[ http://www.xmlforasp.net ](http://www.xmlforasp.net)。

## <a name="debugging-with-web-development-helper"></a>使用 Web Development Helper 进行调试

尽管 Visual Studio 2008 （和 Visual Web Developer Express 2008） 是非常强大的调试工具，但有其他也可以使用的是更轻量级的选项。 若要发布的最新工具之一是 Web Development Helper。 Microsoft 的 Nikhil Kothari （一个 microsoft 密钥的 ASP.NET AJAX 架构师） 编写了该出色的工具，它可以从简单的调试查看 HTTP 请求和响应消息执行许多不同的任务。 下载 web Development Helper [ http://projects.nikhilk.net/Projects/WebDevHelper.aspx ](http://projects.nikhilk.net/Projects/WebDevHelper.aspx)。

可以直接在其中可以方便地使用 Internet Explorer 内使用 web 开发帮助程序。 首先从 Internet 资源管理器菜单中选择工具 Web Development Helper。 这将在浏览器，这是很好，因为无需离开浏览器以执行多个任务，例如 HTTP 请求和响应消息日志记录的下半部分中打开该工具。 图 4 显示了 Web Development Helper 在操作中的样子。


[![Web 开发帮助程序](understanding-asp-net-ajax-debugging-capabilities/_static/image11.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image10.png)

**图 4**: Web Development Helper ([单击以查看实际尺寸的图像](understanding-asp-net-ajax-debugging-capabilities/_static/image12.png))


Web 开发帮助程序不会使用此工具来逐句通过代码与使用 Visual Studio 2008。 但是，它可用于查看跟踪输出、 轻松地计算脚本中的变量或浏览数据是在 JSON 对象内。 还有用于查看 ASP.NET AJAX 页面和服务器来回传递的数据非常有用。

在 Internet Explorer 中打开 Web Development Helper 后，则必须通过脚本启用脚本调试从菜单中选择 Web 开发帮助程序如前面图 4 中所示启用脚本调试。 这样，如运行页面时出现的截距错误工具。 它还允许轻松访问的页面中的输出跟踪消息。 若要查看跟踪信息或执行脚本命令，以在页面内的不同函数进行测试，请从 Web Development Helper 菜单中选择脚本显示脚本控制台。 这提供了对命令窗口和一个简单的即时窗口访问。

*查看跟踪消息和对象的 JSON 数据*

即时窗口可以用于执行脚本命令或甚至加载或保存脚本，用于在页面中测试不同的函数。 命令窗口显示通过查看的页的形式写出的跟踪或调试消息。 列表 2 显示了如何编写使用 Internet Explorer 的 Debug.writeln 函数的跟踪消息。

**代码清单 2。写出使用 Debug 类的客户端的跟踪消息。**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample3.js)]

如果 LastName 属性包含值为 Doe，Web Development Helper 将显示消息"人员姓名： Doe"在脚本控制台的命令窗口 （假设是否已启用调试）。 Web Development Helper 还将顶级 debugService 对象添加到可用于写出跟踪信息或查看其内容的 JSON 对象的页。 列表 3 显示了使用 debugService 类跟踪函数的示例。

**代码清单 3。使用 Web Development Helper debugService 类编写跟踪消息。**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample4.js)]

DebugService 类的一个不错的功能是，使之能够即使未启用调试功能在 Internet Explorer 中轻松地运行 Web Development Helper 时始终访问跟踪数据。 时不要使用该工具来调试页面，跟踪语句将被忽略，因为对 window.debugService 调用将返回 false。

DebugService 类还允许使用 Web Development Helper 检查器窗口来查看 JSON 对象数据。 列表 4 创建包含个人数据的简单 JSON 对象。 在创建对象后调用到 debugService 类的检查函数，以允许要直观检查的 JSON 对象。

**列表 4。DebugService.inspect 函数用于查看 JSON 对象数据。**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample5.js)]

在页中或通过在即时窗口调用 GetPerson() 函数将导致出现如图 5 中所示的对象检查器对话框窗口。 在对象中的属性可以动态更改通过突出显示它们，更改显示在值文本框中的值，然后单击更新链接。 使用对象检查器可以直观地查看对象的 JSON 数据并尝试将不同的值应用于属性。

*调试错误*

除了允许跟踪数据和要显示的 JSON 对象，Web 开发帮助程序也有助于在调试页面中的错误。 如果遇到错误，系统会提示继续到下一行代码，或调试脚本 （请参阅图 6）。 该脚本错误对话框窗口会显示完整的调用堆栈以及行号，以便可以轻松确定在脚本中的问题所在。


[![对象检查器窗口用于查看 JSON 对象。](understanding-asp-net-ajax-debugging-capabilities/_static/image14.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image13.png)

**图 5**： 对象检查器窗口用于查看 JSON 对象。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-debugging-capabilities/_static/image15.png))


选择调试选项，可直接在 Web Development Helper 若要查看变量的值，写出的 JSON 对象，还需要更多的即时窗口中执行脚本语句。 如果再次执行相同操作触发该错误，并且 Visual Studio 2008 的计算机上可用，将提示您启动调试会话，以便可以逐句通过代码逐行上一节中所述。


[![Web 开发帮助程序脚本错误对话框](understanding-asp-net-ajax-debugging-capabilities/_static/image17.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image16.png)

**图 6**: Web Development Helper 脚本错误对话框 ([单击以查看实际尺寸的图像](understanding-asp-net-ajax-debugging-capabilities/_static/image18.png))


*检查请求和响应消息*

调试 ASP.NET AJAX 页面时通常很有用，若要查看的页和服务器之间发送的请求和响应消息。 查看在消息中的内容，可看到是否正在传入的消息大小以及适当的数据。 Web Development Helper 提供了绝佳 HTTP 消息记录器功能，轻松地查看数据作为原始文本或更易读的格式。

若要查看 ASP.NET AJAX 请求和响应消息，必须通过从 Web Development Helper 菜单中选择 HTTP 启用 HTTP 日志记录启用 HTTP 记录器。 启用后，可以在 HTTP 日志查看器，这可以通过选择 HTTP 显示 HTTP 日志访问查看从当前页发送的所有消息。

尽管查看每个请求/响应消息中发送的原始文本是当然还是很有用 （和 Web Development Helper 中的某个选项），它通常是更轻松地以更图形格式查看消息数据。 一旦启用 HTTP 日志记录，且消息已记录，可以通过双击该消息在 HTTP 日志查看器中查看消息数据。 执行此操作将允许您查看与一条消息，以及实际的消息关联的所有标题内容。 图 7 显示了请求消息和响应消息在 HTTP 日志查看器窗口中查看的一个示例。


[![使用 HTTP 日志查看器来查看请求和响应消息数据。](understanding-asp-net-ajax-debugging-capabilities/_static/image20.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image19.png)

**图 7**： 使用 HTTP 日志查看器来查看请求和响应消息数据。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-debugging-capabilities/_static/image21.png))


HTTP 日志查看器会自动分析 JSON 对象，并显示它们使用树视图，使其快速、 轻松地查看对象的属性数据。 当 UpdatePanel ASP.NET AJAX 页面中使用时，在查看器会细分到各个部分的消息的每个部分如图 8 中所示。 这是一项强大功能，便于更轻松地查看和了解相比查看原始消息数据消息中的功能。


[![使用 HTTP 日志查看器查看一个 UpdatePanel 响应消息。](understanding-asp-net-ajax-debugging-capabilities/_static/image23.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image22.png)

**图 8**： 使用 HTTP 日志查看器查看 UpdatePanel 响应消息。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-debugging-capabilities/_static/image24.png))


有几种可用来查看请求和响应消息的 Web Development Helper 其他工具。 另一个不错的选择是 Fiddler 即免费获取网址[ http://www.fiddlertool.com ](http://www.fiddlertool.com)。 尽管未将此处讨论 Fiddler，还有一个不错的选择时需要全面检查消息标头和数据。

## <a name="debugging-with-firefox-and-firebug"></a>使用 Firefox 和 Firebug 进行调试

虽然 Internet Explorer 仍是最广泛使用的浏览器，例如 Firefox 其他浏览器已变得广受欢迎和正在使用的更多。 因此，你将想要查看和调试 ASP.NET AJAX 页面在 Firefox 和 Internet 资源管理器以确保您的应用程序正常工作。 尽管 Firefox 不能直接与 Visual Studio 2008 进行调试，但它具有名为可用于调试页 Firebug 扩展。 可以通过转到免费下载 firebug [ http://www.getfirebug.com ](http://www.getfirebug.com)。

Firebug 可提供可用于单步执行代码逐行、 访问在页内使用的所有脚本、 查看 DOM 结构、 在页面中显示的 CSS 样式和甚至是跟踪事件发生的全功能调试环境。 安装后，可以通过从 Firefox 菜单中选择工具 Firebug 打开 Firebug 访问 Firebug。 像 Web Development Helper Firebug 尽管也可作为独立的应用程序在浏览器中直接使用。

Firebug 开始运行后，可以设置断点上的 JavaScript 文件的任意行是否在脚本嵌入在页中，或不。 若要设置断点，首先加载相应的页你想要在 Firefox 中进行调试。 页面加载后，选择要从下拉列表中 Firebug 的脚本调试的脚本。 将显示页面使用的所有脚本。 通过单击在 Firebug 的灰色栏区域中在行断点应放必须像在 Visual Studio 2008 中设置断点。

在 Firebug 中设置断点后可以执行如单击按钮或刷新浏览器触发 onLoad 事件调试所需脚本执行所需的操作。 包含断点的行上，将自动停止执行。 图 9 在 Firebug 中显示已触发断点的示例。


[![处理在 Firebug 中的断点。](understanding-asp-net-ajax-debugging-capabilities/_static/image26.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image25.png)

**图 9**： 处理在 Firebug 中的断点。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-debugging-capabilities/_static/image27.png))


命中的断点可以单步执行、 逐过程执行或跳出代码使用箭头按钮。 单步执行代码，调试器使您可以看到值和向下钻取到的对象的右半部分中显示脚本变量。 Firebug 还包括一个调用堆栈下拉列表以查看导致正在调试的当前行的脚本的执行步骤。

Firebug 还包括可用于测试不同的脚本语句、 计算变量并查看跟踪输出的控制台窗口。 通过单击 Firebug 窗口顶部的控制台选项卡访问它。 正在调试的页可以还"检查"以通过单击检查选项卡上查看其 DOM 结构和内容。你将突出显示轻松地查看该元素在页面中的使用位置鼠标悬停在检查器窗口中显示此页面的相应部分的不同 DOM 元素。 "实时"尝试将不同宽度、 样式等应用于元素，可以更改与给定元素相关联的属性值。 这是一个不错的功能，使你无需不断地在源代码编辑器和 Firefox 浏览器查看简单的更改会影响页面之间切换。

图 10 显示了使用 DOM 检查器来查找名为 txtCountry 页中的文本框的示例。 Firebug 检查器还可以用于查看在一个页面，以及如跟踪鼠标移动、 按钮单击，还需要更多发生的事件中使用的 CSS 样式。


[![使用 Firebug 的 DOM 检查器。](understanding-asp-net-ajax-debugging-capabilities/_static/image29.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image28.png)

**图 10**： 使用 Firebug DOM 检查器。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-debugging-capabilities/_static/image30.png))


Firebug 可提供快速调试页直接在 Firefox，以及检查不同元素在页面内的理想工具中的轻型方式。

## <a name="debugging-support-in-aspnet-ajax"></a>在 ASP.NET AJAX 中的调试支持

ASP.NET AJAX 库包括许多不同的类可用于简化将添加到网页的 AJAX 功能的过程。 这些类可用于查找在一页内的元素并对其进行处理、 添加新控件、 调用 Web 服务和甚至处理事件。 ASP.NET AJAX 库还包含可用于增强的调试页过程的类。 在本部分将介绍到 Sys.Debug 类并了解如何可以在应用程序中使用它。

*使用 Sys.Debug 类*

Sys.Debug 类 （位于 Sys 命名空间中的 JavaScript 类） 可以用于执行几个不同的功能包括将跟踪输出写入、 执行代码断言和强制代码失败，以便可以进行调试。 它是广泛使用 ASP.NET AJAX 库的调试文件 （默认情况下安装在 C:\Program Files\Microsoft ASP.NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0） 中执行条件检测 （名为断言），确保传递的参数正确对象，包含所需的数据的功能，以及要写入跟踪语句。

Sys.Debug 该类会公开多个不同的函数可用于处理跟踪、 代码断言或故障，如表 1 中所示。

**表 1。Sys.Debug 类函数。**

| **函数名** | **说明** |
| --- | --- |
| assert （条件、 消息、 displayCaller） | 断言的条件参数为 true。 如果被测条件为 false，则将使用一个消息框显示的消息参数值。 如果 displayCaller 参数为 true，该方法还显示有关调用方信息。 |
| clearTrace() | 清除跟踪操作的语句输出。 |
| fail(message) | 会导致程序停止执行并进入调试器。 消息参数可以用于提供失败的原因。 |
| trace(message) | 写入跟踪输出的消息参数。 |
| traceDump （对象、 名称） | 输出可读格式的对象的数据。 可以使用 name 参数以便为跟踪转储提供的标签。 默认情况下，正在转储对象内的任何子对象将写出。 |

客户端跟踪可以使用方法的 ASP.NET 提供的跟踪功能与大致相同。 它允许不同的消息来轻松地看到而不会中断应用程序的流。 列表 5 显示了使用 Sys.Debug.trace 函数来写入跟踪日志的示例。 此函数只获取应作为参数写出的消息。

**列表 5。使用 Sys.Debug.trace 函数。**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample6.js)]

如果您执行列表 5 中所示的代码不会看到页面中的任何跟踪输出。 若要查看它的唯一方法是使用 Visual Studio.NET、 Web Development Helper 或 Firebug 中可用的控制台窗口。 如果确实想要查看的页中的跟踪输出，然后您需要添加文本区标记并为其提供的 id 为 TraceConsole，按如下所示：


[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample7.html)]

在页中的任何 Sys.Debug.trace 语句将写入到 TraceConsole 文本区域。

在想要查看 JSON 对象中包含的数据的情况下可以使用 Sys.Debug 类 traceDump 函数。 此函数采用两个参数，包括应转储到跟踪控制台的对象以及可用于标识跟踪输出中的对象的名称。 列表 6 显示了使用 traceDump 函数的示例。

**代码清单 6。使用 Sys.Debug.traceDump 函数。**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample8.js)]

图 11 显示了调用 Sys.Debug.traceDump 函数的输出。 请注意，除了编写出 Person 对象的数据，它还写出地址子对象的数据。

除了跟踪，Sys.Debug 类还可以使用执行代码断言。 断言用于测试满足特定条件时应用程序运行时。 ASP.NET AJAX 库脚本的调试版本包含多个声明语句来测试在各种条件。

列表 7 显示了使用 Sys.Debug.assert 函数对条件进行测试的示例。 该代码会测试更新 Person 对象之前地址对象为 null。


[![Sys.Debug.traceDump 函数的输出。](understanding-asp-net-ajax-debugging-capabilities/_static/image32.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image31.png)

**图 11**: Sys.Debug.traceDump 函数的输出。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-debugging-capabilities/_static/image33.png))


**列表 7。使用 debug.assert 函数。**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample9.js)]

包括要计算断言返回 false，该值指示应显示有关调用方信息时要显示的消息的条件将三个参数传递。 在断言失败的情况下，将显示消息以及调用方信息，如果第三个参数为 true。 图 12 显示了出现清单 7 中所示的断言失败时的失败对话框的示例。

要介绍的最后一个函数是 Sys.Debug.fail。 当你想要强制代码无法在脚本中某一特定行时可以添加 Sys.Debug.fail 调用而不是通常在 JavaScript 应用程序中使用的调试器语句。 Sys.Debug.fail 函数接受单个字符串参数，表示失败的原因，按如下所示：


[!code-css[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample10.css)]


[![Sys.Debug.assert 失败消息。](understanding-asp-net-ajax-debugging-capabilities/_static/image35.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image34.png)

**图 12**: Sys.Debug.assert 失败消息。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-debugging-capabilities/_static/image36.png))


当遇到 Sys.Debug.fail 语句时执行脚本时，消息参数的值将显示在控制台中调试应用程序，例如 Visual Studio 2008，系统将提示你调试应用程序。 这可以是非常有用的一种情况是当您不能内联脚本上设置断点，Visual Studio 2008，但想要停止特定的行上，使你可以检查变量的值的代码。

*了解 ScriptManager 控件的 ScriptMode 属性*

ASP.NET AJAX 库包括调试和发布脚本版本，默认情况下安装在 C:\Program Files\Microsoft ASP.NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0。 调试脚本是格式良好、 易于阅读，具有多个 Sys.Debug.assert 调用分散在整个它们而发行脚本有去除空格而尽量少使用 Sys.Debug 类最小化其总体大小。

ScriptManager 控件添加到 ASP.NET AJAX 页面读取 web.config 来确定哪些版本的库脚本加载中编译元素的调试属性。 但是，您可以控制如果调试或发布脚本是否已加载 （库脚本或自己的自定义脚本） 通过更改 ScriptMode 属性。 ScriptMode 接受其成员包括自动、 调试、 发布和继承的 ScriptMode 枚举。

ScriptMode 默认为自动，这意味着，ScriptManager 将检查 web.config 中的调试属性的值。调试为 false 时 ScriptManager 将加载 ASP.NET AJAX 库脚本的发行版本。 当调试为 true 时将加载的脚本的调试版本。 更改版本或调试的 ScriptMode 属性将强制 ScriptManager 加载适当的脚本，而不考虑哪些调试属性具有在 web.config 中的值。代码清单 8 显示了使用 ScriptManager 控件从 ASP.NET AJAX 库加载调试脚本的示例。

**代码清单 8。正在加载调试脚本使用 ScriptManager**。


[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample11.aspx)]

此外可以通过列表 9 中所示使用 ScriptManager 的脚本属性以及 ScriptReference 组件加载不同版本 （调试或发布） 的自定义脚本。

**列表 9。使用 ScriptManager 加载自定义脚本。**


[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample12.aspx)]

> [!NOTE]
> 如果你正在加载自定义脚本使用 ScriptReference 组件必须通知 ScriptManager，当脚本加载完成后通过在脚本的底部添加以下代码：


[!code-csharp[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample13.cs)]

列表 9 中所示的代码告知 ScriptManager 以寻找人员脚本的调试版本，因此它将自动寻找而不是 Person.js Person.debug.js。 如果 Person.debug.js 文件未找到将引发错误。

在要调试或发行版本的自定义脚本加载基于 ScriptManager 控件上设置的 ScriptMode 属性的值的情况下，您可以将 ScriptReference 控件的 ScriptMode 属性设置为继承。 这会导致要加载的自定义脚本的适当版本基于 ScriptManager 的 ScriptMode 属性列表 10 中所示。 因为 ScriptManager 控件的 ScriptMode 属性设置为调试，将加载 Person.debug.js 脚本，并将其在页中。

**代码清单 10。继承自定义脚本的 ScriptManager 的 ScriptMode。**


[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample14.aspx)]

通过适当地使用 ScriptMode 属性可以更轻松地调试应用程序和简化整个过程。 ASP.NET AJAX 库的发布脚本是相当困难，单步执行和读取由于格式设置代码格式专门用于调试目的的调试脚本时已删除。

## <a name="conclusion"></a>结束语

Microsoft 的 ASP.NET AJAX 技术，用于构建启用了 AJAX 的应用程序可增强最终用户的整体体验提供了坚实的基础。 但是，作为使用任何编程技术，bug 和其他应用程序问题将肯定会出现。 了解有关各种可用的调试选项可以将大量时间和结果保存在更稳定的产品。

在这篇文章了已向您介绍用于调试 ASP.NET AJAX 页面包括 Internet Explorer 使用 Visual Studio 2008 中，Web Development Helper 和 Firebug 多种不同的方法。 这些工具可以简化整个调试过程，因为可以访问变量的数据、 演练代码逐行和查看跟踪语句。 除了讨论了不同的调试工具，您还了解了如何在应用程序中使用 ASP.NET AJAX 库的 Sys.Debug 类以及如何使用 ScriptManager 类加载调试或发布脚本的版本。

## <a name="bio"></a>个人简介

Dan Wahlin （Microsoft 最有价值专业人员的 ASP.NET 和 XML Web 服务） 是接口的技术培训的.NET 开发讲师和体系结构顾问 ([www.interfacett.com)](http://www.interfacett.com)。 Dan 成立了 XML for ASP.NET 开发人员网站 ([www.XMLforASP.NET](http://www.XMLforASP.NET))、 INETA 演讲者机构上和在多个会议上发表演讲。 Dan 合著了专业版 Windows DNA (Wrox)，ASP.NET： 提示、 教程和代码 (Sam)、 ASP.NET 1.1 Insider 解决方案、 Professional ASP.NET 2.0 AJAX (Wrox)、 ASP.NET 2.0 MVP Hacks 和面向 ASP.NET 开发人员 (Sam) 编写的 XML。 当他不编写代码、 文章或书籍时，Dan 喜欢编写和录制音乐和播放高尔夫和他的妻子和儿童篮球。

Scott Cate 自 1997 年以来一直致力于 Microsoft Web 技术和 myKB.com 总裁 ([www.myKB.com](http://www.myKB.com)) 专门负责编写 ASP.NET 基于侧重于知识库软件解决方案的应用程序。 可以通过电子邮件联系 Scott [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com)或他的博客[ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [上一篇](understanding-asp-net-ajax-web-services.md)
