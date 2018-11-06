---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: Twitter 使用 ASP.NET Web 页面的帮助程序 |Microsoft Docs
author: Rick-Anderson
description: 此主题和应用程序演示如何将 Twitter 帮助程序添加到 WebMatrix 3 项目。 它包含的 Twitter 帮助程序代码，并演示如何调用帮助器...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 89c8c520cd32ca2ee24e6cd90e11f7bdf39c7a80
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020568"
---
<a name="twitter-helper-with-aspnet-web-pages"></a><span data-ttu-id="6410f-104">使用 ASP.NET 网页的 twitter 帮助程序</span><span class="sxs-lookup"><span data-stu-id="6410f-104">Twitter Helper with ASP.NET Web Pages</span></span>
====================
<span data-ttu-id="6410f-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6410f-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6410f-106">此主题和应用程序演示如何将 Twitter 帮助程序添加到 WebMatrix 3 项目。</span><span class="sxs-lookup"><span data-stu-id="6410f-106">This topic and application show how to add a Twitter Helper to your WebMatrix 3 project.</span></span> <span data-ttu-id="6410f-107">它包含的 Twitter 帮助器代码，并演示了如何调用帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="6410f-107">It contains the Twitter Helper code and shows how to call the helper methods.</span></span>
> 
> <span data-ttu-id="6410f-108">这段代码用于 Twitter.cshtml 文件由开发**天平移**Microsoft。</span><span class="sxs-lookup"><span data-stu-id="6410f-108">This code for the Twitter.cshtml file was developed by **Tian Pan** of Microsoft.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6410f-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="6410f-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6410f-110">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="6410f-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="6410f-111">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="6410f-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="introduction"></a><span data-ttu-id="6410f-112">介绍</span><span class="sxs-lookup"><span data-stu-id="6410f-112">Introduction</span></span>

