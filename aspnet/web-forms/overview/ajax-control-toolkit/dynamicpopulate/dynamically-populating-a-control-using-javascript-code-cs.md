---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
title: 动态填充控件使用 JavaScript 代码 (C#) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页面方法），并将生成的值填充到 t 上的目标控件...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: cc4c2def-e88c-4456-ae8b-a6ae0ff8cc2d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 6fa8e0b91481467c7f53e7323b72e4b345833905
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37841615"
---
<a name="dynamically-populating-a-control-using-javascript-code-c"></a><span data-ttu-id="191ba-103">动态填充控件使用 JavaScript 代码 (C#)</span><span class="sxs-lookup"><span data-stu-id="191ba-103">Dynamically Populating a Control Using JavaScript Code (C#)</span></span>
====================
<span data-ttu-id="191ba-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="191ba-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="191ba-105">[下载代码](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="191ba-105">[Download Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span></span>

> <span data-ttu-id="191ba-106">ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页面方法），并将生成的值填充到目标控件在页上，而无需刷新页面。</span><span class="sxs-lookup"><span data-stu-id="191ba-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="191ba-107">还有可能触发使用自定义客户端的 JavaScript 代码的填充。</span><span class="sxs-lookup"><span data-stu-id="191ba-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="191ba-108">概述</span><span class="sxs-lookup"><span data-stu-id="191ba-108">Overview</span></span>

<span data-ttu-id="191ba-109">`DynamicPopulate` ASP.NET AJAX 控件工具包中的控件调用 web 服务 （或页面方法），并将生成的值填充到目标控件在页上，而无需刷新页面。</span><span class="sxs-lookup"><span data-stu-id="191ba-109">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="191ba-110">还有可能触发使用自定义客户端的 JavaScript 代码的填充。</span><span class="sxs-lookup"><span data-stu-id="191ba-110">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="191ba-111">步骤</span><span class="sxs-lookup"><span data-stu-id="191ba-111">Steps</span></span>

<span data-ttu-id="191ba-112">首先，需要 ASP.NET Web 服务实现的方法调用的`DynamicPopulateExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="191ba-112">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="191ba-113">Web 服务实现方法`getDate()`需要一个自变量的类型字符串，调用`contextKey`，因为`DynamicPopulate`控件将发送一条与每个 web 服务调用上下文信息。</span><span class="sxs-lookup"><span data-stu-id="191ba-113">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="191ba-114">下面是代码 (文件`DynamicPopulate.cs.asmx`) 中检索当前日期中三种格式之一：</span><span class="sxs-lookup"><span data-stu-id="191ba-114">Here is the code (file `DynamicPopulate.cs.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample1.aspx)]

<span data-ttu-id="191ba-115">在下一步中，创建一个新的 ASP.NET 站点并开始使用 ASP.NET AJAX ScriptManager 控件：</span><span class="sxs-lookup"><span data-stu-id="191ba-115">In the next step, create a new ASP.NET site and start with the ASP.NET AJAX ScriptManager control:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample2.aspx)]

<span data-ttu-id="191ba-116">然后，添加一个 label 控件 (例如使用具有相同名称的 HTML 控件或`<asp:Label />`web 控件) 的更高版本将显示 web 服务调用的结果。</span><span class="sxs-lookup"><span data-stu-id="191ba-116">Then, add a label control (for instance using the HTML control of the same name, or the `<asp:Label />` web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample3.aspx)]

<span data-ttu-id="191ba-117">接下来，包括`DynamicPopulateExtender`控制并提供 web 服务信息、 目标控件，但不是这会触发这会在更高版本使用自定义 JavaScript 填充该控件的名称 ！</span><span class="sxs-lookup"><span data-stu-id="191ba-117">Next, include a `DynamicPopulateExtender` control and provide web service information, target control, but not the name of the control which triggers the population this will be done later on, using custom JavaScript!</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample4.aspx)]

