---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: "在 ASP.NET Web API 发送 HTML 窗体数据： 文件上载和多部分 MIME |Microsoft 文档"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/21/2012
ms.topic: article
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: 331d0e520a1fd8ec84aecd09a9c9e6d286c5893b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="06b2f-102">在 ASP.NET Web API 发送 HTML 窗体数据： 文件上载和多部分 MIME</span><span class="sxs-lookup"><span data-stu-id="06b2f-102">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>
====================
<span data-ttu-id="06b2f-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="06b2f-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="06b2f-104">第 2 部分： 文件上载和多部分 MIME</span><span class="sxs-lookup"><span data-stu-id="06b2f-104">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="06b2f-105">本教程演示如何将文件上载到 web API。</span><span class="sxs-lookup"><span data-stu-id="06b2f-105">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="06b2f-106">它还描述如何处理多部分 MIME 数据。</span><span class="sxs-lookup"><span data-stu-id="06b2f-106">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="06b2f-107">[下载完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)。</span><span class="sxs-lookup"><span data-stu-id="06b2f-107">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>


<span data-ttu-id="06b2f-108">下面是用于上载文件以 HTML 形式的示例：</span><span class="sxs-lookup"><span data-stu-id="06b2f-108">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="06b2f-109">此表单包含文本输入的控件和文件输入的控件。</span><span class="sxs-lookup"><span data-stu-id="06b2f-109">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="06b2f-110">当窗体包含文件的输入的控件， **enctype**属性应始终为&quot;multipart/窗体数据&quot;，它指定将作为多部分 MIME 消息发送的窗体。</span><span class="sxs-lookup"><span data-stu-id="06b2f-110">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="06b2f-111">多部分 MIME 消息的格式是最简单的方法了解通过查看请求的示例：</span><span class="sxs-lookup"><span data-stu-id="06b2f-111">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="06b2f-112">此消息划分为两个*部件*，一个用于每个窗体控件。</span><span class="sxs-lookup"><span data-stu-id="06b2f-112">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="06b2f-113">通过以短划线开头的行来指示零件边界。</span><span class="sxs-lookup"><span data-stu-id="06b2f-113">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="06b2f-114">一部分边界包括随机组件 (&quot;41184676334&quot;) 以确保的边界字符串是否意外没有内的消息部分。</span><span class="sxs-lookup"><span data-stu-id="06b2f-114">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>


<span data-ttu-id="06b2f-115">每个消息部分包含一个或多个标头，跟部件内容。</span><span class="sxs-lookup"><span data-stu-id="06b2f-115">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="06b2f-116">Content-disposition 标头包括控件的名称。</span><span class="sxs-lookup"><span data-stu-id="06b2f-116">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="06b2f-117">对于文件，它还包含文件名称。</span><span class="sxs-lookup"><span data-stu-id="06b2f-117">For files, it also contains the file name.</span></span>
- <span data-ttu-id="06b2f-118">内容类型标头描述的部分中的数据。</span><span class="sxs-lookup"><span data-stu-id="06b2f-118">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="06b2f-119">如果省略此标头，则默认值为文本/无格式。</span><span class="sxs-lookup"><span data-stu-id="06b2f-119">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="06b2f-120">在前面的示例中，用户上载名 GrandCanyon.jpg，为具有内容类型映像/jpeg; 的文件输入文本的值，&quot;夏天休假&quot;。</span><span class="sxs-lookup"><span data-stu-id="06b2f-120">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="06b2f-121">文件上载</span><span class="sxs-lookup"><span data-stu-id="06b2f-121">File Upload</span></span>

