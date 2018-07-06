---
uid: whitepapers/request-validation
title: 请求验证-阻止脚本攻击 |Microsoft Docs
author: rick-anderson
description: 本白皮书介绍了请求验证功能的位置，默认情况下，应用程序无法处理未编码的 HTML 内容 submitt ASP.NET...
ms.author: aspnetcontent
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 0dfbfcae70792c57d530fc5e6fb73f8f96ec6e02
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809740"
---
<a name="request-validation---preventing-script-attacks"></a><span data-ttu-id="c7e82-103">请求验证-阻止脚本攻击</span><span class="sxs-lookup"><span data-stu-id="c7e82-103">Request Validation - Preventing Script Attacks</span></span>
====================
> <span data-ttu-id="c7e82-104">本白皮书介绍其中，默认情况下，应用程序会阻止处理提交到服务器的未编码的 HTML 内容的 ASP.NET 请求验证功能。</span><span class="sxs-lookup"><span data-stu-id="c7e82-104">This paper describes the request validation feature of ASP.NET where, by default, the application is prevented from processing unencoded HTML content submitted to the server.</span></span> <span data-ttu-id="c7e82-105">当应用程序已被设计来安全地处理 HTML 数据时，可以禁用此请求验证功能。</span><span class="sxs-lookup"><span data-stu-id="c7e82-105">This request validation feature can be disabled when the application has been designed to safely process HTML data.</span></span>
> 
> <span data-ttu-id="c7e82-106">适用于 ASP.NET 1.1 和 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="c7e82-106">Applies to ASP.NET 1.1 and ASP.NET 2.0.</span></span>


<span data-ttu-id="c7e82-107">请求验证的 ASP.NET 版本 1.1，一项功能可阻止服务器接受内容包含未编码 HTML。</span><span class="sxs-lookup"><span data-stu-id="c7e82-107">Request validation, a feature of ASP.NET since version 1.1, prevents the server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="c7e82-108">此功能旨在帮助阻止某些脚本注入攻击，客户端脚本代码或 HTML 可以不知情的情况下提交到服务器、 存储，并随后呈现给其他用户。</span><span class="sxs-lookup"><span data-stu-id="c7e82-108">This feature is designed to help prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted to a server, stored, and then presented to other users.</span></span> <span data-ttu-id="c7e82-109">我们仍强烈建议验证所有输入的数据和 HTML 对其在适当的时候进行编码。</span><span class="sxs-lookup"><span data-stu-id="c7e82-109">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span>

<span data-ttu-id="c7e82-110">例如，您创建一个网页，请求用户的电子邮件地址，然后选择电子邮件地址在数据库中的存储。</span><span class="sxs-lookup"><span data-stu-id="c7e82-110">For example, you create a Web page that requests a user's email address and then stores that email address in a database.</span></span> <span data-ttu-id="c7e82-111">如果用户输入&lt;脚本&gt;警报 （"你好从脚本"）&lt;/script&gt;而不是一个有效的电子邮件地址，当提供该数据时，此脚本可执行如果内容未正确编码。</span><span class="sxs-lookup"><span data-stu-id="c7e82-111">If the user enters &lt;SCRIPT&gt;alert("hello from script")&lt;/SCRIPT&gt; instead of a valid email address, when that data is presented, this script can be executed if the content was not properly encoded.</span></span> <span data-ttu-id="c7e82-112">ASP.NET 请求验证功能可以避免这种情况发生。</span><span class="sxs-lookup"><span data-stu-id="c7e82-112">The request validation feature of ASP.NET prevents this from happening.</span></span>

## <a name="why-this-feature-is-useful"></a><span data-ttu-id="c7e82-113">为什么此功能很有用</span><span class="sxs-lookup"><span data-stu-id="c7e82-113">Why this feature is useful</span></span>

<span data-ttu-id="c7e82-114">许多站点并不知道它们是打开到简单的脚本注入攻击。</span><span class="sxs-lookup"><span data-stu-id="c7e82-114">Many sites are not aware that they are open to simple script injection attacks.</span></span> <span data-ttu-id="c7e82-115">这些攻击的目的是通过显示 HTML，破坏站点还是用于可能执行客户端脚本以将用户重定向到黑客的站点，脚本注入攻击是 Web 开发人员必须应对的问题。</span><span class="sxs-lookup"><span data-stu-id="c7e82-115">Whether the purpose of these attacks is to deface the site by displaying HTML, or to potentially execute client script to redirect the user to a hacker's site, script injection attacks are a problem that Web developers must contend with.</span></span>

