---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs
title: 处理未经处理的异常 (C#) |Microsoft Docs
author: rick-anderson
description: 出现运行时错误，则在生产环境中的 web 应用程序时，若要通知开发人员，以记录该错误，以便它可以在诊断，a la 一定...
ms.author: aspnetcontent
ms.date: 06/09/2009
ms.assetid: 5bc1afd5-2484-4528-b158-ab218ba150e8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs
msc.type: authoredcontent
ms.openlocfilehash: 07272a10ac9b1ddf3afd6b089b05a3f071834efe
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37832624"
---
<a name="processing-unhandled-exceptions-c"></a>处理未经处理的异常 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnet/web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs/samples)（[如何下载](/aspnet/core/tutorials/index#how-to-download-a-sample)）

> 出现运行时错误，则在生产环境中的 web 应用程序时，通知开发人员以及记录错误，以便它可以诊断在以后的时间很重要。 本教程概述 ASP.NET 如何处理运行时错误时，并探讨一种方法的自定义代码执行时由 ASP.NET 运行时未处理的异常气泡。


## <a name="introduction"></a>介绍

在 ASP.NET 应用程序中未经处理的异常时，冒泡到 ASP.NET 运行时，将引发`Error`事件，并显示相应的错误页。 有三种不同类型的错误页： 运行时错误黄色屏幕的死亡 (YSOD);异常详细信息 YSOD;和自定义错误页。 在中[前面的教程](displaying-a-custom-error-page-cs.md)我们配置了应用程序的远程用户和用户访问本地异常详细信息 YSOD 使用自定义错误页。

使用用户友好的自定义错误页相匹配的站点的外观和感觉是优先于默认运行时错误 YSOD，但显示自定义错误页只有一个全面的错误处理解决方案的一部分。 在生产环境中的应用程序中发生错误时, 非常重要，以便他们可以发现异常的原因和解决方法，开发人员将收到的错误。 此外，应记录错误的详细信息，以便可以检查错误和诊断在稍后的时间。

本教程演示如何访问未经处理的异常的详细信息，以便可以记录和开发人员收到通知。 以下此其中两个教程探索错误日志记录库，之后的配置中，将会自动通知开发人员的运行时错误，并记录其详细信息。

> [!NOTE]
> 在本教程中检查的信息是最有用，如果您需要某种唯一或自定义的方式处理未处理的异常。 在其中你只需记录异常并通知开发人员的情况下，使用错误日志记录库是转的方法。 接下来两个教程提供了两个这样的库的概述。


## <a name="executing-code-when-theerrorevent-is-raised"></a>执行代码时`Error`引发事件

事件提供一个对象发出信号，一些有趣的事情发生，以及另一个对象以执行代码以响应一种机制。 作为 ASP.NET 开发人员您习惯于考虑事件。 如果你想要访问者单击特定按钮时运行某些代码，为该按钮创建一个事件处理程序`Click`事件和放置您的代码。 考虑到 ASP.NET 运行时将引发其[`Error`事件](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)每当未处理的异常发生时，它遵循的原则用于记录错误的详细信息的代码将进入事件处理程序。 如何创建事件处理程序，但`Error`事件？

`Error`事件是中的多个事件之一[`HttpApplication`类](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)请求的生存期期间，会引发在 HTTP 管道中的某些阶段。 例如，`HttpApplication`类的[`BeginRequest`事件](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx); 的每个请求开始时引发其[`AuthenticateRequest`事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)安全模块已标识请求者时引发。 这些`HttpApplication`事件为页面开发人员提供了一种方法来执行请求的生存期内的不同位置的自定义逻辑。

事件处理程序`HttpApplication`事件可以放在名为的特殊文件`Global.asax`。 若要在你的网站中创建此文件，向您的网站名称中使用全局应用程序类模板的根添加新项`Global.asax`。

[![](processing-unhandled-exceptions-cs/_static/image2.png)](processing-unhandled-exceptions-cs/_static/image1.png)

**图 1**： 添加`Global.asax`对 Web 应用程序  
([单击此项可查看原尺寸图像](processing-unhandled-exceptions-cs/_static/image3.png))

内容和结构`Global.asax`略有根据使用的 Web 应用程序项目 (WAP) 或网站项目 (WSP) 由 Visual Studio 创建的文件会有所不同。 使用 WAP`Global.asax`实现作为两个单独的文件-`Global.asax`和`Global.asax.cs`。 `Global.asax`文件不包含任何内容，但`@Application`指令，它引用`.cs`文件; 所需的处理程序中定义的事件`Global.asax.cs`文件。 对于 Wsp，都会创建一个文件， `Global.asax`，并在中定义的事件处理程序`<script runat="server">`块。

`Global.asax` WAP 中创建由 Visual Studio 的应用程序的全局类模板文件包含名为事件处理程序`Application_BeginRequest`， `Application_AuthenticateRequest`，和`Application_Error`，这是事件处理程序`HttpApplication`事件`BeginRequest`， `AuthenticateRequest`，和`Error`分别。 此外，还有名为事件处理程序`Application_Start`， `Session_Start`， `Application_End`，和`Session_End`，这是事件处理程序触发的 web 应用程序启动时，当新的会话启动后，应用程序结束时，以及当会话结束时，分别。 `Global.asax`文件的 Visual Studio 中加入 WSP 创建只包含`Application_Error`， `Application_Start`， `Session_Start`， `Application_End`，并`Session_End`事件处理程序。

> [!NOTE]
> 部署 ASP.NET 应用程序时需要将复制`Global.asax`到生产环境的文件。 `Global.asax.cs`文件，在 WAP 中创建的是，不需要将复制到生产环境，因为此代码编译到项目的程序集。


Visual Studio 的应用程序的全局类模板创建的事件处理程序并不详尽。 可以将事件处理程序添加的任何`HttpApplication`通过命名事件处理程序的事件`Application_EventName`。 例如，可以添加以下代码`Global.asax`文件以创建的事件处理程序[`AuthorizeRequest`事件](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx):

[!code-cs[Main](processing-unhandled-exceptions-cs/samples/sample1.cs)]

同样，您可以删除应用程序的全局类模板创建的任何事件处理程序，则不需要。 本教程中我们只需要的事件处理程序`Error`事件; 请随时删除从其他事件处理程序`Global.asax`文件。

> [!NOTE]
> *HTTP 模块*提供了另一种方法来定义事件处理程序`HttpApplication`事件。 HTTP 模块创建为类文件中，可以直接在 web 应用程序项目中放置或者被分隔到单独的类库。 因为它们可以分离到一个类库，HTTP 模块提供用于创建更灵活且可重复使用模型`HttpApplication`事件处理程序。 而`Global.asax`文件是特定于它所在的 web 应用，HTTP 模块可以编译到程序集，此时将 HTTP 模块添加到网站非常简单，只将该程序集放入适当`Bin`文件夹和注册中的模块`Web.config`。 本教程不会查找在创建和使用的 HTTP 模块，但在以下两个教程中使用的两个错误日志记录库作为 HTTP 模块实现的。 有关更多背景 HTTP 模块的优势，请参阅[使用 HTTP 模块和处理程序创建可插入 ASP.NET 组件](https://msdn.microsoft.com/library/aa479332.aspx)。


## <a name="retrieving-information-about-the-unhandled-exception"></a>检索未处理的异常有关的信息

现在我们有的 Global.asax 文件`Application_Error`事件处理程序。 此事件处理程序执行时我们需要通知的错误的开发人员并记录其详细信息。 若要完成这些任务我们首先需要确定所引发的异常的详细信息。 使用服务器对象的[`GetLastError`方法](https://msdn.microsoft.com/library/system.web.httpserverutility.getlasterror.aspx)来检索导致的未处理异常的详细信息`Error`激发的事件。

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample2.cs)]

`GetLastError`方法返回类型的对象`Exception`，这是.NET Framework 中的所有异常的基类型。 但是，在上面的代码中我将强制转换返回的异常对象`GetLastError`到`HttpException`对象。 如果`Error`因为引发了异常处理 ASP.NET 资源期间引发的异常包装中，然后触发事件`HttpException`。 若要获取实际的异常引发错误事件使用`InnerException`属性。 如果`Error`由于基于 HTTP 的异常，例如不存在页的请求而引发事件`HttpException`引发，但它不具有内部异常。

下面的代码使用`GetLastErrormessage`来检索有关触发异常的信息`Error`事件，存储`HttpException`在名为`lastErrorWrapper`。 它然后将存储类型、 消息和原始异常堆栈跟踪在三个字符串变量中，检查是否`lastErrorWrapper`实际异常在触发`Error`事件 （对于基于 HTTP 的异常） 或是否只是处理请求时引发的异常的包装器。

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample3.cs)]

