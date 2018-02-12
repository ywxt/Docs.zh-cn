---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: "用户控件和 JavaScript (VB) 中使用 DynamicPopulate |Microsoft 文档"
author: wenz
description: "ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页方法），并将生成的值填充到 t 上的目标控件..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: 495a3917ca5fa28bc833ccc666b1a5e6db7bf7f2
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
---
<a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a><span data-ttu-id="00eb1-103">用户控件和 JavaScript (VB) 中使用 DynamicPopulate</span><span class="sxs-lookup"><span data-stu-id="00eb1-103">Using DynamicPopulate with a User Control And JavaScript (VB)</span></span>
====================
<span data-ttu-id="00eb1-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="00eb1-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="00eb1-105">[下载代码](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="00eb1-105">[Download Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span></span>

> <span data-ttu-id="00eb1-106">ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页方法），并将生成的值填充到目标控件在页上，而无需页面刷新。</span><span class="sxs-lookup"><span data-stu-id="00eb1-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="00eb1-107">还有可能触发使用自定义客户端 JavaScript 代码的填充。</span><span class="sxs-lookup"><span data-stu-id="00eb1-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="00eb1-108">但是必须格外小心扩展程序驻留在用户控件中时要执行。</span><span class="sxs-lookup"><span data-stu-id="00eb1-108">However special care has to be taken when the extender resides in a user control.</span></span>


## <a name="overview"></a><span data-ttu-id="00eb1-109">概述</span><span class="sxs-lookup"><span data-stu-id="00eb1-109">Overview</span></span>

<span data-ttu-id="00eb1-110">`DynamicPopulate` ASP.NET AJAX 控件工具包中的控件调用 web 服务 （或页方法），并将生成的值填充到目标控件在页上，而无需页面刷新。</span><span class="sxs-lookup"><span data-stu-id="00eb1-110">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="00eb1-111">还有可能触发使用自定义客户端 JavaScript 代码的填充。</span><span class="sxs-lookup"><span data-stu-id="00eb1-111">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="00eb1-112">但是必须格外小心扩展程序驻留在用户控件中时要执行。</span><span class="sxs-lookup"><span data-stu-id="00eb1-112">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="steps"></a><span data-ttu-id="00eb1-113">步骤</span><span class="sxs-lookup"><span data-stu-id="00eb1-113">Steps</span></span>

<span data-ttu-id="00eb1-114">首先，你需要 ASP.NET Web 服务实现调用的方法`DynamicPopulateExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="00eb1-114">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="00eb1-115">Web 服务实现的方法`getDate()`需要一个自变量的类型字符串，调用`contextKey`，因为`DynamicPopulate`控件将发送一条与每个 web 服务调用上下文信息。</span><span class="sxs-lookup"><span data-stu-id="00eb1-115">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="00eb1-116">以下是代码 (文件`DynamicPopulate.vb.asmx`) 来检索当前日期在三种格式之一：</span><span class="sxs-lookup"><span data-stu-id="00eb1-116">Here is the code (files `DynamicPopulate.vb.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="00eb1-117">在下一步的步骤中，创建一个新的用户控件 (`.ascx`文件)，表示由其第一行中的以下声明：</span><span class="sxs-lookup"><span data-stu-id="00eb1-117">In the next step, create a new user control (`.ascx` file), denoted by the following declaration in its first line:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="00eb1-118">A &lt; `label` &gt;元素将用于显示来自服务器的数据。</span><span class="sxs-lookup"><span data-stu-id="00eb1-118">A &lt;`label`&gt; element will be used to display the data coming from the server.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

<span data-ttu-id="00eb1-119">此外在用户控件文件中，我们将使用三个单选按钮，表示 web 服务支持的三个可能的日期格式之一的每个组。</span><span class="sxs-lookup"><span data-stu-id="00eb1-119">Also in the user control file, we will use three radio buttons, each one representing one of the three possible date formats supported by the web service.</span></span> <span data-ttu-id="00eb1-120">当用户单击一个单选按钮时，浏览器将执行 JavaScript 代码将类似如下所示：</span><span class="sxs-lookup"><span data-stu-id="00eb1-120">When the user clicks on one of the radio buttons, the browser will execute JavaScript code which looks like this:</span></span>

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

<span data-ttu-id="00eb1-121">此代码可访问`DynamicPopulateExtender`（不要担心奇怪 ID，但这将稍后介绍），并触发动态填充的数据。</span><span class="sxs-lookup"><span data-stu-id="00eb1-121">This code accesses the `DynamicPopulateExtender` (do not worry about the strange ID yet, this will be covered later on) and triggers the dynamic population with data.</span></span> <span data-ttu-id="00eb1-122">当前的单选按钮的上下文中`this.value`指其值即`format1`，`format2`或`format3`完全什么 web 方法的要求。</span><span class="sxs-lookup"><span data-stu-id="00eb1-122">In the context of the current radio button, `this.value` refers to its value which is `format1`, `format2` or `format3` exactly what the web method expects.</span></span>

<span data-ttu-id="00eb1-123">尚未缺少在用户控件中的唯一操作是`DynamicPopulateExtender`链接到 web 服务的单选按钮控件。</span><span class="sxs-lookup"><span data-stu-id="00eb1-123">The only thing missing in the user control yet is the `DynamicPopulateExtender` control which links the radio buttons to the web service.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="00eb1-124">再次你可能注意到控件中使用的奇怪 ID:`mcd1$myDate`而不是`myDate`。</span><span class="sxs-lookup"><span data-stu-id="00eb1-124">Again you may note the strange ID used in the control: `mcd1$myDate` instead of `myDate`.</span></span> <span data-ttu-id="00eb1-125">以前，使用的 JavaScript 代码`mcd1_dpe1`访问`DynamicPopulateExtender`而不是`dpe1`。此命名策略是特殊的要求，使用时`DynamicPopulateExtender`用户控件内。</span><span class="sxs-lookup"><span data-stu-id="00eb1-125">Previously, the JavaScript code used `mcd1_dpe1` to access the `DynamicPopulateExtender` instead of `dpe1`.This naming strategy is a special requirement when using `DynamicPopulateExtender` within a user control.</span></span> <span data-ttu-id="00eb1-126">而且，你必须将用户控件中以特定的方式，以使其所有工作。</span><span class="sxs-lookup"><span data-stu-id="00eb1-126">Furthermore, you have to embed the user contol in a specific way to make it all work.</span></span> <span data-ttu-id="00eb1-127">创建新的 ASP.NET 页并注册刚刚实现用户控件的标记前缀：</span><span class="sxs-lookup"><span data-stu-id="00eb1-127">Create a new ASP.NET page and register a tag prefix for the user control you have just implemented:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

<span data-ttu-id="00eb1-128">然后，包括 ASP.NET AJAX`ScriptManager`在新页上的控件：</span><span class="sxs-lookup"><span data-stu-id="00eb1-128">Then, include the ASP.NET AJAX `ScriptManager` control on the new page:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

<span data-ttu-id="00eb1-129">最后，将用户控件添加到页面中。</span><span class="sxs-lookup"><span data-stu-id="00eb1-129">Finally, add the user control to the page.</span></span> <span data-ttu-id="00eb1-130">你只需设置其`ID`属性 (和`runat="server"`，这是当然的)，但你还必须将其设置为特定的名称：`mcd1`由于这是在用户控件中使用 JavaScript 访问它，使用的前缀。</span><span class="sxs-lookup"><span data-stu-id="00eb1-130">You only have to set its `ID` attribute (and `runat="server"`, of course), but you also have to set it to a specific name: `mcd1` since this is the prefix used within the user control to access it using JavaScript.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

<span data-ttu-id="00eb1-131">就是这么简单！</span><span class="sxs-lookup"><span data-stu-id="00eb1-131">And that's it!</span></span> <span data-ttu-id="00eb1-132">页行为与预期相同： 用户单击一个单选按钮，该工具包中的控件调用 web 服务并以所需的格式显示当前日期。</span><span class="sxs-lookup"><span data-stu-id="00eb1-132">The page behaves as expected: A user clicks on one of the radio buttons, the control in the Toolkit calls the web service and displays the current date in the desired format.</span></span>


<span data-ttu-id="00eb1-133">[![用户控件中驻留的单选按钮](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="00eb1-133">[![The radio buttons reside in a user control](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="00eb1-134">用户控件中驻留的单选按钮 ([单击以查看实际尺寸的图像](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="00eb1-134">The radio buttons reside in a user control ([Click to view full-size image](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="00eb1-135">上一篇</span><span class="sxs-lookup"><span data-stu-id="00eb1-135">Previous</span></span>](dynamically-populating-a-control-using-javascript-code-vb.md)
