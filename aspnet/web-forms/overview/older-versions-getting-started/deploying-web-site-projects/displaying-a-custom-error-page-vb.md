---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-vb
title: 显示自定义错误页 (VB) |Microsoft Docs
author: rick-anderson
description: Does 用户看到的内容时将 ASP.NET web 应用程序中发生运行时错误？ 答案取决于如何将网站的&lt;customErrors&gt;配置...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: 14873c5d-81a9-455b-bd71-30fb555583e7
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 732aad689b5d427ceb50b0062e7c00de0b7fb401
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362611"
---
<a name="displaying-a-custom-error-page-vb"></a>显示自定义错误页 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_11_VB.zip)或[下载 PDF](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial11_CustomErrors_vb.pdf)

> Does 用户看到的内容时将 ASP.NET web 应用程序中发生运行时错误？ 答案取决于如何将网站的&lt;customErrors&gt;配置。 默认情况下，将显示用户的不雅观的黄色屏幕宣布出现运行时错误。 本教程演示如何自定义这些设置应用于匹配你网站的外观和感觉的审美情趣的显示自定义错误页。


## <a name="introduction"></a>介绍

在理想情况下都将没有运行时错误。 程序员会编写使用 n 元代码 bug 并使用强大的用户输入验证和外部资源，如数据库服务器和电子邮件服务器将永远不会进入脱机状态。 当然，在现实中错误是不可避免的。 .NET Framework 中的类发出错误信号通过引发异常。 例如，调用 SqlConnection 对象的打开方法建立与连接字符串由指定的数据库的连接。 但是，如果数据库已关闭或者如果连接字符串中的凭据无效然后 Open 方法将引发`SqlException`。 可以通过使用处理异常`Try/Catch/Finally`块。 如果中的代码`Try`块引发了异常，将控件传输到适当的 catch 块，开发人员可以尝试从错误中恢复。 如果没有匹配的 catch 块，或如果在 try 块不是引发异常的代码，该异常 percolates search 的调用堆栈中向上`Try/Catch/Finally`块。

如果异常冒泡到 ASP.NET 运行时不被处理的情况下[`HttpApplication`类](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)的[`Error`事件](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)引发和配置*错误页*显示。 默认情况下，ASP.NET 将显示一个错误页面，人们亲切地称为[死亡的黄色屏幕](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)(YSOD)。 有两个版本的 YSOD： 一个显示异常详细信息、 堆栈跟踪，以及其他信息有助于为开发人员调试应用程序 (请参阅**图 1**); 另只是声明出现运行时错误 （请参阅**图 2**)。

异常详细信息 YSOD 是非常有用的开发人员调试应用程序，但向最终用户显示 YSOD 是认为牵扯和不专业。 相反，最终用户应转到一个错误页面，与更加用户友好说明这种情况的 prose 维护站点的外观和感觉。 好消息是，创建自定义错误页是非常简单。 本教程首先介绍在 ASP。NET 的不同错误页。 它然后演示如何配置 web 应用程序，以向用户显示在遇到错误时的自定义错误页。

### <a name="examining-the-three-types-of-error-pages"></a>检查三种类型的错误页

当未经处理的异常发生在 ASP.NET 应用程序的错误页的三种类型之一时，会显示：

- 异常详细信息黄色屏幕死机错误页上，
- 运行时错误黄色屏幕死机错误页上，或
- 自定义错误页

错误页开发人员最熟悉与异常详细信息 YSOD。 默认情况下，此页会向本地访问的用户，因此在开发环境中测试该站点时，将发生错误时，将显示的页。 正如其名，异常详细信息 YSOD 提供了详细描述异常的类型、 消息和堆栈跟踪。 更重要的是，如果您的 ASP.NET 页面的代码隐藏类中的代码引发异常和应用程序配置为调试异常详细信息 YSOD 还会显示这行代码 （和上面的代码和它下面的几行）。

**图 1**显示异常详细信息 YSOD 页。 请注意浏览器地址窗口中的 URL: `http://localhost:62275/Genre.aspx?ID=foo`。 请记住，`Genre.aspx`页列出了特定流派书评。 该配置要求`GenreId`值 ( `uniqueidentifier`) 通过在查询字符串; 例如，若要查看小说评审，相应的 URL 是`Genre.aspx?ID=7683ab5d-4589-4f03-a139-1c26044d0146`。 如果将非`uniqueidentifier`传递值中通过在查询字符串 （例如"foo") 将引发异常。

