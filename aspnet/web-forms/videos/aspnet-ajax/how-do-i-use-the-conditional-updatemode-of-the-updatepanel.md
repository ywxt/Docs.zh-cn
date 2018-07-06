---
uid: web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
title: '[如何实现:]使用 UpdatePanel 的条件 UpdateMode？ | Microsoft Docs'
author: JoeStagner
description: ASP.NET AJAX UpdatePanel 包含一个 UpdateMode 属性，可能会设置为始终或条件。 默认值是始终、 在此情况下 UpdatePan...
ms.author: aspnetcontent
ms.date: 08/01/2007
ms.assetid: 10b5bad3-4c18-464f-9454-0b3e60b7b8be
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
msc.type: video
ms.openlocfilehash: 04b37874bcbdd580edc9182b54eecc9a6f77cb61
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826796"
---
<a name="how-do-i-use-the-conditional-updatemode-of-the-updatepanel"></a><span data-ttu-id="ba3fc-105">[如何实现:]使用 UpdatePanel 的条件 UpdateMode？</span><span class="sxs-lookup"><span data-stu-id="ba3fc-105">[How Do I:] Use the Conditional UpdateMode of the UpdatePanel?</span></span>
====================
<span data-ttu-id="ba3fc-106">通过[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="ba3fc-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="ba3fc-107">ASP.NET AJAX UpdatePanel 包含一个 UpdateMode 属性，可能会设置为始终或条件。</span><span class="sxs-lookup"><span data-stu-id="ba3fc-107">The ASP.NET AJAX UpdatePanel includes an UpdateMode property that may be set to 'Always' or 'Conditional'.</span></span> <span data-ttu-id="ba3fc-108">默认值为往常一样，在这种情况下 UpdatePanel 将始终更新其内容异步回发期间。</span><span class="sxs-lookup"><span data-stu-id="ba3fc-108">The default is Always, in which case the UpdatePanel will always update its content during an asychronous postback.</span></span> <span data-ttu-id="ba3fc-109">在本视频中，我们了解到条件，在其中用例 UpdatePanel 只会更新其内容在我们的服务器端代码调用的 Update 方法时，我们就可以设置 UpdateMode。</span><span class="sxs-lookup"><span data-stu-id="ba3fc-109">In this video we learn how we can set the UpdateMode to Conditional, in which case the UpdatePanel will only update its content when our server-side code calls its Update method.</span></span> <span data-ttu-id="ba3fc-110">这可以使用 C# 或 Visual Basic 代码中的条件逻辑来确定当前的异步回发过程中，UpdatePanel 是否将更新其内容。</span><span class="sxs-lookup"><span data-stu-id="ba3fc-110">This allows you to use conditional logic in your C# or Visual Basic code to determine whether the UpdatePanel will update its content during the current asynchronous postback.</span></span>

[<span data-ttu-id="ba3fc-111">&#9654;观看视频 （13 分钟）</span><span class="sxs-lookup"><span data-stu-id="ba3fc-111">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-conditional-updatemode-of-the-updatepanel)

> [!div class="step-by-step"]
> <span data-ttu-id="ba3fc-112">[上一页](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
> [下一页](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span><span class="sxs-lookup"><span data-stu-id="ba3fc-112">[Previous](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
[Next](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span></span>
