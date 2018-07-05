---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: ASP.NET Web API 中发送 HTML 窗体数据： 文件上传和多部分 MIME |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/21/2012
ms.topic: article
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c1c85f462141daf747e23aa4215d47f2d263140
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386703"
---
<a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a>ASP.NET Web API 中发送 HTML 窗体数据： 文件上传和多部分 MIME
====================
通过[Mike Wasson](https://github.com/MikeWasson)

## <a name="part-2-file-upload-and-multipart-mime"></a>第 2 部分： 文件上传和多部分 MIME

本教程演示如何将文件上传到 web API。 它还介绍了如何处理多部分 MIME 数据。

> [!NOTE]
> [下载已完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)。


下面是 HTML 窗体用于上载文件的示例：

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

此窗体包含一个文本输入的控件和文件输入的控件。 表单包含文件输入的控件**enctype**属性应始终为&quot;multipart/表单数据&quot;，它指定将作为多部分 MIME 消息发送的窗体。

多部分 MIME 消息的格式是最简单的方法了解通过查看示例请求：

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

此消息划分为两个*部件*，一个用于每个窗体控件。 部分边界以短划线开头的行来表示。

> [!NOTE]
> 部分边界包括一个随机的组件 (&quot;41184676334&quot;) 以确保边界字符串不会意外地出现在消息部分。


每个消息部分包含一个或多个标头，跟部件内容。

- 内容处置标头包括控件的名称。 对于文件，它还包含的文件的名称。
- 内容类型标头描述的部分中的数据。 如果省略此标头，则默认值为 text/plain。

在上一示例中，用户上传了名为 GrandCanyon.jpg，内容类型 image/jpeg; 的文件文本输入的值是&quot;暑假之旅&quot;。

## <a name="file-upload"></a>文件上传

现在让我们看看从多部分 MIME 消息读取文件的 Web API 控制器。 控制器将以异步方式读取文件。 Web API 支持异步操作，使用[基于任务的编程模型](https://msdn.microsoft.com/library/dd460693.aspx)。 如果你面向的.NET Framework 4.5 中，它支持第一次，以下是代码**异步**并**await**关键字。

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

请注意，控制器操作不采用任何参数。 这是因为我们处理在操作内的请求正文而不调用媒体类型格式化程序。

**IsMultipartContent**方法检查请求是否包含多部分 MIME 消息。 如果没有，控制器将返回 HTTP 状态代码 415 （不受支持的媒体类型）。

**MultipartFormDataStreamProvider**类是个上传的文件分配文件流的帮助程序对象。 若要读取多部分 MIME 消息，请调用**ReadAsMultipartAsync**方法。 此方法提取所有消息部分，并将其写入到由所提供的流**MultipartFormDataStreamProvider**。

方法完成时，可以获取有关从文件的信息**数据**属性，它是集合的**MultipartFileData**对象。

- **MultipartFileData.FileName**是在服务器上，该文件的保存位置的本地文件名。
- **MultipartFileData.Headers**包含部分标头 (*不*请求标头)。 可以使用此访问内容\_处置和内容类型标头。

顾名思义， **ReadAsMultipartAsync**是一个异步方法。 若要执行的工作，在方法完成后，使用[延续任务](https://msdn.microsoft.com/library/ee372288.aspx)(.NET 4.0) 或**await**关键字 (.NET 4.5)。

下面是代码的前面的.NET Framework 4.0 版本：

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a>读取窗体控件数据

我在上文的 HTML 窗体有文本输入的控件。

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

你可以获取从控件的值**FormData**的属性**MultipartFormDataStreamProvider**。

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

**FormData**是**NameValueCollection** ，其中包含名称/值对的窗体控件。 集合可以包含重复的键。 请考虑这种形式：

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

请求正文可能如下所示：

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

在这种情况下， **FormData**集合将包含以下键/值对：

- 行程： 保存/还原
- 选项： nonstop
- 选项： 日期
- 席位： 窗口
