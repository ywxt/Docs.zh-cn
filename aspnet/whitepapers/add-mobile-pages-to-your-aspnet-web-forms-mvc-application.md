---
uid: whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
title: 如何： 将移动页面添加到 ASP.NET Web 窗体 / MVC 应用程序 |Microsoft Docs
author: rick-anderson
description: 此方法向介绍了各种方法提供针对 ASP.NET Web 窗体中的移动设备优化的页面 / MVC 应用程序，并提供的建议体系结构和...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2011
ms.topic: article
ms.assetid: 3124f28e-cc32-418a-afe3-519fa56f4c36
ms.technology: ''
msc.legacyurl: /whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
msc.type: content
ms.openlocfilehash: 075329087cb5e07d85bba0c546538e7cc55ac463
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366752"
---
<a name="how-to-add-mobile-pages-to-your-aspnet-web-forms--mvc-application"></a>如何： 将移动页面添加到 ASP.NET Web 窗体 / MVC 应用程序
====================
> **适用于**
> 
> - ASP.NET Web 窗体版本 4.0
> - ASP.NET MVC 版本 3.0
> 
> **摘要**
> 
> 此方法向介绍了各种方法提供针对 ASP.NET Web 窗体中的移动设备优化的页面 / MVC 应用程序，并建议体系结构和设计要考虑面向范围广泛的设备时的问题。 本文档还介绍了为什么 ASP.NET 移动控件从 ASP.NET 2.0 到 3.5 现已过时，并讨论某些现代的替代方法。


## <a name="contents"></a>内容

- 概述
- 体系结构选项
- 浏览器和设备检测
- ASP.NET Web 窗体应用程序可以如何提供移动特定页
- ASP.NET MVC 应用程序可以如何提供移动特定页
- 其他资源

本白皮书主要技术演示 ASP.NET Web 窗体和 MVC 的可下载代码示例，请参阅[移动应用和 asp.net 站点](https://docs.microsoft.com/aspnet/mobile/overview)。

## <a name="overview"></a>概述

移动设备 – 智能手机、 功能手机和平板电脑-不断增大作为一种方式来访问 Web 的受欢迎程度。 对于许多 web 开发人员和面向 web 的企业，这意味着它是为使用这些设备的访问者提供了很好的浏览体验越来越重要。

### <a name="how-earlier-versions-of-aspnet-supported-mobile-browsers"></a>如何早期版本的 ASP.NET 支持移动浏览器

ASP.NET 版本 2.0 到 3.5 包含*ASP.NET 移动控件*： 一组中的移动设备的服务器控件*System.Web.Mobile.dll*程序集和*System.Web.UI.MobileControls*命名空间。 程序集仍包含在 ASP.NET 4 中，但不推荐使用。 建议开发人员将迁移到更现代的方法，如本文中所述。

为什么 ASP.NET 移动控件具有已标记为过时的原因是，其设计面向的是常见围绕 2005年及更早版本的手机。 控件主要设计用于呈现 WML 或 cHTML 标记 （而不是常规的 HTML) 的那个时代的 WAP 浏览器。 但 WAP、 WML 和 cHTML 不再适用于大多数项目，因为 HTML 现在已成为移动和桌面浏览器等内容的通用标记语言。

### <a name="the-challenges-of-supporting-mobile-devices-today"></a>现在支持移动设备的挑战

尽管移动浏览器现在普遍支持 HTML，仍将面临着许多挑战，当热情，希望创建强大的移动浏览体验：

- ***屏幕大小***-在表单中，显著不同的移动设备和其屏幕通常是很多小于桌面监视器。 因此，您可能需要为其设计完全不同的页面布局。
- ***输入方法***– 某些设备具有小键盘、 一些具有 styluses、 其他人使用触摸屏输入。 您可能需要考虑多个导航机制和数据的输入的方法。
- ***标准符合性***– 很多移动浏览器不支持的最新的 HTML、 CSS 或 JavaScript 标准。
- ***带宽***-移动电话数据网络性能而发生变化差异很大，和一些最终用户位于关税根据的兆字节。

