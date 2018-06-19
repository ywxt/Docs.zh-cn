---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 在 ASP.NET Web API 发送 HTML 窗体数据： 窗体编码形式数据 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/15/2012
ms.topic: article
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 0ed339c4f9d5854ab5a21cdd077a4d494987101f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26506936"
---
<a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="db7f6-102">在 ASP.NET Web API 发送 HTML 窗体数据： 窗体编码形式的数据</span><span class="sxs-lookup"><span data-stu-id="db7f6-102">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>
====================
<span data-ttu-id="db7f6-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="db7f6-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="db7f6-104">第 1 部分： 窗体编码形式数据</span><span class="sxs-lookup"><span data-stu-id="db7f6-104">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="db7f6-105">这篇文章演示如何窗体编码形式将数据发布到 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="db7f6-105">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="db7f6-106">HTML 窗体概述</span><span class="sxs-lookup"><span data-stu-id="db7f6-106">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="db7f6-107">发送的复杂类型</span><span class="sxs-lookup"><span data-stu-id="db7f6-107">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="db7f6-108">通过 AJAX 发送的窗体数据</span><span class="sxs-lookup"><span data-stu-id="db7f6-108">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="db7f6-109">发送的简单类型</span><span class="sxs-lookup"><span data-stu-id="db7f6-109">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="db7f6-110">[下载完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)。</span><span class="sxs-lookup"><span data-stu-id="db7f6-110">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>


<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="db7f6-111">HTML 窗体概述</span><span class="sxs-lookup"><span data-stu-id="db7f6-111">Overview of HTML Forms</span></span>

<span data-ttu-id="db7f6-112">HTML 窗体使用获取，或者发布将数据发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="db7f6-112">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="db7f6-113">**方法**属性**窗体**元素提供的 HTTP 方法：</span><span class="sxs-lookup"><span data-stu-id="db7f6-113">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="db7f6-114">默认方法为 GET。</span><span class="sxs-lookup"><span data-stu-id="db7f6-114">The default method is GET.</span></span> <span data-ttu-id="db7f6-115">如果窗体使用 GET，窗体的数据被编码为查询字符串的 URI 中。</span><span class="sxs-lookup"><span data-stu-id="db7f6-115">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="db7f6-116">如果窗体使用 POST，表单数据都放在请求正文中。</span><span class="sxs-lookup"><span data-stu-id="db7f6-116">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="db7f6-117">已过帐数据**enctype**属性指定请求正文的格式：</span><span class="sxs-lookup"><span data-stu-id="db7f6-117">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="db7f6-118">enctype</span><span class="sxs-lookup"><span data-stu-id="db7f6-118">enctype</span></span> | <span data-ttu-id="db7f6-119">描述</span><span class="sxs-lookup"><span data-stu-id="db7f6-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="db7f6-120">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="db7f6-120">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="db7f6-121">窗体数据被编码为名称/值对，类似于 URI 查询字符串。</span><span class="sxs-lookup"><span data-stu-id="db7f6-121">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="db7f6-122">这是默认格式为 POST。</span><span class="sxs-lookup"><span data-stu-id="db7f6-122">This is the default format for POST.</span></span> |
| <span data-ttu-id="db7f6-123">multipart/窗体的数据</span><span class="sxs-lookup"><span data-stu-id="db7f6-123">multipart/form-data</span></span> | <span data-ttu-id="db7f6-124">窗体数据被编码为多部分 MIME 消息。</span><span class="sxs-lookup"><span data-stu-id="db7f6-124">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="db7f6-125">如果将文件上载到服务器，请使用此格式。</span><span class="sxs-lookup"><span data-stu-id="db7f6-125">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="db7f6-126">本文的第 1 部分考察 x-响应客户-窗体-urlencoded 格式。</span><span class="sxs-lookup"><span data-stu-id="db7f6-126">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="db7f6-127">[第 2 部分](sending-html-form-data-part-2.md)介绍多部分 MIME。</span><span class="sxs-lookup"><span data-stu-id="db7f6-127">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="db7f6-128">发送的复杂类型</span><span class="sxs-lookup"><span data-stu-id="db7f6-128">Sending Complex Types</span></span>

<span data-ttu-id="db7f6-129">通常情况下，你将发送一个复杂类型，由多个窗体控件中获取的值构成。</span><span class="sxs-lookup"><span data-stu-id="db7f6-129">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="db7f6-130">请考虑以下模型表示的状态更新：</span><span class="sxs-lookup"><span data-stu-id="db7f6-130">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="db7f6-131">下面是接受一个 Web API 控制器`Update`通过 POST 的对象。</span><span class="sxs-lookup"><span data-stu-id="db7f6-131">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="db7f6-132">此控制器使用[基于操作的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)，因此路由模板是&quot;api / {controller} / {action} / {id}&quot;。</span><span class="sxs-lookup"><span data-stu-id="db7f6-132">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="db7f6-133">客户端会将发布到数据&quot;/api/updates/complex&quot;。</span><span class="sxs-lookup"><span data-stu-id="db7f6-133">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>


