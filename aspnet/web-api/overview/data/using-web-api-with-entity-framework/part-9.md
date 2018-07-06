---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: 向数据库添加新项 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 36251ba907a6f580b63f0fded0591c26b6ff879e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818503"
---
<a name="add-a-new-item-to-the-database"></a><span data-ttu-id="cd3a1-102">向数据库添加新项</span><span class="sxs-lookup"><span data-stu-id="cd3a1-102">Add a New Item to the Database</span></span>
====================
<span data-ttu-id="cd3a1-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cd3a1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="cd3a1-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="cd3a1-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="cd3a1-105">在本部分中，将添加为用户创建新的通讯簿的功能。</span><span class="sxs-lookup"><span data-stu-id="cd3a1-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="cd3a1-106">在 app.js 中，将添加到视图模型的以下代码：</span><span class="sxs-lookup"><span data-stu-id="cd3a1-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="cd3a1-107">在 Index.cshtml，将为以下标记：</span><span class="sxs-lookup"><span data-stu-id="cd3a1-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="cd3a1-108">替换为：</span><span class="sxs-lookup"><span data-stu-id="cd3a1-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="cd3a1-109">此标记将创建用于提交新作者的窗体。</span><span class="sxs-lookup"><span data-stu-id="cd3a1-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="cd3a1-110">作者下拉列表的值是数据绑定到`authors`视图模型中可观察量。</span><span class="sxs-lookup"><span data-stu-id="cd3a1-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="cd3a1-111">对于其他窗体输入，值是数据绑定到`newBook`视图模型属性。</span><span class="sxs-lookup"><span data-stu-id="cd3a1-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="cd3a1-112">在窗体上的提交处理程序绑定到`addBook`函数：</span><span class="sxs-lookup"><span data-stu-id="cd3a1-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="cd3a1-113">`addBook`函数读取的数据绑定窗体输入创建一个 JSON 对象的当前值。</span><span class="sxs-lookup"><span data-stu-id="cd3a1-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="cd3a1-114">然后它将发布到的 JSON 对象`/api/books`。</span><span class="sxs-lookup"><span data-stu-id="cd3a1-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cd3a1-115">[上一页](part-8.md)
> [下一页](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="cd3a1-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
