---
uid: web-pages/overview/releases/aspnet-web-pages-2-developer-preview-readme
title: ASP.NET Web Pages 2 开发人员预览版自述文件 |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 09/14/2011
ms.assetid: 159a92e2-e011-4da7-b61d-2edde2a967da
msc.legacyurl: /web-pages/overview/releases/aspnet-web-pages-2-developer-preview-readme
msc.type: authoredcontent
ms.openlocfilehash: 93e3f9c9d7c90f1ebfd9f482166aeb833cae73e9
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831699"
---
<a name="aspnet-web-pages-2-developer-preview-readme"></a>ASP.NET 网页 2 开发人员预览版自述文件
====================
by [Microsoft](https://github.com/microsoft)

## <a name="aspnet-web-pages-2-developer-preview-readme"></a>ASP.NET 网页 2 开发人员预览版自述文件

2011 年 9 月 14日

### <a name="contents"></a>内容

#### <a id="_Toc303701284"></a>  安装说明

若要安装 Web Pages 2 开发人员预览版，你可以使用以下选项：

- 使用安装 WebMatrix 2 Beta [Web 平台安装程序](https://go.microsoft.com/fwlink/?LinkId=226883)。 WebMatrix 是一套免费的 web 开发工具，包括 ASP.NET Web Pages。 有关详细信息，请参阅中的安装部分[ASP.NET Web Pages 2 开发者预览版中的常用功能](https://go.microsoft.com/fwlink/?LinkID=227824)。

- 安装 Web Pages 2 开发人员预览版使用直接[下载链接](https://go.microsoft.com/fwlink/?LinkID=226335)。 如果你想要创建 Web Pages 应用程序使用文本编辑器 （如记事本），请使用此方法。 若要运行 Web Pages 2 应用程序，必须具有 IIS Express 7.5。 （这会自动随 WebMatrix。）有关如何测试使用 IIS Express，某个 Web Pages 页提示中，请参阅侧栏"创建并测试 ASP.NET 页使用你自己的文本编辑器" [Getting Started with WebMatrix 和 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202889)。

ASP.NET Web Pages 2 开发者预览版可以安装和可以运行的同时使用 ASP.NET Web Pages 1。 <a id="a"></a>有关详细信息，参阅的"运行网页的应用程序的并排方案"部分[Web Pages 2 开发者预览版中的常用功能](https://go.microsoft.com/fwlink/?LinkID=227824)。

#### <a id="_Toc303701285"></a>  文档

教程和其他信息有关 ASP.NET Web Pages 页还提供网页的 ASP.NET 网站 ([https://www.asp.net/web-pages/](../../index.md))。 有关新功能和 Web Pages 2 中的增强功能的信息，请参阅[Web Pages 2 开发者预览版中的常用功能](https://go.microsoft.com/fwlink/?LinkID=227824)。

#### <a id="_Toc303701286"></a>  支持

<a id="_Toc209852135"></a><a id="_Toc255833657"></a> 这是预览版本并不正式支持。 如果必须使用此版本有关的问题，请将其发布到 ASP.NET Web Pages 论坛 ([ https://forums.asp.net/1224.aspx/1?WebMatrix ](https://forums.asp.net/1224.aspx/1?WebMatrix) )，ASP.NET 社区的成员是经常能够提供非正式的支持。

#### <a id="_Toc303701287"></a>  软件要求

ASP.NET Web Pages 2 要求.NET Framework 4。 它还适用于.NET Framework 4.5 开发人员预览版。

<a id="_Toc303701288"></a><a id="_Breaking_Changes"></a>

#### <a name="fixes-known-issues-and-breaking-changes"></a>修补程序、 已知的问题和重大更改

<a id="_Toc224729061"></a><a id="_Toc238051347"></a>

- **是\*的所有区域性的方法 (例如，IsDateTime) 现在返回正确值。** 等某些方法*IsDateTime*以前返回*false*当他们本应返回*true*因为它们先前已执行特定于区域性的检查。 已修复这些方法现在将区域性考虑在内。 这是一项重大更改;如果你的应用程序依赖于旧行为，它将中断。
- **Href 方法的行为已更改。** 以前，调用 Href("~/SomeFile") 将返回当前正在执行文件的相对 URL。 现在 Href("~/SomeFile") 始终是绝对路径从返回的应用程序的根。 在大多数情况下，此行为，因此可以忽略返回值中。 此更改是为了解决某些 Ajax 方案。 例如，考虑下面的示例代码： 

    [!code-cshtml[Main](aspnet-web-pages-2-developer-preview-readme/samples/sample1.cshtml)]

    此代码之前将解析为 Images/Logo.jpg，这将会是 Ajax 请求到该页面不正确。 它现在能解析到的根目录 (/ MySite/Images/Logo.jpg)。
- **HttpContext.RedirectLocal 方法已更改**。 此方法现在接受相对于当前应用程序的 Url。 完全限定的 Url 将被拒绝。
- **ModelState.IsValid 方法现在要求您首先调用 Validate**。 如果将转换应用程序以使用新的输入的验证方法，并正在调用*ModelState.IsValid*方法，必须立即调用*Validation.Validate*事先。 例如，您现在必须遵循此模式： 

    [!code-csharp[Main](aspnet-web-pages-2-developer-preview-readme/samples/sample2.cs)]

  但是，我们建议你使用新的输入的验证方法，如果不使用*ModelState.IsValid*。 相反，构建如下代码： 

    [!code-csharp[Main](aspnet-web-pages-2-developer-preview-readme/samples/sample3.cs)]
- **在 Internet Explorer 7 和 Internet Explorer 8，客户端验证不起作用**。 客户端验证不工作，因为不兼容性与 jQuery 1.6.2，包含在默认项目模板。 （服务器端验证的工作方式。）。

#### <a id="_Toc303701289"></a>  免责声明

© 2011 Microsoft Corporation. 保留所有权利。 本文档提供"作为-是。" 恕不另行通知可能会更改的信息和包括 URL 和其他 Internet 网站参考，本文档中表达的观点。 您自行承担其使用风险。
