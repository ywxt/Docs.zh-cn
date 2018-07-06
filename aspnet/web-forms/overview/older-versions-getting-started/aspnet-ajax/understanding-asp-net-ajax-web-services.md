---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
title: 了解 ASP.NET AJAX Web 服务 |Microsoft Docs
author: scottcate
description: Web 服务是.NET framework 为分布式系统之间交换数据提供的跨平台解决方案的重要组成部分。 尽管 Web...
ms.author: aspnetcontent
ms.date: 03/28/2008
ms.assetid: 3332d6e7-e2e1-4144-b805-e71d51e7e415
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
msc.type: authoredcontent
ms.openlocfilehash: b98ef4c27ab7b4b729e9e5b68e7d2642a6418ab6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37838596"
---
<a name="understanding-aspnet-ajax-web-services"></a>了解 ASP.NET AJAX Web 服务
====================
通过[Scott Cate](https://github.com/scottcate)

[下载 PDF](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial05_Web_Services_with_MS_Ajax_cs.pdf)

> Web 服务是.NET framework 为分布式系统之间交换数据提供的跨平台解决方案的重要组成部分。 尽管 Web 服务通常用于允许不同的操作系统、 对象模型和编程语言来发送和接收数据，但它们还可用来动态地将数据注入到 ASP.NET AJAX 页面或将数据从一个页面发送到后端系统。 所有这些都可以进行而不需求助于回发操作。


## <a name="calling-web-services-with-aspnet-ajax"></a>使用 ASP.NET AJAX 调用 Web 服务

Dan Wahlin

Web 服务是.NET framework 为分布式系统之间交换数据提供的跨平台解决方案的重要组成部分。 尽管 Web 服务通常用于允许不同的操作系统、 对象模型和编程语言来发送和接收数据，但它们还可用来动态地将数据注入到 ASP.NET AJAX 页面或将数据从一个页面发送到后端系统。 所有这些都可以进行而不需求助于回发操作。

虽然 ASP.NET AJAX UpdatePanel 控件提供了 AJAX 的简单方法启用任何 ASP.NET 页，则可能是您需要动态访问服务器上的数据而无需使用 UpdatePanel。 在这篇文章将看到如何通过创建和使用 ASP.NET AJAX 页面中的 Web 服务实现此目的。

本文将重点介绍核心 ASP.NET AJAX 扩展，以及名为 AutoCompleteExtender ASP.NET AJAX 工具包中的 Web 服务启用控件中提供的功能。 涵盖的主题包括定义启用了 AJAX 的 Web 服务、 创建客户端代理和调用 Web 服务使用 JavaScript。 您还将了解如何直接向 ASP.NET 页面方法进行 Web 服务调用。

## <a name="web-services-configuration"></a>Web 服务配置

使用 Visual Studio 2008 创建新网站项目后，web.config 文件具有新添加的内容可能不熟悉 Visual Studio 的早期版本的用户的数。 因此，它们可以在页时其他人定义所需的 HttpHandlers 和 HttpModules，这些修改的一些值映射到 ASP.NET AJAX 控件"asp"前缀。 列表 1 显示了所做的修改`<httpHandlers>`影响 Web 服务调用的 web.config 中的元素。 删除 HttpHandler 使用处理.asmx 调用的默认值并将其替换为 ScriptHandlerFactory 类位于 System.Web.Extensions.dll 程序集。 System.Web.Extensions.dll 包含所有由 ASP.NET AJAX 的核心功能。

**代码清单 1。ASP.NET AJAX Web 服务处理程序配置**

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample1.xml)]

使用 JavaScript Web 服务代理以允许 JavaScript 对象表示法 (JSON) 调用，以从 ASP.NET AJAX 页面对.NET Web 服务，进行此 HttpHandler 替换。 ASP.NET AJAX 将 JSON 消息发送到 Web 服务，而不是标准的简单对象访问协议 (SOAP) 调用通常与 Web 服务相关联。 这会导致较小的请求和响应消息的整体。 它还允许针对更高效的客户端处理的数据由于 ASP.NET AJAX JavaScript 库进行优化，以使用 JSON 对象。 列表 2 和清单 3 显示示例的 Web 服务请求和响应消息序列化为 JSON 格式。 代码清单 2 中所示的请求消息传递的值为"比利时"国家/地区参数，而清单 3 中的响应消息传递客户对象的数组和及其相关的属性。

