---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: 使用验证码来防止机器人使用 ASP.NET Web Razor） 站点 |Microsoft Docs
author: microsoft
description: 本文介绍如何使用 ReCaptcha （一种安全措施） 以防止自动的程序 （机器人） 执行的任务在 ASP.NET Web Pages (Razor) 我们...
ms.author: aspnetcontent
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: f67eb60c23e0eec46089ceea9b04779492dfa15e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803066"
---
<a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="43e40-103">使用验证码来防止机器人使用 ASP.NET Web Razor） 站点</span><span class="sxs-lookup"><span data-stu-id="43e40-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>
====================
<span data-ttu-id="43e40-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="43e40-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="43e40-105">本文介绍如何使用 ReCaptcha （一种安全措施） 以防止自动的程序 （机器人） 在 ASP.NET Web Pages (Razor) 的网站中执行任务。</span><span class="sxs-lookup"><span data-stu-id="43e40-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="43e40-106">**你将学习：**</span><span class="sxs-lookup"><span data-stu-id="43e40-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="43e40-107">如何将验证码测试添加到你的站点。</span><span class="sxs-lookup"><span data-stu-id="43e40-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="43e40-108">下面是在本文中引入的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="43e40-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="43e40-109">`ReCaptcha`帮助器。</span><span class="sxs-lookup"><span data-stu-id="43e40-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="43e40-110">在本文中的信息适用于 ASP.NET Web Pages 1.0 和 Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="43e40-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>


## <a name="about-captchas"></a><span data-ttu-id="43e40-111">有关 CAPTCHAs</span><span class="sxs-lookup"><span data-stu-id="43e40-111">About CAPTCHAs</span></span>

<span data-ttu-id="43e40-112">在你的站点，或甚至只是让用户注册任何时间输入的名称和 URL （例如，博客注释），则可能收到大量假名称。</span><span class="sxs-lookup"><span data-stu-id="43e40-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="43e40-113">这些通常保留由自动程序 （机器人） 尝试离开中可以找到的每个网站的 Url。</span><span class="sxs-lookup"><span data-stu-id="43e40-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="43e40-114">（常见的动机是要发布的产品销售的 Url。）</span><span class="sxs-lookup"><span data-stu-id="43e40-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="43e40-115">可帮助确保用户是真实的人并不是计算机的程序，通过使用*CAPTCHA*来注册或否则输入其名称和站点时验证用户。</span><span class="sxs-lookup"><span data-stu-id="43e40-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="43e40-116">CAPTCHA 代表完全自动化的公共图灵测试，以告诉计算机和人类相隔。</span><span class="sxs-lookup"><span data-stu-id="43e40-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="43e40-117">验证码是*质询-响应*是便于人员完成，但难以执行的自动程序的测试要求用户执行某些操作。</span><span class="sxs-lookup"><span data-stu-id="43e40-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="43e40-118">验证码的最常见类型是指您看到一些失真的号或需要键入它们。</span><span class="sxs-lookup"><span data-stu-id="43e40-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="43e40-119">（被应该使机器人能够以解密字母难扭曲）。</span><span class="sxs-lookup"><span data-stu-id="43e40-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="43e40-120">添加 ReCaptcha 测试</span><span class="sxs-lookup"><span data-stu-id="43e40-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="43e40-121">在 ASP.NET 页中，你可以使用`ReCaptcha`帮助器来呈现基于 ReCaptcha 服务的验证码测试 ([http://recaptcha.net](http://recaptcha.net))。</span><span class="sxs-lookup"><span data-stu-id="43e40-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="43e40-122">`ReCaptcha`帮助程序显示用户必须输入正确验证页面之前的两个失真单词的图像。</span><span class="sxs-lookup"><span data-stu-id="43e40-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="43e40-123">由 ReCaptcha.Net 服务验证用户响应。</span><span class="sxs-lookup"><span data-stu-id="43e40-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="43e40-124">注册你的网站在 ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net))。</span><span class="sxs-lookup"><span data-stu-id="43e40-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="43e40-125">完成注册后，您将获得一个公钥和私钥。</span><span class="sxs-lookup"><span data-stu-id="43e40-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="43e40-126">将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未准备好。</span><span class="sxs-lookup"><span data-stu-id="43e40-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="43e40-127">如果还没有 *\_AppStart.cshtml*文件中，网站的根文件夹中创建名为的文件 *\_AppStart.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="43e40-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="43e40-128">添加以下`Recaptcha`中的帮助器设置 *\_AppStart.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="43e40-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="43e40-129">设置`PublicKey`和`PrivateKey`属性使用你自己的公共和私有密钥。</span><span class="sxs-lookup"><span data-stu-id="43e40-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="43e40-130">保存 *\_AppStart.cshtml*文件并将其关闭。</span><span class="sxs-lookup"><span data-stu-id="43e40-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="43e40-131">在网站的根文件夹中，创建名为的新页面*Recaptcha.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="43e40-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="43e40-132">使用以下内容替换现有内容：</span><span class="sxs-lookup"><span data-stu-id="43e40-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="43e40-133">运行*Recaptcha.cshtml*页在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="43e40-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="43e40-134">如果`PrivateKey`值是否有效，该页显示 ReCaptcha 控件和一个按钮。</span><span class="sxs-lookup"><span data-stu-id="43e40-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="43e40-135">如果您必须在全局设置键 *\_AppStart.html*，页面将显示一个错误。</span><span class="sxs-lookup"><span data-stu-id="43e40-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="43e40-136">测试输入单词。</span><span class="sxs-lookup"><span data-stu-id="43e40-136">Enter the words for the test.</span></span> <span data-ttu-id="43e40-137">如果您通过 ReCaptcha 测试，您将看到一条消息以示意。</span><span class="sxs-lookup"><span data-stu-id="43e40-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="43e40-138">否则您会看到一条错误消息和 ReCaptcha 控件重新显示。</span><span class="sxs-lookup"><span data-stu-id="43e40-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="43e40-139">如果您的计算机上使用代理服务器的域中，您可能需要配置`defaultproxy`的元素*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="43e40-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="43e40-140">下面的示例演示*Web.config*文件具有`defaultproxy`元素配置为启用 ReCaptcha 服务正常工作。</span><span class="sxs-lookup"><span data-stu-id="43e40-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="43e40-141">其他资源</span><span class="sxs-lookup"><span data-stu-id="43e40-141">Additional Resources</span></span>


- [<span data-ttu-id="43e40-142">ASP.NET Web Pages 站点的自定义网站的行为</span><span class="sxs-lookup"><span data-stu-id="43e40-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="43e40-143">ReCaptcha 站点</span><span class="sxs-lookup"><span data-stu-id="43e40-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