<span data-ttu-id="191ba-118">现在我们来的 JavaScript 部分。</span><span class="sxs-lookup"><span data-stu-id="191ba-118">Now to the JavaScript part.</span></span> <span data-ttu-id="191ba-119">`$find()`由 ASP.NET AJAX 库定义的函数返回对 ASP.NET AJAX 控件工具包的服务器端对象的引用如`DynamicPopulateExtender`。</span><span class="sxs-lookup"><span data-stu-id="191ba-119">The `$find()` function, defined by the ASP.NET AJAX library, returns a reference to server-side objects of the ASP.NET AJAX Control Toolkit such as `DynamicPopulateExtender`.</span></span> <span data-ttu-id="191ba-120">在当前文件中，`$find("dpe")`返回到一个引用`DynamicPopulateExtender`页中的控件。</span><span class="sxs-lookup"><span data-stu-id="191ba-120">In the current file, `$find("dpe")` returns a reference to the one `DynamicPopulateExtender` control in the page.</span></span> <span data-ttu-id="191ba-121">它公开一个名为方法`populate()`随即将会触发动态填充过程。</span><span class="sxs-lookup"><span data-stu-id="191ba-121">It exposes a method called `populate()` which triggers the dynamic population process.</span></span> <span data-ttu-id="191ba-122">`populate()`方法需要一个参数： 参数作为上下文键`getDate()`web 方法。</span><span class="sxs-lookup"><span data-stu-id="191ba-122">The `populate()` method requires one argument: the context key which will serve as argument to the `getDate()` web method.</span></span> <span data-ttu-id="191ba-123">因此，例如，`$find("dpe").populate("format1")`将填充与月-日-年格式的当前日期的标签。</span><span class="sxs-lookup"><span data-stu-id="191ba-123">So for instance, `$find("dpe").populate("format1")` would populate the label with the current date in month-day-year format.</span></span>

<span data-ttu-id="191ba-124">为了让此示例更具灵活性，用户可能现在多个日期格式之间进行选择。</span><span class="sxs-lookup"><span data-stu-id="191ba-124">In order to make the sample a bit more flexible, the user may now choose between several date formats.</span></span> <span data-ttu-id="191ba-125">对于其中每项显示的单选按钮。</span><span class="sxs-lookup"><span data-stu-id="191ba-125">For each one of them, a radio button is displayed.</span></span> <span data-ttu-id="191ba-126">一次用户单击单选按钮，JavaScript 代码动态填充与所选的日期格式的标签。</span><span class="sxs-lookup"><span data-stu-id="191ba-126">Once the user clicks on a radio button, JavaScript code dynamically populates the label with the selected date format.</span></span> <span data-ttu-id="191ba-127">下面是这些单选按钮：</span><span class="sxs-lookup"><span data-stu-id="191ba-127">Here are those radio buttons:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample5.aspx)]

<span data-ttu-id="191ba-128">请注意，单选按钮，JavaScript 表达式的上下文中`this.value`当前按钮，它恰巧是完全相同的信息的值是指`getDate()`方法可以使用。</span><span class="sxs-lookup"><span data-stu-id="191ba-128">Note that within the context of a radio button, the JavaScript expression `this.value` refers to the value of the current button, which happens to be exactly the same information the `getDate()` method can work with.</span></span>


<span data-ttu-id="191ba-129">[![单击的按钮中指定的格式的服务器中检索日期](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="191ba-129">[![A click on the button retrieves the date from the server, in the format specified](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="191ba-130">单击的按钮中指定的格式的服务器中检索日期 ([单击此项可查看原尺寸图像](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="191ba-130">A click on the button retrieves the date from the server, in the format specified ([Click to view full-size image](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="191ba-131">[上一页](dynamically-populating-a-control-cs.md)
> [下一页](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span><span class="sxs-lookup"><span data-stu-id="191ba-131">[Previous](dynamically-populating-a-control-cs.md)
[Next](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span></span>