**代码清单 2。Web 服务请求消息序列化为 JSON**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample2.json)]

> *> [!NOTE] 操作名称定义为 web 服务中; 的 URL 的一部分此外，通过 JSON 不始终提交请求消息。Web 服务可以利用 ScriptMethod 属性 UseHttpGet 参数设置为 true，这会导致通过传递参数的查询字符串参数。*


**代码清单 3。Web 服务响应消息序列化为 JSON**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample3.json)]

下一节中您将了解如何创建 Web 服务能够处理 JSON 请求消息，并且通过简单和复杂类型。

## <a name="creating-ajax-enabled-web-services"></a>创建启用了 AJAX 的 Web 服务

ASP.NET AJAX 框架提供了多种不同的方式来调用 Web 服务。 可以使用 AutoCompleteExtender 控件 （在 ASP.NET AJAX 工具包中可用） 或 JavaScript。 但是，在调用服务之前必须加入 AJAX 启用它，以便它可以由客户端脚本代码调用。

无论熟悉 ASP.NET Web 服务，您会发现它很容易创建，并启用 AJAX 的服务。 自 2002 年初次发布以来的 ASP.NET Web 服务创建具有支持.NET framework 和 ASP.NET AJAX Extensions 提供其他功能的.NET framework 的默认集为基础的 AJAX 功能。 Visual Studio.NET 2008 Beta 2 具有用于创建.asmx Web 服务文件的内置支持，并自动关联的代码旁置类派生自 System.Web.Services.WebService 类。 将方法添加到类必须应用以使其将调用 Web 服务使用者的 WebMethod 属性。

列表 4 显示了将 WebMethod 特性应用于名为 GetCustomersByCountry() 的方法的示例。

**列表 4。在 Web 服务中使用 WebMethod 属性**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample4.cs)]

GetCustomersByCountry() 方法接受一个国家/地区参数并返回客户对象数组。 传递给该方法的国家/地区值转发到的业务层类调用以从数据库检索数据的数据层类用数据填充客户对象属性，并返回的数组。

## <a name="using-the-scriptservice-attribute"></a>使用 ScriptService 属性

同时将添加 web 方法属性允许 GetCustomersByCountry() 方法调用的标准 SOAP 消息发送到 Web 服务的客户端，它不允许从现成的 ASP.NET AJAX 应用程序进行 JSON 调用。 若要允许你必须应用的 ASP.NET AJAX 扩展进行 JSON 调用`ScriptService`属性为 Web 服务类。 这使 Web 服务，以便将使用 JSON 格式化的响应消息发送，并允许客户端脚本来调用服务通过发送 JSON 消息。

列表 5 显示了将 ScriptService 属性应用于名为 CustomersService 的 Web 服务类的示例。

**列表 5。使用启用 AJAX 的 Web 服务将 ScriptService 属性**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample5.cs)]

ScriptService 属性充当一种标记，指示它可以调用 AJAX 脚本代码中。 它实际上不会处理任何发生在后台的 JSON 序列化或反序列化任务。 （在 web.config 中配置） ScriptHandlerFactory 及其他相关的类执行操作 JSON 处理大的容量。

## <a name="using-the-scriptmethod-attribute"></a>使用 ScriptMethod 属性

ScriptService 属性是必须在.NET Web 服务，以使其以由 ASP.NET AJAX 页面中定义的唯一 ASP.NET AJAX 属性。 但是，也可以直接向服务中的 Web 方法应用名为 ScriptMethod 的另一个属性。 ScriptMethod 定义三个属性，包括`UseHttpGet`，`ResponseFormat`和`XmlSerializeString`。 更改这些属性的值可能会在由 Web 方法已接受请求的类型需要更改为 GET、 Web 方法需要的形式返回原始 XML 数据时的情况下很有用`XmlDocument`或`XmlElement`对象或从返回数据时 始终应该作为 XML 而不是 JSON 序列化服务。

