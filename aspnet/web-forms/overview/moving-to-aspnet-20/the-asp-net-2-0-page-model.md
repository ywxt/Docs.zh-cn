---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 页面模型 |Microsoft Docs
author: microsoft
description: 在 ASP.NET 1.x 中，开发人员必须使用内联代码模型和代码隐藏代码模型之间进行选择。 无法使用任一 Src attr 实现代码隐藏...
ms.author: aspnetcontent
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 2c8a0624af30d93d2ba68dc4b0b0880d6e371616
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811696"
---
<a name="the-aspnet-20-page-model"></a>ASP.NET 2.0 页面模型
====================
by [Microsoft](https://github.com/microsoft)

> 在 ASP.NET 1.x 中，开发人员必须使用内联代码模型和代码隐藏代码模型之间进行选择。 可以使用 Src 属性或代码隐藏文件属性的实现代码隐藏@Page指令。 在 ASP.NET 2.0 中，开发人员仍然可以内联代码和代码隐藏之间进行选择，但有了显著改进代码隐藏模型。


在 ASP.NET 1.x 中，开发人员必须使用内联代码模型和代码隐藏代码模型之间进行选择。 可以使用 Src 属性或代码隐藏文件属性的实现代码隐藏@Page指令。 在 ASP.NET 2.0 中，开发人员仍然可以内联代码和代码隐藏之间进行选择，但有了显著改进代码隐藏模型。

## <a name="improvements-in-the-code-behind-model"></a>在代码隐藏模型中的改进

以全面了解 ASP.NET 2.0 中的代码隐藏模型中的更改，其最大努力来快速查看模型作为它存在于 ASP.NET 1.x。

## <a name="the-code-behind-model-in-aspnet-1x"></a>在 ASP.NET 中的代码隐藏模型 1.x

在 ASP.NET 1.x 中，代码隐藏模型组成一个 ASPX 文件 （web 窗体） 和包含编程代码的代码隐藏文件。 两个文件连接使用@Page指令 ASPX 文件中。 ASPX 页的每个控件实例变量作为代码隐藏文件中有相应的声明。 代码隐藏文件还包含有关事件绑定的代码和生成的 Visual Studio 设计器所需的代码。 此模型的效果非常好，但由于 ASPX 页中的每个 ASP.NET 元素所需的代码隐藏文件中的相应代码，有没有真正分离的代码和内容。 例如，如果设计器添加到 Visual Studio IDE 外部 ASPX 文件新的服务器控件，该应用程序将会破坏由于没有为该控件声明的代码隐藏文件中。

## <a name="the-code-behind-model-in-aspnet-20"></a>ASP.NET 2.0 中的代码隐藏模型

ASP.NET 2.0 可大大提高了此模型。 在 ASP.NET 2.0 中，代码隐藏实现使用新*分部类*ASP.NET 2.0 中提供。 ASP.NET 2.0 中的代码隐藏类是定义为分部类，这意味着它包含仅的类定义的一部分。 类定义的剩余部分是动态生成的 ASP.NET 2.0 在运行时或在预编译网站时使用的 ASPX 页。 使用 @ Page 指令仍建立的代码隐藏文件和 ASPX 页面之间的链接。 但是，而不是代码隐藏文件或 Src 属性中，ASP.NET 2.0 现在使用 CodeFile 属性。 Inherits 特性也用于指定页面的类名称。

典型的 @ Page 指令可能如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

ASP.NET 2.0 代码隐藏文件中的典型类定义可能如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C# 和 Visual Basic 是目前支持分部类的唯一托管的语言。 因此，使用 J# 开发人员将不能使用 ASP.NET 2.0 中的代码隐藏模型。


新模型增强了代码隐藏模型，因为开发人员现在可以包含用户创建的代码的代码文件。 它还提供的则返回 true 的代码和内容分隔由于没有任何实例变量声明中的代码隐藏文件。

> [!NOTE]
> ASPX 页的分部类是事件绑定发生的地方，因为 Visual Basic 开发人员可以通过使用在代码隐藏中的句柄关键字将事件绑定实现性能稍有提升。 C# 具有任何等效的关键字。


## <a name="new--page-directive-attributes"></a>新的 @ Page 指令属性

ASP.NET 2.0 将多个新属性添加到 @ Page 指令。 以下属性是 ASP.NET 2.0 中的新增功能。

## <a name="async"></a>Async

在 Async 属性允许您配置页后，可以以异步方式执行。 我们将介绍更高版本在此模块中的异步页面。

## <a name="asynctimeout"></a>AsyncTimeout

指定异步页面的超时时间。 默认值为 45 秒。

## <a name="codefile"></a>CodeFile

CodeFile 特性将取代 Visual Studio 2002/2003 中的代码隐藏特性。

### <a name="codefilebaseclass"></a>CodeFileBaseClass

在想要从一个基类派生的多个页的情况下使用 CodeFileBaseClass 属性。 由于在 ASP.NET 中，如果不使用此属性的分部类的实现使用共享的常见字段来引用在 ASPX 页面中声明的控件的基类将不能正常工作因为 ASP。网络编译引擎将自动创建基于页面中控件的新成员。 因此，如果想在 ASP.NET 中的两个或多个页面的一个公共基类，您将需要定义 CodeFileBaseClass 属性中指定基类，然后从该基类派生的每个页面类。 CodeFile 特性，还需要使用此属性时。

## <a name="compilationmode"></a>CompilationMode

此属性可以设置 ASPX 页的 CompilationMode 属性。 CompilationMode 属性是一个枚举，包含的值**Always**，**自动**，并**从不**。 默认值是**始终为**。 **自动**设置将阻止 ASP.NET 动态编译页面在可能的情况。 从动态编译中排除页面可以提高性能。 但是，如果排除的页面包含必须编译该代码，浏览页时将会引发错误。

## <a name="enableeventvalidation"></a>EnableEventValidation

此属性指定验证回发和回调事件。 启用此功能后，要回发参数或回调事件就会检查以确保它们源自最初呈现它们的服务器控件。

## <a name="enabletheming"></a>EnableTheming

此属性指定在页面上使用 ASP.NET 主题。 默认值为 false。 中介绍了 ASP.NET 主题[模块 10](profiles-themes-and-web-parts.md)。

## <a name="linepragmas"></a>LinePragmas

此属性指定是否应在编译期间添加行杂注。 行杂注是调试器用于标记代码的特定部分的选项。

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

此属性指定 JavaScript 注入到页面以维护回发之间滚动位置。 此属性是**false**默认情况下。

当此属性是 **，则返回 true**，ASP.NET 将添加&lt;脚本&gt;块在回发时的外观如下所示：

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

请注意，此脚本块的 src WebResource.axd。 此资源不是物理路径。 当请求此脚本时，ASP.NET 动态生成脚本。

### <a name="masterpagefile"></a>MasterPageFile

此属性指定当前页的主控页文件。 路径可以是相对值还是绝对值。 中介绍了母版页[模块 4](master-pages.md)。

## <a name="stylesheettheme"></a>StyleSheetTheme

此属性允许你重写由 ASP.NET 2.0 主题定义的用户界面外观属性。 主题中介绍[模块 10](profiles-themes-and-web-parts.md)。

## <a name="theme"></a>主题

指定的页面的主题。 如果没有为 StyleSheetTheme 属性指定一个值，在 Theme 特性重写应用于控件的页上的所有样式。

## <a name="title"></a>标题

设置页面标题。 此处指定的值将出现在&lt;标题&gt;呈现页面上的元素。

### <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

设置 ViewStateEncryptionMode 枚举的值。 可用值为**Always**，**自动**，并**从不**。 默认值是**自动**。如果此属性设置为值**自动**，加密视图状态是控件请求通过调用**RegisterRequiresViewStateEncryption**方法。

## <a name="setting-public-property-values-via-the--page-directive"></a>设置公共属性的值通过 @ Page 指令

ASP.NET 2.0 中的 @ Page 指令的另一新功能是能够设置基类的公共属性的初始值。 假设，例如，具有公共属性称为**SomeText**基类还意愿它初始化为**Hello**加载页时。 您可以完成此操作通过只需在 @ Page 指令中设置的值如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

**SomeText** @ Page 指令的特性设置到基类中 SomeText 属性的初始值*Hello ！*。 下面的视频是使用 @ Page 指令的基类中设置的公共属性的初始值的演练。


![](the-asp-net-2-0-page-model/_static/image1.png)


[打开的全屏视频](the-asp-net-2-0-page-model/_static/setprop1.wmv)


## <a name="new-public-properties-of-the-page-class"></a>页类的新的公共属性

以下公共属性是 ASP.NET 2.0 中新增的。

## <a name="apprelativetemplatesourcedirectory"></a>AppRelativeTemplateSourceDirectory

返回到页或控件的应用程序相对路径。 例如，对于位于一个页面 http://app/folder/page.aspx，该属性返回 ~ / 文件夹 /。

## <a name="apprelativevirtualpath"></a>AppRelativeVirtualPath

返回的页或控件的相对虚拟目录路径。 例如对于位于一个页面 http://app/folder/page.aspx，该属性返回 ~ / folder/page.aspx。

## <a name="asynctimeout"></a>AsyncTimeout

获取或设置用于异步页处理的超时值。 （异步页面将在后面进行介绍此模块。）

## <a name="clientquerystring"></a>ClientQueryString

返回所请求的 URL 的查询字符串部分的只读属性。 此值进行 URL 编码。 HttpServerUtility 类的 UrlDecode 方法可用于对其进行解码。

## <a name="clientscript"></a>ClientScript

此属性返回可用于管理 ASP.NETs 句子的客户端脚本的 ClientScriptManager 对象。 （ClientScriptManager 类介绍此模块中的更高版本中）。

## <a name="enableeventvalidation"></a>EnableEventValidation

此属性控制启用事件验证回发和回调事件。 启用时，要回发参数或回调事件进行验证以确保它们源自最初呈现它们的服务器控件。

## <a name="enabletheming"></a>EnableTheming

此属性获取或设置一个布尔值，指定 ASP.NET 2.0 主题应用于页面。

## <a name="form"></a>窗体

此属性为 HtmlForm 对象返回 ASPX 页上的 HTML 窗体。

## <a name="header"></a>Header

此属性返回对包含页眉的 HtmlHead 对象的引用。 可以使用返回的 HtmlHead 对象来获取或设置样式表、 Meta 标记，等等。

## <a name="idseparator"></a>IdSeparator

此只读属性获取用于分隔控件标识符，当 ASP.NET 在生成的唯一 ID 的页面上的控件时的字符。 它不可直接通过代码使用。

## <a name="isasync"></a>IsAsync

此属性允许异步页面。 更高版本中此模块讨论了异步页面。

## <a name="iscallback"></a>IsCallback

此只读属性返回 **，则返回 true**如果页是调用返回的结果。 更高版本中此模块讨论了回拨。

## <a name="iscrosspagepostback"></a>IsCrossPagePostBack

此只读属性返回 **，则返回 true**如果页是跨页回发的一部分。 此模块中稍后介绍跨页回发。

## <a name="items"></a>项

返回到 IDictionary 实例，其中包含存储在页上下文中的所有对象的引用。 可以将项添加到此 IDictionary 对象以及他们将在上下文的整个生存期内可用。

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostBack

此属性控制 ASP.NET 发出保持页滚动位置，在浏览器中的，为在回发发生后的 JavaScript。 （此属性的详细信息讨论了之前在此模块中。）

## <a name="master"></a>Master

此只读属性返回对已应用主页面的页面 MasterPage 实例的引用。

## <a name="masterpagefile"></a>MasterPageFile

获取或设置页面的母版页文件名。 仅可以 PreInit 方法中设置此属性。

## <a name="maxpagestatefieldlength"></a>MaxPageStateFieldLength

此属性获取或设置页状态的最大长度以字节为单位。 如果该属性设置为正数，页面视图状态将分解为多个隐藏字段，以便它不会超过指定的字节数。 如果该属性为一个负数，视图状态将不会划分为区块。

## <a name="pageadapter"></a>PageAdapter

返回对修改的页请求的浏览器的 PageAdapter 对象的引用。

## <a name="previouspage"></a>PreviousPage

在 Server.Transfer 或跨页回发的情况下返回到前一页的引用。

## <a name="skinid"></a>SkinID

指定要应用于页的 ASP.NET 2.0 外观。

## <a name="stylesheettheme"></a>StyleSheetTheme

此属性获取或设置应用于页的样式表。

## <a name="templatecontrol"></a>TemplateControl

返回到页包含的控件的引用。

## <a name="theme"></a>主题

获取或设置应用于页面的 ASP.NET 2.0 主题的名称。 必须在 PreInit 方法之前设置此值。

## <a name="title"></a>标题

此属性获取或设置页面标题，从页面标头中获得。

## <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

获取或设置页面的 ViewStateEncryptionMode。 请参阅本模块前面的此属性的详细的讨论。

## <a name="new-protected-properties-of-the-page-class"></a>页类的新的受保护的属性

以下是 ASP.NET 2.0 中的页类的新的受保护的属性。

## <a name="adapter"></a>适配器

返回的引用将在设备上的页呈现了 ControlAdapter 请求它。

## <a name="asyncmode"></a>AsyncMode

此属性指示以异步方式处理页。 由运行时并不是直接在代码中，它被供使用。

## <a name="clientidseparator"></a>ClientIDSeparator

此属性返回时为控件创建唯一的客户端 Id，用作分隔符的字符。 由运行时并不是直接在代码中，它被供使用。

## <a name="pagestatepersister"></a>PageStatePersister

此属性返回页面的 PageStatePersister 对象。 此属性主要由 ASP.NET 控件开发人员使用。

## <a name="uniquefilepathsuffix"></a>UniqueFilePathSuffix

此属性返回唯一 suffic 追加到用于缓存浏览器的文件路径。 默认值是\_ \_ufps = 和一个 6 位数字。

## <a name="new-public-methods-for-the-page-class"></a>用于 Page 类的新公共方法

以下公共方法不熟悉 ASP.NET 2.0 中的页类。

## <a name="addonprerendercompleteasync"></a>AddOnPreRenderCompleteAsync

此方法注册为异步页执行的事件处理程序委托。 更高版本中此模块讨论了异步页面。

## <a name="applystylesheetskin"></a>ApplyStyleSheetSkin

适用于页的页样式表中的属性。

## <a name="executeregisteredasynctasks"></a>ExecuteRegisteredAsyncTasks

此方法才会异步任务。

### <a name="getvalidators"></a>GetValidators

如果未指定，则返回的验证程序指定的验证组或默认验证组的集合。

## <a name="registerasynctask"></a>RegisterAsyncTask

此方法注册一个新的异步任务。 此模块中稍后介绍异步页面。

## <a name="registerrequirescontrolstate"></a>RegisterRequiresControlState

此方法告诉 ASP.NET，必须将页控件状态保存。

## <a name="registerrequiresviewstateencryption"></a>RegisterRequiresViewStateEncryption

此方法会告知 ASP.NET 页视图状态，需要加密。

## <a name="resolveclienturl"></a>ResolveClientUrl

返回可用于图像等的客户端请求的相对 URL。

## <a name="setfocus"></a>SetFocus

此方法会将焦点设置到最初加载页面时指定的控件。

## <a name="unregisterrequirescontrolstate"></a>UnregisterRequiresControlState

此方法将取消注册为不再需要控件状态持久性传递给它的控件。

## <a name="changes-to-the-page-lifecycle"></a>对页面生命周期的更改

在 ASP.NET 2.0 中的页面生命周期尚未发生显著变化，但应注意的一些新方法。 下面列出了在 ASP.NET 2.0 页面生命周期。

## <a name="preinit-new-in-aspnet-20"></a>PreInit （中 ASP.NET 2.0)

PreInit 事件是一名开发人员可以访问的生命周期中的最早阶段。 此事件添加会使可能要以编程方式更改 ASP.NET 2.0 主题，主页面，请访问 ASP.NET 2.0 配置文件等的属性。如果您是在回发状态下，一定要认识到，视图状态具有尚未应用到控件此时生命周期中。 因此，如果在此阶段，开发人员更改控件的属性，它将可能覆盖页面生命周期中更高版本。

## <a name="init"></a>Init

Init 事件未更改从 ASP.NET 1.x。 这是你想要读取或初始化您的页面上的控件的属性。 在此阶段、 母版页、 主题等已应用到的页。

## <a name="initcomplete-new-in-20"></a>InitComplete （中 2.0)

在页初始化阶段结束时，调用 InitComplete 事件。 此时在生命周期中，可以访问控件的页上，但尚未填充其状态。

## <a name="preload-new-in-20"></a>预加载 （2.0 中的新增功能）

已应用所有回发数据后，只需在页之前调用此事件\_负载。

## <a name="load"></a>Load

加载事件未更改从 ASP.NET 1.x。

## <a name="loadcomplete-new-in-20"></a>LoadComplete （中 2.0)

LoadComplete 事件是在页加载阶段中的最后一个事件。 在此阶段，回发和视图状态的所有数据已都应用到的页。

## <a name="prerender"></a>PreRender

如果您要用于视图状态的控件的动态添加到页面中正确维护，PreRender 事件是将其添加的最后机会。

## <a name="prerendercomplete-new-in-20"></a>PreRenderComplete （中 2.0)

在 PreRenderComplete 阶段中，所有控件已都添加到页和页已准备好呈现。 PreRenderComplete 事件是页面视图状态保存之前引发的最后一个事件。

## <a name="savestatecomplete-new-in-20"></a>SaveStateComplete （中 2.0)

已保存所有页面视图状态和控件状态后立即调用 SaveStateComplete 事件。 这是页面实际上呈现到浏览器之前的最后一个事件。

## <a name="render"></a>呈现

Render 方法未更改以来 ASP.NET 1.x。 这是初始化 HtmlTextWriter 和页呈现到浏览器的位置。

## <a name="cross-page-postback-in-aspnet-20"></a>ASP.NET 2.0 中的跨页回发

在 ASP.NET 1.x 中，回发所需发布到相同的页面。 不允许跨页回发。 ASP.NET 2.0 添加了回发到不同的页通过 IButtonControl 接口的功能。 实现新 IButtonControl 接口 （按钮、 LinkButton 和第三方自定义控件除了 ImageButton） 的任何控件可以充分利用这一新功能通过 PostBackUrl 属性的使用。 下面的代码显示回发到第二个页的按钮控件。

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

页面回发，启动回发页面时，可通过第二个页面的 PreviousPage 属性进行访问。 通过新的 web 窗体中实现此功能\_DoPostBackWithOptions 控件回发到不同的页时，ASP.NET 2.0 将呈现给页的客户端函数。 此 JavaScript 函数提供的新的 WebResource.axd 处理程序用来发出到客户端脚本。

下面的视频是跨页回发的演练。


![](the-asp-net-2-0-page-model/_static/image2.png)


[打开的全屏视频](the-asp-net-2-0-page-model/_static/xpage1.wmv)


## <a name="more-details-on-cross-page-postbacks"></a>在跨页回发的更多详细信息

### <a name="viewstate"></a>视图状态

您可能已要求自己已发生视图状态从跨页回发方案中的第一页有关。 毕竟，不实现 IPostBackDataHandler 任何控件将其状态保存通过视图状态，因此有权访问该控件在跨页回发的第二页上的属性，必须具有对页面视图状态的访问。 ASP.NET 2.0 负责这种情况下，使用名为的第二个页中的新的隐藏的字段\_ \_PREVIOUSPAGE。 \_ \_PREVIOUSPAGE 窗体字段包含的第一页的视图状态，以便您可以在第二页中有权访问所有控件的属性。

### <a name="circumventing-findcontrol"></a>绕过 FindControl

在跨页回发的视频演练中，我使用的 FindControl 方法来获取对第一页上的文本框控件的引用。 该方法非常适用于此目的，但 FindControl 很高，它需要编写附加代码。 幸运的是，ASP.NET 2.0 提供了实现此目的，可以在许多方案的 FindControl 的替代方法。 PreviousPageType 指令，可通过使用类型名称或 VirtualPath 属性具有对前一页的强类型引用。 TypeName 特性，可指定前一页的类型，但 VirtualPath 特性，您可以使用虚拟路径的上一页，请参阅。 设置 PreviousPageType 指令后，则必须公开控件，你想要允许使用公共属性的访问等。

## <a name="lab-1-cross-page-postback"></a>实验室 1 跨页回发

在此实验中，将创建使用新的 ASP.NET 2.0 跨页回发的功能的应用程序。

1. 打开 Visual Studio 2005 并创建新的 ASP.NET Web 站点。
2. 添加名为 page2.aspx 的新 web 窗体。
3. 在设计视图中打开 Default.aspx 并添加一个按钮控件和文本框控件。 

    1. 提供的 ID 的按钮控件**SubmitButton**和 TextBox 控件的 ID**用户名**。
    2. 将按钮的 PostBackUrl 属性设置为 page2.aspx。
4. 在源视图中打开 page2.aspx。
5. 添加一个 @ PreviousPageType 指令，如下所示：
6. 将以下代码添加到页\_page2.aspx 的代码隐藏的负载： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. 通过单击生成菜单上生成中生成项目。
8. 将以下代码添加到 Default.aspx 代码隐藏： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. 更改的页\_中所示的 page2.aspx 负载： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. 生成项目。
11. 运行该项目。
12. 在文本框中输入你的名称，然后单击按钮。
13. 结果是什么？

## <a name="asynchronous-pages-in-aspnet-20"></a>ASP.NET 2.0 中异步页面

在 ASP.NET 中的很多争用问题所引起的延迟的外部调用 （例如 Web 服务或数据库调用），文件 IO 延迟，等等。当针对 ASP.NET 应用程序发出请求时，ASP.NET 将使用其工作线程之一来该请求提供服务。 该请求拥有该线程，直到完成该请求并发送响应。 ASP.NET 2.0 致力于通过添加以异步方式执行页的功能来解决这些类型的问题的延迟问题。 这意味着工作线程可以启动请求，然后移交到另一个线程，从而快速返回到可用的线程池的其他执行。 完成后的文件 IO、 数据库调用等，请从线程池，以完成请求获取新的线程。

进行异步执行的页的第一步是设置**异步**页指令的特性如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

此属性告知 ASP.NET 实现 IHttpAsyncHandler 页。

下一步是在之前 PreRender 页生命周期中的点调用 AddOnPreRenderCompleteAsync 方法。 (此方法通常在页面中调用\_负载。)AddOnPreRenderCompleteAsync 方法采用两个参数;来和 EndEventHandler。 来返回到 EndEventHandler 然后作为参数传递的 IAsyncResult。

以下视频是异步页请求的演练。


![](the-asp-net-2-0-page-model/_static/image3.png)


[打开的全屏视频](the-asp-net-2-0-page-model/_static/async1.wmv)


> [!NOTE]
> 直到完成 EndEventHandler 某个异步页面不呈现到浏览器中。 毫无疑问，但某些开发人员将认为视作类似于异步回调的异步请求。 请务必认识到它们不是。 异步请求的好处是，第一个工作线程可以返回到线程池来支持新请求，从而减少了由于 IO 绑定的争用，等等。


## <a name="script-callbacks-in-aspnet-20"></a>ASP.NET 2.0 中的脚本回调

Web 开发人员一直查找有关如何防止闪烁与回调相关联。 在 ASP.NET 1.x 中，SmartNavigation 避免闪烁，最常用方法但 SmartNavigation 导致问题的一些开发人员由于其在客户端上实现的复杂性。 ASP.NET 2.0 解决了这一问题的脚本回调。 脚本回调使用 XMLHttp 针对通过 JavaScript 的 Web 服务器发出请求。 XMLHttp 请求返回 XML 数据，然后可以操作通过浏览器的 dom。 XMLHttp 代码是对用户隐藏的新 WebResource.axd 处理程序。

有几个步骤所需以便配置 ASP.NET 2.0 中的脚本回调。

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>步骤 1： 实现 ICallbackEventHandler 接口

为了使 ASP.NET 可以识别您的页面为参与的脚本回调，您必须实现 ICallbackEventHandler 接口。 您可以执行此操作在代码隐藏文件如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

您也可以这样做因此使用 @ Implements 指令类似于：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

使用内联 ASP.NET 代码时，通常会使用 @ Implements 指令。

## <a name="step-2--call-getcallbackeventreference"></a>步骤 2： 调用 GetCallbackEventReference

正如前面提到，XMLHttp 调用被封装在 WebResource.axd 处理程序。 ASP.NET 呈现页面时，将添加对 web 窗体的调用\_DoCallback，WebResource.axd 的支持提供的客户端脚本。 该 web 窗体\_DoCallback 函数将替换\_ \_doPostBack 回调函数。 请记住， \_ \_doPostBack 以编程方式提交窗体页上的。 在回调方案中，你想要防止在回发，因此\_ \_doPostBack 将无法满足需要。

> [!NOTE]
> \_\_doPostBack 仍呈现到客户端脚本回调情形中的页。 但是，它不用于回调。


该 web 窗体的自变量\_DoCallback 客户端函数提供通过服务器端函数通常会在页面中调用的 GetCallbackEventReference\_负载。 对 GetCallbackEventReference 的典型调用如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> 在这种情况下，cm 是 ClientScriptManager 实例。 ClientScriptManager 类将在此模块的后面进行介绍。


有多个重载的版本的 GetCallbackEventReference。 在这种情况下，参数是按如下所示：

`this`

对调用 GetCallbackEventReference 控件的引用。 在这种情况下，它是页面本身。

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

服务器端事件将从客户端代码中传递一个字符串参数。 在这种情况下，将下拉列表中的值传递的 Im 调用 ddlCompany。

`ShowCompanyName`

将接受的返回值 （作为字符串） 从服务器端的回调事件的客户端函数的名称。 服务器端的回调成功后，将仅调用此函数。 因此，为了可靠性，通常建议使用 GetCallbackEventReference 使用指定的要发生错误时执行的客户端的函数名称的其他字符串参数的重载的版本。

`null`

一个表示它在回调到服务器之前启动的客户端函数的字符串。 在这种情况下，没有任何此类脚本，因此该参数为 null。

`true`

一个布尔值，指定以异步方式执行回调。

对 web 窗体调用\_DoCallback 客户端上的会将这些参数传递。 因此，在客户端上呈现此页面时，该代码看起来如下所示：

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

请注意，在客户端上函数的签名稍有不同。 5 个字符串和布尔值，将传递客户端函数。 （这是 null，在上面的示例中） 的附加字符串包含将处理服务器端的回调中的所有错误的客户端函数。

## <a name="step-3--hook-the-client-side-control-event"></a>步骤 3： 挂接的客户端的控件事件

请注意，上述 GetCallbackEventReference 的返回值分配给字符串变量。 该字符串用于挂接启动回调的控件的客户端的事件。 在此示例中，该回调由启动下拉列表中的页上，我想要挂接*OnChange*事件。

若要挂接客户端事件中，只需将一个处理程序添加到客户端的标记，如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

请记住， *cbRef* GetCallbackEventReference 调用的返回值。 它包含对 web 窗体调用\_DoCallback 上面所示。

## <a name="step-4--register-the-client-side-script"></a>步骤 4： 注册客户端脚本

回想一下，对 GetCallbackEventReference 调用指定客户端脚本调用**ShowCompanyName**服务器端的回调成功时将执行。 该脚本需要添加到使用 ClientScriptManager 实例的页面。 （ClientScriptManager 类将是更高版本在此模块中的讨论。）因此执行操作，类似于：

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>步骤 5： 调用 ICallbackEventHandler 接口的方法

ICallbackEventHandler 包含你需要在代码中实现的两个方法。 它们是**RaiseCallbackEvent**并**GetCallbackEvent**。

**RaiseCallbackEvent**采用字符串作为参数并不返回任何内容。 字符串参数传递到 web 窗体客户端调用\_DoCallback。 在这种情况下，此值是*值*调用 ddlCompany 下拉列表中的属性。 服务器端代码应置于 RaiseCallbackEvent 方法。 例如，如果您的回调正在对外部资源 WebRequest，该代码应放置在 RaiseCallbackEvent。

**GetCallbackEvent**负责处理回调的返回到客户端。 它不采用任何参数并返回一个字符串。 它将返回的字符串将被作为参数传递给客户端的函数，在这种情况下*ShowCompanyName*。

完成上述步骤后，你现可在 ASP.NET 2.0 中执行的脚本回调。


![](the-asp-net-2-0-page-model/_static/image4.png)


[打开的全屏视频](the-asp-net-2-0-page-model/_static/callback1.wmv)


在 ASP.NET 中的脚本回调中支持使 XMLHttp 调用任何浏览器支持。 中包括的所有新式浏览器中使用今天。 Internet Explorer 使用 XMLHttp ActiveX 对象，而其他现代浏览器 （包括即将推出的 IE 7） 使用的内部的 XMLHttp 对象。 若要以编程方式确定是否浏览器支持回调，则可以使用**Request.Browser.SupportCallback**属性。 此属性将返回 **，则返回 true**如果请求的客户端支持的脚本回调。

## <a name="working-with-client-script-in-aspnet-20"></a>使用 ASP.NET 2.0 中的客户端脚本

在 ASP.NET 2.0 中的客户端脚本通过 ClientScriptManager 类的使用进行管理。 跟踪客户端脚本使用一种类型和名称的 ClientScriptManager 类。 这可以防止同一个脚本以编程方式插入页面上一次以上。

> [!NOTE]
> 脚本已成功注册页面上后，任何后续尝试注册相同的脚本只需将导致未注册第二次该脚本。 添加任何重复的脚本，并且没有发生异常。 若要避免不必要的计算，有可用于确定脚本是否已注册，以便不尝试超过一次注册的方法。


Clientscriptmanager 处理的方法应为所有当前的 ASP.NET 开发人员所熟悉:

## <a name="registerclientscriptblock"></a>RegisterClientScriptBlock

此方法将脚本添加到呈现的页的顶部。 这可用于添加将在客户端显式调用的函数。

有两个重载的版本，此方法。 三个四个参数是在它们之间通用。 它们是：

`type (string)`

***类型***参数标识脚本的类型。 它通常是一个好办法，请使用页面的类型 （这。GetType()) 的类型。