此时您具有所需编写代码，会将记录到数据库表的异常的详细信息的所有信息。 为每个感兴趣的类型、 消息、 堆栈跟踪等-以及其他有用的信息，如请求的页面的 URL 和当前登录用户的名称部分的错误详细信息，可以使用列创建一个数据库表。 在`Application_Error`然后连接到数据库，并向表插入记录的事件处理程序。 同样，可以添加代码以提醒开发人员通过电子邮件错误。

在接下来两个教程中检查错误日志记录库提供默认情况下，此类功能，因此无需自行生成此错误日志记录和通知。 但是，为了说明这一点`Error`引发事件，`Application_Error`事件处理程序可用于记录错误详细信息和通知开发人员，让我们添加当发生错误时通知开发人员的代码。

## <a name="notifying-a-developer-when-an-unhandled-exception-occurs"></a>未经处理的异常发生时通知开发人员

在生产环境中发生未经处理的异常时，一定向开发团队发出警报，以便它们可以评估该错误并确定需要采取的操作。 例如，如果没有连接到数据库，则需要为双精度值中的错误检查连接字符串和，这样一来，与您的 web 托管公司开具支持票证。 如果由于编程错误导致出现异常，可能需要额外的代码或验证逻辑添加以防止将来出现此类错误。

.NET Framework 中的类[`System.Net.Mail`命名空间](https://msdn.microsoft.com/library/system.net.mail.aspx)轻松地将发送一封电子邮件。 [ `MailMessage`类](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx)表示一封电子邮件并具有属性，如`To`， `From`， `Subject`， `Body`，和`Attachments`。 `SmtpClass`用于发送`MailMessage`对象使用指定的 SMTP 服务器; 可以以编程方式或以声明方式在指定的 SMTP 服务器设置[`<system.net>`元素](https://msdn.microsoft.com/library/6484zdc1.aspx)中`Web.config file`。 有关发送电子邮件的详细信息中的 ASP.NET 应用程序的消息查看我的文章[在 ASP.NET 中发送电子邮件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)，并[System.Net.Mail 常见问题解答](http://systemnetmail.com/)。

> [!NOTE]
> `<system.net>`元素包含使用的 SMTP 服务器设置`SmtpClient`类时发送一封电子邮件。 您的 web 托管公司可能具有可用于从您的应用程序发送电子邮件的 SMTP 服务器。 有关应在 web 应用程序中使用的 SMTP 服务器设置的信息，请参阅 web 主机的支持部分。


将以下代码添加到`Application_Error`事件处理程序发送的一名开发人员电子邮件时出现错误：

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample4.cs)]

