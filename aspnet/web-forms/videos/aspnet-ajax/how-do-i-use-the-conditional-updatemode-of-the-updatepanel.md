---
uid: web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
title: '[如何实现:]使用 UpdatePanel 的条件 UpdateMode？ | Microsoft Docs'
author: JoeStagner
description: ASP.NET AJAX UpdatePanel 包含一个 UpdateMode 属性，可能会设置为始终或条件。 默认值是始终、 在此情况下 UpdatePan...
ms.author: riande
ms.date: 08/01/2007
ms.assetid: 10b5bad3-4c18-464f-9454-0b3e60b7b8be
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
msc.type: video
ms.openlocfilehash: 96d7bc95fd80e410feb332264695835e68793ae2
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824234"
---
<a name="how-do-i-use-the-conditional-updatemode-of-the-updatepanel"></a><span data-ttu-id="6eaac-105">[如何实现:]使用 UpdatePanel 的条件 UpdateMode？</span><span class="sxs-lookup"><span data-stu-id="6eaac-105">[How Do I:] Use the Conditional UpdateMode of the UpdatePanel?</span></span>
====================
<span data-ttu-id="6eaac-106">通过[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="6eaac-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="6eaac-107">ASP.NET AJAX UpdatePanel 包含一个 UpdateMode 属性，可能会设置为始终或条件。</span><span class="sxs-lookup"><span data-stu-id="6eaac-107">The ASP.NET AJAX UpdatePanel includes an UpdateMode property that may be set to 'Always' or 'Conditional'.</span></span> <span data-ttu-id="6eaac-108">默认值为往常一样，在这种情况下 UpdatePanel 将始终更新其内容异步回发期间。</span><span class="sxs-lookup"><span data-stu-id="6eaac-108">The default is Always, in which case the UpdatePanel will always update its content during an asychronous postback.</span></span> <span data-ttu-id="6eaac-109">在本视频中，我们了解到条件，在其中用例 UpdatePanel 只会更新其内容在我们的服务器端代码调用的 Update 方法时，我们就可以设置 UpdateMode。</span><span class="sxs-lookup"><span data-stu-id="6eaac-109">In this video we learn how we can set the UpdateMode to Conditional, in which case the UpdatePanel will only update its content when our server-side code calls its Update method.</span></span> <span data-ttu-id="6eaac-110">这可以使用 C# 或 Visual Basic 代码中的条件逻辑来确定当前的异步回发过程中，UpdatePanel 是否将更新其内容。</span><span class="sxs-lookup"><span data-stu-id="6eaac-110">This allows you to use conditional logic in your C# or Visual Basic code to determine whether the UpdatePanel will update its content during the current asynchronous postback.</span></span>

[<span data-ttu-id="6eaac-111">&#9654;观看视频 （13 分钟）</span><span class="sxs-lookup"><span data-stu-id="6eaac-111">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-conditional-updatemode-of-the-updatepanel)

> [!div class="step-by-step"]
> <span data-ttu-id="6eaac-112">[上一页](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
> [下一页](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span><span class="sxs-lookup"><span data-stu-id="6eaac-112">[Previous](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
[Next](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span></span>