<span data-ttu-id="06b2f-122">现在让我们看一下从多部分 MIME 消息中读取文件的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="06b2f-122">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="06b2f-123">控制器将以异步方式读取文件。</span><span class="sxs-lookup"><span data-stu-id="06b2f-123">The controller will read the files asynchronously.</span></span> <span data-ttu-id="06b2f-124">Web API 支持异步操作，使用[基于任务的编程模型](https://msdn.microsoft.com/library/dd460693.aspx)。</span><span class="sxs-lookup"><span data-stu-id="06b2f-124">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="06b2f-125">如果你正面向.NET Framework 4.5，支持首先，以下是代码**异步**和**await**关键字。</span><span class="sxs-lookup"><span data-stu-id="06b2f-125">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="06b2f-126">请注意控制器操作不采用任何参数。</span><span class="sxs-lookup"><span data-stu-id="06b2f-126">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="06b2f-127">这是因为我们处理请求正文内操作，而无需调用媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="06b2f-127">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="06b2f-128">**IsMultipartContent**方法检查请求是否包含多部分 MIME 消息。</span><span class="sxs-lookup"><span data-stu-id="06b2f-128">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="06b2f-129">如果没有，则控制器将返回 HTTP 状态代码 415 （不支持的媒体类型）。</span><span class="sxs-lookup"><span data-stu-id="06b2f-129">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="06b2f-130">**MultipartFormDataStreamProvider**类是一个分配为上载的文件的文件流的帮助器对象。</span><span class="sxs-lookup"><span data-stu-id="06b2f-130">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="06b2f-131">若要读取多部分 MIME 消息，请调用**ReadAsMultipartAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="06b2f-131">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="06b2f-132">此方法提取所有的消息部分，并将其写入到流提供的**MultipartFormDataStreamProvider**。</span><span class="sxs-lookup"><span data-stu-id="06b2f-132">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="06b2f-133">方法完成时，你可以获取有关中的文件信息**数据**属性，这是集合的**MultipartFileData**对象。</span><span class="sxs-lookup"><span data-stu-id="06b2f-133">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="06b2f-134">**MultipartFileData.FileName**是在服务器上，保存文件的本地文件名称。</span><span class="sxs-lookup"><span data-stu-id="06b2f-134">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="06b2f-135">**MultipartFileData.Headers**包含部分标头 (*不*请求标头)。</span><span class="sxs-lookup"><span data-stu-id="06b2f-135">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="06b2f-136">可以使用此访问内容\_处置和内容类型标头。</span><span class="sxs-lookup"><span data-stu-id="06b2f-136">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="06b2f-137">顾名思义， **ReadAsMultipartAsync**是异步方法。</span><span class="sxs-lookup"><span data-stu-id="06b2f-137">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="06b2f-138">若要执行工作，该方法完成后，使用[延续任务](https://msdn.microsoft.com/library/ee372288.aspx)(.NET 4.0) 或**await**关键字 (.NET 4.5)。</span><span class="sxs-lookup"><span data-stu-id="06b2f-138">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="06b2f-139">下面是代码的前面的.NET Framework 4.0 版本：</span><span class="sxs-lookup"><span data-stu-id="06b2f-139">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="06b2f-140">读取窗体控件数据</span><span class="sxs-lookup"><span data-stu-id="06b2f-140">Reading Form Control Data</span></span>

<span data-ttu-id="06b2f-141">我在前面显示的 HTML 窗体有一个文本输入的控件。</span><span class="sxs-lookup"><span data-stu-id="06b2f-141">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="06b2f-142">你可以从控件的值**FormData**属性**MultipartFormDataStreamProvider**。</span><span class="sxs-lookup"><span data-stu-id="06b2f-142">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="06b2f-143">**FormData**是**NameValueCollection**包含窗体控件的名称/值对。</span><span class="sxs-lookup"><span data-stu-id="06b2f-143">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="06b2f-144">集合可以包含重复键。</span><span class="sxs-lookup"><span data-stu-id="06b2f-144">The collection can contain duplicate keys.</span></span> <span data-ttu-id="06b2f-145">请考虑此窗体：</span><span class="sxs-lookup"><span data-stu-id="06b2f-145">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="06b2f-146">请求正文可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="06b2f-146">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="06b2f-147">在这种情况下， **FormData**集合将包含以下键/值对：</span><span class="sxs-lookup"><span data-stu-id="06b2f-147">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="06b2f-148">行程： 往返</span><span class="sxs-lookup"><span data-stu-id="06b2f-148">trip: round-trip</span></span>
- <span data-ttu-id="06b2f-149">选项： nonstop</span><span class="sxs-lookup"><span data-stu-id="06b2f-149">options: nonstop</span></span>
- <span data-ttu-id="06b2f-150">选项： 日期</span><span class="sxs-lookup"><span data-stu-id="06b2f-150">options: dates</span></span>
- <span data-ttu-id="06b2f-151">座位： 窗口</span><span class="sxs-lookup"><span data-stu-id="06b2f-151">seat: window</span></span>
