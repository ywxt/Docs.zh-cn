---
uid: web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
title: '[如何实现:]将 ASP.NET 服务器控件映射到用于呈现该适配器 |Microsoft Docs'
author: rick-anderson
description: 在此视频的 Chris Pels 将显示如何使用控件适配器为 ASP.NET 服务器控件提供不同呈现，而无需实际更改 c...
ms.author: aspnetcontent
ms.date: 06/19/2008
ms.assetid: d4b498ef-8e1c-4fa2-9c35-1f32f20bb9b7
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
msc.type: video
ms.openlocfilehash: 951f494a82566ad35db464aedcab8bf2ab28b5fd
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831208"
---
<a name="how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it"></a><span data-ttu-id="6245a-103">[如何实现:]映射到用于呈现该适配器的 ASP.NET 服务器控件</span><span class="sxs-lookup"><span data-stu-id="6245a-103">[How Do I:] Map an ASP.NET Server Control to the Adaptor Used to Render It</span></span>
====================
<span data-ttu-id="6245a-104">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="6245a-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="6245a-105">在此视频的 Chris Pels 将演示如何使用控件适配器不实际更改控件本身的 ASP.NET 服务器控件提供不同的呈现。</span><span class="sxs-lookup"><span data-stu-id="6245a-105">In this video Chris Pels will show how to use a control adaptor to provide different renderings for an ASP.NET server control without actually changing the control itself.</span></span> <span data-ttu-id="6245a-106">在此视频中，ASP.NET BulletList 控件将进行适配以便显示每个列表项使用而不传统的 UL 元素水平 DIV 元素。</span><span class="sxs-lookup"><span data-stu-id="6245a-106">In this video, an ASP.NET BulletList control will be adapted to display each list item horizontally using DIV elements instead of the traditional UL elements.</span></span> <span data-ttu-id="6245a-107">首先，请参阅如何创建一个类继承 WebControlAdaptor，然后实现要呈现的新列表格式的代码。</span><span class="sxs-lookup"><span data-stu-id="6245a-107">First, see how to create a class that inherits WebControlAdaptor and then implements the code to render the new list format.</span></span> <span data-ttu-id="6245a-108">接下来，了解如何将新的控件适配器映射到.browser 定义文件中的 ASP.NET 服务器控件。</span><span class="sxs-lookup"><span data-stu-id="6245a-108">Next, learn how to map the new control adaptor to the ASP.NET server control in the .browser definition file.</span></span> <span data-ttu-id="6245a-109">然后了解如何在 web 站点中的页面上使用新的控件适配器。</span><span class="sxs-lookup"><span data-stu-id="6245a-109">Then see how to use the new control adaptor on pages in a web site.</span></span> <span data-ttu-id="6245a-110">最后，了解如何控制适配器可与所有浏览器或特定类型的浏览器相关联。</span><span class="sxs-lookup"><span data-stu-id="6245a-110">Finally, learn how a control adaptor can be associated with either all browsers or specific types of browsers.</span></span>

[<span data-ttu-id="6245a-111">&#9654;观看视频 （23 分钟）</span><span class="sxs-lookup"><span data-stu-id="6245a-111">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it)
