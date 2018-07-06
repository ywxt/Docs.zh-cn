---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: 仅允许特定字符在文本框中 (VB) |Microsoft Docs
author: wenz
description: ASP.NET 验证控件可以确保用户输入中允许的仅某些字符。 但是这仍然不会阻止用户根据键入的无效...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: e53d7282237c94b88c712e53bf607dcb94ccf1f2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830741"
---
<a name="allowing-only-certain-characters-in-a-text-box-vb"></a><span data-ttu-id="55d11-104">仅允许特定字符在文本框中 (VB)</span><span class="sxs-lookup"><span data-stu-id="55d11-104">Allowing Only Certain Characters in a Text Box (VB)</span></span>
====================
<span data-ttu-id="55d11-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="55d11-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="55d11-106">[下载代码](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="55d11-106">[Download Code](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span></span>

> <span data-ttu-id="55d11-107">ASP.NET 验证控件可以确保用户输入中允许的仅某些字符。</span><span class="sxs-lookup"><span data-stu-id="55d11-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="55d11-108">但是这仍然不会阻止用户键入无效的字符，并尝试提交窗体。</span><span class="sxs-lookup"><span data-stu-id="55d11-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>


## <a name="overview"></a><span data-ttu-id="55d11-109">概述</span><span class="sxs-lookup"><span data-stu-id="55d11-109">Overview</span></span>

<span data-ttu-id="55d11-110">ASP.NET 验证控件可以确保用户输入中允许的仅某些字符。</span><span class="sxs-lookup"><span data-stu-id="55d11-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="55d11-111">但是这仍然不会阻止用户键入无效的字符，并尝试提交窗体。</span><span class="sxs-lookup"><span data-stu-id="55d11-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="55d11-112">步骤</span><span class="sxs-lookup"><span data-stu-id="55d11-112">Steps</span></span>

<span data-ttu-id="55d11-113">ASP.NET AJAX 控件工具包包含`FilteredTextBox`控件扩展了文本框。</span><span class="sxs-lookup"><span data-stu-id="55d11-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="55d11-114">激活后，某些组的字符可能会输入到字段。</span><span class="sxs-lookup"><span data-stu-id="55d11-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="55d11-115">为实现此目的，我们首先需要像往常一样 ASP.NET AJAX`ScriptManager`这会加载哪些还由 ASP.NET AJAX 控件工具包的 JavaScript 库：</span><span class="sxs-lookup"><span data-stu-id="55d11-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

<span data-ttu-id="55d11-116">然后，我们需要一个文本框：</span><span class="sxs-lookup"><span data-stu-id="55d11-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

<span data-ttu-id="55d11-117">最后，`FilteredTextBoxExtender`控件负责限制允许用户键入的字符。</span><span class="sxs-lookup"><span data-stu-id="55d11-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="55d11-118">首先，设置`TargetControlID`归于`ID`的`TextBox`控件。</span><span class="sxs-lookup"><span data-stu-id="55d11-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="55d11-119">然后，选择一个可用`FilterType`值：</span><span class="sxs-lookup"><span data-stu-id="55d11-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="55d11-120">`Custom` 默认设置;你必须提供一组有效字符为单位</span><span class="sxs-lookup"><span data-stu-id="55d11-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="55d11-121">`LowercaseLetters` 仅小写字母</span><span class="sxs-lookup"><span data-stu-id="55d11-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="55d11-122">`Numbers` 仅为数字</span><span class="sxs-lookup"><span data-stu-id="55d11-122">`Numbers` digits only</span></span>
- <span data-ttu-id="55d11-123">`UppercaseLetters` 大写的字母</span><span class="sxs-lookup"><span data-stu-id="55d11-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="55d11-124">如果`Custom FilterType`使用时，`ValidChars`属性必须设置，并提供可能键入的字符的列表。</span><span class="sxs-lookup"><span data-stu-id="55d11-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="55d11-125">顺便提一下： 如果尝试将文本粘贴到文本框中，删除所有无效字符。</span><span class="sxs-lookup"><span data-stu-id="55d11-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="55d11-126">下面是针对标记`FilteredTextBoxExtender`仅允许数字的控件 (也是可能具有的某些内容`FilterType="Numbers"`):</span><span class="sxs-lookup"><span data-stu-id="55d11-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

<span data-ttu-id="55d11-127">运行页面，然后重试输入一个字母，如果启用 JavaScript，它不起作用;但是，数字显示在页上。</span><span class="sxs-lookup"><span data-stu-id="55d11-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="55d11-128">但是请注意，保护`FilteredTextBox`提供不是高防护： 如果 JavaScript 已启用，因此您必须使用其他验证方法，即 ASP 可能会在文本框中输入任何数据。NET 的验证控件。</span><span class="sxs-lookup"><span data-stu-id="55d11-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>


<span data-ttu-id="55d11-129">[![可能输入仅数字](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="55d11-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span></span>

<span data-ttu-id="55d11-130">可能输入仅数字 ([单击此项可查看原尺寸图像](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="55d11-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="55d11-131">上一篇</span><span class="sxs-lookup"><span data-stu-id="55d11-131">Previous</span></span>](allowing-only-certain-characters-in-a-text-box-cs.md)