没有一刀切的解决方案;你的应用程序将需要的外观和行为以不同的方式根据设备对其进行访问。 具体取决于所需的移动设备级别，这可以是支持的面向 web 开发人员比以往桌面"浏览器大战"一个更大挑战。

通常最初接近的第一次移动浏览器支持的开发人员认为务必仅支持最新和最复杂的智能手机 （例如，Windows Phone 7、 iPhone 或 Android），可能是因为开发人员通常个人拥有此类设备。 但是，更便宜的手机仍然非常受欢迎，而且其所有者使用它们来浏览 web – 尤其是在移动电话是比使用宽带连接更容易获取的国家/地区。 你的业务需要决定哪些设备，以支持通过考虑其有可能购买产品的范围。 如果您正在构建 luxury 运行状况 spa 联机手册，您可能会使的业务决策仅面向高级智能手机，而如果要创建电影的票证预订系统，可能需要考虑使用较不强大的功能的访问者手机。

## <a name="architectural-options"></a>体系结构选项

我们进入 ASP.NET Web 窗体或 MVC 的特定技术细节之前，请注意，web 开发人员通常具有三个主要的可能选项，以支持移动浏览器：

1. ***不执行任何操作 –*** 只需创建标准的、 面向桌面的 web 应用程序，并依赖于移动浏览器的呈现效果可接受。 

    - **利用**： 它是最便宜的选项来实施和维护-无需额外工作
    - **缺点**： 提供的最差的最终用户体验： 

        - 最新的智能手机与桌面浏览器中，可能会呈现在 HTML，但用户仍必须来缩放和水平滚动和垂直来使用您在小屏幕上的内容。 这是与最佳相差甚远。
        - 较旧的设备和功能手机可能会失败的令人满意的方式呈现您的标记。
        - 甚至在最新的 tablet 设备 （其屏幕可以是笔记本电脑屏幕一样大），不同的交互的规则适用。 基于触控的输入最适用于较大的按钮和链接跨页进一步相隔，并且没有办法鼠标光标悬停在飞出式菜单。