`key (string)`

***密钥***参数是该脚本的用户定义键。 这应该是唯一的每个脚本。 如果尝试添加具有相同的密钥和已添加了脚本的类型的脚本，将不会添加它。

`script (string)`

***脚本***参数是一个包含要添加的实际脚本的字符串。 建议使用 StringBuilder 创建脚本，然后使用 StringBuilder 上的 tostring （） 方法来分配***脚本***参数。

如果使用重载的 RegisterClientScriptBlock 只使用三个参数，则必须包括脚本元素 (&lt;脚本&gt;并&lt;/script&gt;) 在脚本中。

您可以选择使用 RegisterClientScriptBlock 第四个自变量的重载。 第四个参数是一个布尔值，指定 ASP.NET 应为您添加脚本元素。 如果此参数，则 **，则返回 true**，您的脚本不应包含的脚本元素显式。

IsClientScriptBlockRegistered 方法用于确定是否已注册脚本。 这可以避免尝试重新注册已注册的脚本。

### <a name="registerclientscriptinclude-new-in-20"></a>RegisterClientScriptInclude （中 2.0)

RegisterClientScriptInclude 标记创建一个脚本块链接到外部脚本文件。 它有两个重载。 一种采用密钥和 URL。 第二个将添加第三个参数指定的类型。