属性可用于 Web 方法应接受的 UseHttpGet GET 请求而不是发出的 POST 请求。 使用带 Web 方法的输入参数的 URL 转换为查询字符串参数发送请求。 UseHttpGet 属性默认值为 false，并仅应设置为`true`时已知的操作将 safe 和敏感数据时未传递给 Web 服务。 列表 6 显示了与 UseHttpGet 属性使用 ScriptMethod 属性的示例。

**代码清单 6。将用于 UseHttpGet 属性 ScriptMethod 属性。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample6.cs)]

列表 6 中所示的 HttpGetEcho Web 方法调用时发送的标头的示例将如下所示：

`GET /CustomerViewer/DemoService.asmx/HttpGetEcho?input=%22Input Value%22 HTTP/1.1`

当需要从服务，而不是 JSON 返回 XML 响应时，也可以还允许 Web 方法接受 HTTP GET 请求，使用 ScriptMethod 属性。 例如，Web 服务可能会从远程站点中检索 RSS 源，然后将其作为一个 XmlDocument 或 XmlElement 对象。 处理 XML 的数据然后会在客户端上。

列表 7 显示了使用 ResponseFormat 属性来指定应从 Web 方法返回的 XML 数据的示例。

**列表 7。将用于 ResponseFormat 属性 ScriptMethod 属性。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample7.cs)]

ResponseFormat 属性还可以与 XmlSerializeString 属性一起使用。 XmlSerializeString 属性具有默认值为 false，这意味着所有返回除从 Web 方法返回的字符串之外的类型序列化为 XML 时`ResponseFormat`属性设置为`ResponseFormat.Xml`。 当`XmlSerializeString`设置为`true`，从 Web 方法返回的所有类型都序列化为 XML 包括字符串类型。 如果 ResponseFormat 属性的值为`ResponseFormat.Json`XmlSerializeString 属性将被忽略。

代码清单 8 显示了使用 XmlSerializeString 属性以强制将其序列化为 XML 的字符串的示例。

**代码清单 8。ScriptMethod 属性将用于 XmlSerializeString 属性**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample8.cs)]

从调用代码清单 8 中所示的 GetXmlString Web 方法返回的值是如下所示：

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample9.cs)]

虽然默认 JSON 格式的请求和响应消息的总体大小降至最低，并且跨浏览器的方式更轻松地使用 ASP.NET AJAX 客户端，可以是 ResponseFormat 和 XmlSerializeString 属性时使用客户端例如，Internet Explorer 5 或更高版本的应用程序预期要从 Web 方法返回的 XML 数据。

## <a name="working-with-complex-types"></a>使用复杂类型

列表 5 说明了返回名为从 Web 服务的客户的复杂类型的示例。 Customer 类在内部定义为 FirstName 和 LastName 之类的属性的几种不同的简单类型。 在启用了 AJAX 的 Web 方法的返回类型将自动序列化到 JSON 发送到客户端之前或复杂类型作为输入参数使用。 但是，嵌套的复杂类型 （中定义的内部另一种类型） 都不会提供给客户端作为独立对象默认情况下。

在其中嵌套复杂类型由 Web 服务还必须使用在客户端页面中的情况下，ASP.NET AJAX generatescripttype; 属性可以添加到 Web 服务。 例如，列表 9 中所示的 CustomerDetails 类包含地址和性别属性的***表示嵌套的复杂类型。***

**列表 9。如下所示的 CustomerDetails 类包含两个嵌套的复杂类型。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample10.cs)]

列表 9 中所示 CustomerDetails 类中定义的地址和性别对象不会自动上提供可用于通过 JavaScript 客户端由于它们是嵌套的类型 （地址是一个类和性别是一个枚举）。 可以在其中使用 Web 服务中的嵌套的类型必须在客户端上可用的情况下，使用前面所述 generatescripttype; 属性 （请参阅列表 10）。 在其中从服务返回其他嵌套的复杂类型的情况下，此属性可以添加多个时间。 它可以应用到 Web 服务类直接或更高版本特定的 Web 方法。

**代码清单 10。使用 GenerateScriptService 属性定义嵌套的类型应可供客户端。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample11.cs)]

通过应用`GenerateScriptType`属性为 Web 服务、 地址和性别类型将自动成为可供使用的客户端的 ASP.NET AJAX JavaScript 代码。 自动生成并发送到客户端通过 Web 服务上添加 generatescripttype; 属性的 JavaScript 的示例列表 11 所示。 您将了解如何在本文后面部分使用嵌套的复杂类型。

