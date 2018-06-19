---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 显示项的详细信息 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 94863e94f2a8b3f1ce8a8fb85d877bc0768f3d8a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868082"
---
<a name="display-item-details"></a><span data-ttu-id="f9305-102">显示项详细信息</span><span class="sxs-lookup"><span data-stu-id="f9305-102">Display Item Details</span></span>
====================
<span data-ttu-id="f9305-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f9305-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="f9305-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="f9305-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="f9305-105">在此部分中，你将添加的功能，若要查看的每本书的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f9305-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="f9305-106">在 app.js，添加到视图模型的以下代码：</span><span class="sxs-lookup"><span data-stu-id="f9305-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="f9305-107">在 Views/Home/Index.cshtml，将添加到详细信息链接的数据绑定元素：</span><span class="sxs-lookup"><span data-stu-id="f9305-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="f9305-108">这会将绑定的单击处理程序&lt;&gt;元素`getBookDetail`视图模型上的函数。</span><span class="sxs-lookup"><span data-stu-id="f9305-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="f9305-109">在同一文件中，将以下标记向上：</span><span class="sxs-lookup"><span data-stu-id="f9305-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="f9305-110">替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="f9305-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="f9305-111">此标记将创建一个表，其中被数据绑定到的属性`detail`可观察到视图模型中。</span><span class="sxs-lookup"><span data-stu-id="f9305-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="f9305-112">"&lt;！-Ko-&gt; &quot;语法，您可以包含在 DOM 元素之外的 Knockout 绑定。</span><span class="sxs-lookup"><span data-stu-id="f9305-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="f9305-113">在这种情况下，`if`绑定会导致要显示的标记的本部分仅当`details`为非 null。</span><span class="sxs-lookup"><span data-stu-id="f9305-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="f9305-114">现在，如果你运行应用并单击其中一个&quot;详细信息&quot;链接，该应用程序将显示簿详细信息。</span><span class="sxs-lookup"><span data-stu-id="f9305-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="f9305-115">[上一页](part-7.md)
> [下一页](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="f9305-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