例如，下面的代码的脚本块链接到 jsfunctions.js 根目录中生成的应用程序的 scripts 文件夹：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

此代码生成呈现的页面中的以下代码：

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> 脚本块呈现在页面底部。


IsClientScriptIncludeRegistered 方法用于确定是否已注册脚本。 这可以避免尝试重新注册的脚本。

## <a name="registerstartupscript"></a>RegisterStartupScript

RegisterStartupScript 方法采用与 RegisterClientScriptBlock 方法相同的参数。 RegisterStartupScript 中注册的脚本执行在页面加载之后、 但在 OnLoad 客户端的事件。 在 1.X 中，使用 RegisterStartupScript 已注册的脚本已放恰好在关闭之前&lt;/形成&gt;标记而 RegisterClientScriptBlock 与已注册的脚本已被放在打开后立即&lt;窗体&gt;标记。 在 ASP.NET 2.0 中，同时位于结束之前立即&lt;/&gt;标记。

> [!NOTE]
> 如果对 RegisterStartupScript 注册了一个函数，该函数不会执行，直到显式需在客户端代码中调用它即可。


IsStartupScriptRegistered 方法用于确定是否已注册一个脚本，从而避免尝试重新注册的脚本。

## <a name="other-clientscriptmanager-methods"></a>其他 ClientScriptManager 方法

以下是一些其他有用的 ClientScriptManager 类方法。


|  <strong>GetCallbackEventReference</strong>   |                                                 请参阅本模块前面的脚本回调。                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>GetPostBackClientHyperlink</strong>  |                获取 JavaScript 参考 (javascript:&lt;调用&gt;) 可用于从客户端事件重新发布。                 |
|  <strong>GetPostBackEventReference</strong>   |                                   获取一个字符串，可用来发起从客户端返回 post 调用。                                    |
|      <strong>GetWebResourceUrl</strong>       | 返回到程序集内嵌入的资源的 URL。 必须与结合使用<strong>RegisterClientScriptResource</strong>。 |
| <strong>RegisterClientScriptResource</strong> |     向页注册的 Web 资源。 以下是资源嵌入程序集中并由新的 WebResource.axd 处理程序处理。      |
|     <strong>RegisterHiddenField</strong>      |                                                 向页注册隐藏窗体字段。                                                 |
|  <strong>RegisterOnSubmitStatement</strong>   |                                  注册客户端代码执行时提交的 HTML 窗体。                                   |