**代码清单 11。提供给 ASP.NET AJAX 页面嵌套的复杂类型。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample12.cs)]

现在，已了解如何创建 Web 服务并使其可以访问 ASP.NET AJAX 页面，让我们看看如何创建和使用的 JavaScript 代理，以便可以检索数据，或将其发送到 Web 服务。

## <a name="creating-javascript-proxies"></a>创建的 JavaScript 代理

调用标准的 Web 服务 （.NET 或另一个平台） 通常涉及到创建代理对象，使您可以避免发送 SOAP 请求和响应消息的复杂性。 使用 ASP.NET AJAX Web 服务调用，可以创建和使用轻松调用服务，而无需担心序列化和反序列化 JSON 消息的 JavaScript 代理。 使用 ASP.NET AJAX ScriptManager 控件可以自动生成的 JavaScript 代理。

创建可调用 Web 服务的 JavaScript 代理被通过使用 ScriptManager 的服务属性。 此属性可以定义一个或多个服务的 ASP.NET AJAX 页面可以以异步方式调用发送或接收数据，而不需要回发的操作。 定义服务定义通过使用 ASP.NET AJAX`ServiceReference`控件并将 Web 服务 URL 分配给控件的`Path`属性。 列表 12 显示了引用一个名为 CustomersService.asmx 服务的示例。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample13.aspx)]

**列表 12。定义 ASP.NET AJAX 页面中使用的 Web 服务。**

添加对通过 ScriptManager 控件 CustomersService.asmx 的引用会导致要动态生成并且由页面引用的 JavaScript 代理。 通过使用嵌入代理&lt;脚本&gt;标记并通过调用 CustomersService.asmx 文件并向它的末尾追加 /js 动态加载。 下面的示例演示如何 JavaScript 代理嵌入在页中调试在 web.config 中处于禁用状态时：

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample14.html)]

> *> [!NOTE] 如果想要查看实际生成的 JavaScript 代理代码可以 Internet Explorer 的地址框中键入所需的.NET Web 服务的 URL，它的后面附加 /js。*


如果在 web.config 中作为页将嵌入的 JavaScript 代理的调试版本中启用调试，如下所示：

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample15.html)]

创建通过 ScriptManager 的 JavaScript 代理也可以嵌入到页面中直接而不是使用引用&lt;脚本&gt;标记的 src 属性。 这可以通过 ServiceReference 控件的 InlineScript 属性设置为 true （默认值为 false）。 当代理不会共享跨多个页面和你想要减少对服务器进行网络调用的数量时，这很有用。 不会由浏览器缓存当 InlineScript 设置为 true 的代理脚本，因此在其中多个页面的 ASP.NET AJAX 应用程序中使用的代理的情况下，默认值为 false。 使用 InlineScript 属性的示例是如下所示：

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample16.aspx)]

## <a name="using-javascript-proxies"></a>使用的 JavaScript 代理

后由 ASP.NET AJAX 页面使用 ScriptManager 控件引用 Web 服务，则可以针对 Web 服务进行调用，并可以使用回调函数来处理返回的数据。 Web 服务调用 （如果存在） 引用其命名空间、 类名和 Web 方法名称。 以及用于处理返回的数据的回调函数，可以定义传递给 Web 服务的任何参数。

使用 JavaScript 代理来调用一个名为 GetCustomersByCountry() 的 Web 方法的示例所示列表 13。 当最终用户单击页面上的按钮时调用 GetCustomersByCountry() 函数。

**代码清单 13。调用 Web 服务时使用的 JavaScript 代理。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample17.js)]

此调用引用 InterfaceTraining 命名空间，在服务中定义 CustomersService 类和 GetCustomersByCountry Web 方法。 它将传递从 textbox 获取的国家/地区值，以及一个名为 OnWSRequestComplete 异步 Web 服务调用返回时应调用的回调函数。 OnWSRequestComplete 处理从服务返回的客户对象数组，并将其转换到页面中显示的表。 从调用生成的输出是图 1 所示。


[![获取对 Web 服务的异步 AJAX 调用，从而将数据绑定。](understanding-asp-net-ajax-web-services/_static/image2.png)](understanding-asp-net-ajax-web-services/_static/image1.png)

