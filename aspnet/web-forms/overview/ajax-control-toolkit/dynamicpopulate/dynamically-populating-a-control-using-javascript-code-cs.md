---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
title: 动态填充控件使用 JavaScript 代码 (C#) |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页方法），并将生成的值填充到 t 上的目标控件...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: cc4c2def-e88c-4456-ae8b-a6ae0ff8cc2d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
msc.type: authoredcontent
ms.openlocfilehash: c9fd11ea0348eb7fe9a7634f7b26031339146828
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873178"
---
<a name="dynamically-populating-a-control-using-javascript-code-c"></a><span data-ttu-id="8c7d6-103">动态填充控件使用 JavaScript 代码 (C#)</span><span class="sxs-lookup"><span data-stu-id="8c7d6-103">Dynamically Populating a Control Using JavaScript Code (C#)</span></span>
====================
<span data-ttu-id="8c7d6-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8c7d6-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8c7d6-105">[下载代码](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8c7d6-105">[Download Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span></span>

> <span data-ttu-id="8c7d6-106">ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页方法），并将生成的值填充到目标控件在页上，而无需页面刷新。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="8c7d6-107">还有可能触发使用自定义客户端 JavaScript 代码的填充。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="8c7d6-108">概述</span><span class="sxs-lookup"><span data-stu-id="8c7d6-108">Overview</span></span>

<span data-ttu-id="8c7d6-109">`DynamicPopulate` ASP.NET AJAX 控件工具包中的控件调用 web 服务 （或页方法），并将生成的值填充到目标控件在页上，而无需页面刷新。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-109">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="8c7d6-110">还有可能触发使用自定义客户端 JavaScript 代码的填充。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-110">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="8c7d6-111">步骤</span><span class="sxs-lookup"><span data-stu-id="8c7d6-111">Steps</span></span>

<span data-ttu-id="8c7d6-112">首先，你需要 ASP.NET Web 服务实现调用的方法`DynamicPopulateExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-112">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="8c7d6-113">Web 服务实现的方法`getDate()`需要一个自变量的类型字符串，调用`contextKey`，因为`DynamicPopulate`控件将发送一条与每个 web 服务调用上下文信息。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-113">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="8c7d6-114">以下是代码 (文件`DynamicPopulate.cs.asmx`) 来检索当前日期在三种格式之一：</span><span class="sxs-lookup"><span data-stu-id="8c7d6-114">Here is the code (file `DynamicPopulate.cs.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample1.aspx)]

<span data-ttu-id="8c7d6-115">在下一步的步骤中，创建一个新的 ASP.NET 站点并启动与 ASP.NET AJAX ScriptManager 控件：</span><span class="sxs-lookup"><span data-stu-id="8c7d6-115">In the next step, create a new ASP.NET site and start with the ASP.NET AJAX ScriptManager control:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample2.aspx)]

<span data-ttu-id="8c7d6-116">然后，添加一个标签控件 (例如使用相同的名称，该 HTML 控件或`<asp:Label />`web 控件) 的更高版本将显示 web 服务调用的结果。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-116">Then, add a label control (for instance using the HTML control of the same name, or the `<asp:Label />` web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample3.aspx)]

<span data-ttu-id="8c7d6-117">接下来，包括`DynamicPopulateExtender`控制并提供 web 服务信息、 目标控件，但不是随即将会触发这将会更高版本，使用自定义 JavaScript 的填充控件的名称 ！</span><span class="sxs-lookup"><span data-stu-id="8c7d6-117">Next, include a `DynamicPopulateExtender` control and provide web service information, target control, but not the name of the control which triggers the population this will be done later on, using custom JavaScript!</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample4.aspx)]

<span data-ttu-id="8c7d6-118">现在我们来的 JavaScript 部分。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-118">Now to the JavaScript part.</span></span> <span data-ttu-id="8c7d6-119">`$find()`由 ASP.NET AJAX 库中，定义的函数返回的 ASP.NET AJAX 控件工具包的服务器端对象的引用如`DynamicPopulateExtender`。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-119">The `$find()` function, defined by the ASP.NET AJAX library, returns a reference to server-side objects of the ASP.NET AJAX Control Toolkit such as `DynamicPopulateExtender`.</span></span> <span data-ttu-id="8c7d6-120">在当前的文件中，`$find("dpe")`返回到一个引用`DynamicPopulateExtender`页中的控件。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-120">In the current file, `$find("dpe")` returns a reference to the one `DynamicPopulateExtender` control in the page.</span></span> <span data-ttu-id="8c7d6-121">它公开一个方法，该方法调用`populate()`随即将会触发动态填充过程。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-121">It exposes a method called `populate()` which triggers the dynamic population process.</span></span> <span data-ttu-id="8c7d6-122">`populate()`方法需要一个参数： 作为自变量的上下文项`getDate()`web 方法。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-122">The `populate()` method requires one argument: the context key which will serve as argument to the `getDate()` web method.</span></span> <span data-ttu-id="8c7d6-123">例如，`$find("dpe").populate("format1")`将填充月-日-年格式的当前日期的标签。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-123">So for instance, `$find("dpe").populate("format1")` would populate the label with the current date in month-day-year format.</span></span>

<span data-ttu-id="8c7d6-124">为了使示例更具灵活性，用户现在可能有多种日期格式之间进行选择。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-124">In order to make the sample a bit more flexible, the user may now choose between several date formats.</span></span> <span data-ttu-id="8c7d6-125">其中的每个，将显示一个单选按钮。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-125">For each one of them, a radio button is displayed.</span></span> <span data-ttu-id="8c7d6-126">一次用户单击一个单选按钮上的，JavaScript 代码动态填充具有所选的日期格式标签。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-126">Once the user clicks on a radio button, JavaScript code dynamically populates the label with the selected date format.</span></span> <span data-ttu-id="8c7d6-127">下面是这些单选按钮：</span><span class="sxs-lookup"><span data-stu-id="8c7d6-127">Here are those radio buttons:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample5.aspx)]

<span data-ttu-id="8c7d6-128">注意，在单选按钮，JavaScript 表达式的上下文中`this.value`当前按钮，这种情况是完全相同的信息的值是指`getDate()`方法可以使用。</span><span class="sxs-lookup"><span data-stu-id="8c7d6-128">Note that within the context of a radio button, the JavaScript expression `this.value` refers to the value of the current button, which happens to be exactly the same information the `getDate()` method can work with.</span></span>


<span data-ttu-id="8c7d6-129">[![单击此按钮会检索在服务器上，指定的格式的日期](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8c7d6-129">[![A click on the button retrieves the date from the server, in the format specified](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="8c7d6-130">单击按钮从服务器上，在指定的格式中检索日期 ([单击以查看实际尺寸的图像](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8c7d6-130">A click on the button retrieves the date from the server, in the format specified ([Click to view full-size image](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8c7d6-131">[上一页](dynamically-populating-a-control-cs.md)
> [下一页](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8c7d6-131">[Previous](dynamically-populating-a-control-cs.md)
[Next](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span></span>