2. ***解决此问题在客户端上的*–** 与小心使用 CSS 并[渐进式增强](http://en.wikipedia.org/wiki/Progressive_enhancement)标记、 样式和适应任何浏览器运行这些脚本可以创建。 例如，对于[CSS 3 媒体查询](http://www.w3.org/TR/2010/CR-css3-mediaqueries-20100727/)，可以创建在屏幕的窄于所选阈值的设备将变为单列布局的多列布局。 

    - **利用**： 优化中使用，即使对于根据它们具有的任何屏幕和输入的特征的未知未来设备的特定设备的呈现
    - **利用**： 轻松地允许您跨所有设备类型-最小重复代码或工作量共享服务器端逻辑
    - **缺点**： 移动设备会因此不同于桌面版设备，你可能非常希望移动页是完全不同于桌面页面，显示不同的信息。 此类变体可能效率很低或不可能实现能够稳定地通过 CSS 独立的尤其要考虑如何不一致较旧的设备解释 CSS 规则。 这是 CSS 3 属性尤其如此。
    - **缺点**： 提供对不同的服务器端逻辑和适用于不同设备的工作流不支持。 例如，不能通过 CSS 单独实现的简化购物车签出工作流为移动用户。
    - **缺点**： 效率低下的带宽使用。 你的服务器可能要传输的标记和样式应用于所有可能的设备，即使目标设备将仅使用该信息的子集。
3. ***解决此问题在服务器上的*–** 服务器知道哪些设备正在访问它 – 或在该设备，例如，其屏幕大小和输入的法的最少的特征以及是否是移动设备-它可以运行不同的逻辑和输出不同的 HTML 标记。 

    - **优点：** 最大的灵活性。 没有任何限制到多少可以改变您的服务器端逻辑面向移动或优化您的标记所需的、 特定于设备的布局。
    - **优点：** 高效的带宽使用。 只需传输的标记和目标设备要使用的样式信息。
    - **缺点：** 有时会强制的工作或代码重复 （例如，使你创建的 Web 窗体页或 MVC 视图的类似但略有不同副本项）。 其中可能您应考虑常见逻辑基础层或服务，但仍，UI 代码或标记的某些部分可能要复制，然后同时维护。
    - **缺点：** 设备检测并非易事。 它要求的列表或已知的设备类型和它们的特征 （这可能始终无法完全保持最新） 的数据库，并且不能保证每个传入请求进行准确匹配。 本文档介绍一些选项和其缺陷更高版本。

若要获取最佳结果，大多数开发人员找到所需组合选项 (2) 和 (3)。 使用 CSS 或甚至 JavaScript 在客户端上最容纳样式的不同之处，而在服务器端代码中最有效地实现数据、 工作流或标记中的主要差异。

### <a name="this-paper-focuses-on-server-side-techniques"></a>本白皮书主要介绍服务器端技术

由于 ASP.NET Web 窗体和 MVC 这两种主要的服务器端技术，本白皮书将重点介绍服务器端的技巧，以帮助您生成不同的标记和移动浏览器的逻辑。 当然，还可以将此合并任何客户端技术 （例如，CSS 3 媒体查询，渐进式增强 JavaScript），但这是更多的是 web 设计的 ASP.NET 开发比。

## <a name="browser-and-device-detection"></a>浏览器和设备检测

有关支持的移动设备的所有服务器端方法的关键先决条件是知道您访问者使用哪些设备。 事实上，甚至更好了解该设备的制造商和型号的数知道*特征*的设备。 特征可能包括：

- 为移动设备？
- 输入的法 （鼠标/键盘、 触摸、 键盘、 游戏杆，...）
- 屏幕大小 （以物理方式和以像素为单位）
- 支持的媒体和数据格式
- 等等。

更好一些，因为做出决策基于特征与型号，则您将能够更好地处理的未来设备。

### <a name="using-aspnets-built-in-browser-detection-support"></a>使用 ASP。NET 的内置浏览器检测支持

ASP.NET Web 窗体和 MVC 开发人员可以立即发现正在访问的浏览器的重要特征，通过检查的属性*Request.Browser*对象。 有关示例，请参阅

- Request.Browser.IsMobileDevice
- Request.Browser.MobileDeviceManufacturer Request.Browser.MobileDeviceModel
- Request.Browser.ScreenPixelsWidth
- Request.Browser.SupportsXmlHttp
- ...和许多其他

在后台，ASP.NET 平台匹配传入*用户代理*(UA) HTTP 标头与一系列浏览器定义 XML 文件中的正则表达式。 默认情况下该平台包括许多常见的移动设备的定义，并可以将自定义浏览器定义文件添加为其他人想要识别。 有关更多详细信息，请参阅 MSDN 页面[ASP.NET Web 服务器控件和浏览器功能](https://msdn.microsoft.com/library/x3k2ssx2.aspx)。

### <a name="using-the-wurfl-device-database-via-51degreesmobi-foundation"></a>使用 WURFL 设备数据库通过 51Degrees.mobi Foundation

尽管 ASP。NET 的内置浏览器检测的支持足以满足许多应用程序，有两种主要情况时它可能不够：

- ***你想要识别的最新设备***（而无需手动创建它们的浏览器定义文件）。 请注意.NET 4 的浏览器定义文件不是不够高，无法识别 Windows Phone 7、 Android 手机、 Opera Mobile 浏览器或 Apple Ipad。
- ***你需要有关设备功能的更多详细的信息***。 可能需要了解的有关设备的输入法 （例如，触摸 vs 键盘），或哪些音频格式浏览器支持。 在标准的浏览器定义文件中，此信息不可用。

[*无线通用资源文件*(WURFL) 项目](http://wurfl.sourceforge.net/)维护更多最新信息和详细信息中使用的移动设备有关今天。

面向.NET 开发人员欣慰的是该 ASP。NET 的浏览器检测功能是可扩展的因此可以增强它，以解决这些问题。 例如，可以添加开放源代码[ *51Degrees.mobi Foundation* ](https://github.com/51Degrees/dotNET-Device-Detection)到你的项目的库。 它是一个 ASP.NET IHttpModule 或浏览器功能提供程序 （Web 窗体和 MVC 应用程序上可用），直接读取 WURFL 数据并将其挂钩到 ASP。NET 的内置浏览器检测机制。 安装该模块后*Request.Browser*突然将包含更准确、 最详细的信息： 它将正确识别的许多设备如前面所述，并列出其功能 （包括其他功能等输入法）。 请参阅更多详细信息的项目的文档。

## <a name="how-web-forms-applications-can-present-mobile-specific-pages"></a>Web 窗体应用程序可以如何提供移动特定页

默认情况下，下面是一个全新的 Web 窗体应用程序常见移动设备上的显示方式：

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image1.png)

很明显，既不布局看起来非常适合移动应用-此页专为大型的、 面向布局的监视器，不适用于较小的面向纵向的屏幕。 那么可以你如何做它？

如之前在本白皮书中所述，有很多种定制您的移动设备的页面。 一些技术是基于服务器的其他人在客户端上运行。

### <a name="creating-a-mobile-specific-master-page"></a>创建移动特定的母版页

具体取决于您的需求，您可能能够使用相同的 Web 窗体的所有访问者，但有两个单独的主页面： 一个用于桌面的访问者、 另一个用于移动访问者。 这样，你可以灵活地更改的 CSS 样式表或你的顶级 HTML 标记以适应移动设备，而不会迫使您可以复制任何页面逻辑。

这很容易地执行操作。 例如，可以将如下所示的 PreInit 处理程序添加到 Web 窗体：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample1.cs)]

现在，创建主页面在应用程序的顶级文件夹中调用 Mobile.Master 和将检测到移动设备时使用它。 如有必要，移动母版页可以引用特定于移动的 CSS 样式表。 桌面的访问者仍会看到默认主页面，一个不移动。

### <a name="creating-independent-mobile-specific-web-forms"></a>创建独立的特定于移动 Web 窗体

最大的灵活性，可以进一步得比只让不同设备类型的单独主页面。 您可以实现两个*完全不同的 Web 窗体页集*– 一个为桌面浏览器设置，另一个为设置移动设备。 此效果最佳，如果你想要向移动访客提供非常不同的信息或工作流。 本部分的其余部分将介绍这种方法在详细信息。

假设已设计用于桌面浏览器的 Web 窗体应用程序，以继续操作的最简单方法是创建您的项目内名为"Mobile"的子文件夹和生成移动页面存在。 您可以构造整个子站点，具有其自己的母版页、 样式表和页，使用完全相同，会使用任何其他 Web 窗体应用程序技术。 您不一定要生成移动等效于*每个*在桌面网站页上，你可以选择哪些功能的子集有意义的移动访问者。

移动页面可以共享公共静态资源 (如图像、 JavaScript 或 CSS 文件) 如果你想在正则页面使用。 由于"Mobile"文件夹将*不*标记作为单独的应用程序时承载于 IIS （它是只是 Web 窗体页的简单子文件夹），它将还共享所有相同的配置、 会话数据和其他基础结构，即你桌面的页数。

> [!NOTE]
> 由于这种方法通常涉及一些重复代码 （移动页面有可能与桌面页面共享一些相似之处），务必分离出任何常见业务逻辑或数据访问代码到共享的基础层或服务。 否则，你将双精度的创建和维护你的应用程序的工作量。


#### <a name="redirecting-mobile-visitors-to-your-mobile-pages"></a>重定向移动的访客移动页面

通常很方便为仅在重定向移动的访客移动页面*第一个*请求在其浏览会话中 （而不对其会话中的每个请求），因为：

- 然后，您可以轻松地允许移动访问者可以根据自己的意愿 – 只需将链接放上将转到"桌面版本"到母版页访问桌面页面。 访问者不会重定向回到移动页，因为它不能再在第一个请求在其会话。
- 它可避免干扰 （例如，如果必须在你的网站的桌面和移动部件会显示在 IFRAME 中或某些 Ajax 处理程序的常见 Web 窗体） 的你的站点的桌面和移动部分之间共享的所有动态资源的请求的风险

若要执行此操作，可以将放置在你重定向逻辑**会话\_启动**方法。 例如，将以下方法添加到 Global.asax.cs 文件：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample2.cs)]

#### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>配置窗体身份验证遵循移动页面

请注意窗体身份验证做出了假设，它可以将重定向访问者期间和之后的身份验证过程：

- 当用户需要进行身份验证时，窗体身份验证将它们重定向到您的桌面登录页，而不考虑它们是桌面或移动用户 (因为它仅有的概念*一个*登录 URL)。 假定你想要以不同方式设置您的移动登录页的样式，您需要增强您的桌面登录页，以便它将移动用户重定向到一个单独移动登录页面。 例如，以下代码添加到您**桌面**隐藏代码的登录页： 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample3.cs)]
- 用户成功登录后，窗体身份验证将默认情况下将它们重定向到桌面的主页 (因为它仅有的概念*一个*默认页)。 您需要增强您的移动登录页，以便它将重定向到移动主页后成功日志中。 例如，以下代码添加到您**移动**隐藏代码的登录页： 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample4.cs)]
  
  此代码假定您的页面具有名为 LoginUser，如下所示的默认项目模板的登录服务器控件。

### <a name="working-with-output-caching"></a>使用输出缓存

如果您使用输出缓存，请注意，默认情况下，它是桌面的用户可以访问特定 URL （导致要缓存其输出） 后, 跟然后接收缓存的桌面输出的移动用户。 无论是只是不同的主页面按设备类型，还是实现完全独立的 Web 窗体，每个设备类型，将应用此警告。

