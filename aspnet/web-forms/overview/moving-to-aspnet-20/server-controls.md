---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 服务器控件 |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 增强了服务器控件在许多方面。 在此模块中，我们将介绍一些方法 ASP.NET 2.0 和 Visual Studio 200 体系结构的更改...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: ecf99fa894c1f662542aa8a613195b828bf2c67b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830892"
---
<a name="server-controls"></a>服务器控件
====================
by [Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 增强了服务器控件在许多方面。 在此模块中，我们将介绍一些 ASP.NET 2.0 的方式对体系结构更改，Visual Studio 2005 处理服务器控件。


ASP.NET 2.0 增强了服务器控件在许多方面。 在此模块中，我们将介绍一些 ASP.NET 2.0 的方式对体系结构更改，Visual Studio 2005 处理服务器控件。

## <a name="view-state"></a>视图状态

在视图状态在 ASP.NET 2.0 中的主要更改是大大缩短了大小。 请考虑仅在其上一个日历控件的页。 下面是在 ASP.NET 1.1 中的视图状态。

[!code-css[Main](server-controls/samples/sample1.css)]

现在这是视图状态在相同页上中 ASP.NET 2.0。

[!code-css[Main](server-controls/samples/sample2.css)]

这是相当明显的更改，并考虑在网络上来回传送视图状态，此更改可以为开发人员提供性能将显著提高。 大小减少的视图状态是很大程度上因为我们在内部处理的方式。 请记住，视图状态是 Base64 编码的字符串。 若要更好地了解 ASP.NET 2.0 中在视图状态更改，让我们来看，在上面的示例中的已解码值。

以下是解码的 1.1 的视图状态：

[!code-css[Main](server-controls/samples/sample3.css)]

这可能看上去有点像乱码，但此处的模式。 在 ASP.NET 1.x 中，我们使用的单个字符来标识数据类型和分隔的值使用&lt;&gt;字符。 上面的视图状态示例中的"t"表示三联数。 三元数组包含一对 Arraylist （"l"表示 ArrayList。）这些 ArrayLists 之一包含为 int32 类型 ("i")，值为 1，另一个包含另一个三联数。 三元数组包含一对 Arraylist，等等。需要记住的重要一点是，我们使用三个一组包含对，我们确定的数据类型，通过以字母，我们使用&lt;和&gt;作为分隔符的字符。

在 ASP.NET 2.0 中，已解码的视图状态看起来有点不同。

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

您应注意到出现的已解码的视图状态大的变化。 此更改有多个体系结构的基础。 视图状态在 ASP.NET 1.x 使用 losformatter 将其中的数据序列。 在 2.0 中，我们将使用新的 ObjectStateFormatter 类。 此类被专门用于帮助进行序列化和反序列化的视图状态和控件状态。 （控件状态中将会讨论下一节。）有很多更改的序列化和反序列化发生的方法所获得的好处。 一个最显著的是与使用 TextWriter LosFormatter，不同 ObjectStateFormatter 使用 BinaryWriter 的事实。 这样，ASP.NET 2.0 存储视图状态一系列字节而不是字符串。 例如，采用一个整型。 在 ASP.NET 1.1 中，整数所需的视图状态的 4 个字节。 在 ASP.NET 2.0 中，该同一个整数只需要 1 个字节。 为了减少存储的视图状态的进行了其他增强功能。 日期时间值，例如，现在使用存储 TickCount 而不是一个字符串。

像所有的不够，特别要注意是支付给 1.x 中的视图状态的最大使用者之一是数据网格和类似控件的这一事实。 控件，如数据网格视图状态而言的主要缺点是信息的它通常包含大量重复。 在 ASP.NET 1.x 中，重复信息只需通过和重新生成了臃肿的视图状态存储。 在 ASP.NET 2.0 中，我们将使用新的 IndexedString 类来存储此类数据。 如果字符串重复发生，我们只需 IndexedString 和 IndexedString 对象的正在运行表中的索引存储令牌。

## <a name="control-state"></a>控件状态

开发人员必须与视图状态的主要牢骚之一是将其添加到 HTTP 有效负载的大小。 如前所述，视图状态的最大使用者之一是数据网格控件。 若要避免生成的数据网格视图状态的数量庞大，许多开发人员只需禁用该控件的视图状态。 遗憾的是，该解决方案不始终是一个较好。 视图状态在 ASP.NET 1.x 包含不仅为该控件的正确功能所需的数据。 它还包含有关控件的用户界面的状态信息。 这意味着如果你想要允许分页上 DataGrid 中，必须启用视图状态，即使不需要的所有查看 UI 信息，包含状态。 它是一个要么方案。

在 ASP.NET 2.0 中，控件状态便可解决很好地通过引入控件状态的问题。 控件状态包含绝对有必要让的特有功能的控件的数据。 与不同的视图状态，无法禁用控件状态。 因此，务必严格控制在控件状态中存储的数据。

> [!NOTE]
> 控件状态保存视图状态以及\_ \_VIEWSTATE 的隐藏窗体字段。


本视频是演练的视图状态和控件状态。


![](server-controls/_static/image1.png)


[打开的全屏视频](server-controls/_static/state1.wmv)


在读取和写入来控制状态的服务器控件的顺序，您必须执行三个步骤。

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>步骤 1： 调用 RegisterRequiresControlState 方法

RegisterRequiresControlState 方法将通知 ASP.NET 控件需要以保持控件状态。 它采用一个参数的类型是要注册的控件的控件。

请务必注意注册不会保留请求。 因此，此方法必须对每个请求调用如果一个控件，以保持控件状态。 建议在 OnInit 调用该方法。

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>步骤 2： 重写 savecontrolstate 来

Savecontrolstate 来方法保存自上次回发控件的控件的状态更改。 它返回一个表示控件的状态对象。

## <a name="step-3-override-loadcontrolstate"></a>步骤 3： 重写 LoadControlState

LoadControlState 方法加载到控件的已保存的状态。 该方法采用一个参数的类型对象，其中包含该控件的已保存的状态。

## <a name="full-xhtml-compliance"></a>完整的 XHTML 符合性

任何 Web 开发人员知道 Web 应用程序中的标准的重要性。 为了维护的基于标准的开发环境，ASP.NET 2.0 是完全符合 XHTML。 因此，所有标记都都根据 XHTML 标准中支持 HTML 4.0 的浏览器呈现或更高版本。

ASP.NET 1.1 中的文档类型定义如下所示：

[!code-html[Main](server-controls/samples/sample6.html)]

在 ASP.NET 2.0 中，默认文档类型定义如下所示：

[!code-html[Main](server-controls/samples/sample7.html)]

如果愿意，您可以更改通过配置文件中的 xhtmlConformance 节点的默认 XHML 符合性。 例如，web.config 文件中的以下节点将更改为 XHTML 1.0 Strict 的 XHTML 符合性：

[!code-xml[Main](server-controls/samples/sample8.xml)]

如果愿意，还可以配置 ASP.NET 用于在 ASP.NET 中使用的旧配置，如下所示的 1.x:

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>自适应呈现使用适配器

在 ASP.NET 1.x 中，包含的配置文件&lt;browserCaps&gt;填充 HttpBrowserCapabilities 对象的部分。 此对象允许开发人员能够确定哪些设备正在发出特定请求，并相应地呈现代码。 在 ASP.NET 2.0 中，模型改进了，现在使用新的 ControlAdapter 类。 ControlAdapter 类重写控件的生命周期中的事件，并控制在呈现控件基于用户代理的功能。 由浏览器定义文件 （.browser 文件扩展名的文件） 存储在 c:\windows\microsoft.net\framework\v2.0 中定义的特定用户代理的功能。\* \* \* \*\CONFIG\Browsers 文件夹。

> [!NOTE]
> ControlAdapter 类是一个抽象类。


更喜欢&lt;browserCaps&gt;部分 1.x 中，浏览器定义文件中的使用正则表达式来分析用户代理字符串以确定请求浏览器。 它它们定义为该用户代理的特定功能。 ControlAdapter 呈现控件通过呈现方法。 因此，如果重写的 Render 方法，您不应在基础类上调用呈现。 执行此操作可能会导致呈现发生两次，一次针对适配器，一次控件本身。

## <a name="developing-a-custom-adapter"></a>开发自定义适配器

可以通过继承了 ControlAdapter 开发自定义适配器。 此外，可以继承的抽象类 PageAdapter 在其中进行页面需要适配器的情况下。 通过完成的控件，以便自定义适配器的映射&lt;controlAdapters&gt;浏览器定义文件中的元素。 例如，浏览器定义文件中的以下 XML 将菜单控件映射到 MenuAdapter 类：

[!code-html[Main](server-controls/samples/sample10.html)]

使用此模型，它将成为控件开发人员若要针对某个特定设备或浏览器可以非常容易。 它还是开发人员可以完全控制每个设备上呈现页的方式非常简单。

## <a name="per-device-rendering"></a>每个设备呈现

在 ASP.NET 2.0 中的服务器控件属性可以指定每个设备使用特定于浏览器的前缀。 例如，下面的代码将更改取决于哪种设备用于浏览页面的标签的文本。

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

当从 Internet Explorer 浏览网页包含此标签时，标签将显示文本说"您将浏览 Internet Explorer。" 从 Firefox 浏览页面后，标签将显示文本"您将浏览 Firefox。" 当从其他设备浏览页面后时，它将显示"您将浏览未知设备。" 可以使用此特殊语法指定任何属性。

## <a name="setting-focus"></a>设置焦点

ASP.NET 1.x 开发人员经常询问如何在特定控件上设置初始焦点。 例如，在登录页上，为用户 ID 文本框中首次加载页面时获得焦点很有用。 在 ASP.NET 1.x 中，执行此操作需要编写一些客户端脚本。 即使此类脚本是一个简单的任务，它不再需要在 ASP.NET 2.0 中由于 SetFocus 方法。 SetFocus 方法采用一个参数，该值指示应接收焦点的控件。 此参数可以是控件的字符串形式表示的客户端 ID 或控件对象形式表示的服务器控件的名称。 例如，若要将初始焦点设置到 TextBox 控件调用 txtUserID 首次加载页面时，以下代码添加到页\_负载：

[!code-csharp[Main](server-controls/samples/sample12.cs)]

-或

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0 使用 Webresource.axd 处理程序 （前面讨论过） 来呈现一个设置焦点的客户端函数。 客户端函数的名称是 web 窗体\_AutoFocus 如下所示：

[!code-html[Main](server-controls/samples/sample14.html)]

或者，可以使用控件的焦点方法初始焦点设置到该控件。 Focus 方法派生控件类，可供所有 ASP.NET 2.0 控件。 还有可能发生验证错误时，将焦点设置到特定控件。 在更高版本的模块，将介绍的。

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2.0 中的新服务器控件

以下是在 ASP.NET 2.0 中的新服务器控件。 我们将介绍更高版本的模块中的其中一些更多详细信息。

## <a name="imagemap-control"></a>ImageMap 控件

ImageMap 控件，可通过添加热点可以启动回发或导航到的 URL 的图像。 有三种类型的热点;CircleHotSpot、 RectangleHotSpot 和 PolygonHotSpot。 在 Visual Studio 中或以编程方式在代码中的集合编辑器通过添加热点。 可用于在图像上绘制热点是没有用户界面。 必须以声明方式指定坐标和大小或 radius 的热点。 此外，还有在设计器中的一个热点没有可视化表示形式。 热点配置为导航到的 URL，如果是通过热点的 NavigateUrl 属性指定的 URL。 对于 post 回热点，PostBackValue 属性可用于在服务器端代码中传递回发中可检索的字符串。


![在 Visual Studio 中的作用点集合编辑器](server-controls/_static/image1.jpg)

**图 1**： 在 Visual Studio 中的作用点集合编辑器


## <a name="bulletedlist-control"></a>BulletedList 控件

BulletedList 控件是可以轻松地进行数据绑定的项目符号列表。 可排序列表 （编号） 或未通过 BulletStyle 属性排序。 列表中的每个项由 ListItem 对象表示。


![Visual Studio 中的 BulletedList 控件](server-controls/_static/image1.gif)

**图 2**： 在 Visual Studio 中的 BulletedList 控件


## <a name="hiddenfield-control"></a>HiddenField 控件

HiddenField 控件将隐藏窗体字段添加到您的页面，其值是服务器端代码中提供。 隐藏的窗体字段的值通常需要回发之间保持不变。 但是，它是恶意的用户可以更改回发值之前。 如果发生这种情况，HiddenField 控件将引发 ValueChanged 事件。 如果 HiddenField 控件中有敏感的信息和你想要确保其保持不变，则应在代码中处理 ValueChanged 事件。

## <a name="fileupload-control"></a>FileUpload 控件

ASP.NET 2.0 中的 FileUpload 控件使可能将文件上传到 Web 服务器通过 ASP.NET 页面。 此控件是非常类似于 ASP.NET 1.x HtmlInputFile 类有少数例外。 在 ASP.NET 1.x 中，会建议 PostedFile 属性，将检查是否为 null 以确定是否有一个很好的文件。 ASP.NET 2.0 中的 FileUpload 控件添加新的 HasFile 属性可用于同一目的和更高效。

PostedFile 属性仍可用于访问 HttpPostedFile 对象，但一些 HttpPostedFile 功能现已推出本质上与 FileUpload 控件。 例如，若要将上传的文件保存在 ASP.NET 1.x 中，调用 SaveAs 方法 HttpPostedFile 对象上。 使用 FileUpload 控件在 ASP.NET 2.0 中，将在 FileUpload 控件自身上调用 SaveAs 方法。

2.0 的行为 （和可能的最重要的更改） 中的另一个重大变化是，它不再需要之前将其保存到内存中加载整个上传的文件。 在 1.x 中，任何已上传的文件保存整个读入内存之前写入到磁盘。 此体系结构可防止大型文件上的传。

在 ASP.NET 2.0 中，httpRuntime 元素的 requestLengthDiskThreshold 属性，可配置多少千字节为单位保存在内存之前写入的缓冲区中到磁盘。

**重要**: MSDN 文档 （和其他位置的文档） 指定此值是以字节为单位 （而不是千字节），默认值为 256。 实际上在千字节为单位指定的值和默认值为 80。 通过默认值为 80 K，我们确保缓冲区不会不结束大型对象堆上。

## <a name="wizard-control"></a>向导控件

它是相当常见，会遇到 ASP.NET 开发人员尝试收集序列中的信息的使用面板"页"或通过将传输的页面所困扰。 在大多数情况，这项工作是一个令人沮丧，并且是较长时间。 新的向导控件允许用户熟悉的向导界面中的线性和非线性步骤，从而解决了问题。 向导控件显示输入窗体中的一系列步骤。 每个步骤是控件的特定类型 StepType 属性指定。 可用的步骤类型如下所示：

| **步骤类型** | **说明** |
| --- | --- |
| 自动 | 该向导会自动确定基于步骤层次结构中其位置的步骤的类型。 |
| Start | 第一步，通常用于提供介绍性语句。 |
| 步骤 | 正常的步骤。 |
| 完成 | 最后一步，通常用于呈现按钮以完成向导。 |
| 完成 | 提供了通信成功或失败的消息。 |

> [!NOTE]
> 跟踪其状态使用 ASP.NET 控件状态的向导控件。 因此，EnableViewState 属性可以设置为 false，而无需任何从而不利。


此视频是向导控件的演练。


![](server-controls/_static/image2.png)


[打开的全屏视频](server-controls/_static/wizard1.wmv)


## <a name="localize-control"></a>本地化控件

Localize 控件是类似于文字控件。 但是，Localize 控件有**模式下**控件添加到它的标记的呈现方式的属性。 模式属性支持以下值：

| **模式** | **说明** |
| --- | --- |
| Transform | 根据浏览器发出请求的协议转换标记。 |
| 传递 | 标记呈现为的是。 |
| 编码 | 使用 HtmlEncode 编码添加到控件的标记。 |

## <a name="multiview-and-view-controls"></a>多视图和视图控件

多视图控件可用作视图控件的容器，并查看控件充当其他控件 （类似于在面板控件） 的容器。 多视图控件中的每个视图均由单个视图控件表示。 多视图中的第一个视图控件是视图，0，第二个是 1，视图等。可以通过指定的多视图控件 ActiveViewIndex 切换视图。

## <a name="substitution-control"></a>Substitution 控件

Substitution 控件结合使用 ASP.NET 缓存。 在其中你想要充分利用缓存，但具有必须在每个请求 （换句话说，页面列出了部分受缓存限制） 更新的页的部分的情况下，替换组件提供了很好的解决方案。 该控件实际上不会呈现在其自己的任何输出。 相反，它绑定到服务器端代码中的方法。 当请求页面时，调用该方法并返回的标记呈现替换控件的位置。

通过指定 Substitution 控件绑定到的方法**MethodName**属性。 该方法必须满足以下条件：

- 它必须是静态 (在中共享 VB) 方法。
- 它接受一个类型参数的 HttpContext。
- 它返回一个字符串，表示应将为页面上的控件的标记。

替换控件不具有修改的页上，任何其他控件的功能，但它确实有权访问的当前 HttpContext 中，通过其参数。

## <a name="gridview-control"></a>GridView 控件

GridView 控件是 DataGrid 控件的替代。 此控件将在更高版本的模块中的更详细地介绍。

## <a name="detailsview-control"></a>在 DetailsView 控件

在 DetailsView 控件可以显示来自数据源的单个记录，还可以编辑或删除它。 更高版本的模块中的更详细地介绍了它。

## <a name="formview-control"></a>FormView 控件

使用 FormView 控件在可配置界面中显示来自数据源的单个记录。 更高版本的模块中的更详细地介绍了它。

## <a name="accessdatasource-control"></a>AccessDataSource 控件

AccessDataSource 控件是用于将数据绑定的 Access 数据库。 更高版本的模块中的更详细地介绍了它。

## <a name="objectdatasource-control"></a>ObjectDataSource 控件

ObjectDataSource 控件用于支持三层体系结构，以便控件可以进行数据绑定到中间层业务对象而不是一个两层模型其中控件直接绑定到数据源。 它将在更高版本的模块中的更详细地讨论。

## <a name="xmldatasource-control"></a>XmlDataSource 控件

XmlDataSource 控件用于将数据绑定到 XML 数据源。 更高版本的模块中的更详细地介绍了它。

## <a name="sitemapdatasource-control"></a>SiteMapDataSource 控件

SiteMapDataSource 控件提供了基于站点图站点导航控件的数据绑定。 它将在更高版本的模块中的更详细地讨论。

## <a name="sitemappath-control"></a>SiteMapPath 控件

SiteMapPath 控件显示一的系列通常称为痕迹导航链接。 更高版本的模块中的更详细地介绍了它。

## <a name="menu-control"></a>Menu 控件

菜单控件将显示使用 DHTML 的动态菜单。 更高版本的模块中的更详细地介绍了它。

## <a name="treeview-control"></a>TreeView 控件

TreeView 控件用于显示数据的层次结构树视图。 更高版本的模块中的更详细地介绍了它。

## <a name="login-control"></a>Login 控件

Login 控件提供一种机制来登录到网站。 更高版本的模块中的更详细地介绍了它。

## <a name="loginview-control"></a>LoginView 控件

LoginView 控件可让不同的模板根据用户的登录状态的显示器。 更高版本的模块中的更详细地介绍了它。

## <a name="passwordrecovery-control"></a>PasswordRecovery 控件

PasswordRecovery 控件用于 ASP.NET 应用程序的用户检索忘记的密码。 更高版本的模块中的更详细地介绍了它。

## <a name="loginstatus"></a>LoginStatus

LoginStatus 控件显示用户的登录状态。 更高版本的模块中的更详细地介绍了它。

## <a name="loginname"></a>LoginName

登录到 ASP.NET 应用程序后，LoginName 控件显示用户的用户名。 更高版本的模块中的更详细地介绍了它。

## <a name="createuserwizard"></a>CreateUserWizard

CreateUserWizard 是一个可配置向导，使用户能够创建 ASP.NET 应用程序中使用的 ASP.NET 成员资格帐户。 更高版本的模块中的更详细地介绍了它。

## <a name="changepassword"></a>ChangePassword

ChangePassword 控件允许用户更改其密码为 ASP.NET 应用程序。 更高版本的模块中的更详细地介绍了它。

## <a name="various-webparts"></a>各种 web 部件

ASP.NET 2.0 随附了各种 Web 部件。 这些将在更高版本的模块中的详细介绍。
