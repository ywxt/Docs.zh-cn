---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: 创建视图 (UI) |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 5052d7cca4a5c12a9ea56eb929d4794b19e82603
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878797"
---
<a name="create-the-view-ui"></a><span data-ttu-id="c19bb-102">创建视图 (UI)</span><span class="sxs-lookup"><span data-stu-id="c19bb-102">Create the View (UI)</span></span>
====================
<span data-ttu-id="c19bb-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c19bb-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c19bb-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="c19bb-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="c19bb-105">在本部分中，你将开始定义应用程序中的 HTML 和添加 HTML 和视图模型之间的数据绑定。</span><span class="sxs-lookup"><span data-stu-id="c19bb-105">In this section, you will start to define the HTML for the app, and add data binding between the HTML and the view model.</span></span>

<span data-ttu-id="c19bb-106">打开文件 Views/Home/Index.cshtml。</span><span class="sxs-lookup"><span data-stu-id="c19bb-106">Open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="c19bb-107">将该文件的全部内容替换为以下。</span><span class="sxs-lookup"><span data-stu-id="c19bb-107">Replace the entire contents of that file with the following.</span></span>

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

<span data-ttu-id="c19bb-108">大部分`div`元素还有适用于[Bootstrap](http://getbootstrap.com/)样式。</span><span class="sxs-lookup"><span data-stu-id="c19bb-108">Most of the `div` elements are there for [Bootstrap](http://getbootstrap.com/) styling.</span></span> <span data-ttu-id="c19bb-109">重要的元素是带有的`data-bind`属性。</span><span class="sxs-lookup"><span data-stu-id="c19bb-109">The important elements are the ones with `data-bind` attributes.</span></span> <span data-ttu-id="c19bb-110">此属性链接到视图模型的 HTML。</span><span class="sxs-lookup"><span data-stu-id="c19bb-110">This attribute links the HTML to the view model.</span></span>

<span data-ttu-id="c19bb-111">例如：</span><span class="sxs-lookup"><span data-stu-id="c19bb-111">For example:</span></span>

[!code-html[Main](part-7/samples/sample2.html)]

<span data-ttu-id="c19bb-112">在此示例中， &quot; `text` &quot;绑定原因`<p>`元素以显示的值`error`从视图模型的属性。</span><span class="sxs-lookup"><span data-stu-id="c19bb-112">In this example, the &quot;`text`&quot; binding causes the `<p>` element to show the value of the `error` property from the view model.</span></span> <span data-ttu-id="c19bb-113">回想一下，`error`被声明为`ko.observable`:</span><span class="sxs-lookup"><span data-stu-id="c19bb-113">Recall that `error` was declared as a `ko.observable`:</span></span>

[!code-javascript[Main](part-7/samples/sample3.js)]

<span data-ttu-id="c19bb-114">每当一个新值分配给`error`，Knockout 更新中的文本`<p>`元素。</span><span class="sxs-lookup"><span data-stu-id="c19bb-114">Whenever a new value is assigned to `error`, Knockout updates the text in the `<p>` element.</span></span>

<span data-ttu-id="c19bb-115">`foreach`绑定告知 Knockout 循环访问的内容`books`数组。</span><span class="sxs-lookup"><span data-stu-id="c19bb-115">The `foreach` binding tells Knockout to loop through the contents of the `books` array.</span></span> <span data-ttu-id="c19bb-116">对于数组中每个项，请 Knockout 创建一个新&lt;li&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="c19bb-116">For each item in the array, Knockout creates a new &lt;li&gt; element.</span></span> <span data-ttu-id="c19bb-117">绑定的上下文中的`foreach`引用数组项的属性。</span><span class="sxs-lookup"><span data-stu-id="c19bb-117">Bindings inside the context of the `foreach` refer to properties on the array item.</span></span> <span data-ttu-id="c19bb-118">例如：</span><span class="sxs-lookup"><span data-stu-id="c19bb-118">For example:</span></span>

[!code-html[Main](part-7/samples/sample4.html)]

<span data-ttu-id="c19bb-119">此处`text`绑定读取每本书的作者属性。</span><span class="sxs-lookup"><span data-stu-id="c19bb-119">Here the `text` binding reads the Author property of each book.</span></span>

<span data-ttu-id="c19bb-120">如果你运行应用程序现在，它应如下所示：</span><span class="sxs-lookup"><span data-stu-id="c19bb-120">If you run the application now, it should look like this:</span></span>

![](part-7/_static/image1.png)

<span data-ttu-id="c19bb-121">在页面加载之后，以异步方式加载的书籍列表。</span><span class="sxs-lookup"><span data-stu-id="c19bb-121">The list of books loads asynchronously, after the page loads.</span></span> <span data-ttu-id="c19bb-122">现在，&quot;详细信息&quot;链接不起作用。</span><span class="sxs-lookup"><span data-stu-id="c19bb-122">Right now, the &quot;Details&quot; links are not functional.</span></span> <span data-ttu-id="c19bb-123">我们将在下一部分中添加此功能。</span><span class="sxs-lookup"><span data-stu-id="c19bb-123">We'll add this functionality in the next section.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c19bb-124">[上一页](part-6.md)
> [下一页](part-8.md)</span><span class="sxs-lookup"><span data-stu-id="c19bb-124">[Previous](part-6.md)
[Next](part-8.md)</span></span>
