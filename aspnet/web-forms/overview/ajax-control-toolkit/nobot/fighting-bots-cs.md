---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: 反击机器人 (C#) |Microsoft 文档
author: wenz
description: 自动化的机器人石膏的垃圾邮件，提交注释窗体，而无需任何用户交互的网络日志和其他网站。 在 ASP.NET AJAX Con NoBot 控件...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: 1ea3aaa5461c2f58a927ae975568f18a34a4729b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="fighting-bots-c"></a><span data-ttu-id="371b6-104">反击机器人 (C#)</span><span class="sxs-lookup"><span data-stu-id="371b6-104">Fighting Bots (C#)</span></span>
====================
<span data-ttu-id="371b6-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="371b6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="371b6-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="371b6-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span></span>

> <span data-ttu-id="371b6-107">自动化的机器人石膏的垃圾邮件，提交注释窗体，而无需任何用户交互的网络日志和其他网站。</span><span class="sxs-lookup"><span data-stu-id="371b6-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="371b6-108">ASP.NET AJAX 控件工具包中的 NoBot 控件可帮助防范这些机器人。</span><span class="sxs-lookup"><span data-stu-id="371b6-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>


## <a name="overview"></a><span data-ttu-id="371b6-109">概述</span><span class="sxs-lookup"><span data-stu-id="371b6-109">Overview</span></span>

<span data-ttu-id="371b6-110">自动化的机器人石膏的垃圾邮件，提交注释窗体，而无需任何用户交互的网络日志和其他网站。</span><span class="sxs-lookup"><span data-stu-id="371b6-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="371b6-111">ASP.NET AJAX 控件工具包中的 NoBot 控件可帮助防范这些机器人。</span><span class="sxs-lookup"><span data-stu-id="371b6-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="371b6-112">步骤</span><span class="sxs-lookup"><span data-stu-id="371b6-112">Steps</span></span>

<span data-ttu-id="371b6-113">一种常见的方法来攻克机器人是使用 CAPTCHAs 完全自动公共执行测试来告诉计算机和理解相隔。</span><span class="sxs-lookup"><span data-stu-id="371b6-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="371b6-114">执行测试最初测试人需要用来确定通信合作伙伴是否用户或计算机。</span><span class="sxs-lookup"><span data-stu-id="371b6-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="371b6-115">在 web 中，验证码通常由以在其上某些失真字母的图像组成。</span><span class="sxs-lookup"><span data-stu-id="371b6-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="371b6-116">思路是仅用户可以读取在图像上的字母而 OCR 算法将失败。</span><span class="sxs-lookup"><span data-stu-id="371b6-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="371b6-117">有几个优点和缺点，这种方法，但本主题的讨论不在本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="371b6-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="371b6-118">但是还有 ASP.NET AJAX 控件工具包提供类似的方法中的控件： `NoBot`。</span><span class="sxs-lookup"><span data-stu-id="371b6-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="371b6-119">它可以更轻松地克服比验证码，但非常易于使用以及如其中它被视为成功，如果大多数垃圾邮件尝试博客网站上的运行状况非常好的可为失败，其中`NoBot`控件可以执行操作。</span><span class="sxs-lookup"><span data-stu-id="371b6-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="371b6-120">`NoBot` 截获当前的 ASP.NET web 窗体回的发，如果满足至少这些条件之一：</span><span class="sxs-lookup"><span data-stu-id="371b6-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="371b6-121">浏览器无法解决一个 JavaScript 难题 （例如当 JavaScript 停用）</span><span class="sxs-lookup"><span data-stu-id="371b6-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="371b6-122">用户提交到快速表单</span><span class="sxs-lookup"><span data-stu-id="371b6-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="371b6-123">客户端 IP 地址太通常在一段时间中提交了表单。</span><span class="sxs-lookup"><span data-stu-id="371b6-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="371b6-124">请检查这些条件，以便`NoBot`控件需要这些属性 （所有这些可选）：</span><span class="sxs-lookup"><span data-stu-id="371b6-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="371b6-125">`ResponseMinimumDelaySeconds` 最小量之间回发的秒数</span><span class="sxs-lookup"><span data-stu-id="371b6-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="371b6-126">`CutoffWindowSeconds` 从一个 IP 的回发中度量值的时间间隔的长度</span><span class="sxs-lookup"><span data-stu-id="371b6-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="371b6-127">`CutoffMaximumInstances` 每个时间间隔的秒的最大量</span><span class="sxs-lookup"><span data-stu-id="371b6-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="371b6-128">以下标记要求至少两个秒之间回发经过和有只有五回发或小于 30 秒间隔内：</span><span class="sxs-lookup"><span data-stu-id="371b6-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

<span data-ttu-id="371b6-129">然后照常确保包括`ScriptManager`在页中，以便加载 ASP.NET AJAX 库，并可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="371b6-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

<span data-ttu-id="371b6-130">因为大多数检查`NoBot`正在执行的操作发生在服务器端中，你需要检查这些验证的结果。</span><span class="sxs-lookup"><span data-stu-id="371b6-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="371b6-131">这可以通过调用`NoBot`的`IsValid()`方法。</span><span class="sxs-lookup"><span data-stu-id="371b6-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="371b6-132">它具有一个自变量 (作为`out`参数 /`ByRef`参数) 它属于类型`NoBotState`。</span><span class="sxs-lookup"><span data-stu-id="371b6-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="371b6-133">如果检查失败，其字符串表示形式包含的原因和`Valid`否则为。</span><span class="sxs-lookup"><span data-stu-id="371b6-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="371b6-134">以下代码将输出一条消息，根据`NoBot`的结果：</span><span class="sxs-lookup"><span data-stu-id="371b6-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

<span data-ttu-id="371b6-135">最后，你需要一个用于提交窗体和 label 元素将消息输出，你已完成 ！</span><span class="sxs-lookup"><span data-stu-id="371b6-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

<span data-ttu-id="371b6-136">当运行此脚本和停用 JavaScript 或在前两秒内提交表单或在 30 秒内七次提交表单时，你将收到错误消息。</span><span class="sxs-lookup"><span data-stu-id="371b6-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="371b6-137">但是合理地使用此控件，因为只有大约 90 95%的用户具有激活的 JavaScript，因此将失败 5-10%的用户`NoBot`的测试。</span><span class="sxs-lookup"><span data-stu-id="371b6-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>


<span data-ttu-id="371b6-138">[![此错误消息可能已引起 bot](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="371b6-138">[![This error message could have been caused by a bot](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)</span></span>

<span data-ttu-id="371b6-139">此错误消息可能已由 bot ([单击以查看实际尺寸的图像](fighting-bots-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="371b6-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="371b6-140">下一篇</span><span class="sxs-lookup"><span data-stu-id="371b6-140">Next</span></span>](fighting-bots-vb.md)