**图 1**： 将数据绑定到 Web 服务的异步 AJAX 调用，从而获得。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-web-services/_static/image3.png))


JavaScript 代理还可以对 Web 服务的单向调用应调用 Web 方法，但代理不应等待的响应。 例如，你可能想要调用 Web 服务，以便启动如工作流的进程，但不是等待从服务返回值。 在单向调用需要对服务的情况下，只是可以省略列表 13 中所示的回调函数。 由于不定义任何回调函数的代理对象不会等待 Web 服务返回的数据。

## <a name="handling-errors"></a>处理错误

对 Web 服务的异步回调可能会遇到不同类型的错误，例如网络已关闭 Web 服务不可用或返回异常。 幸运的是，通过 ScriptManager 生成 JavaScript 代理对象允许多个回调被定义为处理错误和失败除了前面所示的 success 回调。 可以对 Web 方法的调用中的标准的回调函数后立即定义错误回调函数，如列表 14 中所示。

**代码清单 14。定义了错误的回调函数并显示错误。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample18.js)]

调用 Web 服务时出现的任何错误都将触发 OnWSRequestFailed() 回调函数调用，它接受一个表示错误作为参数的对象。 错误对象公开若干不同的功能以确定错误的原因以及在调用已超时。列表 14 显示了使用不同的错误函数的示例，图 2 显示的函数生成的输出的示例。


[![通过调用 ASP.NET AJAX 错误函数生成的输出。](understanding-asp-net-ajax-web-services/_static/image5.png)](understanding-asp-net-ajax-web-services/_static/image4.png)

**图 2**： 通过调用 ASP.NET AJAX 错误函数生成的输出。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-web-services/_static/image6.png))


## <a name="handling-xml-data-returned-from-a-web-service"></a>处理从 Web 服务返回的 XML 数据

前面有一个 Web 方法如何通过使用 ScriptMethod 属性以及其 ResponseFormat 属性无法返回原始 XML 数据。 当 ResponseFormat 设置为 ResponseFormat.Xml 时，从 Web 服务返回的数据序列化为 XML 而不是 JSON。 需要可直接传递到客户端使用 JavaScript 或 XSLT 处理 XML 数据时，这很有用。 在当前时间，Internet Explorer 5 或更高版本提供了最佳的客户端对象模型以进行分析和筛选 XML 数据，因为它对 MSXML 的内置支持。

从 Web 服务中检索 XML 数据是比检索其他数据类型没有什么不同。 首先调用 JavaScript 代理来调用相应的函数，并定义一个回调函数。 在调用返回后可以然后处理回调函数中的数据。

列表 15 显示了调用一个名为 GetRssFeed() 返回一个 XmlElement 对象的 Web 方法的示例。 GetRssFeed() 接受一个参数表示的 rss 源检索的 URL。

**代码清单 15。使用从 Web 服务返回的 XML 数据。**

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample19.html)]

此示例将 URL 传递到 RSS 源，并处理 OnWSRequestComplete() 函数中返回的 XML 数据。 OnWSRequestComplete() 首先检查以查看浏览器是否知道 MSXML 分析器是可用的 Internet Explorer。 如果是，使用 XPath 语句查找全部&lt;项&gt;RSS 源中的标记。 然后循环访问每个项和关联&lt;标题&gt;并&lt;链接&gt;标记是位于和处理以显示每个项的数据。 图 3 显示了进行 ASP.NET AJAX 通过 GetRssFeed() Web 方法的 JavaScript 代理调用生成的输出示例。

## <a name="handling-complex-types"></a>处理复杂类型

通过 JavaScript 代理自动公开接受或 Web 服务返回的复杂类型。 但是，除非 generatescripttype; 属性应用于服务，如前文所述嵌套的复杂类型不直接访问客户端上。 为什么要在客户端使用嵌套的复杂类型？

若要回答此问题，假设 ASP.NET AJAX 页面显示客户数据，并允许最终用户能够更新客户的地址。 如果 Web 服务指定的地址类型 （CustomerDetails 类中定义的复杂类型），可以发送到客户端的更新过程可以分为分隔功能，以便更好的代码重新使用。


