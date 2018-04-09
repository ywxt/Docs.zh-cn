---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: 启动从服务器代码 (C#) 模式弹出窗口 |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 ModalPopup 控制提供一种简单的方法，以创建模式的弹出项，使用客户端的方式。 但是，某些情况下需要该 t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 04bb056ee29065a472a70d480568b897a789ae59
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="launching-a-modal-popup-window-from-server-code-c"></a><span data-ttu-id="0b3e8-104">启动从服务器代码 (C#) 模式弹出窗口</span><span class="sxs-lookup"><span data-stu-id="0b3e8-104">Launching a Modal Popup Window from Server Code (C#)</span></span>
====================
<span data-ttu-id="0b3e8-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0b3e8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0b3e8-106">[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="0b3e8-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span></span>

> <span data-ttu-id="0b3e8-107">AJAX 控件工具包中的 ModalPopup 控制提供一种简单的方法，以创建模式的弹出项，使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="0b3e8-108">但是一些方案要求在服务器端时触发的模式的弹出窗口打开。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>


## <a name="overview"></a><span data-ttu-id="0b3e8-109">概述</span><span class="sxs-lookup"><span data-stu-id="0b3e8-109">Overview</span></span>

<span data-ttu-id="0b3e8-110">AJAX 控件工具包中的 ModalPopup 控制提供一种简单的方法，以创建模式的弹出项，使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="0b3e8-111">但是一些方案要求在服务器端时触发的模式的弹出窗口打开。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="0b3e8-112">步骤</span><span class="sxs-lookup"><span data-stu-id="0b3e8-112">Steps</span></span>

<span data-ttu-id="0b3e8-113">首先，ASP.NET 按钮 web 控件需要演示 ModalPopup 控制工作原理。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="0b3e8-114">添加此类中的某个按钮&lt;窗体&gt;在新页上的元素：</span><span class="sxs-lookup"><span data-stu-id="0b3e8-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

<span data-ttu-id="0b3e8-115">然后，你需要针对你想要创建弹出项标记。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="0b3e8-116">它定义为`<asp:Panel>`控制并确保它包括一个按钮控件。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="0b3e8-117">ModalPopup 控件提供功能，以便让此类按钮关闭弹出窗口;否则，没有让它消失的轻松方法。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

<span data-ttu-id="0b3e8-118">接下来向页面添加 ASP.NET AJAX 工具包中的 ModalPopup 控件。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="0b3e8-119">设置了加载控件的按钮，这样就会消失，按钮和实际的弹出项的 ID 属性。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

<span data-ttu-id="0b3e8-120">与基于 ASP.NET AJAX; 的所有 web 页脚本管理器需要加载另一个目标浏览器的必要 JavaScript 库：</span><span class="sxs-lookup"><span data-stu-id="0b3e8-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

<span data-ttu-id="0b3e8-121">在浏览器中运行示例。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-121">Run the example in the browser.</span></span> <span data-ttu-id="0b3e8-122">当你单击按钮时，将显示模式的弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="0b3e8-123">若要实现使用服务器端代码相同的效果，新按钮是必需的：</span><span class="sxs-lookup"><span data-stu-id="0b3e8-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

<span data-ttu-id="0b3e8-124">如你所见，单击按钮生成回发，并执行`ServerButton_Click()`服务器上的方法。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="0b3e8-125">在此方法，调用 JavaScript 函数`launchModal()`执行要准确，JavaScript 函数将执行加载页面后：</span><span class="sxs-lookup"><span data-stu-id="0b3e8-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

<span data-ttu-id="0b3e8-126">作业`launchModal()`是显示 ModalPopup。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="0b3e8-127">`launchModal()`加载完整的 HTML 页后，将执行函数。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="0b3e8-128">在该时刻，但是，ASP.NET AJAX 框架尚未完全加载。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="0b3e8-129">因此，`launchModal()`函数只会将设置 ModalPopup 控件都必须更高版本显示的变量：</span><span class="sxs-lookup"><span data-stu-id="0b3e8-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

<span data-ttu-id="0b3e8-130">`pageLoad()` JavaScript 函数是 ASP.NET AJAX 已完全加载后执行的特殊函数。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="0b3e8-131">因此我们将代码添加到此函数可显示 ModalPopup 控件，但仅当`launchModal()`之前已调用：</span><span class="sxs-lookup"><span data-stu-id="0b3e8-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

<span data-ttu-id="0b3e8-132">`$find()`函数正在寻找的页上的已命名元素，并需要服务器端 ID 作为参数。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="0b3e8-133">因此，`$find("mpe")`返回的客户端表示形式 ModalPopup 控件; 其`show()`方法允许显示弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="0b3e8-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>


<span data-ttu-id="0b3e8-134">[![模式的弹出窗口出现时的任一按钮单击](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0b3e8-134">[![The modal popup appears when either of the buttons is clicked](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="0b3e8-135">模式的弹出窗口出现时的任一按钮单击 ([单击以查看实际尺寸的图像](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0b3e8-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0b3e8-136">下一篇</span><span class="sxs-lookup"><span data-stu-id="0b3e8-136">Next</span></span>](using-modalpopup-with-a-repeater-control-cs.md)
