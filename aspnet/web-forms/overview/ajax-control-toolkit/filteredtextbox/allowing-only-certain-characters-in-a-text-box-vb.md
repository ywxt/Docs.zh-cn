---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: "允许文本框 (VB) 中的某些字符 |Microsoft 文档"
author: wenz
description: "ASP.NET 验证控件可以确保只有某些字符允许在用户输入。 但是这仍不会阻止用户键入无效..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: b41ec1dfda5d85c625026e1f1e1ecd7e190ee3ce
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="allowing-only-certain-characters-in-a-text-box-vb"></a><span data-ttu-id="9bafd-104">允许仅某些字符在文本框中 (VB)</span><span class="sxs-lookup"><span data-stu-id="9bafd-104">Allowing Only Certain Characters in a Text Box (VB)</span></span>
====================
<span data-ttu-id="9bafd-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="9bafd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9bafd-106">[下载代码](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="9bafd-106">[Download Code](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span></span>

> <span data-ttu-id="9bafd-107">ASP.NET 验证控件可以确保只有某些字符允许在用户输入。</span><span class="sxs-lookup"><span data-stu-id="9bafd-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="9bafd-108">但是这仍不会阻止用户键入无效的字符并尝试提交表单。</span><span class="sxs-lookup"><span data-stu-id="9bafd-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>


## <a name="overview"></a><span data-ttu-id="9bafd-109">概述</span><span class="sxs-lookup"><span data-stu-id="9bafd-109">Overview</span></span>

<span data-ttu-id="9bafd-110">ASP.NET 验证控件可以确保只有某些字符允许在用户输入。</span><span class="sxs-lookup"><span data-stu-id="9bafd-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="9bafd-111">但是这仍不会阻止用户键入无效的字符并尝试提交表单。</span><span class="sxs-lookup"><span data-stu-id="9bafd-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="9bafd-112">步骤</span><span class="sxs-lookup"><span data-stu-id="9bafd-112">Steps</span></span>

<span data-ttu-id="9bafd-113">ASP.NET AJAX 控件工具包中包含`FilteredTextBox`控件扩展了一个文本框。</span><span class="sxs-lookup"><span data-stu-id="9bafd-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="9bafd-114">一旦激活，可能会在字段中输入某组的字符。</span><span class="sxs-lookup"><span data-stu-id="9bafd-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="9bafd-115">为此，我们首先需要像往常一样 ASP.NET AJAX`ScriptManager`这会将加载 JavaScript 库，后者也由 ASP.NET AJAX 控件工具包：</span><span class="sxs-lookup"><span data-stu-id="9bafd-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

<span data-ttu-id="9bafd-116">然后，我们需要一个文本框：</span><span class="sxs-lookup"><span data-stu-id="9bafd-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

<span data-ttu-id="9bafd-117">最后，`FilteredTextBoxExtender`控件负责限制允许用户键入的字符。</span><span class="sxs-lookup"><span data-stu-id="9bafd-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="9bafd-118">首先，设置`TargetControlID`属性设为`ID`的`TextBox`控件。</span><span class="sxs-lookup"><span data-stu-id="9bafd-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="9bafd-119">然后，选择的某个可用`FilterType`值：</span><span class="sxs-lookup"><span data-stu-id="9bafd-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="9bafd-120">`Custom`默认设置;你必须提供有效的字符的列表</span><span class="sxs-lookup"><span data-stu-id="9bafd-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="9bafd-121">`LowercaseLetters`仅为小写字母</span><span class="sxs-lookup"><span data-stu-id="9bafd-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="9bafd-122">`Numbers`仅为数字</span><span class="sxs-lookup"><span data-stu-id="9bafd-122">`Numbers` digits only</span></span>
- <span data-ttu-id="9bafd-123">`UppercaseLetters`仅大写字母</span><span class="sxs-lookup"><span data-stu-id="9bafd-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="9bafd-124">如果`Custom FilterType`使用时，`ValidChars`属性必须是一组并提供可能键入的字符的列表。</span><span class="sxs-lookup"><span data-stu-id="9bafd-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="9bafd-125">顺便说一下： 如果你尝试将文本粘贴到文本框中，删除所有的无效字符。</span><span class="sxs-lookup"><span data-stu-id="9bafd-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="9bafd-126">下面是有关标记`FilteredTextBoxExtender`仅允许数字的控件 (这也已经可能与`FilterType="Numbers"`):</span><span class="sxs-lookup"><span data-stu-id="9bafd-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

<span data-ttu-id="9bafd-127">运行页，然后重试如果启用 JavaScript，请输入一个字母，它不起作用;但是，页上会显示数字。</span><span class="sxs-lookup"><span data-stu-id="9bafd-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="9bafd-128">但是请注意，保护`FilteredTextBox`提供不是高防护： 启用如果 JavaScript，因此你必须使用其他验证方法，即 ASP 可能在文本框中，输入任何数据。NET 的验证控件。</span><span class="sxs-lookup"><span data-stu-id="9bafd-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>


<span data-ttu-id="9bafd-129">[![可能输入仅位数字](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9bafd-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span></span>

<span data-ttu-id="9bafd-130">可能输入仅数字 ([单击以查看实际尺寸的图像](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9bafd-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="9bafd-131">上一篇</span><span class="sxs-lookup"><span data-stu-id="9bafd-131">Previous</span></span>](allowing-only-certain-characters-in-a-text-box-cs.md)