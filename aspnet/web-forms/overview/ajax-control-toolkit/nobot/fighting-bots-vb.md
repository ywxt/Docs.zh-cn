---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
title: 外部测试机器人 (VB) |Microsoft Docs
author: wenz
description: 自动化的智能机器人塑料效果网络日志和其他网站垃圾邮件，提交注释窗体而无需任何用户交互。 在 ASP.NET AJAX Con NoBot 控件...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: e9803150-452d-4521-97e3-d75d5599383c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
msc.type: authoredcontent
ms.openlocfilehash: e79a973f721c1feeddb00ecbf9d6a76786afb4bb
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833438"
---
<a name="fighting-bots-vb"></a><span data-ttu-id="922b2-104">外部测试机器人 (VB)</span><span class="sxs-lookup"><span data-stu-id="922b2-104">Fighting Bots (VB)</span></span>
====================
<span data-ttu-id="922b2-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="922b2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="922b2-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="922b2-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span></span>

> <span data-ttu-id="922b2-107">自动化的智能机器人塑料效果网络日志和其他网站垃圾邮件，提交注释窗体而无需任何用户交互。</span><span class="sxs-lookup"><span data-stu-id="922b2-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="922b2-108">ASP.NET AJAX 控件工具包中的 NoBot 控件可帮助抵御这些机器人。</span><span class="sxs-lookup"><span data-stu-id="922b2-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>


## <a name="overview"></a><span data-ttu-id="922b2-109">概述</span><span class="sxs-lookup"><span data-stu-id="922b2-109">Overview</span></span>

<span data-ttu-id="922b2-110">自动化的智能机器人塑料效果网络日志和其他网站垃圾邮件，提交注释窗体而无需任何用户交互。</span><span class="sxs-lookup"><span data-stu-id="922b2-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="922b2-111">ASP.NET AJAX 控件工具包中的 NoBot 控件可帮助抵御这些机器人。</span><span class="sxs-lookup"><span data-stu-id="922b2-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="922b2-112">步骤</span><span class="sxs-lookup"><span data-stu-id="922b2-112">Steps</span></span>

<span data-ttu-id="922b2-113">以击败智能机器人的一个常用方法是使用 CAPTCHAs 完全自动化的公共 Turing 测试来告诉计算机和人类相隔。</span><span class="sxs-lookup"><span data-stu-id="922b2-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="922b2-114">Turing 测试最初是一个测试，有人需要确定通信合作伙伴用户，也可以在计算机的位置。</span><span class="sxs-lookup"><span data-stu-id="922b2-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="922b2-115">在 web 中，验证码通常由一些失真字母都在其上的图像组成。</span><span class="sxs-lookup"><span data-stu-id="922b2-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="922b2-116">其思路是只有用户可以读取该图像，字母而 OCR 算法将会失败。</span><span class="sxs-lookup"><span data-stu-id="922b2-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="922b2-117">有几个优点和缺点，这种方法，但本主题的讨论不在本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="922b2-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="922b2-118">但是没有 ASP.NET AJAX 控件工具包提供了类似的方法中的控件： `NoBot`。</span><span class="sxs-lookup"><span data-stu-id="922b2-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="922b2-119">它更容易克服比验证码，但非常易于使用和支付特别适合在其中它被视为成功完成，如果大多数垃圾邮件尝试博客等网站上的费用会大大降低，这`NoBot`控件可以执行操作。</span><span class="sxs-lookup"><span data-stu-id="922b2-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="922b2-120">`NoBot` 如果满足这些条件中至少一个则，截获当前 ASP.NET web 窗体的回发：</span><span class="sxs-lookup"><span data-stu-id="922b2-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="922b2-121">浏览器无法解决 JavaScript 难题 （例如当 JavaScript 停用）</span><span class="sxs-lookup"><span data-stu-id="922b2-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="922b2-122">用户提交窗体进行快速</span><span class="sxs-lookup"><span data-stu-id="922b2-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="922b2-123">客户端 IP 地址通常在一段时间中提交了表单。</span><span class="sxs-lookup"><span data-stu-id="922b2-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="922b2-124">若要检查这些条件，`NoBot`控件需要这些属性 （全部可选的）：</span><span class="sxs-lookup"><span data-stu-id="922b2-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="922b2-125">`ResponseMinimumDelaySeconds` 最少的回发之间的秒数</span><span class="sxs-lookup"><span data-stu-id="922b2-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="922b2-126">`CutoffWindowSeconds` 在其中一个 IP 发是度量值的时间间隔的时间长度</span><span class="sxs-lookup"><span data-stu-id="922b2-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="922b2-127">`CutoffMaximumInstances` 每个时间间隔的秒的最大数量</span><span class="sxs-lookup"><span data-stu-id="922b2-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="922b2-128">以下标记要求至少两秒回发和之间，有超过五次回发或小于 30 秒间隔内：</span><span class="sxs-lookup"><span data-stu-id="922b2-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample1.aspx)]

<span data-ttu-id="922b2-129">然后照常请确保包括`ScriptManager`页中，以便加载 ASP.NET AJAX 库，可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="922b2-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample2.aspx)]

<span data-ttu-id="922b2-130">因为大多数检查`NoBot`正在执行的操作发生在服务器端，您需要检查这些验证结果。</span><span class="sxs-lookup"><span data-stu-id="922b2-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="922b2-131">这可以通过调用`NoBot`的`IsValid()`方法。</span><span class="sxs-lookup"><span data-stu-id="922b2-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="922b2-132">它有一个参数 (作为`out`参数 /`ByRef`参数) 它属于类型`NoBotState`。</span><span class="sxs-lookup"><span data-stu-id="922b2-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="922b2-133">如果检查失败，其字符串表示形式包含的原因和`Valid`否则为。</span><span class="sxs-lookup"><span data-stu-id="922b2-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="922b2-134">以下代码将输出一条消息，根据`NoBot`的结果：</span><span class="sxs-lookup"><span data-stu-id="922b2-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample3.aspx)]

<span data-ttu-id="922b2-135">最后，你需要表单以提交和一个标签元素将其输出消息，并完成 ！</span><span class="sxs-lookup"><span data-stu-id="922b2-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample4.aspx)]

<span data-ttu-id="922b2-136">运行此脚本和停用 JavaScript 或在前两秒内提交窗体或在 30 秒内七次提交窗体时, 将收到一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="922b2-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="922b2-137">但是恰当地使用此控件，因为只有大约 90 95%的用户可以使用 JavaScript 激活，因此 5-10%的用户将会失败`NoBot`的测试。</span><span class="sxs-lookup"><span data-stu-id="922b2-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>


<span data-ttu-id="922b2-138">[![此错误消息可能被引起的智能机器人应用程序](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="922b2-138">[![This error message could have been caused by a bot](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span></span>

<span data-ttu-id="922b2-139">此错误消息可能已由智能机器人应用程序 ([单击此项可查看原尺寸图像](fighting-bots-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="922b2-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="922b2-140">上一篇</span><span class="sxs-lookup"><span data-stu-id="922b2-140">Previous</span></span>](fighting-bots-cs.md)
