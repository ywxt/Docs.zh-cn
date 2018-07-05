---
uid: mvc/overview/performance/bundling-and-minification
title: 捆绑和缩小 |Microsoft Docs
author: Rick-Anderson
description: 捆绑和缩小是两种方法在 ASP.NET 4.5 中用于提高请求加载时间。 捆绑和缩小 reducin 通过提高加载时间...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/23/2012
ms.topic: article
ms.assetid: 5894dc13-5d45-4dad-8096-136499120f1d
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/performance/bundling-and-minification
msc.type: authoredcontent
ms.openlocfilehash: 4f21184f0917cd957e9e1719c63769e1a027961c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384772"
---
<a name="bundling-and-minification"></a>捆绑和缩小
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> 捆绑和缩小是两种方法在 ASP.NET 4.5 中用于提高请求加载时间。 捆绑和缩小的请求数减少到服务器并减少请求的资产 （如 CSS 和 JavaScript。） 的大小，从而提高加载时间


当前的主流浏览器的大多数限制的数量[同时连接](http://www.browserscope.org/?category=network)每六个到每个主机名。 这意味着，所处理的六个请求，同时在主机上的资产的其他请求将排队等候，由浏览器。 下图中的 IE F12 开发人员工具网络选项卡显示了示例应用程序的关于视图所需的资产的计时。

![B/M](bundling-and-minification/_static/image1.png)

灰色条形显示请求排队等待六个连接限制浏览器的时间。 黄色条为第一个字节的请求时间，即发送请求并接收来自服务器的第一个响应所花的时间。 蓝色条显示从服务器收到响应数据所花的时间。 你可以双击资产中，以获取详细的计时信息。 例如下, 图显示加载的计时详细信息 */Scripts/MyScripts/JavaScript6.js*文件。

![](bundling-and-minification/_static/image2.png)

以上图像所示**启动**事件，其中给出了由于浏览器的请求已排入队列的时间限制同时连接数。 在这种情况下，请求已排队等待 46 毫秒内等待另一个请求完成。

## <a name="bundling"></a>捆绑

捆绑是 ASP.NET 4.5，轻松地组合或多个文件捆绑到一个文件中的新功能。 您可以创建 CSS、 JavaScript 和其他捆绑包。 更少的文件意味着较少的 HTTP 请求，可以提高第一个页面加载性能。

下图显示了关于视图显示以前，但这次使用捆绑和缩小已启用的同一个计时视图。

![](bundling-and-minification/_static/image3.png)

## <a name="minification"></a>缩小

缩小执行各种不同的代码优化脚本或 css，如删除不必要的空格和提出的意见并缩短为一个字符的变量名称。 请考虑以下的 JavaScript 函数。

[!code-javascript[Main](bundling-and-minification/samples/sample1.js)]

后缩小，函数会减少所示：

[!code-javascript[Main](bundling-and-minification/samples/sample2.js)]

除了删除注释和不必要的空格，以下参数和变量名称已重命名 （缩短），如下所示：

| **源语言** | **重命名** |
| --- | --- |
| imageTagAndImageID | n |
| imageContext | t |
| imageElement | i |

## <a name="impact-of-bundling-and-minification"></a>影响的捆绑和缩小

下表显示了单独列出所有资产并在示例程序中使用绑定和缩减 (B/M) 的几个重要区别。

|  | **使用 B/M** | **而无需 B/M** | **更改** |
| --- | --- | --- | --- |
| **文件请求** | 9 | 34 | 256% |
| **发送的 KB** | 3.26 | 11.92 | 266% |
| **接收到的 KB** | 388.51 | 530 | 36% |
| **加载时间** | 510 MS | 780 MS | 53% |

发送的字节数必须与捆绑的浏览器将它们应用请求的 HTTP 标头包含的非常详细的显著降低。 接收的字节减少不是大因为最大的文件 (*Scripts\jquery-ui-1.8.11.min.js*并*Scripts\jquery-1.7.1.min.js*) 已缩小。 注意： 示例程序使用计时[Fiddler](http://www.fiddler2.com/fiddler2/)工具来模拟慢速网络。 (从 Fiddler**规则**菜单中，选择**性能**然后**模拟调制解调器速度**。)

## <a name="debugging-bundled-and-minified-javascript"></a>调试捆绑的和缩减 JavaScript

很容易地调试在开发环境中的 JavaScript (其中[compilation 元素](https://msdn.microsoft.com/library/s10awwz0.aspx)中*Web.config*文件设置为`debug="true"`) 由于未捆绑 JavaScript 文件或缩小。 此外可以调试版本生成的 JavaScript 文件会捆绑的和缩减。 使用 IE F12 开发人员工具，调试在缩小的绑定使用以下方法中包含的 JavaScript 函数：

1. 选择**脚本**选项卡，然后选择**开始调试**按钮。
2. 选择包含你想要使用的资产按钮进行调试的 JavaScript 函数的绑定。  
    ![](bundling-and-minification/_static/image4.png)
3. 选择格式缩减的 JavaScript**配置按钮** ![](bundling-and-minification/_static/image5.png)，然后选择**格式 JavaScript**。
4. 在中**搜索脚本**t 输入的框中，选择你想要调试的函数的名称。 在下图中， **AddAltToImg**中输入**搜索脚本**t 输入的框。  
    ![](bundling-and-minification/_static/image6.png)

有关使用 F12 开发人员工具进行调试的详细信息，请参阅 MSDN 文章[使用 F12 开发人员工具调试 JavaScript 错误](https://msdn.microsoft.com/library/ie/gg699336(v=vs.85).aspx)。

## <a name="controlling-bundling-and-minification"></a>控制捆绑和缩小

启用或禁用的值中的调试属性设置绑定和缩减[compilation 元素](https://msdn.microsoft.com/library/s10awwz0.aspx)中*Web.config*文件。 在下面的 XML，`debug`设置为 true，因此捆绑和缩小功能被禁用。

[!code-xml[Main](bundling-and-minification/samples/sample3.xml?highlight=2)]

若要启用捆绑和缩小，设置`debug`值为"false"。 您可以重写*Web.config*设置，并`EnableOptimizations`属性`BundleTable`类。 以下代码启用捆绑和缩小和重写中的任何设置*Web.config*文件。

[!code-csharp[Main](bundling-and-minification/samples/sample4.cs?highlight=7)]

> [!NOTE]
> 除非`EnableOptimizations`是`true`或中的调试属性[compilation 元素](https://msdn.microsoft.com/library/s10awwz0.aspx)中*Web.config*文件设置为`false`，文件将不捆绑或缩小。 此外，将不使用.min 版本文件，将选择完整的调试版本。 `EnableOptimizations` 重写中的调试属性[compilation 元素](https://msdn.microsoft.com/library/s10awwz0.aspx)中*Web.config*文件


## <a name="using-bundling-and-minification-with-aspnet-web-forms-and-web-pages"></a>使用绑定和缩减与 ASP.NET Web 窗体和 Web Pages

- 有关 Web 页，请参阅博客文章[添加到 Web Pages 站点的 Web 优化](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx)。
- Web 窗体，请参阅博客文章[添加绑定和缩减到 Web 窗体](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx)。

## <a name="using-bundling-and-minification-with-aspnet-mvc"></a>使用捆绑和缩小使用 ASP.NET MVC

在本部分中我们将创建 ASP.NET MVC 项目，以检查捆绑和缩小。 首先，创建一个名为的新 ASP.NET MVC internet 项目**MvcBM**无需更改任何默认值。

打开*应用程序\_Start\BundleConfig.cs*文件并检查`RegisterBundles`方法用于创建、 注册和配置捆绑包。 下面的代码显示了部分`RegisterBundles`方法。

[!code-csharp[Main](bundling-and-minification/samples/sample5.cs)]

上面的代码创建名为新的 JavaScript 捆绑 *~/bundles/jquery* ，其中包含所有相应 (为调试或缩减的但不是。*vsdoc*) 中的文件*脚本*通配符字符串"~/Scripts/jquery-{version}.js"相匹配的文件夹。 对于 ASP.NET MVC 4 中，这意味着使用调试配置时，该文件*jquery 1.7.1.js*将添加到此捆绑包。 在发布配置中， *jquery 1.7.1.min.js*将添加。 捆绑 framework 如遵循几个常见约定：

- "FileX.min.js"和"FileX.js"存在时，请选择".min"文件版本。
- 选择调试的非".min"版本。
- 忽略"-vsdoc"文件 （例如 jquery-1.7.1-vsdoc.js)，IntelliSense 仅使用它们。

`{version}`通配符匹配如上所示用于自动创建具有合适版本的中的 jQuery 的 jQuery 捆绑你*脚本*文件夹。 在此示例中，使用通配符提供以下优势：

- 可以使用 NuGet 更新到较新的 jQuery 版本，而无需更改上述绑定代码或在视图页面中的 jQuery 引用。
- 自动选择用于调试配置的完整版本和发布的".min"版本生成。

## <a name="using-a-cdn"></a>使用 CDN

 下面的代码将替换为 CDN 的 jQuery 捆绑本地 jQuery 捆绑包。

[!code-csharp[Main](bundling-and-minification/samples/sample6.cs)]

在上述代码中，将 jQuery 请求从 CDN 这是在版本模式和 jQuery 的调试版本将提取本地在调试模式下时。 在使用 CDN，你应 CDN 请求失败的情况下可以回退机制。 以下标记片段从添加请求 jQuery 如果 CDN 故障的布局文件显示了脚本的末尾。

[!code-cshtml[Main](bundling-and-minification/samples/sample7.cshtml?highlight=5-13)]

## <a name="creating-a-bundle"></a>创建一个捆绑包

[捆绑](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx)类`Include`方法采用字符串数组，其中每个字符串是资源的虚拟路径。 下面的代码中的 RegisterBundles 方法从*应用程序\_Start\BundleConfig.cs*文件演示如何将多个文件添加到一个捆绑包：

[!code-csharp[Main](bundling-and-minification/samples/sample8.cs)]

[捆绑](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx)类`IncludeDirectory`提供方法以添加一个目录 （以及根据需要所有子目录） 中的搜索模式匹配的所有文件。 [捆绑](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx)类`IncludeDirectory`API 如下所示：

[!code-csharp[Main](bundling-and-minification/samples/sample9.cs)]

使用 Render 方法中，视图中引用捆绑包 ( `Styles.Render` css 和`Scripts.Render`javascript)。 中的以下标记*views/shared\\_Layout.cshtml*文件显示默认 ASP.NET internet 项目视图如何引用 CSS 和 JavaScript 的捆绑包。

[!code-cshtml[Main](bundling-and-minification/samples/sample10.cshtml?highlight=5-6,11)]

请注意，呈现方法采用数组的字符串，因此你可以在一行代码中添加多个捆绑包。 通常，您将想要使用创建所需的 HTML 引用资产的呈现方法。 可以使用`Url`方法以生成资产的 URL，而引用资产所需的标记。 假设你想要使用新的 HTML5[异步](http://www.whatwg.org/specs/web-apps/current-work/#attr-script-async)属性。 下面的代码演示如何引用 modernizr 使用`Url`方法。

[!code-cshtml[Main](bundling-and-minification/samples/sample11.cshtml?highlight=11)]

## <a name="using-the--wildcard-character-to-select-files"></a>使用"\*"通配符字符，可以选择文件

中指定的虚拟路径`Include`方法，并搜索模式中`IncludeDirectory`方法可接受一个"\*"通配符字符作为前缀或后缀中的最后路径段。 不区分大小写的搜索字符串。 `IncludeDirectory`方法具有的搜索子目录选项。

使用以下 JavaScript 文件，请考虑一个项目：

- *Scripts\Common\AddAltToImg.js*
- *Scripts\Common\ToggleDiv.js*
- *Scripts\Common\ToggleImg.js*
- *Scripts\Common\Sub1\ToggleLinks.js*

![dir imag](bundling-and-minification/_static/image7.png)

下表显示添加到使用通配符，如所示的捆绑的文件：

| **Call** | **添加文件或引发异常** |
| --- | --- |
| Include("~/Scripts/Common/\*.js") | *AddAltToImg.js，ToggleDiv.js，ToggleImg.js* |
| Include("~/Scripts/Common/T\*.js") | 无效的模式的异常。 通配符字符只能在前缀或后缀上。 |
| Include("~/Scripts/Common/\*og.\*") | 无效的模式的异常。 允许将只有一个通配符字符。 |
| "Include("~/Scripts/Common/T\*") | *ToggleDiv.js ToggleImg.js* |
| "Include("~/Scripts/Common/\*") | 无效的模式的异常。 纯通配符段不是有效的。 |
| IncludeDirectory("~/Scripts/Common", "T\*") | *ToggleDiv.js ToggleImg.js* |
| IncludeDirectory("~/Scripts/Common", "T\*",true) | *ToggleDiv.js，ToggleImg.js，ToggleLinks.js* |

显式将每个文件添加到一个捆绑包是通常优先通过通配符加载的文件的原因如下：

- 将脚本通过通配符的默认值添加到按字母顺序，通常不是你想要加载它们。 经常需要 （非字母） 特定的顺序添加 CSS 和 JavaScript 文件。 您可以通过添加自定义来缓解此风险[为 IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx)的实现，而显式添加每个文件都不容易出错。 例如，您可能添加的文件夹在将来它可能需要您修改的新资产你[为 IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx)实现。
- 查看特定文件添加到使用加载的通配符为目录可以包含在引用该捆绑包的所有视图。 如果查看特定脚本添加到一个捆绑包，可能会引用此捆绑包的其他视图的 JavaScript 错误。
- 导入其他文件的 CSS 文件导致导入的文件加载了两次。 例如，下面的代码的大部分加载两次的 jQuery UI 主题 CSS 文件创建一个捆绑包。 

    [!code-csharp[Main](bundling-and-minification/samples/sample12.cs)]

  通配符选择器"\*.css"的文件夹中，每个 CSS 文件中将包括*Content\themes\base\jquery.ui.all.css*文件。 *Jquery.ui.all.css*文件导入其他 CSS 文件。

## <a name="bundle-caching"></a>捆绑包缓存

捆绑包设置创建捆绑包时从 HTTP 过期标头一年。 如果导航到以前查看过的页上，Fiddler 显示 IE 不会进行条件请求捆绑包，即，有 IE 的捆绑包中没有 HTTP GET 请求和来自服务器的任何 HTTP 304 响应。 您可以强制 IE 以便每个捆绑包的条件请求 （导致 HTTP 304 响应的每个捆绑包） 的 F5 键。 可以使用强制完全刷新 ^ F5 （导致每个捆绑包的 HTTP 200 响应）。

下图显示**Caching** Fiddler 响应窗格的选项卡：

![fiddler 缓存图像](bundling-and-minification/_static/image8.png)

请求   
`http://localhost/MvcBM_time/bundles/AllMyScripts?v=r0sLDicvP58AIXN_mc3QdyVvVj5euZNzdsa2N1PKvb81`  
 是捆绑包**AllMyScripts**和包含查询字符串对**v = r0sLDicvP58AIXN\_mc3QdyVvVj5euZNzdsa2N1PKvb81**。 查询字符串**v**令牌，它是用于缓存的唯一标识符的值。 ASP.NET 应用程序，只要绑定不会更改，将请求**AllMyScripts**捆绑在一起使用此令牌。 如果在绑定中的任何文件发生更改，ASP.NET 优化框架将生成新的令牌，确保捆绑包的浏览器请求将获取最新的捆绑包。

如果运行 IE9 F12 开发人员工具，并导航到先前加载的页面，IE 错误地显示对每个捆绑包和返回 HTTP 304 服务器所做的条件性 GET 请求。 你可以阅读 IE9 具有确定是否在博客文章中创建条件的请求是问题的原因[使用 Cdn 和提高网站性能的 Expires](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)。

## <a name="less-coffeescript-scss-sass-bundling"></a>较低，CoffeeScript、 SCSS，Sass 捆绑。

捆绑和缩小 framework 提供了一种机制来处理中间语言，如[SCSS](http://sass-lang.com/)， [Sass](http://sass-lang.com/)，[较少](http://www.dotlesscss.org/)或[Coffeescript](http://coffeescript.org/)，并将如缩小转换应用到生成的捆绑包。 例如，若要添加[.less](http://www.dotlesscss.org/)到 MVC 4 项目的文件：

1. 创建更少内容的文件夹。 下面的示例使用*Content\MyLess*文件夹。
2. 添加[.less](http://www.dotlesscss.org/) NuGet 包**无点**到你的项目。  
    ![NuGet 无点安装](bundling-and-minification/_static/image9.png)
3. 添加一个类，实现[IBundleTransform](https://msdn.microsoft.com/library/system.web.optimization.ibundletransform(VS.110).aspx)接口。 .Less 转换到你的项目中添加以下代码。

    [!code-csharp[Main](bundling-and-minification/samples/sample13.cs)]
4. 创建使用更少文件的绑定`LessTransform`并[CssMinify](https://msdn.microsoft.com/library/system.web.optimization.cssminify(VS.110).aspx)转换。 将以下代码添加到`RegisterBundles`中的方法*应用程序\_Start\BundleConfig.cs*文件。

    [!code-csharp[Main](bundling-and-minification/samples/sample14.cs)]
5. 将以下代码添加到引用较少捆绑包的任何视图。

    [!code-cshtml[Main](bundling-and-minification/samples/sample15.cshtml)]

## <a name="bundle-considerations"></a>捆绑包的注意事项

创建捆绑包时，请执行较好的做法是包括"捆绑"作为前缀的捆绑包名称。 这将防止可能发生[路由冲突](https://forums.asp.net/post/5012037.aspx)。

更新后在绑定中的一个文件，为捆绑的查询字符串参数生成一个新的令牌，完整捆绑必须下载的下次客户端请求一个包含绑定的页面。 在其中将单独列出每个资产传统标记中，会下载已更改的文件。 批的情况下，经常发生变化的资产可能不是理想的选择。

捆绑和缩小主要提高第一个页面请求加载时间。 在浏览器后已请求网页，缓存的资产 （JavaScript、 CSS 和图像） 以便在同一站点请求相同的资产或捆绑和缩小请求同一页面时，不会提供任何性能提升。 如果未设置 expires 标头在你的资产上正常和不使用绑定和缩减、 浏览器刷新试探方法会将标记资产过时几天后和在浏览器将为每个资产需要验证请求。 在这种情况下，捆绑和缩小后的第一个页请求提供性能提升。 有关详细信息，请参阅博客[使用 Cdn 和提高网站性能的 Expires](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)。

通过使用可以降低每个主机名每六个同时连接的浏览器限制[CDN](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)。 由于 CDN 将比你的托管站点具有不同的主机名，从 CDN 资产请求将不计入到你的托管环境的六个同时连接限制。 CDN 还可以提供常见包缓存和边缘缓存优势。

捆绑包应进行分区的页需要它们。 例如，默认的 internet 应用程序的 ASP.NET MVC 模板创建 jQuery 验证捆绑独立于 jQuery。 由于创建的默认视图不产生任何影响，并且不发布值，它们不包括验证捆绑包。

`System.Web.Optimization`中 System.Web.Optimization.DLL 实现命名空间。 它利用 WebGrease 库 (WebGrease.dll) 以缩小功能，后者又使用 Antlr3.Runtime.dll。

*我使用 Twitter 进行快速发布和共享的链接。我的 Twitter 句柄是*: [@RickAndMSFT](http://twitter.com/RickAndMSFT)

## <a name="additional-resources"></a>其他资源

- 视频：[捆绑和优化](https://channel9.msdn.com/Events/aspConf/aspConf/Bundling-and-Optimizing)通过[Howard Dierking](https://twitter.com/#!/howard_dierking)
- [向 Web Pages 站点中添加 Web 优化](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx)。
- [添加绑定和缩减到 Web 窗体](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx)。
- [性能影响的捆绑和缩小上的 Web 浏览](https://blogs.msdn.com/b/henrikn/archive/2012/06/17/performance-implications-of-bundling-and-minification-on-http.aspx)通过[Henrik F Nielsen](http://en.wikipedia.org/wiki/Henrik_Frystyk_Nielsen) [@frystyk](https://twitter.com/frystyk)
- [使用 Cdn 和过期以提高网站性能](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)由 Rick Anderson [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)
- [最大程度减少 RTT （往返次数）](https://developers.google.com/speed/docs/best-practices/rtt)

## <a name="contributors"></a>参与者

- Hao 永远
- [Howard Dierking](https://twitter.com/#!/howard_dierking)
- Diana LaRose
