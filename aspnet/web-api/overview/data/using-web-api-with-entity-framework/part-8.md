---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 显示项的详细信息 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 83f291326307a4964afdd5e8b50f2c375348ed0e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830047"
---
<a name="display-item-details"></a><span data-ttu-id="4c131-102">显示项详细信息</span><span class="sxs-lookup"><span data-stu-id="4c131-102">Display Item Details</span></span>
====================
<span data-ttu-id="4c131-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4c131-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="4c131-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="4c131-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="4c131-105">在本部分中，将添加能够查看每个工作簿的详细信息。</span><span class="sxs-lookup"><span data-stu-id="4c131-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="4c131-106">在 app.js 中，将添加到视图模型的以下代码：</span><span class="sxs-lookup"><span data-stu-id="4c131-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="4c131-107">在 Views/Home/Index.cshtml，数据绑定元素添加到详细信息链接：</span><span class="sxs-lookup"><span data-stu-id="4c131-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="4c131-108">这会将绑定的单击处理程序&lt;&gt;元素`getBookDetail`视图模型上的函数。</span><span class="sxs-lookup"><span data-stu-id="4c131-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="4c131-109">在同一文件中，将为以下标记上：</span><span class="sxs-lookup"><span data-stu-id="4c131-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="4c131-110">替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="4c131-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="4c131-111">此标记将创建一个表，其中是数据绑定到的属性`detail`视图模型中可观察量。</span><span class="sxs-lookup"><span data-stu-id="4c131-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="4c131-112">"&lt;！-Ko-&gt; &quot;语法允许您包括 Knockout 绑定之外的 DOM 元素。</span><span class="sxs-lookup"><span data-stu-id="4c131-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="4c131-113">在这种情况下，`if`绑定会导致标记要显示的此部分时，才`details`为非 null。</span><span class="sxs-lookup"><span data-stu-id="4c131-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="4c131-114">现在，如果运行应用并单击其中一个&quot;详细信息&quot;的链接，该应用将显示书籍详细信息。</span><span class="sxs-lookup"><span data-stu-id="4c131-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="4c131-115">[上一页](part-7.md)
> [下一页](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="4c131-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