[![从调用返回 RSS 数据的 Web 服务创建的输出。](understanding-asp-net-ajax-web-services/_static/image8.png)](understanding-asp-net-ajax-web-services/_static/image7.png)

**图 3**： 输出从调用返回 RSS 数据的 Web 服务创建。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-web-services/_static/image9.png))


列表 16 显示了调用模型命名空间中定义的地址对象的客户端代码的示例使用更新后的数据填充它，并将其分配给 CustomerDetails 对象的地址属性。 然后将 CustomerDetails 对象传递给 Web 服务进行处理。

**代码清单 16。使用嵌套的复杂类型**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample20.js)]

## <a name="creating-and-using-page-methods"></a>创建和使用页面方法

Web 服务提供公开到各种客户端包括 ASP.NET AJAX 页面的可重用服务的极佳途径。 但是，可能的需要检索数据，而不会使用或由其他页面共享页面。 在这种情况下，.asmx 文件来允许访问的数据页可能看起来有些多余由于服务仅由单个页面。

ASP.NET AJAX 提供了另一种机制以 Web 服务类似于调用而无需创建独立.asmx 文件。 这是通过使用一种技术称为"页面方法"。 页面方法是直接在页面或代码旁置文件中嵌入具有 WebMethod 特性应用于它们的静态 (共享在 VB.NET) 方法。 通过将 WebMethod 特性应用它们可以调用使用名为 PageMethods 获取在运行时动态创建的特殊 JavaScript 对象。 PageMethods 对象充当一个代理，使您可以从 JSON 序列化/反序列化进程。 请注意，若要使用的 PageMethods 对象必须将 ScriptManager 的 EnablePageMethods 属性设置为 true。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample21.aspx)]

列表 17 显示了在 ASP.NET 代码旁置类中定义两个页面方法的示例。 这些方法从应用中的业务层类中检索数据\_网站的代码文件夹。

**列表 17。定义页面方法。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample22.cs)]

ScriptManager 的页中检测存在 Web 方法时它会生成对上文所述的 PageMethods 对象的动态引用。 调用 Web 方法是通过引用该方法应传递任何必需的参数数据的名称后跟 PageMethods 类实现的。 列表 18 显示了调用前面所示的两个页面方法的示例。

**列表 18。调用页面方法与 PageMethods JavaScript 对象。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample23.js)]

使用 PageMethods 对象是非常类似于使用 JavaScript 代理对象。 第一次指定所有应传递给页面方法，然后定义异步调用返回时，应调用的回调函数的参数数据。 此外可以指定失败回调 （请参阅列表 14 有关处理故障的示例）。

## <a name="the-autocompleteextender-and-the-aspnet-ajax-toolkit"></a>AutoCompleteExtender 和 ASP.NET AJAX 工具包

ASP.NET AJAX 工具包 (可从[ http://ajax.asp.net ](http://ajax.asp.net)) 提供了可用于访问 Web 服务的多个控件。 具体而言，此工具包中包含一个名为的有用控件`AutoCompleteExtender`，可以用来调用 Web 服务和页面中显示数据，而无需编写任何 JavaScript 代码。

AutoCompleteExtender 控件可用来扩展现有功能的 textbox 和帮助用户更轻松地找到所需的数据。 键入到文本框控件可用于查询 Web 服务和动态显示文本框下的结果。 图 4 显示了使用 AutoCompleteExtender 控件以显示支持应用程序的客户 id 的示例。 以用户在文本框中键入不同的字符，它基于其输入下面会显示不同的项。 然后，用户可以选择所需的客户 id。

使用 ASP.NET AJAX 页面中的 AutoCompleteExtender 需要 AjaxControlToolkit.dll 程序集被添加到网站的 bin 文件夹。 后已添加工具包程序集，你将想要在 web.config 中进行引用，以便它包含的控件的可用应用程序中的所有页面。 这可以通过添加以下标记内 web.config 的&lt;控件&gt;标记：

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample24.xml)]

在其中只需使用中的特定页面的控件的情况下您可以引用它通过将该引用指令添加到页面顶部，而不是更新 web.config 如下所示：

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample25.aspx)]


[![使用 AutoCompleteExtender 控件。](understanding-asp-net-ajax-web-services/_static/image11.png)](understanding-asp-net-ajax-web-services/_static/image10.png)