若要避免此问题，您可以指示 ASP.NET 来改变缓存项根据访问者是否正在使用移动设备。 将 VaryByCustom 参数添加到页面的 OutputCache 声明，如下所示：

[!code-aspx[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample5.aspx)]

接下来，定义*isMobileDevice*作为自定义缓存参数通过添加以下方法重写到 Global.asax.cs 文件：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample6.cs)]

这将确保移动到页面的访问者未收到以前桌面的访问者放入缓存的输出。

### <a name="a-working-example"></a>运行示例

若要查看这些技术中操作，请下载[本白皮书的代码示例](https://docs.microsoft.com/aspnet/mobile/overview)。 Web 窗体示例应用程序自动重定向到一组特定于移动的页名为移动的子文件夹中的移动用户。 您可以看到与以下屏幕截图针对移动浏览器，更好地优化的标记和这些页面的样式：

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image2.png)

有关针对移动浏览器优化您的标记和 CSS 的信息的更多技巧，请参阅"样式移动页针对移动浏览器"在本文档后面的部分。

## <a name="how-aspnet-mvc-applications-can-present-mobile-specific-pages"></a>ASP.NET MVC 应用程序可以如何提供移动特定页

由于模型-视图-控制器模式将 （在控制器） （在视图中） 的表示逻辑从应用程序逻辑中分离出来，你可以处理在服务器端代码中的移动支持到选择从任何以下方法之一：

1. ***对于桌面和移动浏览器，使用相同的控制器和视图，但呈现的视图具有不同的 Razor 布局，具体取决于设备类型 *。** 如果要在所有设备上显示相同的数据，但只是想要提供不同的 CSS 样式表或更改的几个面向移动的顶级 HTML 元素，此选项效果最佳。
2. ***对于桌面和移动浏览器，使用相同的控制器，但呈现不同的视图，具体取决于设备类型***。 如果您是显示大致相同的数据并提供相同的工作流对于最终用户，此选项效果最佳，但想要呈现非常不同的 HTML 标记，以满足所用设备。
3. ***创建桌面和移动浏览器，为每个实现独立的控制器和视图的单独区域 *。** 如果您是显示非常不同的屏幕、 包含不同的信息并导致用户针对其设备类型进行了优化的不同工作流完成时，此选项效果最佳。 这可能意味着一些重复代码，但你可以最小化它通过分离出常见逻辑到基础层或服务。

