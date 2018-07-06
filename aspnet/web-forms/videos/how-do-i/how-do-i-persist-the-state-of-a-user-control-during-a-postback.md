---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[How Do I]: Persist the State of a User Control During a Postback | Microsoft Docs'
author: rick-anderson
description: 在此视频的 Chris Pels 中显示了如何持久保存在用户控件中的一个或多个对象的状态。 首先，将创建一个用户控件表示 abilit...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/02/2009
ms.topic: article
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: fde95af4f639d778a108a0267fb738ac2e0a2d46
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372606"
---
<a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a>[如何操作]: 在回发过程中保留用户控件的状态
[How Do I]: Persist the State of a User Control During a Postback
====================
<span data-ttu-id="a4059-104">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="a4059-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="a4059-105">在此视频的 Chris Pels 中显示了如何持久保存在用户控件中的一个或多个对象的状态。</span><span class="sxs-lookup"><span data-stu-id="a4059-105">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="a4059-106">首先，用户控件创建表示用户指定的搜索筛选器条件的能力。</span><span class="sxs-lookup"><span data-stu-id="a4059-106">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="a4059-107">此外，创建一个辅助性筛选器类用于存储的筛选器信息。</span><span class="sxs-lookup"><span data-stu-id="a4059-107">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="a4059-108">多个用户界面元素添加到筛选器控件和一些方法和属性筛选器类实例中存储的当前筛选器信息。</span><span class="sxs-lookup"><span data-stu-id="a4059-108">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="a4059-109">接下来，使用 RegisterRequiresControlState 方法和关联的保存/还原方法实现用户控件持久性。</span><span class="sxs-lookup"><span data-stu-id="a4059-109">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="a4059-110">这些方法在页回发期间存储筛选器类和其数据的实例。</span><span class="sxs-lookup"><span data-stu-id="a4059-110">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="a4059-111">最后，还有讨论了如何将多个对象存储在控件状态实现。</span><span class="sxs-lookup"><span data-stu-id="a4059-111">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="a4059-112">&#9654;观看视频 （23 分钟）</span><span class="sxs-lookup"><span data-stu-id="a4059-112">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)