虽然上面的代码是非常长，它的大容量创建显示的 HTML 发送到开发人员的电子邮件中。 该代码以引用`HttpException`返回的`GetLastError`方法 (`lastErrorWrapper`)。 通过检索实际请求由引发的异常`lastErrorWrapper.InnerException`并分配给变量`lastError`。 类型、 消息和堆栈跟踪信息检索从`lastError`，存储在三个字符串变量。

下一步，`MailMessage`名为对象`mm`创建。 电子邮件正文为 HTML 格式，并显示请求的页面的 URL、 当前登录的用户，以及有关异常 （类型、 消息和堆栈跟踪） 信息的名称。 有关很酷的事情之一`HttpException`类是可以生成用于创建异常的详细信息黄色屏幕的死亡 (YSOD) 通过调用的 HTML [GetHtmlErrorMessage 方法](https://msdn.microsoft.com/library/system.web.httpexception.gethtmlerrormessage.aspx)。 此处使用此方法检索异常详细信息 YSOD 标记并将其添加到的电子邮件的附件。 一句警告： 如果该异常的触发`Error`事件，基于 HTTP 的异常 （如不存在页的请求），然后`GetHtmlErrorMessage`方法将返回`null`。

最后一步是发送`MailMessage`。 这是通过创建一个新`SmtpClient`方法，并调用其`Send`方法。

> [!NOTE]
> 在 web 应用程序中使用此代码之前你将想要更改中的值`ToAddress`并`FromAddress`常量从support@example.com对任何电子邮件地址错误通知电子邮件应发送到和来自。 您还需要指定在 SMTP 服务器设置`<system.net>`主题中`Web.config`。 请咨询你的 web 主机提供商，以确定要使用的 SMTP 服务器设置。


利用此代码存在由错误的任何时间开发人员是发送汇总了错误并且包括 YSOD 的电子邮件。 前面的教程演示运行时错误通过访问 Genre.aspx 并传入无效`ID`通过在查询字符串，如值`Genre.aspx?ID=foo`。 访问与页面`Global.asax`文件后的生成相同的用户体验与在前面的教程-在开发环境中你将继续查看异常详细信息黄色屏幕死机，而在生产环境中，你就请参阅自定义错误页。 除了此现有行为，开发人员会发送一封电子邮件。

**图 2**显示了访问时收到的电子邮件`Genre.aspx?ID=foo`。 电子邮件正文总结了异常的信息，而`YSOD.htm`附件显示的异常详细信息 YSOD 中所示的内容 (请参阅**图 3**)。

[![](processing-unhandled-exceptions-cs/_static/image5.png)](processing-unhandled-exceptions-cs/_static/image4.png)

**图 2**： 开发人员在未经处理的异常时发送电子邮件通知  
([单击此项可查看原尺寸图像](processing-unhandled-exceptions-cs/_static/image6.png))

[![](processing-unhandled-exceptions-cs/_static/image8.png)](processing-unhandled-exceptions-cs/_static/image7.png)

**图 3**： 电子邮件通知中包括异常详细信息作为附件 YSOD  
([单击此项可查看原尺寸图像](processing-unhandled-exceptions-cs/_static/image9.png))

## <a name="what-about-using-the-custom-error-page"></a>使用自定义错误页怎么样呢？

本教程介绍了如何使用`Global.asax`和`Application_Error`事件处理程序以未经处理的异常发生时执行代码。 具体而言，我们使用此事件处理程序通知的错误，开发人员我们可以扩展它还在数据库中记录错误详细信息。 是否存在`Application_Error`事件处理程序不会影响最终用户体验。 它们仍看到配置的错误页，比如错误详细信息 YSOD、 运行时错误 YSOD 或自定义错误页。

很自然地想知道是否`Global.asax`文件和`Application_Error`事件时是必需的使用自定义错误页。 当出错时向用户显示自定义错误页因此为什么不能我们的代码以通知开发人员并登录到自定义错误页的代码隐藏类的错误详细信息？ 虽然当然可以将代码添加到自定义错误页的代码隐藏类没有访问触发异常的详细信息`Error`使用我们在前面的教程中探讨了该技术时的事件。 调用`GetLastError`从自定义错误页的方法将返回`Nothing`。

此行为的原因是因为通过重定向访问自定义错误页。 当未经处理的异常到达 ASP.NET 运行时 ASP.NET 引擎引发其`Error`事件 (它将执行`Application_Error`事件处理程序)，然后*将重定向*用户可以通过发出自定义错误页`Response.Redirect(customErrorPageUrl)`. `Response.Redirect`方法将发送到客户端使用 HTTP 302 状态代码，指示浏览器请求新的 URL，即自定义错误页的响应。 然后，在浏览器会自动请求这一新页面。 您所见，从页面中自定义错误页分别请求错误源于何处因为浏览器地址栏更改为自定义错误页面的 URL (请参阅**图 4**)。

[![](processing-unhandled-exceptions-cs/_static/image11.png)](processing-unhandled-exceptions-cs/_static/image10.png)

**图 4**： 发生错误时在浏览器获取重定向到自定义错误页 URL  
([单击此项可查看原尺寸图像](processing-unhandled-exceptions-cs/_static/image12.png))

实际效果是未经处理的异常发生位置请求结束时服务器的响应使用 HTTP 302 重定向。 对自定义错误页的后续请求是全新的请求;此时 ASP.NET 引擎已丢弃的错误信息和，此外，有没有办法将上一个请求中未经处理的异常与自定义错误页的新请求相关联。 这就是为什么`GetLastError`返回`null`时从自定义错误页调用。

但是，很可能有导致该错误在同一个请求期间执行的自定义错误页。 [ `Server.Transfer(url)` ](https://msdn.microsoft.com/library/system.web.httpserverutility.transfer.aspx)方法将执行转移到指定的 URL，并在同一请求中对其进行处理。 您可以将代码移动`Application_Error`事件处理程序替换中的自定义错误页的代码隐藏类`Global.asax`使用以下代码：

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample5.cs)]