如果你想要采取**第一个**选项以及更改仅 Razor 布局每种设备类型，它是非常简单。 只需修改你\_ViewStart.cshtml 文件，如下所示：

[!code-cshtml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample7.cshtml)]

现在，你可以创建一种称为移动特定布局\_LayoutMobile.cshtml 与页结构和 CSS 规则针对移动设备进行了优化。

如果你想要采取**第二个**选项根据访问者的设备类型的呈现器完全不同视图，请参阅[Scott Hanselman 的博客文章](http://www.hanselman.com/blog/ABetterASPNETMVCMobileDeviceCapabilitiesViewEngine.aspx)。

本白皮书的其余部分重点介绍**第三个**选项 – 创建单独的控制器*和*移动设备 – 以便您可以控制完全移动访客提供哪些功能的子集的视图。

### <a name="setting-up-a-mobile-area-within-your-aspnet-mvc-application"></a>在 ASP.NET MVC 应用程序中的移动区域设置

您可以添加以正常方式调用"移动"到现有的 ASP.NET MVC 应用程序的区域： 右键单击项目名称在解决方案资源管理器，然后选择添加-> 区域。 根据需要对 ASP.NET MVC 应用程序内的任何其他区域，然后可以添加控制器和视图。 例如，将添加到您移动的区域的新控制器名为 HomeController，将其用作主页移动访客。

### <a name="ensuring-the-url-mobile-reaches-the-mobile-homepage"></a>确保 URL 网站达到移动主页

如果你想要访问在您移动的区域内 HomeController 的索引操作的 URL 网站，您需要对路由配置进行两个较小的更改。 首先，更新 MobileAreaRegistration 类以便 HomeController 默认控制器在您移动的区域，如下面的代码中所示：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample8.cs)]

这意味着移动主页现在将位于的网站，而不是移动/主页，因为"Home"现在是隐式的移动页的默认控制器名称。

接下来，请注意，通过将第二个 HomeController 添加到你的应用程序 （即，移动的一个，除了一个现有的桌面），在将已中断了常规桌面主页。 它将失败并出现错误"*找到多个类型符合名为 Home 控制器*"。 若要解决此问题，更新顶层路由配置 （在 Global.asax.cs) 指定多义性时，桌面 HomeController 的执行优先级：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample9.cs)]

现在，该错误会随手可得，，URL http://<em>yoursite</em>/ 桌面主页和 http:// 将到达<em>yoursite</em>/mobile/ 将到达移动的主页。

### <a name="redirecting-mobile-visitors-to-your-mobile-area"></a>重定向到您移动的区域的移动访问者

有许多不同的扩展点在 ASP.NET MVC 中，因此有许多种方法，以插入重定向逻辑。 一种巧妙方法是创建一个筛选器属性，[RedirectMobileDevicesToMobileArea] 执行的重定向，如果满足以下条件：

1. 它是用户的会话中的第一个请求 （即，Session.IsNewSession 等于 true）
2. 请求来自移动浏览器 （即，Request.Browser.IsMobileDevice 等于 true）
3. 用户已不请求移动的区域中的资源 (即*路径*与网站的 URL 的一部分不会开始)

此白皮书随附的可下载示例包含一个实现，此逻辑。 它作为授权筛选器，从 AuthorizeAttribute，这意味着它可以正常起作用，即使您使用输出缓存 （否则为如果桌面的访问者首次访问特定 URL，桌面输出可能会缓存，然后提供给派生实现后续移动访问者）。

由于它是一个筛选器，您可以选择将其应用到特定控制器和操作，例如，

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample10.cs)]

… 也可以为 MVC 3 应用它的所有控制器和操作*全局筛选器*Global.asax.cs 文件中：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample11.cs)]

