---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 第 8 部分： 最终页面、 异常处理和结论 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 8 部分添加一个联系人页，有关页和异常...
ms.author: aspnetcontent
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 4fb0147a5cd8621e5341e4995960adf2f00fffc0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804712"
---
<a name="part-8-final-pages-exception-handling-and-conclusion"></a>第 8 部分： 最终页面、 异常处理和结论
====================
通过[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。 它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。
> 
> 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 8 部分将添加联系人的页上，有关页和异常处理。 这是系列教程的结论。


## <a id="_Toc260221680"></a>  请联系页 （从 ASP.NET 发送电子邮件）

创建一个名为 ContactUs.aspx 的新页

使用设计器，创建以下形式采用特殊的注释，以包括 ToolkitScriptManager 和从 AjaxdControlToolkit 编辑器控件。 .

![](tailspin-spyworks-part-8/_static/image1.jpg)

双击"提交"按钮以在代码隐藏文件中生成一个 click 事件处理程序并实现为一封电子邮件发送的联系信息的方法。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

此代码需要在 web.config 文件包含指定要用于发送邮件的 SMTP 服务器的配置节中的条目。

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>  有关页

创建一个名为 AboutUs.aspx 页并添加您喜欢的任何内容。

## <a id="_Toc260221682"></a>  全局异常处理程序

最后，整个应用程序中，我们已引发异常并且未预见情况下，冷还可在 web 应用程序中导致未经处理的异常。

我们永远不会想要显示给网站访问者未经处理的异常。

![](tailspin-spyworks-part-8/_static/image2.jpg)

除了可怕的用户体验未经处理的异常也可以是安全问题。

若要解决此问题，我们将实现全局异常处理程序。

若要执行此操作，打开 Global.asax 文件，并请注意以下预生成的事件处理程序。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

添加代码以实现应用程序\_，如下所示的错误处理程序。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

然后添加一个名为到解决方案的 Error.aspx 页并添加此标记片段。

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

现在，在页面\_从请求对象中加载事件处理程序提取的错误消息。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>  结论

我们所见，ASP.NET WebForms 可以轻松创建复杂的网站具有数据库访问，成员身份，AJAX，等等。 很快就会变。

希望本教程提供若要开始构建你自己的 ASP.NET WebForms 应用程序所需的工具 ！

> [!div class="step-by-step"]
> [上一篇](tailspin-spyworks-part-7.md)