<span data-ttu-id="c7e82-116">脚本注入攻击是需考虑的所有 web 开发人员，无论他们使用的 ASP.NET、 ASP 或其他 web 开发技术。</span><span class="sxs-lookup"><span data-stu-id="c7e82-116">Script injection attacks are a concern of all web developers, whether they are using ASP.NET, ASP, or other web development technologies.</span></span>

<span data-ttu-id="c7e82-117">ASP.NET 请求验证功能主动防止这些攻击通过不允许未编码的 HTML 内容，除非开发人员决定以允许该内容由服务器进行处理。</span><span class="sxs-lookup"><span data-stu-id="c7e82-117">The ASP.NET request validation feature proactively prevents these attacks by not allowing unencoded HTML content to be processed by the server unless the developer decides to allow that content.</span></span>

## <a name="what-to-expect-error-page"></a><span data-ttu-id="c7e82-118">出现的情况: 错误页</span><span class="sxs-lookup"><span data-stu-id="c7e82-118">What to expect: Error Page</span></span>

<span data-ttu-id="c7e82-119">下面的屏幕快照显示了一些示例 ASP.NET 代码：</span><span class="sxs-lookup"><span data-stu-id="c7e82-119">The screen shot below shows some sample ASP.NET code:</span></span>

![](request-validation/_static/image1.png)

<span data-ttu-id="c7e82-120">运行此代码会生成一个简单的页面，您可以在文本框中输入一些文本中，单击按钮，并在标签控件中显示文本：</span><span class="sxs-lookup"><span data-stu-id="c7e82-120">Running this code results in a simple page that allows you to enter some text in the textbox, click the button, and display the text in the label control:</span></span>

![](request-validation/_static/image2.png)

<span data-ttu-id="c7e82-121">但是，如是 JavaScript，`<script>alert("hello!")</script>`输入并提交，则会得到了异常：</span><span class="sxs-lookup"><span data-stu-id="c7e82-121">However, were JavaScript, such as `<script>alert("hello!")</script>` to be entered and submitted we would get an exception:</span></span>

![](request-validation/_static/image3.png)

<span data-ttu-id="c7e82-122">错误消息指出潜在的危险 Request.Form 的检测到值，并提供更多详细信息中并完全发生了什么以及如何更改行为的说明。</span><span class="sxs-lookup"><span data-stu-id="c7e82-122">The error message states that a 'potentially dangerous Request.Form value was detected' and provides more details in the description as to exactly what occurred and how to change the behavior.</span></span> <span data-ttu-id="c7e82-123">例如：</span><span class="sxs-lookup"><span data-stu-id="c7e82-123">For example:</span></span>

<span data-ttu-id="c7e82-124">请求验证程序检测到潜在危险的客户端的输入的值，并在请求处理已中止。</span><span class="sxs-lookup"><span data-stu-id="c7e82-124">Request validation has detected a potentially dangerous client input value, and processing of the request has been aborted.</span></span> <span data-ttu-id="c7e82-125">此值可能表明攻击者尝试破坏应用程序，如跨站点脚本攻击的安全。</span><span class="sxs-lookup"><span data-stu-id="c7e82-125">This value may indicate an attempt to compromise the security of your application, such as a cross-site scripting attack.</span></span> <span data-ttu-id="c7e82-126">可以通过设置禁用请求验证`validateRequest=false`Page 指令中或在配置部分中。</span><span class="sxs-lookup"><span data-stu-id="c7e82-126">You can disable request validation by setting `validateRequest=false` in the Page directive or in the configuration section.</span></span> <span data-ttu-id="c7e82-127">但是，强烈建议，你的应用程序显式检查所有输入在这种情况下。</span><span class="sxs-lookup"><span data-stu-id="c7e82-127">However, it is strongly recommended that your application explicitly check all inputs in this case.</span></span>

## <a name="disabling-request-validation-on-a-page"></a><span data-ttu-id="c7e82-128">禁用页面上的请求验证</span><span class="sxs-lookup"><span data-stu-id="c7e82-128">Disabling request validation on a page</span></span>

<span data-ttu-id="c7e82-129">若要禁用请求验证，必须设置的页面上`validateRequest`到 Page 指令属性`false`:</span><span class="sxs-lookup"><span data-stu-id="c7e82-129">To disable request validation on a page you must set the `validateRequest` attribute of the Page directive to `false`:</span></span>

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> <span data-ttu-id="c7e82-130">禁用请求验证后，可将内容提交到页;它是页面开发人员，以确保该内容的责任是正确编码或处理。</span><span class="sxs-lookup"><span data-stu-id="c7e82-130">When request validation is disabled, content can be submitted to a page; it is the responsibility of the page developer to ensure that content is properly encoded or processed.</span></span>

## <a name="disabling-request-validation-for-your-application"></a><span data-ttu-id="c7e82-131">禁用你的应用程序的请求验证</span><span class="sxs-lookup"><span data-stu-id="c7e82-131">Disabling request validation for your application</span></span>