可下载的示例还演示了如何创建此属性将重定向到您移动的区域中的特定位置的子类。 例如，这意味着您可以：

- 注册全局筛选器如下所示更高版本，默认情况下发送到移动主页的移动访问者。
- 也适用于采用移动到具有请求的任何产品页面的移动版本的访问者的"查看产品"操作的特殊 [RedirectMobileDevicesToMobileProductPage] 筛选器。
- 也适用于特定操作，将重定向到等效的移动页的移动访问者的筛选器的其他特殊子类

### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>配置窗体身份验证遵循移动页面

如果使用的窗体身份验证，则应注意，当用户需要登录时，它会自动将用户重定向到单个特定"登录"的 URL，即默认情况下 **/帐户/登录**。 这意味着可能会移动用户重定向到你的桌面"登录"操作。

若要避免此问题，请将逻辑添加到桌面"登录"操作，以便它将重定向移动用户再次到"登录"的移动操作。 如果使用默认 ASP.NET MVC 应用程序模板，请按如下所示更新 AccountController 的登录操作：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample12.cs)]

… 然后在您移动的区域中称为 AccountController 的控制器上实现一个适合移动特定"登录"操作。

### <a name="working-with-output-caching"></a>使用输出缓存

如果你使用 [OutputCache] 筛选器，必须强制执行要因设备类型的缓存项。 例如，编写：

[!code-javascript[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample13.js)]

然后，将以下方法添加到 Global.asax.cs 文件：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample14.cs)]

这将确保移动到页面的访问者未收到以前桌面的访问者放入缓存的输出。

### <a name="a-working-example"></a>运行示例

若要查看这些技术中操作，请下载[此白皮书代码关联示例](https://docs.microsoft.com/aspnet/mobile/overview)。 此示例包含了增强，可支持移动设备使用上面所述的方法的 ASP.NET MVC 3 （候选发布） 应用程序。

## <a name="further-guidance-and-suggestions"></a>更多指导和建议

下面的讨论同时适用于 Web 窗体和 MVC 开发人员使用本文档中介绍的技术。

### <a name="enhancing-your-redirection-logic-using-51degreesmobi-foundation"></a>增强你使用 51Degrees.mobi Foundation 的重定向逻辑

本文档中所示的重定向逻辑可以完全满足您的应用程序，但它不起作用，如果你需要禁用会话，或与拒绝 （它们不能具有会话） cookie，因为它不会知道是否给定请求的移动浏览器第一个从该访问者。

您已经了解开放源代码 51Degrees.mobi Foundation 可以如何改进 ASP 的准确性。NET 的浏览器检测。 它还具有一项内置功能将重定向到在 Web.config 中配置的特定位置的移动访问者。可以在无需具体取决于 ASP.NET 会话 (并因此 cookie) 通过将存储的哈希值的访问者的 HTTP 标头和 IP 地址的临时日志，因此它知道每个请求是否是从给定见的第一个。

以下元素添加到 web.config 文件的 fiftyOne 部分将重定向到的页检测到的移动设备从第一个请求 ~ / Mobile/Default.aspx。 对移动文件夹下的页面的任何请求将*不*重定向，而不考虑设备类型。 如果移动设备已被一段非活动状态 20 分钟或更多设备的系统将忘记和后续请求将被视为新的重定向的目的。

[!code-xml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample15.xml)]

