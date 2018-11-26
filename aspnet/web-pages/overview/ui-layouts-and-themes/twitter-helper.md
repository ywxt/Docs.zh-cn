---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: Twitter 使用 ASP.NET Web 页面的帮助程序 |Microsoft Docs
author: Rick-Anderson
description: 此主题和应用程序演示如何将 Twitter 帮助程序添加到 WebMatrix 3 项目。 它包含的 Twitter 帮助程序代码，并演示如何调用帮助器...
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: fabe9f2b84d278a766dc8d8b7bfc00e1eb967127
ms.sourcegitcommit: 710fc5fcac258cc8415976dc66bdb355b3e061d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2018
ms.locfileid: "52299425"
---
<a name="twitter-helper-with-aspnet-web-pages"></a><span data-ttu-id="3d751-104">使用 ASP.NET 网页的 twitter 帮助程序</span><span class="sxs-lookup"><span data-stu-id="3d751-104">Twitter Helper with ASP.NET Web Pages</span></span>
====================
<span data-ttu-id="3d751-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3d751-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d751-106">Twitter 帮助程序已过时。</span><span class="sxs-lookup"><span data-stu-id="3d751-106">Twitter Helpers are obsolete.</span></span> <span data-ttu-id="3d751-107">关于 Twitter 的最新 engagement 工具的网站，请参阅[Twitter 网站概述](https://developer.twitter.com/en/docs/twitter-for-websites/overview)。</span><span class="sxs-lookup"><span data-stu-id="3d751-107">For Twitter's latest engagement tools for websites, see [Twitter for Websites Overview](https://developer.twitter.com/en/docs/twitter-for-websites/overview).</span></span>

> <span data-ttu-id="3d751-108">此主题和应用程序演示如何将 Twitter 帮助程序添加到 WebMatrix 3 项目。</span><span class="sxs-lookup"><span data-stu-id="3d751-108">This topic and application show how to add a Twitter Helper to your WebMatrix 3 project.</span></span> <span data-ttu-id="3d751-109">它包含的 Twitter 帮助器代码，并演示了如何调用帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="3d751-109">It contains the Twitter Helper code and shows how to call the helper methods.</span></span>
> 
> <span data-ttu-id="3d751-110">这段代码用于 Twitter.cshtml 文件由开发**天平移**Microsoft。</span><span class="sxs-lookup"><span data-stu-id="3d751-110">This code for the Twitter.cshtml file was developed by **Tian Pan** of Microsoft.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3d751-111">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="3d751-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="3d751-112">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="3d751-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="3d751-113">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="3d751-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="introduction"></a><span data-ttu-id="3d751-114">介绍</span><span class="sxs-lookup"><span data-stu-id="3d751-114">Introduction</span></span>

<span data-ttu-id="3d751-115">本主题演示如何将 Twitter 帮助程序添加到你的应用程序并使用 Razor 语法来调用帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="3d751-115">This topic demonstrates how to add a Twitter Helper to your application and use Razor syntax to call the helper methods.</span></span> <span data-ttu-id="3d751-116">Twitter 帮助程序轻松合并 Twitter 按钮和应用程序中的小组件。</span><span class="sxs-lookup"><span data-stu-id="3d751-116">The Twitter Helper makes it easy to incorporate Twitter buttons and widgets in your application.</span></span> <span data-ttu-id="3d751-117">若要使用 Twitter 小组件，如用户的时间线或井号标签的搜索结果必须先创建[Twitter 上的小组件](https://twitter.com/settings/widgets)。</span><span class="sxs-lookup"><span data-stu-id="3d751-117">To use a Twitter widget, such as a user's timeline or the search results for a hashtag, you must first create the [widget on Twitter](https://twitter.com/settings/widgets).</span></span> <span data-ttu-id="3d751-118">创建小组件后, 会收到一个小组件 id。显示小组件的帮助器方法在调用时作为参数传递此小组件 id。</span><span class="sxs-lookup"><span data-stu-id="3d751-118">After creating your widget, you will receive a widget id. You pass this widget id as a parameter when calling the helper methods that show widget.</span></span>

<span data-ttu-id="3d751-119">本主题已针对 Twitter API 的 1.1 版编写。</span><span class="sxs-lookup"><span data-stu-id="3d751-119">This topic was written for version 1.1 of the Twitter API.</span></span> <span data-ttu-id="3d751-120">通过直接将 Twitter 帮助程序代码添加到你的项目，可以更新的帮助器代码，如果 Twitter API 发生更改。</span><span class="sxs-lookup"><span data-stu-id="3d751-120">By directly adding the Twitter Helper code to your project, you can update the helper code if the Twitter API changes.</span></span>

<span data-ttu-id="3d751-121">有关 WebMatrix 的安装信息，请参阅[引入了 ASP.NET Web Pages 2-Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="3d751-121">For information about installing WebMatrix, see [Introducing ASP.NET Web Pages 2 - Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span></span>

## <a name="add-twitter-helper-to-your-project"></a><span data-ttu-id="3d751-122">将 Twitter 帮助程序添加到你的项目</span><span class="sxs-lookup"><span data-stu-id="3d751-122">Add Twitter Helper to your project</span></span>

<span data-ttu-id="3d751-123">若要添加 Twitter 帮助程序，首先，添加名为的文件夹**应用程序\_代码**到你的项目。</span><span class="sxs-lookup"><span data-stu-id="3d751-123">To add the Twitter Helper, first, add a folder named **App\_Code** to your project.</span></span> <span data-ttu-id="3d751-124">然后，创建名为的文件**Twitter.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="3d751-124">Then, create a file named **Twitter.cshtml**.</span></span>

![App_Code 文件夹](twitter-helper/_static/image1.png)

<span data-ttu-id="3d751-126">Twitter.cshtml 中的默认代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="3d751-126">Replace the default code in Twitter.cshtml with the following code.</span></span>

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a><span data-ttu-id="3d751-127">从您的 web 页面调用 Twitter 方法</span><span class="sxs-lookup"><span data-stu-id="3d751-127">Call Twitter methods from your web pages</span></span>

<span data-ttu-id="3d751-128">下面的示例演示如何在项目中使用从一个页面的 Twitter 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="3d751-128">The following example shows how to use the Twitter Helper methods from a page in your project.</span></span> <span data-ttu-id="3d751-129">在项目中，你将想要的参数值替换为与你的需求相关的值。</span><span class="sxs-lookup"><span data-stu-id="3d751-129">In your project, you will want to replace the parameter values with values that are relevant to your needs.</span></span> <span data-ttu-id="3d751-130">可以使用提供的小组件 id 来探索方法的工作方式，但想要生成你自己的小组件为你的项目。</span><span class="sxs-lookup"><span data-stu-id="3d751-130">You can use the provided widget ids to explore how the methods work, but you will want to generate your own widgets for your project.</span></span>

<span data-ttu-id="3d751-131">需要不是所有的参数如下所示。</span><span class="sxs-lookup"><span data-stu-id="3d751-131">Not all of the parameters shown below are required.</span></span> <span data-ttu-id="3d751-132">可选参数用于自定义按钮或小组件的显示方式。</span><span class="sxs-lookup"><span data-stu-id="3d751-132">The optional parameters are used to customize how the button or widget is displayed.</span></span> <span data-ttu-id="3d751-133">例如，执行按钮只需要用户名称，若要执行，但该示例演示如何包含数量的关注者，并指定大小的按钮和语言的方式。</span><span class="sxs-lookup"><span data-stu-id="3d751-133">For example, the Follow Button only requires the user name to follow, but the example shows how to include the number of followers, and how specify the size of the button and the language.</span></span>

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a><span data-ttu-id="3d751-134">查看结果</span><span class="sxs-lookup"><span data-stu-id="3d751-134">See the results</span></span>

<span data-ttu-id="3d751-135">上面的代码生成以下按钮和小组件。</span><span class="sxs-lookup"><span data-stu-id="3d751-135">The above code produces the following buttons and widgets.</span></span> <span data-ttu-id="3d751-136">这些按钮和小组件是功能完整的不是屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="3d751-136">These buttons and widgets are fully-functional, not screenshots.</span></span> <span data-ttu-id="3d751-137">请按照按钮显示在西班牙语中，因为语言参数设置为**es**。</span><span class="sxs-lookup"><span data-stu-id="3d751-137">The Follow Button is displayed in Spanish because the language parameter was set to **es**.</span></span>

### <a name="follow-button"></a><span data-ttu-id="3d751-138">请按照按钮</span><span class="sxs-lookup"><span data-stu-id="3d751-138">Follow Button</span></span>

<span data-ttu-id="3d751-139">[请按照@aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="3d751-139">[Follow @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="tweet-button"></a><span data-ttu-id="3d751-140">推文按钮</span><span class="sxs-lookup"><span data-stu-id="3d751-140">Tweet Button</span></span>

<span data-ttu-id="3d751-141">[推文](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="3d751-141">[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="user-timeline-profile"></a><span data-ttu-id="3d751-142">用户时间线 （配置文件）</span><span class="sxs-lookup"><span data-stu-id="3d751-142">User Timeline (Profile)</span></span>

<span data-ttu-id="3d751-143">[通过推文 @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="3d751-143">[Tweets by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="favorites"></a><span data-ttu-id="3d751-144">收藏夹</span><span class="sxs-lookup"><span data-stu-id="3d751-144">Favorites</span></span>

<span data-ttu-id="3d751-145">[收藏的推文作者 @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="3d751-145">[Favorite Tweets by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="list"></a><span data-ttu-id="3d751-146">列表</span><span class="sxs-lookup"><span data-stu-id="3d751-146">List</span></span>

<span data-ttu-id="3d751-147">[从推文@Microsoft/MS\_使用者\_带区](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="3d751-147">[Tweets from @Microsoft/MS\_Consumer\_Bands](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="search"></a><span data-ttu-id="3d751-148">搜索</span><span class="sxs-lookup"><span data-stu-id="3d751-148">Search</span></span>

<span data-ttu-id="3d751-149">[有关推文&quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="3d751-149">[Tweets about &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>