未经处理的异常发生时现在`Application_Error`事件处理程序将控制转移到基于 HTTP 状态代码的相应的自定义错误页。 自定义错误页传输控件，因为有权访问的未处理的异常信息通过`Server.GetLastError`和可以通知开发人员的错误并记录其详细信息。 `Server.Transfer`调用停止 ASP.NET 引擎从将用户重定向到自定义错误页。 相反，作为对生成错误的页的响应返回自定义错误页的内容。

## <a name="summary"></a>总结

ASP.NET 运行时将 ASP.NET web 应用程序中发生未经处理的异常时引发`Error`事件，并显示配置的错误页。 我们可以通知开发人员的错误，记录其详细信息，或以某种其他方式处理它通过创建错误事件的事件处理程序。 有两种方法创建的事件处理程序`HttpApplication`事件，如`Error`： 在`Global.asax`文件或从 HTTP 模块。 本教程介绍了如何创建`Error`中的事件处理程序`Global.asax`通过电子邮件通知的错误的开发人员的文件。

创建`Error`事件处理程序需要某种唯一或自定义的方式处理未处理的异常的情况下很有用。 但是，创建你自己`Error`事件处理程序来记录异常或通知开发人员不是最有效地利用您的时间，因为存在已存在免费且易于使用的错误日志记录库，可以在几分钟内设置。 接下来两个教程检查两个这样的库。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET HTTP 模块和 HTTP 处理程序概述](https://support.microsoft.com/kb/307985)
- [适当地响应未经处理的异常的处理未经处理的异常](http://aspnet.4guysfromrolla.com/articles/091306-1.aspx)
- [`HttpApplication` 类和 ASP.NET 应用程序对象](http://www.eggheadcafe.com/articles/20030211.asp)
- [HTTP 处理程序和 ASP.NET 中的 HTTP 模块](http://www.15seconds.com/Issue/020417.htm)
- [在 ASP.NET 中发送电子邮件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [了解`Global.asax`文件](http://aspalliance.com/1114_Understanding_the_Globalasax_file.all)
- [使用 HTTP 模块和处理程序来创建可插入的 ASP.NET 组件](https://msdn.microsoft.com/library/aa479332.aspx)
- [使用 ASP.NET`Global.asax`文件](http://articles.techrepublic.com.com/5100-10878_11-5771721.html)
- [使用`HttpApplication`实例](https://msdn.microsoft.com/library/a0xez8f2.aspx)

> [!div class="step-by-step"]
> [上一页](displaying-a-custom-error-page-cs.md)
> [下一页](logging-error-details-with-asp-net-health-monitoring-cs.md)