有关更多详细信息，请参阅[51degrees.mobi Foundation 文档](https://github.com/51Degrees/dotNET-Device-Detection)。

> [!NOTE]
> 您*可以*使用 51Degrees.mobi Foundation 重定向功能在 ASP.NET MVC 应用程序，但您将需要定义您在普通的 Url，不是作为路由参数或通过将置于 MVC 筛选器方面的重定向配置上的操作。 这是因为 （在撰写本文时） 51Degrees.mobi Foundation 不能识别筛选器或路由。


### <a name="disabling-transcoders-and-proxy-servers"></a>禁用转码器和代理服务器

移动网络运营商在其移动 internet 方法中具有两个广泛的目标：

1. 提供作为尽可能得多相关内容
2. 最大程度提高可共享的有限的广播网络带宽的客户数

由于大多数 web 页面为大尺寸桌面屏幕和快速修复行宽带连接设计，使用很多运算符*转码器*或*代理服务器*动态更改 web 内容。 它们可能会修改你的 HTML 标记或 CSS 以适合较小的屏幕 （尤其是对于"功能手机"缺少的处理能力来处理复杂的布局的），并且它们可能会重新压缩映像 （显著减少其质量） 以提高页传递速度。

但如果您执行了生成移动优化你的站点版本的工作，您可能不希望要进行干预任何进一步的网络运算符。 可以将以下行添加到页面\_任何 ASP.NET Web 窗体中的 Load 事件：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample16.cs)]

或者，为 ASP.NET MVC 控制器，你可以添加以下方法重写，以便它适用于该控制器上的所有操作：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample17.cs)]

生成的 HTTP 消息通知 W3C 兼容转码器和代理服务器不以更改内容。 当然，就移动网络运营商将遵守此消息不能保证。

### <a name="styling-mobile-pages-for-mobile-browsers"></a>针对移动浏览器样式移动页面

它不在范围内的此文档，以详细说明哪些类型的 HTML 标记工作正确或哪些 web 设计技术最大限度地在特定设备上的可用性。 它已经注册到你要查找足够简单的布局，优化移动大小的屏幕，而无需使用不可靠 HTML 或 CSS 定位技巧。 但是，是一个重要的技术，值得一提的是，*视区 meta 标记*。

某些新型移动浏览器，适用于桌面监视器，工作量显示网页中的呈现在虚拟的画布上，也称为"视区"页面 （例如，虚拟视区是 980 像素宽，在 iPhone 和 850 像素宽 Opera Mobile 在默认情况下），然后缩减结果以适合屏幕的物理像素。 用户可以然后缩放和平移围绕该视区。 这样做的好处，它允许在其预期布局中显示页面的浏览器，但它也是具有它会强制缩放和平移，这对于用户是不方便的缺点。 如果您正在设计的移动，最好是设计为窄的屏幕，以便有必要采取任何缩放或水平滚动。

指出在移动浏览器宽度应是视区的方法是通过使用了非标准*视区*meta 标记。 例如，如果您将以下代码添加到页面的 HEAD 部分中，

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample18.html)]

… 然后支持智能手机浏览器将布局 480 像素范围虚拟画布上的页面。 这意味着，如果你的 HTML 元素以百分比表示定义其宽度，百分比将解释相对于此 480 像素宽度，不默认视区宽度。 因此，用户很少需要缩放和平移水平 – 显著提高的移动浏览体验。

如果你想要匹配设备的物理像素的视区宽度，您可以指定以下各项：

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample19.html)]

此才能正常工作，您必须显式强制元素超过该宽度 (例如，使用*宽度*属性或 CSS 属性)，否则在浏览器将强制使用更大的视区而不考虑。 另请参阅：[更多详细信息使用了非标准的视区标记](https://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html)。

支持大多数现代智能手机*双方向*： 它们可以保存在纵向或横向模式中。 因此，务必不要假设屏幕宽度以像素为单位。 不要甚至假设屏幕宽度的固定不变，因为用户可以在页面上，则重定向其设备。

页标头以通知其内容中的以下元标记已针对移动进行优化，因此不应转换，可能会也接受较旧的 Windows Mobile 和 Blackberry 设备。

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample20.html)]

## <a name="additional-resources"></a>其他资源

有关移动设备仿真程序和模拟器可用于测试移动的 ASP.NET web 应用程序的列表，请参阅页面[模拟常用移动设备进行测试](../mobile/device-simulators.md)。

## <a name="credits"></a>信用

- 主要作者： Steven Sanderson
- 审阅者 / 其他内容作者： James Rosewell、 Mikael Söderström、 Scott Hanselman、 Scott Hunter
