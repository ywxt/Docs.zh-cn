---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[如何操作]: 将用户控件的状态保存在回发期间 |Microsoft 文档'
author: rick-anderson
description: 在此视频 Chris Pels 演示如何以保留在用户控件中的一个或多个对象的状态。 首先，将创建一个用户控件表示 abilit...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/02/2009
ms.topic: article
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: 47d7d7a3f83586104ab2d2a3c288b4a51879ca06
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26525966"
---
<a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a>[如何操作]: 将用户控件的状态保存在回发期间
[How Do I]: Persist the State of a User Control During a Postback
====================
<span data-ttu-id="a695d-105">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="a695d-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="a695d-106">在此视频 Chris Pels 演示如何以保留在用户控件中的一个或多个对象的状态。</span><span class="sxs-lookup"><span data-stu-id="a695d-106">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="a695d-107">首先，用户控件将创建表示指定的搜索筛选器条件的用户的能力。</span><span class="sxs-lookup"><span data-stu-id="a695d-107">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="a695d-108">此外，一起提供筛选器类被创建用于存储的筛选器信息。</span><span class="sxs-lookup"><span data-stu-id="a695d-108">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="a695d-109">多个用户界面元素添加到筛选器控件以及某些方法和属性，以将当前的筛选器信息存储在筛选器类实例。</span><span class="sxs-lookup"><span data-stu-id="a695d-109">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="a695d-110">接下来，使用 RegisterRequiresControlState 方法和关联的保存/还原方法实现用户控件持久性。</span><span class="sxs-lookup"><span data-stu-id="a695d-110">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="a695d-111">这些方法在页回发期间存储的实例的筛选器类和其数据。</span><span class="sxs-lookup"><span data-stu-id="a695d-111">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="a695d-112">最后，是如何在控制状态实现中存储多个对象的讨论。</span><span class="sxs-lookup"><span data-stu-id="a695d-112">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="a695d-113">&#9654;观看视频 （23 分钟）</span><span class="sxs-lookup"><span data-stu-id="a695d-113">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)
