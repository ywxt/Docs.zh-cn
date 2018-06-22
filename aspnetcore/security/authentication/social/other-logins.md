---
title: 简短的调查的其他身份验证提供程序
author: rick-anderson
ms.author: riande
ms.date: 11/03/2016
uid: security/authentication/otherlogins
ms.openlocfilehash: 9c2ce02f4613fddbe0e767724019d80ac056bf7b
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36274048"
---
# <a name="short-survey-of-other-authentication-providers"></a><span data-ttu-id="b57a1-102">简短的调查的其他身份验证提供程序</span><span class="sxs-lookup"><span data-stu-id="b57a1-102">Short survey of other authentication providers</span></span>

<a name="security-authentication-other-logins"></a>

<span data-ttu-id="b57a1-103">通过[Rick Anderson](https://twitter.com/RickAndMSFT)， [Pranav Rastogi](https://github.com/rustd)，和[Valeriy Novytskyy](https://github.com/01binary)</span><span class="sxs-lookup"><span data-stu-id="b57a1-103">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Pranav Rastogi](https://github.com/rustd), and [Valeriy Novytskyy](https://github.com/01binary)</span></span>

<span data-ttu-id="b57a1-104">此处会设置对于某些其他常见 OAuth 提供程序的说明。</span><span class="sxs-lookup"><span data-stu-id="b57a1-104">Here are set up instructions for some other common OAuth providers.</span></span> <span data-ttu-id="b57a1-105">第三方 NuGet 包，例如由维护的[aspnet contrib](https://www.nuget.org/packages?q=owners%3Aaspnet-contrib+title%3AOAuth)可以用于补充由 ASP.NET Core 团队实现的身份验证提供程序。</span><span class="sxs-lookup"><span data-stu-id="b57a1-105">Third-party NuGet packages such as the ones maintained by [aspnet-contrib](https://www.nuget.org/packages?q=owners%3Aaspnet-contrib+title%3AOAuth) can be used to complement authentication providers implemented by the ASP.NET Core team.</span></span>

* <span data-ttu-id="b57a1-106">设置**LinkedIn**登录： [ https://www.linkedin.com/developer/apps ](https://www.linkedin.com/developer/apps)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-106">Set up **LinkedIn** sign in: [https://www.linkedin.com/developer/apps](https://www.linkedin.com/developer/apps).</span></span> <span data-ttu-id="b57a1-107">请参阅[官方步骤](https://developer.linkedin.com/docs/oauth2)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-107">See [official steps](https://developer.linkedin.com/docs/oauth2).</span></span>

* <span data-ttu-id="b57a1-108">设置**Instagram**登录： [ https://www.instagram.com/developer/register/ ](https://www.instagram.com/developer/register/)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-108">Set up **Instagram** sign in: [https://www.instagram.com/developer/register/](https://www.instagram.com/developer/register/).</span></span> <span data-ttu-id="b57a1-109">请参阅[官方步骤](https://www.instagram.com/developer/authentication/)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-109">See [official steps](https://www.instagram.com/developer/authentication/).</span></span>

* <span data-ttu-id="b57a1-110">设置**Reddit**登录： [ https://www.reddit.com/login?dest=https%3A%2F%2Fwww.reddit.com%2Fprefs%2Fapps ](https://www.reddit.com/login?dest=https%3A%2F%2Fwww.reddit.com%2Fprefs%2Fapps)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-110">Set up **Reddit** sign in: [https://www.reddit.com/login?dest=https%3A%2F%2Fwww.reddit.com%2Fprefs%2Fapps](https://www.reddit.com/login?dest=https%3A%2F%2Fwww.reddit.com%2Fprefs%2Fapps).</span></span> <span data-ttu-id="b57a1-111">请参阅[官方步骤](https://github.com/reddit/reddit/wiki/OAuth2-Quick-Start-Example)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-111">See [official steps](https://github.com/reddit/reddit/wiki/OAuth2-Quick-Start-Example).</span></span>

* <span data-ttu-id="b57a1-112">设置**Github**登录： [ https://github.com/login?return_to=https%3A%2F%2Fgithub.com%2Fsettings%2Fapplications%2Fnew ](https://github.com/login?return_to=https%3A%2F%2Fgithub.com%2Fsettings%2Fapplications%2Fnew)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-112">Set up **Github** sign in: [https://github.com/login?return_to=https%3A%2F%2Fgithub.com%2Fsettings%2Fapplications%2Fnew](https://github.com/login?return_to=https%3A%2F%2Fgithub.com%2Fsettings%2Fapplications%2Fnew).</span></span> <span data-ttu-id="b57a1-113">请参阅[官方步骤](https://developer.github.com/v3/oauth/)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-113">See [official steps](https://developer.github.com/v3/oauth/).</span></span>

* <span data-ttu-id="b57a1-114">设置**Yahoo**登录： [ https://login.yahoo.com/config/login?src=devnet&.done=http%3A%2F%2Fdeveloper.yahoo.com%2Fapps%2Fcreate%2F ](https://login.yahoo.com/config/login?src=devnet&.done=http%3A%2F%2Fdeveloper.yahoo.com%2Fapps%2Fcreate%2F)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-114">Set up **Yahoo** sign in: [https://login.yahoo.com/config/login?src=devnet&.done=http%3A%2F%2Fdeveloper.yahoo.com%2Fapps%2Fcreate%2F](https://login.yahoo.com/config/login?src=devnet&.done=http%3A%2F%2Fdeveloper.yahoo.com%2Fapps%2Fcreate%2F).</span></span> <span data-ttu-id="b57a1-115">请参阅[官方步骤](https://developer.yahoo.com/bbauth/user.html)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-115">See [official steps](https://developer.yahoo.com/bbauth/user.html).</span></span>

* <span data-ttu-id="b57a1-116">设置**Tumblr**登录： [ https://www.tumblr.com/oauth/apps ](https://www.tumblr.com/oauth/apps)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-116">Set up **Tumblr** sign in: [https://www.tumblr.com/oauth/apps](https://www.tumblr.com/oauth/apps).</span></span> <span data-ttu-id="b57a1-117">请参阅[官方步骤](https://www.tumblr.com/docs/api/v2#auth)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-117">See [official steps](https://www.tumblr.com/docs/api/v2#auth).</span></span>

* <span data-ttu-id="b57a1-118">设置**Pinterest**登录： [ https://www.pinterest.com/login/?next=http%3A%2F%2Fdevsite%2Fapps%2F ](https://www.pinterest.com/login/?next=http%3A%2F%2Fdevsite%2Fapps%2F)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-118">Set up **Pinterest** sign in: [https://www.pinterest.com/login/?next=http%3A%2F%2Fdevsite%2Fapps%2F](https://www.pinterest.com/login/?next=http%3A%2F%2Fdevsite%2Fapps%2F).</span></span> <span data-ttu-id="b57a1-119">请参阅[官方步骤](https://developers.pinterest.com/docs/api/overview/?)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-119">See [official steps](https://developers.pinterest.com/docs/api/overview/?).</span></span>

* <span data-ttu-id="b57a1-120">设置**Pocket**登录： [ https://getpocket.com/developer/apps/new ](https://getpocket.com/developer/apps/new)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-120">Set up **Pocket** sign in: [https://getpocket.com/developer/apps/new](https://getpocket.com/developer/apps/new).</span></span> <span data-ttu-id="b57a1-121">请参阅[官方步骤](https://getpocket.com/developer/docs/authentication)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-121">See [official steps](https://getpocket.com/developer/docs/authentication).</span></span>

* <span data-ttu-id="b57a1-122">设置**Flickr**登录： [ https://www.flickr.com/services/apps/create ](https://www.flickr.com/services/apps/create)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-122">Set up **Flickr** sign in: [https://www.flickr.com/services/apps/create](https://www.flickr.com/services/apps/create).</span></span> <span data-ttu-id="b57a1-123">请参阅[官方步骤](https://www.flickr.com/services/api/auth.oauth.html)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-123">See [official steps](https://www.flickr.com/services/api/auth.oauth.html).</span></span>

* <span data-ttu-id="b57a1-124">设置**Dribble**登录： [ https://dribbble.com/signup ](https://dribbble.com/signup)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-124">Set up **Dribble** sign in: [https://dribbble.com/signup](https://dribbble.com/signup).</span></span> <span data-ttu-id="b57a1-125">请参阅[官方步骤](http://developer.dribbble.com/v1/oauth/)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-125">See [official steps](http://developer.dribbble.com/v1/oauth/).</span></span>

* <span data-ttu-id="b57a1-126">设置**Vimeo**登录： [ https://vimeo.com/join ](https://vimeo.com/join)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-126">Set up **Vimeo** sign in: [https://vimeo.com/join](https://vimeo.com/join).</span></span> <span data-ttu-id="b57a1-127">请参阅[官方步骤](https://developer.vimeo.com/api/authentication)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-127">See [official steps](https://developer.vimeo.com/api/authentication).</span></span>

* <span data-ttu-id="b57a1-128">设置**SoundCloud**登录： [ https://soundcloud.com/you/apps/new ](https://soundcloud.com/you/apps/new)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-128">Set up **SoundCloud** sign in: [https://soundcloud.com/you/apps/new](https://soundcloud.com/you/apps/new).</span></span> <span data-ttu-id="b57a1-129">请参阅[官方步骤](https://developers.soundcloud.com/blog/we-love-oauth-2)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-129">See [official steps](https://developers.soundcloud.com/blog/we-love-oauth-2).</span></span>

* <span data-ttu-id="b57a1-130">设置**VK**登录： [ https://vk.com/apps?act=manage ](https://vk.com/apps?act=manage)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-130">Set up **VK** sign in: [https://vk.com/apps?act=manage](https://vk.com/apps?act=manage).</span></span> <span data-ttu-id="b57a1-131">请参阅[官方步骤](https://vk.com/pages?oid=-17680044&p=Authorizing_Sites)。</span><span class="sxs-lookup"><span data-stu-id="b57a1-131">See [official steps](https://vk.com/pages?oid=-17680044&p=Authorizing_Sites).</span></span>

## <a name="multiple-authentication-providers"></a><span data-ttu-id="b57a1-132">多个身份验证提供程序</span><span class="sxs-lookup"><span data-stu-id="b57a1-132">Multiple authentication providers</span></span>

[!INCLUDE[](~/includes/chain-auth-providers.md)]