**图 4**： 使用 AutoCompleteExtender 控件。  ([单击此项可查看原尺寸图像](understanding-asp-net-ajax-web-services/_static/image12.png))


一旦网站已配置为使用 ASP.NET AJAX 工具包，AutoCompleteExtender 控件可以添加到页更像添加常规的 ASP.NET 服务器控件。 列表 19 显示了使用该控件以调用 Web 服务的示例。

**列表 19。使用 ASP.NET AJAX 工具包 AutoCompleteExtender 控件。**

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample26.aspx)]

AutoCompleteExtender 具有多个不同的属性包括在服务器控件上找到的标准 ID 和 runat 属性。 除此之外，它允许你定义 Web 服务之前最终用户类型查询的数据的字符数。 列表 19 中所示的 MinimumPrefixLength 属性会导致在文本框中键入字符每次调用服务。 你需要请谨慎设置此值，因为每次用户键入的字符 Web 服务将调用以搜索与在文本框中的字符匹配的值。 要调用的 Web 服务，以及目标 Web 方法分别使用 ServicePath 和 ServiceMethod 属性进行定义。 最后，TargetControlID 属性标识要挂接到 AutoCompleteExtender 控件的文本框。

被调用的 Web 服务必须具有应用，如前面所述，ScriptService 属性和目标 Web 方法必须接受名为 prefixText 和计数的两个参数。 PrefixText 参数表示的最终用户键入的字符，计数参数表示要返回的邮件数 （默认值为 10）。 列表 20 显示了由前面的列表 19 所示 AutoCompleteExtender 控件调用 GetCustomerIDs Web 方法的示例。 Web 方法调用，反过来调用数据层处理筛选数据并返回匹配结果的方法的业务层方法。 数据层方法的代码列出 21 所示。

**列表 20。筛选从 AutoCompleteExtender 控件发送的数据。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample27.cs)]

**列表 21。筛选基于最终用户输入的结果。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample28.cs)]

## <a name="conclusion"></a>结束语

ASP.NET AJAX 调用 Web 服务，而无需编写大量的自定义 JavaScript 代码来处理请求和响应消息提供卓越的支持。 在这篇文章，已了解如何启用 AJAX 的.NET Web 服务，以使它们能够处理 JSON 消息以及如何定义使用 ScriptManager 控件的 JavaScript 代理。 您已了解如何使用代理来调用 Web 服务的 JavaScript 处理简单和复杂类型和处理失败。 最后，您已了解如何使用页面方法来简化创建和进行 Web 服务调用的过程和如何 AutoCompleteExtender 控件可以提供给最终用户的帮助，在键入时。 尽管可在 ASP.NET AJAX UpdatePanel 肯定将从其简单性的许多 AJAX 程序员的所选的控件，了解如何通过 JavaScript 代理调用 Web 服务可在许多应用程序。

## <a name="bio"></a>个人简介

Dan Wahlin （Microsoft 最有价值专业人员的 ASP.NET 和 XML Web 服务） 是接口的技术培训的.NET 开发讲师和体系结构顾问 ([http://www.interfacett.com](http://www.interfacett.com))。 Dan 成立了 XML for ASP.NET 开发人员网站 ([www.XMLforASP.NET](http://www.XMLforASP.NET))、 INETA 演讲者机构上和在多个会议上发表演讲。 Dan 合著了专业版 Windows DNA (Wrox)，ASP.NET： 提示、 教程和代码 (Sam)、 ASP.NET 1.1 Insider 解决方案、 Professional ASP.NET 2.0 AJAX (Wrox)、 ASP.NET 2.0 MVP Hacks 和面向 ASP.NET 开发人员 (Sam) 编写的 XML。 当他不编写代码、 文章或书籍时，Dan 喜欢编写和录制音乐和播放高尔夫和他的妻子和儿童篮球。

Scott Cate 自 1997 年以来一直致力于 Microsoft Web 技术和 myKB.com 总裁 ([www.myKB.com](http://www.myKB.com)) 专门负责编写 ASP.NET 基于侧重于知识库软件解决方案的应用程序。 可以通过电子邮件联系 Scott [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com)或他的博客[ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [上一页](understanding-asp-net-ajax-localization.md)
> [下一页](understanding-asp-net-ajax-debugging-capabilities.md)
