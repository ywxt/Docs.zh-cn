---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: 使用验证码来防止机器人使用 ASP.NET Web Razor） 站点 |Microsoft Docs
author: microsoft
description: 本文介绍如何使用 ReCaptcha （一种安全措施） 以防止自动的程序 （机器人） 执行的任务在 ASP.NET Web Pages (Razor) 我们...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/21/2012
ms.topic: article
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: cfdc8561f8ee4b97cc1ef2111113846a1c579d5c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389067"
---
<a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>使用验证码来防止机器人使用 ASP.NET Web Razor） 站点
====================
by [Microsoft](https://github.com/microsoft)

> 本文介绍如何使用 ReCaptcha （一种安全措施） 以防止自动的程序 （机器人） 在 ASP.NET Web Pages (Razor) 的网站中执行任务。
> 
> **你将学习：** 
> 
> - 如何将验证码测试添加到你的站点。
> 
> 下面是在本文中引入的 ASP.NET 功能：
> 
> - `ReCaptcha`帮助器。
> 
> > [!NOTE]
> > 在本文中的信息适用于 ASP.NET Web Pages 1.0 和 Web Pages 2。


## <a name="about-captchas"></a>有关 CAPTCHAs

在你的站点，或甚至只是让用户注册任何时间输入的名称和 URL （例如，博客注释），则可能收到大量假名称。 这些通常保留由自动程序 （机器人） 尝试离开中可以找到的每个网站的 Url。 （常见的动机是要发布的产品销售的 Url。）

可帮助确保用户是真实的人并不是计算机的程序，通过使用*CAPTCHA*来注册或否则输入其名称和站点时验证用户。 CAPTCHA 代表完全自动化的公共图灵测试，以告诉计算机和人类相隔。 验证码是*质询-响应*是便于人员完成，但难以执行的自动程序的测试要求用户执行某些操作。 验证码的最常见类型是指您看到一些失真的号或需要键入它们。 （被应该使机器人能够以解密字母难扭曲）。

## <a name="adding-a-recaptcha-test"></a>添加 ReCaptcha 测试

在 ASP.NET 页中，你可以使用`ReCaptcha`帮助器来呈现基于 ReCaptcha 服务的验证码测试 ([http://recaptcha.net](http://recaptcha.net))。 `ReCaptcha`帮助程序显示用户必须输入正确验证页面之前的两个失真单词的图像。 由 ReCaptcha.Net 服务验证用户响应。

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. 注册你的网站在 ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net))。 完成注册后，您将获得一个公钥和私钥。
2. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未准备好。
3. 如果还没有 *\_AppStart.cshtml*文件中，网站的根文件夹中创建名为的文件 *\_AppStart.cshtml*。
4. 添加以下`Recaptcha`中的帮助器设置 *\_AppStart.cshtml*文件： 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. 设置`PublicKey`和`PrivateKey`属性使用你自己的公共和私有密钥。
6. 保存 *\_AppStart.cshtml*文件并将其关闭。
7. 在网站的根文件夹中，创建名为的新页面*Recaptcha.cshtml*。
8. 使用以下内容替换现有内容： 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. 运行*Recaptcha.cshtml*页在浏览器中。 如果`PrivateKey`值是否有效，该页显示 ReCaptcha 控件和一个按钮。 如果您必须在全局设置键 *\_AppStart.html*，页面将显示一个错误。 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. 测试输入单词。 如果您通过 ReCaptcha 测试，您将看到一条消息以示意。 否则您会看到一条错误消息和 ReCaptcha 控件重新显示。

> [!NOTE]
> 如果您的计算机上使用代理服务器的域中，您可能需要配置`defaultproxy`的元素*Web.config*文件。 下面的示例演示*Web.config*文件具有`defaultproxy`元素配置为启用 ReCaptcha 服务正常工作。
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源


- [ASP.NET Web Pages 站点的自定义网站的行为](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ReCaptcha 站点](https://www.google.com/recaptcha)