> [!NOTE]
> 若要重现的演示 web 应用程序中出现此错误可供下载您可以访问`Genre.aspx?ID=foo`直接单击中的"生成运行时错误"链接或`Default.aspx`。


请注意中提供的异常信息**图 1**。 异常消息，"转换失败时将字符串转换为 uniqueidentifier"会出现在页面顶部。 异常的类型`System.Data.SqlClient.SqlException`，已列出，以及。 此外，还有的堆栈跟踪。

[![](displaying-a-custom-error-page-vb/_static/image2.png)](displaying-a-custom-error-page-vb/_static/image1.png)

**图 1**： 异常详细信息 YSOD 包括有关异常的信息  
 ([单击此项可查看原尺寸图像](displaying-a-custom-error-page-vb/_static/image3.png))

其他类型的 YSOD 是运行时错误 YSOD，和中所示**图 2**。 运行时错误 YSOD 通知访问者发生运行时错误，但它不包括有关所引发的异常的任何信息。 (但是，存在，将说明了如何通过修改，使错误详细信息可查看`Web.config`文件，即的作用是将查找不专业的此类 YSOD。)

默认情况下，运行时错误 YSOD 显示到远程访问的用户 (通过 http://www.yoursite.com) ，如按 URL 在浏览器的地址栏中出现**图 2**: `http://httpruntime.web703.discountasp.net/Genre.aspx?ID=foo`。 存在两个不同 YSOD 屏幕，因为开发人员都希望了解错误详细信息，但此类信息应在实时站点上中显示，因为它可能会泄露潜在的安全漏洞和其他敏感信息的所有访问者都在站点。

> [!NOTE]
> 如果遵循此过程，并使用 DiscountASP.NET 作为 web 主机，您可能会注意到运行时错误 YSOD 不会显示访问实时网站时。 这是因为 DiscountASP.NET 已配置为显示异常详细信息 YSOD 默认情况下其服务器。 值得高兴的是，可以通过添加覆盖此默认行为`<customErrors>`部分为你`Web.config`文件。 "配置错误页显示"部分将检查`<customErrors>`中详细信息部分。


[![](displaying-a-custom-error-page-vb/_static/image5.png)](displaying-a-custom-error-page-vb/_static/image4.png)

**图 2**： 运行时错误 YSOD 不包括任何错误的详细信息  
 ([单击此项可查看原尺寸图像](displaying-a-custom-error-page-vb/_static/image6.png))

错误页的第三种类型是自定义错误页上，这是你创建的网页。 自定义错误页的好处是您可以完全控制显示给页面的外观和感觉; 以及用户的信息自定义错误页可以为其他页面使用的相同的母版页和样式。 "使用自定义错误页"部分将指导完成创建自定义错误页并将其配置为发生未经处理的异常时显示。 **图 3**提供历时此自定义错误页。 正如您所看到的错误页的外观会是更多专业外观的以外的黄色屏幕死机图 1 和 2 中所示。

[![](displaying-a-custom-error-page-vb/_static/image8.png)](displaying-a-custom-error-page-vb/_static/image7.png)

**图 3**： 自定义错误页提供了更加个性化的外观和感觉  
 ([单击此项可查看原尺寸图像](displaying-a-custom-error-page-vb/_static/image9.png))

请花费片刻时间来检查中的浏览器地址栏**图 3**。 请注意，在地址栏显示自定义错误页的 URL (`/ErrorPages/Oops.aspx`)。 图 1 和 2 中导致错误的同一页面中显示黄色死亡屏幕 (`Genre.aspx`)。 自定义错误页传递通过发生错误的页面的 URL`aspxerrorpath`查询字符串参数。

## <a name="configuring-which-error-page-is-displayed"></a>显示配置的错误页

这三个可能的错误页面，系统会基于两个变量：

- 中的配置信息`<customErrors>`部分中，并
- 无论用户本地或远程访问网站。

[ `<customErrors>`部分](https://msdn.microsoft.com/library/h0hfz6fc.aspx)中`Web.config`有影响哪些错误页所示的两个属性：`defaultRedirect`和`mode`。 `defaultRedirect` 属性是可选项。 如果提供，它指定自定义错误页的 URL，并指示应而不是运行时错误 YSOD 显示自定义错误页。 `mode`属性是必需的接受三个值之一： `On`， `Off`，或`RemoteOnly`。 这些值具有以下行为：

- `On` -指示自定义错误页或运行时错误 YSOD 显示所有访问者，而不管它们是本地或远程。
- `Off` -指定异常的详细信息 YSOD 会向所有访问者，而不管它们是本地或远程。
- `RemoteOnly` -指示自定义错误页或运行时错误 YSOD 显示给远程访问者，而异常详细信息 YSOD 显示对本地的访客。

除非另外指定，否则 ASP.NET 看起来就像有将 mode 属性设置为`RemoteOnly`且具有未指定`defaultRedirect`值。 换而言之，默认行为是而运行时错误 YSOD 显示对远程访客，异常详细信息 YSOD 显示本地访问者。 可以通过添加替代此默认行为`<customErrors>`到 web 应用程序的部分 `Web.config file.`

## <a name="using-a-custom-error-page"></a>使用自定义错误页

每个 web 应用程序应具有自定义错误页。 它提供了运行时错误 YSOD 的更专业的替代方法，是轻松创建、 配置应用程序以使用自定义错误页需要仅几分钟。 第一步创建自定义错误页。 我已添加到名为书评应用程序的新文件夹`ErrorPages`并添加到新的 ASP.NET 页面名为`Oops.aspx`。 已为你的站点上的页面的其余部分使用相同的母版页，以便它将自动继承相同的外观和感觉的页。

[![](displaying-a-custom-error-page-vb/_static/image11.png)](displaying-a-custom-error-page-vb/_static/image10.png)

**图 4**： 创建自定义错误页

接下来，花几分钟时间创建错误页的内容。 我创建了一个非常简单的自定义错误页，一条消息表明，遇到意外的错误，链接回站点的主页。

[![](displaying-a-custom-error-page-vb/_static/image13.png)](displaying-a-custom-error-page-vb/_static/image12.png)

**图 5**： 设计自定义错误页  
 ([单击此项可查看原尺寸图像](displaying-a-custom-error-page-vb/_static/image14.png))

与已完成的错误页，配置 web 应用程序使用运行时错误 YSOD 代替自定义错误页。 这可以通过指定的错误页的 URL`<customErrors>`节的`defaultRedirect`属性。 将以下标记添加到应用程序的`Web.config`文件：

[!code-xml[Main](displaying-a-custom-error-page-vb/samples/sample1.xml)]

上述标记将配置应用程序要向用户访问本地，同时为远程访问这些用户使用自定义错误页 Oops.aspx 显示异常详细信息 YSOD。 若要了解此操作，请将你的网站部署到生产环境，然后访问 Genre.aspx 页面上具有无效的查询字符串值的实时站点。 你应看到自定义错误页 (回头**图 3**)。

若要验证自定义错误页仅显示给远程用户，请访问`Genre.aspx`页具有无效的查询字符串从开发环境。 应仍请参阅异常详细信息 YSOD (回头**图 1**)。 `RemoteOnly`设置可确保在生产环境中访问网站的用户看到自定义错误页，而本地工作的开发人员可以继续查看异常的详细信息。

## <a name="notifying-developers-and-logging-error-details"></a>通知开发人员和日志记录错误详细信息

在开发环境中发生的错误的原因由开发人员坐在她的计算机。 她所示的异常详细信息 YSOD，异常的信息，并且她知道她在发生错误时正在执行哪些步骤。 但开发人员时生产上发生错误，并不知道最终用户访问网站需要时间来报告错误，除非发生了错误。 并且，即使用户超出其办法通知发生了错误，而不必知道异常类型、 消息和堆栈跟踪，它可能很难诊断错误的原因，更不用说修复此错误的开发团队。

出于这些原因是极其重要的生产环境中的任何错误将记录到某些永久存储中的 （如数据库），开发人员提醒你此错误。 自定义错误页可能看起来操作日志记录以及通知的好时机。 遗憾的是，自定义错误页面不能访问到错误详细信息，因此不能用于记录此信息。 好消息是，通过多种方式来截获错误详细信息和日志，，接下来三个教程探索此主题中更多详细信息。

## <a name="using-different-custom-error-pages-for-different-http-error-statuses"></a>将不同的自定义错误页用于不同的 HTTP 错误状态

当异常引发由 ASP.NET 页面，未处理异常 percolates ASP.NET 运行时，其中显示了配置的错误页。 如果请求进入 ASP.NET 引擎，但由于某种原因而无法处理-可能是请求的文件未找到或读取文件-已禁用的权限，则 ASP.NET 引擎将引发`HttpException`。 此异常，如从 ASP.NET 页中，引发的异常冒泡到运行时，导致相应的错误页后，可以显示。

这在生产环境中的 web 应用程序的含义是如果用户请求未找到，则他们将看到自定义错误页的页。 **图 6**显示了此类示例。 因为该请求是针对不存在页 (`NoSuchPage.aspx`)、 一个`HttpException`引发，并显示自定义错误页面 (请注意对引用`NoSuchPage.aspx`中`aspxerrorpath`查询字符串参数)。

[![](displaying-a-custom-error-page-vb/_static/image16.png)](displaying-a-custom-error-page-vb/_static/image15.png)**图 6**: ASP.NET 运行时在无效的请求响应中显示配置的错误页  
 ([单击此项可查看原尺寸图像](displaying-a-custom-error-page-vb/_static/image17.png)) 

默认情况下，所有类型的错误会都导致相同的自定义错误页，显示。 但是，可以指定特定的 HTTP 状态代码使用的不同自定义错误页`<error>`内的子元素`<customErrors>`部分。 例如，在不同的错误页面中找不到错误，具有 HTTP 状态代码 404，页面的情况下显示更新`<customErrors>`部分以包括以下标记：

[!code-xml[Main](displaying-a-custom-error-page-vb/samples/sample2.xml)]

使用此更改后，每当用户远程访问请求 ASP.NET 资源不存在，它们将重定向到`404.aspx`而不是自定义错误页`Oops.aspx`。 作为**图 7**所示，`404.aspx`页面可以包含比常规自定义错误页更特定的消息。

> [!NOTE]
> 请查看[404 错误页面，一个需要更多时间](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)有关创建有效的 404 错误页的指南。


[![](displaying-a-custom-error-page-vb/_static/image19.png)](displaying-a-custom-error-page-vb/_static/image18.png)**图 7**： 自定义 404 错误页显示比更有针对性的消息 `Oops.aspx`  
 ([单击此项可查看原尺寸图像](displaying-a-custom-error-page-vb/_static/image20.png)) 

因为您知道`404.aspx`用户发出用于找不到的页面请求时，才会达到页，可以增强此自定义错误页以包含功能，以帮助用户解决此特定类型的错误。 例如，您无法生成映射已知的良好 Url 不正确的 Url 的数据库表，然后具有`404.aspx`运行查询的表并建议用户可能尝试访问的页面的自定义错误页。

> [!NOTE]
> 当请求由 ASP.NET 引擎处理的资源，仅显示自定义错误页。 如中所述[核心 IIS 之间的差异和 ASP.NET Development Server](core-differences-between-iis-and-the-asp-net-development-server-vb.md)教程中，web 服务器可能会处理某些请求本身。 默认情况下，IIS web 服务器进程请求的静态内容，如图像和 HTML 文件，而无需调用 ASP.NET 引擎。 因此，在用户请求不存在图像文件时用户将会得到 IIS 的默认 404 错误消息而不是 ASP。NET 的配置错误页。


## <a name="summary"></a>总结

在 ASP.NET 应用程序中未经处理的异常时，向用户显示一个三个错误页： 异常详细信息黄色屏幕死机;运行时错误黄色屏幕死机紫;或自定义错误页。 显示的错误页面取决于应用程序的`<customErrors>`配置和用户是否访问本地或远程。 默认行为是向远程访问者显示异常详细信息 YSOD 对本地的访客和运行时错误 YSOD。

尽管运行时错误 YSOD 隐藏可能敏感的错误信息，从用户访问网站，它将从站点的外观和感觉会中断并使应用程序看起来有问题。 更好的方法是使用自定义错误页，其中涉及到创建和设计自定义错误页，并指定在其 URL`<customErrors>`节的`defaultRedirect`属性。 甚至可以让不同的 HTTP 错误状态的多个自定义错误页。

自定义错误页是一个全面的错误处理策略用于在生产环境中网站的第一步。 警报的开发人员和日志记录其详细信息也是错误的重要的步骤。 接下来三个教程探索错误通知和日志记录的技术。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [错误页，一次](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)
- [异常的设计准则](https://msdn.microsoft.com/library/ms229014.aspx)
- [用户友好错误页](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [处理和引发异常](https://msdn.microsoft.com/library/5b2yeyab.aspx)
- [在 ASP.NET 中正确使用自定义错误页](http://professionalaspnet.com/archive/2007/09/30/Properly-Using-Custom-Error-Pages-in-ASP.NET.aspx)

> [!div class="step-by-step"]
> [上一页](strategies-for-database-development-and-deployment-vb.md)
> [下一页](processing-unhandled-exceptions-vb.md)
