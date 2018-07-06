---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: 如何使用 HTML 编辑器控件？ (C#) |Microsoft Docs
author: microsoft
description: HTMLEditor 是 ASP.NET AJAX 控件，您可以轻松地创建和编辑通过按钮在工具栏中的 HTML 内容。
ms.author: aspnetcontent
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 775cb113ea11e582806b0bd9397778cff6761940
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809402"
---
<a name="how-do-i-use-the-html-editor-control-c"></a>如何使用 HTML 编辑器控件？ (C#)
====================
by [Microsoft](https://github.com/microsoft)

> HTMLEditor 是 ASP.NET AJAX 控件，您可以轻松地创建和编辑通过按钮在工具栏中的 HTML 内容。


本教程的目的是为你提供了 AJAX 控件工具包中包含的 HTML 编辑器控件的概述。 HTML 编辑器包含可用于更改字体大小、 选择一种字体、 更改背景色、 修改的前景色，选项添加链接，添加图像，更改文本对齐方式，并执行剪切、 复制和粘贴 （见图 1） 的操作。


[![HTML 编辑器](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)

**图 01**： 使用 HTML 编辑器 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-cs/_static/image2.png))


HTML 编辑器，您可以输入使用设计模式下的内容，也可以直接输入 HTML。 你还提供用于预览 HTML 内容的选项 （请参见图 2）。


[![设计、 HTML 和预览按钮](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)

**图 02**： 设计、 HTML 和预览按钮 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-cs/_static/image4.png))


在本教程中，您将学习如何显示 HTML 编辑器、 如何自定义工具栏按钮显示在 HTML 编辑器中，以及如何避免跨站点脚本攻击。

## <a name="displaying-the-html-editor"></a>显示 HTML 编辑器

在 ASP.NET 页面中使用 HTML 编辑器之前，必须首先将 ScriptManager 控件添加到页面。 ScriptManager 控件位于 Visual Studio/Visual Web Developer 速成版工具箱中的 AJAX 扩展选项卡下。

应将 ScriptManager 控件放在之前的页的页上的任何其他控件的顶部。 例如，您可以将其放立即打开服务器端下面&lt;窗体&gt;标记。

HTML 编辑器控件位于与其他 AJAX 控件工具包控件工具箱中。 它名为编辑器控件 （请参见图 3）。


[![HTML 编辑器控件](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)

**图 03**： 使用 HTML 编辑器控件 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-cs/_static/image6.png))


HTML 编辑器将拖到页后，你可以在属性表中设置其属性。 例如，你通常想要设置宽度和高度属性。 代码清单 1 包含一个包含 HTML 编辑器的 ASP.NET 页面的源。

**代码清单 1-SimpleEditor.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

在列表 1 中的页包含的 HTML 编辑器控件、 一个按钮控件和文字控件。 当单击按钮时，内容的 HTML 编辑器中显示文本控件中 （请参阅图 4）。


[![提交窗体使用 HTML 编辑器](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)

**图 04**： 提交窗体使用 HTML 编辑器 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-cs/_static/image8.png))


HTML 编辑器内容属性用于检索输入到 HTML 编辑器中的 HTML 内容。 请注意，此 HTML 内容可以包含 JavaScript。 在下一部分中，我们讨论了如何阻止 JavaScript 注入攻击。

## <a name="customizing-the-html-editor-toolbar"></a>自定义 HTML 编辑器工具栏

你可以自定义完全的按钮出现在编辑器中。 例如，可能想要删除 HTML 选项卡以防止用户在 HTML 编辑器切换到 HTML 模式。 或者，可能想要删除字体大小下拉列表，以防止用户在论坛中创建过大文本 post 消息 （请参见图 5）。


[![自定义 HTML 编辑器](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)

**图 05**： 一个自定义 HTML 编辑器 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-cs/_static/image10.png))


您通过从编辑器的基类中派生新的 HTML 编辑器自定义工具栏按钮。 例如，代码清单 2 中的自定义编辑器仅包含粗体和斜体的工具栏按钮。 已删除所有其他工具栏按钮。 此外，HTML 选项卡已删除从编辑器的底部 （但在设计和预览选项卡仍有）。

**代码清单 2-应用\_Code\CustomEditor.cs**

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

必须向应用程序清单 2 中添加类\_代码文件夹，以便将自动编译的类。 如果应用\_代码文件夹中你的网站不存在，则可以只需将文件夹添加。

创建自定义编辑器后，您可以将其添加到 ASP.NET 页面中的相同方式添加普通 HTML 编辑器 （请参阅代码清单 3）。

**代码清单 3-ShowCustomEditor.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>避免跨站点脚本 (XSS) 攻击

只要您接受来自用户的输入，并且重新该输入显示在网站上，你可能会打开你受到跨站点脚本 (XSS) 攻击的网站。 从理论上讲，恶意黑客无法提交输入重新显示时执行的 JavaScript 代码。 无法使用 JavaScript 来窃取用户密码或其他敏感信息。

通常情况下，可以抵御 XSS 攻击的 HTML 编码在网页中显示之前从用户检索任何输入。 但是，HTML 编码的 HTML 编辑器中的输出将只对进行编码&lt;脚本&gt;标记，它还对所有 HTML 标记进行都编码。 换而言之，就会丢失的所有格式如字体、 字体大小和背景色。

如果您收集的敏感信息来自您的用户-例如密码、 信用卡卡号和社会安全号码-然后应不显示未编码使用 HTML 编辑器中的用户从检索的内容。 到你的网站由受信任方，应仅在某些情况下在其中不会重新显示的 HTML 内容，或正在提交的 HTML 内容中使用 HTML 编辑器。

例如，假设您要创建的博客应用程序。 在此情况下，最好使用 HTML 编辑器，在撰写博客文章时。 是唯一将提交一篇博客文章的人，并且有可能可以信任自己无法提交恶意 JavaScript。 但是，它不难理解时要使用 HTML 编辑器允许匿名用户发表评论。 您应在用户将提交敏感信息，如密码的情况下特别小心。 可能的恶意用户可以将发布包含适用于窃取密码右侧的 JavaScript 的注释。

## <a name="summary"></a>总结

在本教程中，你已提供了 AJAX 控件工具包中包含的 HTML 编辑器控件的简要概述。 您学习了如何使用 HTML 编辑器以接受来自用户的丰富内容并提交到服务器的内容。 我们还讨论了如何自定义工具栏按钮显示的 HTML 编辑器中。 最后，您学习了如何使用 HTML 编辑器接受潜在的恶意输入时，避免出现跨站点脚本攻击。

> [!div class="step-by-step"]
> [下一篇](how-do-i-use-the-html-editor-control-vb.md)
