---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: 为 ASP.NET 网页 (Razor) 站点自定义站点范围的行为 |Microsoft Docs
author: tfitzmac
description: 本章介绍如何对整个网站或整个文件夹，而不只是一个页面进行设置。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: a6737c05d3326a2cd7535f32e99482b0de394575
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826635"
---
<a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a>ASP.NET Web Pages (Razor) 站点的自定义网站的行为
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET Web Pages (Razor) 网站中进行站点端设置的页面。
> 
> 你将学习：
> 
> - 如何运行代码，您可以设置的站点中的所有页面值 （全局值或帮助器设置）。
> - 如何运行代码，可设置一个文件夹中的所有页面。
> - 如何运行代码之前和之后的页加载。
> - 如何将错误发送到中央错误页。
> - 如何将身份验证添加到文件夹中的所有页面。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 2
> - WebMatrix 3
> - ASP.NET Web Helpers Library （NuGet 包）
>   
> 
> 本教程还适用于 ASP.NET 网页 3 和 Visual Studio 2013 （或 Visual Studio Express 2013 for Web），除非您不能使用 ASP.NET Web Helpers Library。


<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a>添加 ASP.NET Web pages 网站启动代码

对于多编写 ASP.NET Web Pages 中的代码，单个页面可以包含对该页面所需的所有代码。 例如，如果页面发送一封电子邮件，则可以将该操作的所有代码都放在单个页面。 这可能包括代码以初始化用于发送电子邮件的设置 (即，SMTP 服务器) 和用于发送电子邮件消息。

但是，在某些情况下，你可能想要运行之前任何页站点上的运行一些代码。 这可用于设置可以在站点中的任意位置使用的值 (称为*全局值*。)例如，一些帮助程序要求您提供值，如电子邮件设置或帐户密钥。 它可能会比较方便保留这些设置的全局值。

您可以执行此操作通过创建一个名为页 *\_AppStart.cshtml*站点的根目录中。 如果存在此页，它运行在首次请求该站点中的任意页面。 因此，它是运行代码以设置全局值的好时机。 (因为 *\_AppStart.cshtml*具有下划线的前缀，即使用户直接请求 ASP.NET 不会向页发送到浏览器。)

下图显示如何 *\_AppStart.cshtml*页上的工作原理。 当请求传入的页面，并且如果这是第一个请求的任何页在站点中，ASP.NET 首先检查是否 *\_AppStart.cshtml*页存在。 如果是这样中的任一代码 *\_AppStart.cshtml*页上运行，并运行请求的页面。