<span data-ttu-id="6410f-113">本主题演示如何将 Twitter 帮助程序添加到你的应用程序并使用 Razor 语法来调用帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="6410f-113">This topic demonstrates how to add a Twitter Helper to your application and use Razor syntax to call the helper methods.</span></span> <span data-ttu-id="6410f-114">Twitter 帮助程序轻松合并 Twitter 按钮和应用程序中的小组件。</span><span class="sxs-lookup"><span data-stu-id="6410f-114">The Twitter Helper makes it easy to incorporate Twitter buttons and widgets in your application.</span></span> <span data-ttu-id="6410f-115">若要使用 Twitter 小组件，如用户的时间线或井号标签的搜索结果必须先创建[Twitter 上的小组件](https://twitter.com/settings/widgets)。</span><span class="sxs-lookup"><span data-stu-id="6410f-115">To use a Twitter widget, such as a user's timeline or the search results for a hashtag, you must first create the [widget on Twitter](https://twitter.com/settings/widgets).</span></span> <span data-ttu-id="6410f-116">创建小组件后, 会收到一个小组件 id。显示小组件的帮助器方法在调用时作为参数传递此小组件 id。</span><span class="sxs-lookup"><span data-stu-id="6410f-116">After creating your widget, you will receive a widget id. You pass this widget id as a parameter when calling the helper methods that show widget.</span></span>

<span data-ttu-id="6410f-117">本主题已针对 Twitter API 的 1.1 版编写。</span><span class="sxs-lookup"><span data-stu-id="6410f-117">This topic was written for version 1.1 of the Twitter API.</span></span> <span data-ttu-id="6410f-118">通过直接将 Twitter 帮助程序代码添加到你的项目，可以更新的帮助器代码，如果 Twitter API 发生更改。</span><span class="sxs-lookup"><span data-stu-id="6410f-118">By directly adding the Twitter Helper code to your project, you can update the helper code if the Twitter API changes.</span></span>

<span data-ttu-id="6410f-119">有关 WebMatrix 的安装信息，请参阅[引入了 ASP.NET Web Pages 2-Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6410f-119">For information about installing WebMatrix, see [Introducing ASP.NET Web Pages 2 - Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span></span>

## <a name="add-twitter-helper-to-your-project"></a><span data-ttu-id="6410f-120">将 Twitter 帮助程序添加到你的项目</span><span class="sxs-lookup"><span data-stu-id="6410f-120">Add Twitter Helper to your project</span></span>

<span data-ttu-id="6410f-121">若要添加 Twitter 帮助程序，首先，添加名为的文件夹**应用程序\_代码**到你的项目。</span><span class="sxs-lookup"><span data-stu-id="6410f-121">To add the Twitter Helper, first, add a folder named **App\_Code** to your project.</span></span> <span data-ttu-id="6410f-122">然后，创建名为的文件**Twitter.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="6410f-122">Then, create a file named **Twitter.cshtml**.</span></span>

![App_Code 文件夹](twitter-helper/_static/image1.png)

<span data-ttu-id="6410f-124">Twitter.cshtml 中的默认代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="6410f-124">Replace the default code in Twitter.cshtml with the following code.</span></span>

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a><span data-ttu-id="6410f-125">从您的 web 页面调用 Twitter 方法</span><span class="sxs-lookup"><span data-stu-id="6410f-125">Call Twitter methods from your web pages</span></span>

<span data-ttu-id="6410f-126">下面的示例演示如何在项目中使用从一个页面的 Twitter 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="6410f-126">The following example shows how to use the Twitter Helper methods from a page in your project.</span></span> <span data-ttu-id="6410f-127">在项目中，你将想要的参数值替换为与你的需求相关的值。</span><span class="sxs-lookup"><span data-stu-id="6410f-127">In your project, you will want to replace the parameter values with values that are relevant to your needs.</span></span> <span data-ttu-id="6410f-128">可以使用提供的小组件 id 来探索方法的工作方式，但想要生成你自己的小组件为你的项目。</span><span class="sxs-lookup"><span data-stu-id="6410f-128">You can use the provided widget ids to explore how the methods work, but you will want to generate your own widgets for your project.</span></span>

<span data-ttu-id="6410f-129">需要不是所有的参数如下所示。</span><span class="sxs-lookup"><span data-stu-id="6410f-129">Not all of the parameters shown below are required.</span></span> <span data-ttu-id="6410f-130">可选参数用于自定义按钮或小组件的显示方式。</span><span class="sxs-lookup"><span data-stu-id="6410f-130">The optional parameters are used to customize how the button or widget is displayed.</span></span> <span data-ttu-id="6410f-131">例如，执行按钮只需要用户名称，若要执行，但该示例演示如何包含数量的关注者，并指定大小的按钮和语言的方式。</span><span class="sxs-lookup"><span data-stu-id="6410f-131">For example, the Follow Button only requires the user name to follow, but the example shows how to include the number of followers, and how specify the size of the button and the language.</span></span>

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a><span data-ttu-id="6410f-132">查看结果</span><span class="sxs-lookup"><span data-stu-id="6410f-132">See the results</span></span>

<span data-ttu-id="6410f-133">上面的代码生成以下按钮和小组件。</span><span class="sxs-lookup"><span data-stu-id="6410f-133">The above code produces the following buttons and widgets.</span></span> <span data-ttu-id="6410f-134">这些按钮和小组件是功能完整的不是屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="6410f-134">These buttons and widgets are fully-functional, not screenshots.</span></span> <span data-ttu-id="6410f-135">请按照按钮显示在西班牙语中，因为语言参数设置为**es**。</span><span class="sxs-lookup"><span data-stu-id="6410f-135">The Follow Button is displayed in Spanish because the language parameter was set to **es**.</span></span>

### <a name="follow-button"></a><span data-ttu-id="6410f-136">请按照按钮</span><span class="sxs-lookup"><span data-stu-id="6410f-136">Follow Button</span></span>

<span data-ttu-id="6410f-137">[请按照@aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="6410f-137">[Follow @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="tweet-button"></a><span data-ttu-id="6410f-138">推文按钮</span><span class="sxs-lookup"><span data-stu-id="6410f-138">Tweet Button</span></span>

<span data-ttu-id="6410f-139">[推文](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="6410f-139">[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="user-timeline-profile"></a><span data-ttu-id="6410f-140">用户时间线 （配置文件）</span><span class="sxs-lookup"><span data-stu-id="6410f-140">User Timeline (Profile)</span></span>

<span data-ttu-id="6410f-141">[通过推文 @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="6410f-141">[Tweets by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="favorites"></a><span data-ttu-id="6410f-142">收藏夹</span><span class="sxs-lookup"><span data-stu-id="6410f-142">Favorites</span></span>

<span data-ttu-id="6410f-143">[收藏的推文作者 @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="6410f-143">[Favorite Tweets by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="list"></a><span data-ttu-id="6410f-144">列表</span><span class="sxs-lookup"><span data-stu-id="6410f-144">List</span></span>

<span data-ttu-id="6410f-145">[从推文@Microsoft/MS\_使用者\_带区](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="6410f-145">[Tweets from @Microsoft/MS\_Consumer\_Bands](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="search"></a><span data-ttu-id="6410f-146">搜索</span><span class="sxs-lookup"><span data-stu-id="6410f-146">Search</span></span>

<span data-ttu-id="6410f-147">[有关推文&quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="6410f-147">[Tweets about &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>
