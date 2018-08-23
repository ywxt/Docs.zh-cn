---
uid: single-page-application/overview/templates/hottowel-template
title: 热 Towel 模板 |Microsoft Docs
author: madskristensen
description: HotTowel 模板
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: b80b5940b5733a0ae2af3491ccdfa05b84b50343
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833735"
---
<a name="hot-towel-template"></a>Hot Towel 模板
====================
通过[Mads Kristensen](https://github.com/madskristensen)

> John papa 编写热总是随身携带毛巾 MVC 模板
> 
> 选择要下载哪个版本：
> 
> [适用于 Visual Studio 2012 的热总是随身携带毛巾 MVC 模板](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [Visual Studio 2013 的热总是随身携带毛巾 MVC 模板](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> 热总是随身携带毛巾： 因为不想要转到没有 SPA ！


想要生成 SPA，但不能确定从何处着手？ 使用热总是随身携带毛巾，以秒为单位，您将得到一个 SPA 和其上构建所需的所有工具 ！

热总是随身携带毛巾创建用于构建单页应用程序 (SPA) 使用 ASP.NET 的良好起点。 现成的它提供模块化结构为代码、 查看导航、 数据绑定、 丰富的数据管理和简单但简洁的样式设置。 热总是随身携带毛巾提供构建 SPA，因此你可以专注于应用，不的基本功能所需的所有内容。

> 深入了解如何构建从 SPA [John Papa 视频、 教程和 Pluralsight 课程](http://johnpapa.net/spa?vsix)。


## <a name="application-structure"></a>应用程序结构

热总是随身携带毛巾 SPA 提供应用程序文件夹，其中包含定义你的应用程序的 JavaScript 和 HTML 文件。

在应用程序文件夹的内容：

- Durandal
- 服务
- viewmodel
- 视图

应用程序文件夹中包含模块的集合。 这些模块封装功能，并在其他模块中声明的依赖关系。 视图文件夹包含你的应用程序的 HTML，viewmodels 文件夹包含视图 （常用的 MVVM 模式） 的表示逻辑。 服务文件夹非常适合用于容纳任何公用服务，这些应用程序可能需要等 HTTP 数据检索或本地存储的交互。 它是常见的多个 viewmodel 重新使用服务模块中的代码。

## <a name="aspnet-mvc-server-side-application-structure"></a>ASP.NET MVC 服务器端应用程序结构

热总是随身携带毛巾基于熟悉且功能强大的 ASP.NET MVC 结构。

- 应用\_开始
- 内容
- Controllers
- 模型
- 脚本
- 视图

## <a name="featured-libraries"></a>特色的库

- ASP.NET MVC
- ASP.NET Web API
- ASP.NET Web 优化的绑定和缩减
- [Breeze.js](http://Breezejs.com) -丰富的数据管理
- [Durandal.js](http://Durandaljs.com) -导航和视图构成
- [Knockout.js](http://Knockoutjs.com) -数据绑定
- [Require.js](http://requirejs.org) -模块使用 AMD 和优化
- [Toastr.js](http://jpapa.me/c7toastr)的弹出消息
- [Twitter Bootstrap](http://twitter.github.com/bootstrap/) -功能强大的 CSS 样式

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a>通过 Visual Studio 2012 热总是随身携带毛巾 SPA 模板安装

热总是随身携带毛巾可以安装为 Visual Studio 2012 模板。 只需单击`File`  |  `New Project` ，然后选择`ASP.NET MVC 4 Web Application`。 然后选择热总是随身携带毛巾单页面应用程序"模板并运行 ！

## <a name="installing-via-the-nuget-package"></a>通过 NuGet 包安装

热总是随身携带毛巾也是一个 NuGet 包，增加现有空 ASP.NET MVC 项目的内容。 只需使用 Nuget 安装并运行 ！

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a>如何生成热总是随身携带毛巾？

只需启动添加代码 ！

1. 添加你自己的服务器端代码，最好是实体框架和 WebAPI （其中的亮点在于与 Breeze.js）
2. 添加到视图`App/views`文件夹
3. 添加到 viewmodel`App/viewmodels`文件夹
4. 将 HTML 和 Knockout 数据绑定添加到你的新视图
5. 更新中的导航路由 `shell.js`

## <a name="walkthrough-of-the-htmljavascript"></a>HTML/JavaScript 的演练

### <a name="viewshottowelindexcshtml"></a>Views/HotTowel/index.cshtml

index.cshtml 是起始路由和视图的 MVC 应用程序。 它包含所有标准 meta 标记、 css 链接和你所期望的 JavaScript 引用。 正文包含一个`<div>`即全部内容 （视图） 将在要求时放置。 `@Scripts.Render` Require.js 用于运行中包含的应用程序的代码的入口点`main.js`文件。 提供初始屏幕是为了演示如何创建初始屏幕，您的应用程序加载时。

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a>App/main.js

`main.js`文件包含将运行您的应用程序加载的代码。 这是你想要定义导航路由、 设置视图，你启动和执行任何安装程序/启动如填充应用程序的数据。

`main.js`文件定义了多个 durandal 的模块，以帮助启动应用程序启动。 定义语句可帮助解决模块依赖项，以便它们可为函数。 首次启用调试消息，该发送哪些事件的消息应用程序执行到控制台窗口。 在 app.start 代码指示 durandal 框架在启动应用程序。 以便 durandal 知道所有视图和 viewmodel 分别包含在同一个命名的文件夹中，设置约定。 最后，`app.setRoot`介入负载`shell`使用一个预定义`entrance`动画。

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a>视图

视图中找到`App/views`文件夹。

### <a name="shellhtml"></a>shell.html

`shell.html`包含在 HTML 母版布局。 将角的某个位置构成所有其他视图在`shell`视图。 提供了热总是随身携带毛巾`shell`具有三个这样的区域： 标头、 内容区域和页脚。 每个区域将以加载内容构成请求时的其他视图。

`compose`页眉和页脚的绑定是硬编码在热总是随身携带毛巾以指向`nav`和`footer`视图，分别。 部分中的 compose 绑定`#content`绑定到`router`模块的活动项。 换而言之，当您单击时它是对应的视图的导航链接加载在此区域中。

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a>nav.html

`nav.html` Spa 包含导航链接。 这是菜单结构可以放置的位置，例如。 通常是数据绑定 （使用 Knockout） 到`router`模块来显示中定义的导航`shell.js`。 Knockout 将会查找数据绑定属性，并将绑定到`shell`viewmodel 来显示导航路线并显示进度栏 （使用 Twitter Bootstrap） 如果`router`模块正在进行从一个视图导航到另一个 （请参阅`router.isNavigating`).

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a>home.html 和 details.html

对于自定义视图，这些视图包含 HTML。 当`home`中的链接`nav`单击视图的菜单时，`home`视图将位于的内容区域`shell`视图。 这些视图可以增强或替换为你自己的自定义视图。

### <a name="footerhtml"></a>footer.html

`footer.html`包含在页脚中，在底部显示的 HTML`shell`视图。

## <a name="viewmodels"></a>ViewModels

Viewmodel 中找到`App/viewmodels`文件夹。

### <a name="shelljs"></a>shell.js

`shell` Viewmodel 包含属性和绑定到的函数`shell`视图。 通常这是在其中找到菜单导航绑定 (请参阅`router.mapNav`逻辑)。

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a>home.js 和 details.js

这些 viewmodel 包含的属性和绑定到的函数`home`视图。 它还包含表示逻辑视图，并且数据与视图之间的胶水。

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a>服务

在应用/服务文件夹中找到服务。 理想情况下无法放置如 dataservice 模块，负责获取和发送远程数据，您将来的服务。

### <a name="loggerjs"></a>logger.js

提供了热总是随身携带毛巾`logger`服务文件夹中的模块。 `logger`模块非常适合于日志记录消息到控制台和弹出 toast 中的用户。