![[image]](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a>为你的网站设置的全局值

1. 在 WebMatrix 网站的根文件夹中，创建名为的文件 *\_AppStart.cshtml*。 该文件必须在站点的根目录中。
2. 使用以下内容替换现有内容： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    此代码将值存储在`AppState`字典中，这是自动提供给该站点中的所有页。 请注意，  *\_AppStart.cshtml*文件中没有任何标记。 该页将运行代码，然后将重定向到最初请求的页面。

    > [!NOTE]
    > 将代码放入时要小心 *\_AppStart.cshtml*文件。 如果在代码中出现任何错误 *\_AppStart.cshtml*文件，该网站将不会启动。
3. 在根文件夹中，创建一个名为的新页*AppName.cshtml*。
4. 使用以下内容替换默认标记和代码： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    此代码将提取的值从`AppState`设置中的对象 *\_AppStart.cshtml*页。
5. 运行*AppName.cshtml*页在浏览器中。 (请确保的页中选择**文件**工作区之前运行它。)该页面显示的全局值。 

    ![[image]](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a>帮助程序的设置值

为充分利用 *\_AppStart.cshtml*文件时设置的帮助程序，在网站中使用，且必须在初始化值。 典型的示例包括电子邮件设置`WebMail`帮助器和的专用和公共密钥`ReCaptcha`帮助器。 在类似这样的情况下，可以设置一次中的值 *\_AppStart.cshtml*然后它们是已经为设置所有页在你的站点中。

此过程演示如何设置`WebMail`设置全局范围内。 (有关使用详细信息`WebMail`帮助器，请参阅[添加到 ASP.NET Web Pages 站点的电子邮件](../getting-started/11-adding-email-to-your-web-site.md)。)

1. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未添加它。
2. 如果还没有 *\_AppStart.cshtml*文件中，网站的根文件夹中创建名为的文件 *\_AppStart.cshtml*。
3. 添加以下`WebMail`设置应用于 *\_AppStart.cshtml*文件： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    修改以下电子邮件在代码中的相关的设置：

   - 设置`your-SMTP-host`到有权访问 SMTP 服务器的名称。
   - 设置`your-user-name-here`到 SMTP 服务器帐户的用户名。
   - 设置`your-account-password`为 SMTP 服务器帐户的密码。
   - 设置`your-email-address-here`到电子邮件地址。 这是从发送消息的电子邮件地址。 (某些电子邮件提供程序不会允许您指定其他`From`地址，并且将你的用户名称作为`From`地址。)

     有关 SMTP 设置的详细信息，请参阅[配置电子邮件设置](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings)一文中[发送电子邮件从 ASP.NET Web Pages (Razor) 站点](https://go.microsoft.com/fwlink/?LinkID=202899)和[问题发送电子邮件](https://go.microsoft.com/fwlink/?LinkId=253001#email)中[ASP.NET Web Pages (Razor) 疑难解答指南](https://go.microsoft.com/fwlink/?LinkId=253001)。
4. 保存 *\_AppStart.cshtml*文件并将其关闭。
5. 在网站的根文件夹中，创建名为的新页面*TestEmail.cshtml*。
6. 使用以下内容替换现有内容： 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. 运行*TestEmail.cshtml*页在浏览器中。
8. 填写字段，向自己发送一封电子邮件，然后单击**发送**。
9. 检查电子邮件，请确保您已经看到了该消息。

此示例中的重要部分是，通常不更改的设置 — 喜欢你的 SMTP 服务器和电子邮件凭据的名称 — 在中设置 *\_AppStart.cshtml*文件。 不需要再次设置这些属性在每个页中，电子邮件发送这种方式。 （尽管如果出于某种原因需要更改这些设置，您可以设置它们分别在页面中。）在页中，仅设置通常每次发生变化，如收件人和电子邮件的正文的值。

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a>运行代码之前和之后文件夹中的文件

就像可以使用 *\_AppStart.cshtml*站点中的页面运行之前，请编写代码，您可以编写代码运行之前 （和之后） 运行的特定文件夹中的任意页面。 这可将相同布局页面设置为一个文件夹中的所有页面或检查文件夹中运行一个页面之前登录用户等。

对于页特别是文件夹，您可以创建代码在名为的文件中 *\_PageStart.cshtml*。 下图显示如何 *\_PageStart.cshtml*页上的工作原理。 当请求的页面，ASP.NET 首先检查 *\_AppStart.cshtml*页上，并运行的。 然后 ASP.NET 检查是否存在 *\_PageStart.cshtml*页，然后如果是这样，在运行。 然后，运行请求的页面。

内部 *\_PageStart.cshtml*页上，您可以在要运行通过包括在请求的上的处理过程中指定位置`RunPage`方法。 这样就可以在请求的页面运行之前运行代码，然后在它后再次。 如果您没有`RunPage`中的所有代码 *\_PageStart.cshtml*运行，然后请求的页自动运行。

![[image]](18-customizing-site-wide-behavior/_static/image3.jpg)

ASP.NET 允许您创建的层次结构 *\_PageStart.cshtml*文件。 可以将放 *\_PageStart.cshtml*文件根目录中的站点和任何子文件夹中。 请求页时，  *\_PageStart.cshtml*文件 （最接近的站点根目录中） 的最顶层级别运行后, 跟 *\_PageStart.cshtml*在接下来的文件子文件夹，直至请求到达包含请求的页面的文件夹的子文件夹结构下，依此类推。 之后所有适用 *\_PageStart.cshtml*运行文件，运行请求的页面。

例如，可能有以下的组合 *\_PageStart.cshtml*文件并*Default.cshtml*文件：

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

在运行时 */myfolder/default.cshtml*，可以看到如下：

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a>运行初始化代码文件夹中的所有页面

为充分利用 *\_PageStart.cshtml*文件是初始化的相同的布局页的单个文件夹中的所有文件。

1. 在根文件夹中，创建名为的新文件夹*InitPages*。
2. 在中*InitPages*您的网站的文件夹中创建名为的文件 *\_PageStart.cshtml*和默认标记和代码替换为以下代码： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. 在该网站的根目录中创建名为的文件夹*共享*。
4. 在中*共享*文件夹中，创建名为的文件 *\_Layout1.cshtml*和默认标记和代码替换为以下代码： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. 在中*InitPages*文件夹中，创建名为的文件*Content1.cshtml*和现有内容替换为以下代码： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. 在中*InitPages*文件夹中，创建名为的另一个文件*Content2.cshtml*和默认标记替换为以下代码： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. 运行*Content1.cshtml*在浏览器中。 

    ![[image]](18-customizing-site-wide-behavior/_static/image4.jpg)

    当*Content1.cshtml*页上运行，  *\_PageStart.cshtml*文件中设置`Layout`还将设置和`PageData["MyBackground"]`为一种颜色。 在中*Content1.cshtml*，应用的布局和颜色。
8. 显示*Content2.cshtml*在浏览器中。 

    布局是相同的因为这两个页面初始化中使用相同的布局页和颜色 *\_PageStart.cshtml*。

## <a name="using-pagestartcshtml-to-handle-errors"></a>使用\_PageStart.cshtml 来处理错误

为使用另一个良好 *\_PageStart.cshtml*文件将创建一种方法来处理可能会出现在任何编程错误 （异常） *.cshtml*文件夹中的页。 此示例演示了一种方法执行此操作。

1. 在根文件夹中，创建名为的文件夹*InitCatch*。
2. 在中*InitCatch*您的网站的文件夹中创建名为的文件 *\_PageStart.cshtml*和现有标记和代码替换为以下代码： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    在此代码中，你尝试通过调用显式运行请求的页面`RunPage`方法内的`try`块。 如果在请求中出现的任何编程错误页上，在代码`catch`块将运行。 在这种情况下，代码将重定向到一个页面 (*Error.cshtml*)，并将传递作为 URL 的一部分遇到错误的文件的名称。 （您将创建页不久。）
3. 在中*InitCatch*您的网站的文件夹中创建名为的文件*Exception.cshtml*和现有标记和代码替换为以下代码： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    对于此示例中，你要在此页中执行的操作有意创建错误通过尝试打开不存在的数据库文件。
4. 在根文件夹中，创建名为的文件*Error.cshtml*和现有标记和代码替换为以下代码： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    在此页中，表达式`@Request["source"]`获取在 url 的值并将其显示。
5. 在工具栏中，单击**保存**。
6. 运行*Exception.cshtml*在浏览器中。 

    ![[image]](18-customizing-site-wide-behavior/_static/image5.jpg)

    因为中出现错误*Exception.cshtml*，则 *\_PageStart.cshtml*页将重定向到*Error.cshtml*文件，将显示的消息。

    有关异常的详细信息，请参阅[ASP.NET Web Pages 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkID=251587)。

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-pagestartcshtml-to-restrict-folder-access"></a>使用\_PageStart.cshtml 限制文件夹访问权限

此外可以使用 *\_PageStart.cshtml*文件，以限制对文件夹中的所有文件的访问。

1. 在 WebMatrix 中，使用以下工具创建新网站**从模板**选项。
2. 从可用模板中选择**入门网站**。
3. 在根文件夹中，创建名为的文件夹*AuthenticatedContent*。
4. 在中*AuthenticatedContent*文件夹中，创建名为的文件 *\_PageStart.cshtml*和现有标记和代码替换为以下代码： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    代码将开始通过防止缓存文件夹中的所有文件。 （这 （如公共计算机） 不需要一个用户的缓存的页可用于下一个用户的方案所必需的。）接下来，代码确定是否用户登录到站点之前他们可以查看文件夹中的任何页面。 如果用户未登录，该代码将重定向到登录页。 登录页可以将用户返回到最初请求如果包含一个名为查询字符串值的页面`ReturnUrl`。
5. 创建新的页面中*AuthenticatedContent*名为文件夹*Page.cshtml*。
6. 使用以下内容替换默认标记：  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. 运行*Page.cshtml*在浏览器中。 该代码将你重定向到登录页。 中的日志记录之前必须注册。 已注册并登录后，可以导航到的页并查看其内容。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

[编程使用 Razor 语法的 ASP.NET 网页简介](https://go.microsoft.com/fwlink/?LinkID=251587)