<span data-ttu-id="c7e82-132">若要为应用程序禁用请求验证，必须修改或为应用程序创建 Web.config 文件并将设置的 validateRequest 特性`<pages />`部分`false`:</span><span class="sxs-lookup"><span data-stu-id="c7e82-132">To disable request validation for your application, you must modify or create a Web.config file for your application and set the validateRequest attribute of the `<pages />` section to `false`:</span></span>

[!code-xml[Main](request-validation/samples/sample2.xml)]

<span data-ttu-id="c7e82-133">如果你想要禁用请求验证的服务器上的所有应用程序，您可以执行此项修改 Machine.config 文件。</span><span class="sxs-lookup"><span data-stu-id="c7e82-133">If you wish to disable request validation for all applications on your server, you can make this modification to your Machine.config file.</span></span>

> [!CAUTION]
> <span data-ttu-id="c7e82-134">禁用请求验证后，可将内容提交到你的应用程序;它是应用程序开发人员，以确保该内容的责任是正确编码或处理。</span><span class="sxs-lookup"><span data-stu-id="c7e82-134">When request validation is disabled, content can be submitted to your application; it is the responsibility of the application developer to ensure that content is properly encoded or processed.</span></span>

<span data-ttu-id="c7e82-135">下面的代码修改以关闭请求验证：</span><span class="sxs-lookup"><span data-stu-id="c7e82-135">The code below is modified to turn off request validation:</span></span>

![](request-validation/_static/image4.png)

<span data-ttu-id="c7e82-136">现在，如果以下 JavaScript 已输入到 textbox`<script>alert("hello!")</script>`结果将是：</span><span class="sxs-lookup"><span data-stu-id="c7e82-136">Now if the following JavaScript was entered into the textbox `<script>alert("hello!")</script>` the result would be:</span></span>

![](request-validation/_static/image5.png)

<span data-ttu-id="c7e82-137">若要防止这种情况发生，与处于关闭状态的请求验证，我们需要为 HTML 编码内容。</span><span class="sxs-lookup"><span data-stu-id="c7e82-137">To prevent this from happening, with request validation turned off, we need to HTML encode the content.</span></span>

## <a name="how-to-html-encode-content"></a><span data-ttu-id="c7e82-138">如何为 HTML 编码内容</span><span class="sxs-lookup"><span data-stu-id="c7e82-138">How to HTML encode content</span></span>

<span data-ttu-id="c7e82-139">如果禁用了请求验证，所以最好对 HTML 编码的内容将存储以供将来使用。</span><span class="sxs-lookup"><span data-stu-id="c7e82-139">If you have disabled request validation, it is good practice to HTML-encode content that will be stored for future use.</span></span> <span data-ttu-id="c7e82-140">HTML 编码将自动替换任何 '&lt;或&gt;（以及其他多个符号） 与相应的 HTML 编码表示形式。</span><span class="sxs-lookup"><span data-stu-id="c7e82-140">HTML encoding will automatically replace any ‘&lt;' or ‘&gt;' (together with several other symbols) with their corresponding HTML encoded representation.</span></span> <span data-ttu-id="c7e82-141">例如，'&lt;替换为&amp;l t; 和&gt;将替换为&amp;g t;。</span><span class="sxs-lookup"><span data-stu-id="c7e82-141">For example, ‘&lt;' is replaced by ‘&amp;lt;' and ‘&gt;' is replaced by ‘&amp;gt;'.</span></span> <span data-ttu-id="c7e82-142">浏览器使用这些特殊的代码以显示&lt;或&gt;在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="c7e82-142">Browsers use these special codes to display the ‘&lt;' or ‘&gt;' in the browser.</span></span>

<span data-ttu-id="c7e82-143">内容可以轻松地在服务器使用的编码 HTML `Server.HtmlEncode(string)` API。</span><span class="sxs-lookup"><span data-stu-id="c7e82-143">Content can be easily HTML-encoded on the server using the `Server.HtmlEncode(string)` API.</span></span> <span data-ttu-id="c7e82-144">内容也可以很容易 HTML 解码，也就是说，就会返回到标准 HTML 使用`Server.HtmlDecode(string)`方法。</span><span class="sxs-lookup"><span data-stu-id="c7e82-144">Content can also be easily HTML-decoded, that is, reverted back to standard HTML using the `Server.HtmlDecode(string)` method.</span></span>

![](request-validation/_static/image6.png)

<span data-ttu-id="c7e82-145">生成中：</span><span class="sxs-lookup"><span data-stu-id="c7e82-145">Resulting in:</span></span>

![](request-validation/_static/image7.png)