<span data-ttu-id="db7f6-134">现在让我们来编写用户提交状态更新以 HTML 形式。</span><span class="sxs-lookup"><span data-stu-id="db7f6-134">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="db7f6-135">请注意，**操作**窗体上的属性是我们控制器操作的 URI。</span><span class="sxs-lookup"><span data-stu-id="db7f6-135">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="db7f6-136">下面是具有某些值中输入的窗体：</span><span class="sxs-lookup"><span data-stu-id="db7f6-136">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="db7f6-137">当用户单击提交时，则浏览器将发送 HTTP 请求与以下类似：</span><span class="sxs-lookup"><span data-stu-id="db7f6-137">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="db7f6-138">请注意，请求正文包含格式为名称/值对的窗体数据。</span><span class="sxs-lookup"><span data-stu-id="db7f6-138">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="db7f6-139">Web API 会自动将名称/值对转换到的实例`Update`类。</span><span class="sxs-lookup"><span data-stu-id="db7f6-139">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="db7f6-140">通过 AJAX 发送的窗体数据</span><span class="sxs-lookup"><span data-stu-id="db7f6-140">Sending Form Data via AJAX</span></span>

<span data-ttu-id="db7f6-141">当用户提交表单时，浏览器导航离开当前页，并呈现响应消息的正文。</span><span class="sxs-lookup"><span data-stu-id="db7f6-141">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="db7f6-142">这是确定时响应是 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="db7f6-142">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="db7f6-143">与 web API，但是，响应正文是通常为空或包含结构化的数据，例如 JSON。</span><span class="sxs-lookup"><span data-stu-id="db7f6-143">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="db7f6-144">在这种情况下，它更有意义发送的窗体数据使用 AJAX 请求，以便该页可以处理响应。</span><span class="sxs-lookup"><span data-stu-id="db7f6-144">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="db7f6-145">下面的代码演示如何发布使用 jQuery 的窗体数据。</span><span class="sxs-lookup"><span data-stu-id="db7f6-145">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="db7f6-146">JQuery**提交**函数窗体操作替换为新的函数。</span><span class="sxs-lookup"><span data-stu-id="db7f6-146">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="db7f6-147">此设置将替代提交按钮的默认行为。</span><span class="sxs-lookup"><span data-stu-id="db7f6-147">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="db7f6-148">**序列化**函数名称/值对序列化为窗体数据。</span><span class="sxs-lookup"><span data-stu-id="db7f6-148">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="db7f6-149">若要向服务器发送的窗体数据，调用`$.post()`。</span><span class="sxs-lookup"><span data-stu-id="db7f6-149">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="db7f6-150">完成请求后，`.success()`或`.error()`处理程序为用户显示相应的消息。</span><span class="sxs-lookup"><span data-stu-id="db7f6-150">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="db7f6-151">发送的简单类型</span><span class="sxs-lookup"><span data-stu-id="db7f6-151">Sending Simple Types</span></span>

<span data-ttu-id="db7f6-152">在前面的部分中，我们将发送一个复杂类型，Web API 反序列化到模型类的实例。</span><span class="sxs-lookup"><span data-stu-id="db7f6-152">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="db7f6-153">你还可以发送简单类型，例如字符串。</span><span class="sxs-lookup"><span data-stu-id="db7f6-153">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="db7f6-154">在发送之前简单类型，请考虑改为在复杂类型中包装值。</span><span class="sxs-lookup"><span data-stu-id="db7f6-154">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="db7f6-155">这使您在服务器端的模型验证的优点，并轻松地根据需要扩展您的模型。</span><span class="sxs-lookup"><span data-stu-id="db7f6-155">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>


<span data-ttu-id="db7f6-156">要发送的简单类型的基本步骤都相同，但有两个细微的差异。</span><span class="sxs-lookup"><span data-stu-id="db7f6-156">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="db7f6-157">首先，在控制器中，必须修饰参数名称后的加**FromBody**属性。</span><span class="sxs-lookup"><span data-stu-id="db7f6-157">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="db7f6-158">默认情况下，Web API 尝试于请求 URI 中获取简单类型。</span><span class="sxs-lookup"><span data-stu-id="db7f6-158">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="db7f6-159">**FromBody**属性告知 Web API 以从请求正文中读取值。</span><span class="sxs-lookup"><span data-stu-id="db7f6-159">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="db7f6-160">Web API 读取响应正文最多一次，以便只有一个操作的参数可来自于请求正文。</span><span class="sxs-lookup"><span data-stu-id="db7f6-160">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="db7f6-161">如果你需要从请求正文中获取多个值，定义复杂类型。</span><span class="sxs-lookup"><span data-stu-id="db7f6-161">If you need to get multiple values from the request body, define a complex type.</span></span>


<span data-ttu-id="db7f6-162">其次，客户端需要发送具有以下格式的值：</span><span class="sxs-lookup"><span data-stu-id="db7f6-162">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="db7f6-163">具体而言，名称/值对的名称部分必须是简单类型为空。</span><span class="sxs-lookup"><span data-stu-id="db7f6-163">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="db7f6-164">并非所有浏览器都支持这对于 HTML 窗体，但你创建此格式，在脚本中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="db7f6-164">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="db7f6-165">下面是一个示例表单：</span><span class="sxs-lookup"><span data-stu-id="db7f6-165">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="db7f6-166">和下面是用于将此窗体值提交脚本。</span><span class="sxs-lookup"><span data-stu-id="db7f6-166">And here is the script to submit the form value.</span></span> <span data-ttu-id="db7f6-167">与前一个脚本中的唯一差异是自变量传递给**文章**函数。</span><span class="sxs-lookup"><span data-stu-id="db7f6-167">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="db7f6-168">可以使用相同的方法将发送一个简单的类型数组：</span><span class="sxs-lookup"><span data-stu-id="db7f6-168">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="db7f6-169">其他资源</span><span class="sxs-lookup"><span data-stu-id="db7f6-169">Additional Resources</span></span>

[<span data-ttu-id="db7f6-170">第 2 部分： 文件上载和多部分 MIME</span><span class="sxs-lookup"><span data-stu-id="db7f6-170">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
