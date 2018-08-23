---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: 了解 ASP.NET AJAX 本地化 |Microsoft Docs
author: scottcate
description: 本地化是设计并将对特定语言和区域性的支持集成到应用程序或应用程序组件的过程。 Mic...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 86cbf150708f1db711b40ccbc25345afeb3e542a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832893"
---
<a name="understanding-aspnet-ajax-localization"></a>了解 ASP.NET AJAX 本地化
====================
通过[Scott Cate](https://github.com/scottcate)

[下载 PDF](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> 本地化是设计并将对特定语言和区域性的支持集成到应用程序或应用程序组件的过程。 Microsoft ASP.NET 平台通过集成标准.NET 本地化模型; 为标准 ASP.NET 应用程序的本地化提供广泛支持Microsoft AJAX 框架利用集成的模型，以支持可在其中执行本地化的各种方案。


## <a name="introduction"></a>介绍

Microsoft 的 ASP.NET 技术带来了面向对象和事件驱动的编程模型，并将其与已编译的代码的好处结合在一起。 但是，其服务器端处理模型有几个缺点固有的技术，其中很多可以通过 System.Web.Extensions 命名空间，它封装在.NET Framework 中的 Microsoft AJAX 服务中包括的新功能进行寻址3.5。 使用这些扩展，许多丰富的客户端功能，以前为 ASP.NET 2.0 AJAX Extensions 的一部分，但现在的 Framework 基类库的一部分提供。 控件和此命名空间中的功能而无需整页刷新，客户端脚本 （包括 ASP.NET 分析 API），通过访问 Web 服务的功能包括部分呈现的页和扩展的客户端的 API 设计要镜像的许多了解在 ASP.NET 服务器端控件集中控制方案。

本白皮书将检查中的 Microsoft AJAX Framework 和 Microsoft AJAX 脚本库，用于本地化支持和进行审阅已集成 web 中的本地化支持业务需求的上下文中存在的本地化功能提供的.NET Framework 的应用程序。 Microsoft AJAX 脚本库利用.resx 文件格式已由.NET 应用程序，它提供了集成的 IDE 支持和可共享的资源类型。

此白皮书基于在 Microsoft Visual Studio 2008 Beta 2 版本上。 本白皮书还假定你将使用 Visual Studio 2008 中，不 Visual Web Developer 速成版，并且将提供根据 Visual Studio 的用户界面的演练。 一些代码示例将使用可能是在 Visual Web Developer 速成版中不可用的项目模板。

## <a name="the-need-for-localization"></a>*需要本地化*

特别是对于企业应用程序开发人员和组件开发人员，创建可以随时了解区域性和语言之间的差异的工具的功能已成为越来越有必要。 设计组件能够适应客户端的区域设置提高了开发人员工作效率并减少组件的自适应的全局函数所需的工作量。

本地化是设计并将对特定语言和区域性的支持集成到应用程序或应用程序组件的过程。 Microsoft ASP.NET 平台通过集成标准.NET 本地化模型; 为标准 ASP.NET 应用程序的本地化提供广泛支持Microsoft AJAX 框架利用集成的模型，以支持可在其中执行本地化的各种方案。 正在部署到附属程序集中，或使用静态文件系统结构，也可以使用 Microsoft AJAX 框架，本地化脚本。

## <a name="embedding-scripts-with-satellite-assemblies"></a>*将脚本嵌入附属程序集*

与标准.NET Framework 本地化策略保持一致，资源可以包含在附属程序集。 附属程序集提供几项优势通过传统的资源包含在二进制文件的任何给定的本地化可以更新而不更新可查看大图像，可以只需通过安装附属程序集到部署其他本地化信息项目文件夹和附属程序集可以部署而不会导致主项目程序集的重新加载。 特别是在 ASP.NET 项目中，此功能非常有用，它可以显著减少增量更新所使用的系统资源的数量和最小日志会中断生产网站使用情况。

脚本嵌入到程序集将这些命令包含在管理.resx （或编译.resources） 文件，都将包括在编译时程序集。 其资源然后都提供给脚本的应用程序通过 AJAX 运行时生成的代码，通过程序集级别属性

*对于嵌入的脚本文件命名约定*

Microsoft AJAX Framework 脚本管理支持在部署和测试的脚本中使用的各种选项并提供指导原则以促进这些选项。

*为了便于调试：*

发行 （生产） 脚本不应包含`.debug`文件名中的限定符。 此演示适合对于调试应包含的脚本`.debug`文件名中。

*为了便于本地化：*

非特定区域性的脚本不应包括的文件的名称的任何区域性标识符。 对于包含本地化的资源的脚本，应在文件名中指定 ISO 语言代码。 例如，`es-CO`代表西班牙语 （哥伦比亚）。

下表总结了文件命名约定的示例：

| Filename | 含义 |
| --- | --- |
| Script.js | 一个发行版本的非特定于区域性的脚本。 |
| Script.debug.js | 一个调试版本的非特定于区域性的脚本。 |
| Script.en-US.js | 发行版适用于英语，美国脚本。 |
| Script.debug.es-CO.js | 调试版本西班牙语，哥伦比亚脚本。 |

## <a name="walkthrough-create-an-localized-embedded-script"></a>演练： 创建本地化的嵌入式脚本

*请注意： 本演练需要 Visual Studio 2008 的使用，因为 Visual Web Developer 速成版不包括用于类库项目的项目模板。*

1. 使用集成的 ASP.NET AJAX Extensions 中创建新网站项目。 创建另一个项目，一个类库项目，名为 LocalizingResources 解决方案中。
2. 将添加到 LocalizingResources 项目名 VerifyDeletion.js 的 Jscript 文件，以及名为 DeletionResources.resx 和 DeletionResources.es.resx.resx 资源文件。 前者将包含非特定区域性的资源;后一种将包含西班牙语语言资源。
3. 将以下代码添加到 VerifyDeletion.js:

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

熟悉 JavaScript 正则表达式语法中，在单个正斜杠的文本 （在上一示例中，/FILENAME/ 是一个例子） 表示的 RegExp 对象。 MSDN 库中包含大量的 JavaScript 引用，并可以在线找到 JavaScript 本机对象上的资源。

1. 将以下资源字符串添加到 DeletionResources.resx: 

    **VerifyDelete**： 是否确实要删除文件名？

    **删除**： 文件名已被删除。

1. 将以下资源字符串添加到 DeletionResources.es.resx: 

    **VerifyDelete**： 美国东部时间 seguro que desee quitar 文件名？

    **删除**: FILENAME se ha quitado。
2. 将以下代码行添加到程序集信息文件：

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. 向 LocalizingResources 项目中添加对 System.Web 和 System.Web.Extensions 的引用。
2. 添加对 LocalizingResources 项目中的网站项目的引用。
3. 在 default.aspx 中，在网站项目下，使用以下其他标记中更新 ScriptManager 控件：

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. 在 default.aspx 中，任意位置在页上，包括此标记：

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. 按 F5。 如果系统提示，请启用调试。 加载页面时，按删除按钮。 请注意，您会提示您在英语中 （除非默认情况下，您的计算机设置为首选西班牙语语言资源） 进行确认。
2. 关闭浏览器窗口并返回到 default.aspx。 在@Page标头指令，使用 ES-ES 区域性和 UICulture 替换为自动。 按 F5 再次启动 web 浏览器中一次应用程序。 这一次，请注意，系统会提示删除在西班牙语中的文件：


[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

([单击此项可查看原尺寸图像](understanding-asp-net-ajax-localization/_static/image3.png))


[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

([单击此项可查看原尺寸图像](understanding-asp-net-ajax-localization/_static/image6.png))


请注意，在本演练中的多个变体。 例如，脚本不能注册使用 ScriptManager 控件以编程方式在页面加载过程。

## <a name="including-a-static-script-file-structure"></a>*包括静态脚本文件结构*

当使用静态脚本文件进行部署，您会失去一些使用固有的.NET 本地化方案的好处。 主要可见，则是你将失去包括脚本资源文件; 从生成的自动类型在上面的演练，例如，资源已公开由称为消息从 ScriptManager 控件自动生成类型。

有，但是，到使用静态脚本文件结构的一些好处。 可以执行更新而无需重新编译和重新部署附属程序集，并使用静态文件结构也可以重写嵌入的脚本，以将一次要项可能尚未装运的功能与组件相集成。

Microsoft 建议避免通过自动在项目编译期间生成的脚本资源的版本控制问题。 维护大量的脚本代码基，它会变为越来越困难，以确保代码更改会反映在每个本地化的脚本。 或者，您可以只需维护一个逻辑脚本和多个本地化脚本，生成项目的同时合并文件。

由于不是以声明方式包含的资源，应包含文件的静态脚本引用通过添加`<asp:ScriptElement>`元素作为子级`<Scripts>`标记的 ScriptManager 控件，或以编程方式添加`ScriptReference`对象向`Scripts`属性的`ScriptManager`在运行时页面上的控件。

## <a name="the-scriptmanager-and-its-role-in-localization"></a>*ScriptManager 和本地化中的其角色*

ScriptManager 使本地化的应用程序的多个自动行为：

- 它会自动查找基于设置和命名约定; 的脚本文件例如，它将加载在调试模式下，启用了调试的脚本，并加载本地化基于浏览器的用户界面选择的脚本。
- 它使您能够定义包括自定义区域性的区域性。
- 它支持通过 HTTP 的脚本文件的压缩。
- 它将缓存脚本来有效地管理多个请求。
- 它将一个间接层添加到脚本中，其通过管道通过加密的 URL。

可以将脚本引用添加到 ScriptManager 控件，通过编程方式或声明性标记。 声明性标记时，尤其是使用脚本中嵌入的程序集，而不是网站项目本身，如脚本的名称可能不会更改如修订推送。

## <a name="summary"></a>总结

随着 web 应用程序扩大受众更大，需要能够访问更广泛的区域性和社区将成为核心的业务模型;电子商务 web 应用程序需要能够处理外币，内容管理系统要求是其内容，但还其导航提示和其他语言和公司中的窗体字段需要知道这种需求不仅能存在可访问。

.NET Framework 本质上支持的丰富本地化框架，利用附属程序集和 XML 资源 (.resx) 文件以提供统一的方法来查找资源字符串和图像。 ASP.NET AJAX 扩展，其中包括 Microsoft AJAX Framework 和 Microsoft AJAX 脚本库中，为提供支持这一编程模型到客户端代码中，启用简单的资源字符串查找。 只要文件名遵循给定的命名方案，附属程序集支持自动包含通过 ScriptResource.axd 脚本资源 （实际的.js 文件）。 利用此支持，ASP.NET AJAX Extensions 简化脚本的本地化和全球化应用程序。

## <a name="bio"></a>*个人简介*

Scott Cate 自 1997 年以来一直致力于 Microsoft Web 技术和 myKB.com 总裁 ([www.myKB.com](http://www.myKB.com)) 专门负责编写 ASP.NET 基于侧重于知识库软件解决方案的应用程序。 可以通过电子邮件联系 Scott [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com)或他的博客[ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [上一页](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
> [下一页](understanding-asp-net-ajax-web-services.md)
