---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: 启动模式弹出窗口通过服务器代码 (C#) |Microsoft Docs
author: wenz
description: 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 但是，某些情况下需要该 t...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: b7b486c4b99e5ddcb9bc244a9c5dcf193d33b696
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815299"
---
<a name="launching-a-modal-popup-window-from-server-code-c"></a><span data-ttu-id="6b9d3-104">启动模式弹出窗口通过服务器代码 (C#)</span><span class="sxs-lookup"><span data-stu-id="6b9d3-104">Launching a Modal Popup Window from Server Code (C#)</span></span>
====================
<span data-ttu-id="6b9d3-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6b9d3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6b9d3-106">[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6b9d3-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span></span>

> <span data-ttu-id="6b9d3-107">在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="6b9d3-108">但是某些情况下需要打开模式弹出框在服务器端上触发。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>


## <a name="overview"></a><span data-ttu-id="6b9d3-109">概述</span><span class="sxs-lookup"><span data-stu-id="6b9d3-109">Overview</span></span>

<span data-ttu-id="6b9d3-110">在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="6b9d3-111">但是某些情况下需要打开模式弹出框在服务器端上触发。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="6b9d3-112">步骤</span><span class="sxs-lookup"><span data-stu-id="6b9d3-112">Steps</span></span>

<span data-ttu-id="6b9d3-113">首先，需要一个 ASP.NET 按钮 web 控件来演示 ModalPopup 控件的工作原理。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="6b9d3-114">添加此类中的某个按钮&lt;窗体&gt;新页上的元素：</span><span class="sxs-lookup"><span data-stu-id="6b9d3-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

<span data-ttu-id="6b9d3-115">然后，您需要标记为你想要创建的弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="6b9d3-116">其定义为`<asp:Panel>`控制并确保它包含一个按钮控件。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="6b9d3-117">ModalPopup 控件可提供的功能，若要使此类按钮关闭弹出框;否则将无法轻松地使其消失。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

<span data-ttu-id="6b9d3-118">接下来向页面添加从 ASP.NET AJAX 工具包的 ModalPopup 控件。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="6b9d3-119">设置加载控件的按钮，这样就会消失，按钮和实际弹出项的 ID 属性。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

<span data-ttu-id="6b9d3-120">与使用基于 ASP.NET AJAX; 的所有网页加载所需的 JavaScript 库获取不同的目标的浏览器所需脚本管理器：</span><span class="sxs-lookup"><span data-stu-id="6b9d3-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

<span data-ttu-id="6b9d3-121">在浏览器中运行示例。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-121">Run the example in the browser.</span></span> <span data-ttu-id="6b9d3-122">当单击按钮时，将显示模式弹出框。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="6b9d3-123">若要实现使用服务器端代码相同的效果，一个新按钮，则需要：</span><span class="sxs-lookup"><span data-stu-id="6b9d3-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

<span data-ttu-id="6b9d3-124">正如您所看到的按钮单击生成的回发，并执行`ServerButton_Click()`在服务器上的方法。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="6b9d3-125">此方法中调用 JavaScript 函数`launchModal()`执行确切地，JavaScript 函数将执行加载页面后：</span><span class="sxs-lookup"><span data-stu-id="6b9d3-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

<span data-ttu-id="6b9d3-126">作业的`launchModal()`是显示 ModalPopup。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="6b9d3-127">`launchModal()`加载完整的 HTML 页后执行函数。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="6b9d3-128">在该时间点，但是，ASP.NET AJAX 框架尚未完全加载。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="6b9d3-129">因此，`launchModal()`函数只设置 ModalPopup 控件必须更高版本显示的变量：</span><span class="sxs-lookup"><span data-stu-id="6b9d3-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

<span data-ttu-id="6b9d3-130">`pageLoad()` JavaScript 函数是 ASP.NET AJAX 完全加载后执行的特殊函数。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="6b9d3-131">因此我们将代码添加到此函数可显示 ModalPopup 控件，但是只有当`launchModal()`已调用之前：</span><span class="sxs-lookup"><span data-stu-id="6b9d3-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

<span data-ttu-id="6b9d3-132">`$find()`函数查找的页面上命名元素，并需要服务器端的 ID 作为参数。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="6b9d3-133">因此，`$find("mpe")`返回的客户端表示形式 ModalPopup 控件; 它`show()`方法，可以显示的弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="6b9d3-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>


<span data-ttu-id="6b9d3-134">[![模式弹出框时出现的任一按钮单击](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6b9d3-134">[![The modal popup appears when either of the buttons is clicked](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="6b9d3-135">模式弹出框时出现的任一按钮单击 ([单击此项可查看原尺寸图像](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6b9d3-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6b9d3-136">下一篇</span><span class="sxs-lookup"><span data-stu-id="6b9d3-136">Next</span></span>](using-modalpopup-with-a-repeater-control-cs.md)
