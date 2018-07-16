---
title: ASP.NET Core 中的 Less、Sass 和字体 Awesome
author: ardalis
description: 了解如何在 ASP.NET Core 应用程序中使用Less，Sass，和ont Awesome。
ms.author: tdykstra
ms.date: 10/14/2016
uid: client-side/less-sass-fa
ms.openlocfilehash: 2229c4e3b0238ff17c15e78f657b9acb10495c72
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275560"
---
# <a name="less-sass-and-font-awesome-in-aspnet-core"></a>ASP.NET Core 中的Less、Sass 和字体 Awesome

作者：[Steve Smith](https://ardalis.com/)

Web 应用程序的用户对样式和总体体验的期望越来越高。新式 web 应用程序频繁地利用丰富的工具和框架，以一致的方式定义和管理其外观和整体设计。[Bootstrap](http://getbootstrap.com/) 等框架可以在很大程度上定义一组通用的网站样式和布局选项。但大多数设计简洁的网站还因能够有效定义和维护样式和级联样式表 (CSS) 文件，以及使用户能够轻松访问可帮助更直观显示站点界面的非图像图标而受益。这正是支持 [Less](http://lesscss.org/) 和 [Sass](http://sass-lang.com/) 以及 [Font Awesome](http://fontawesome.io/) 等库的语言和工具所起到的作用。

## <a name="css-preprocessor-languages"></a>CSS 预处理器语言

为了改进基础语言的使用体验，编译成其它语言的语言被称为预处理器。有两种常用的 CSS 预处理器：Less 和 Sass。这些预处理器可向 CSS 添加功能，如对变量和嵌套规则的支持，可改善大型复杂样式表的可维护性。CSS 是一种非常基本的语言，甚至无法支持简单的变量，这使得 CSS 文件显得过于冗繁。通过预处理器添加真实的编程语言功能可帮助减少重复性，更好地组织样式设置规则。Visual Studio 同时提供对 Less 和 Sass 的内置支持，以及可进一步提升使用这些语言时的开发体验的扩展。

作为预处理器可以如何改进可读性和可维护性的样式信息的快速示例，请考虑以下 CSS:

```css
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    color: black;
    font-weight: bold;
    font-size: 14px;
    font-family: Helvetica, Arial, sans-serif;
}
```

使用 Less，可将此进行重写，消除所有重复内容，具体方法是使用 *mixin*（如此命名是因为使用它可将属性从一个类或规则集“混入”另一个：

```less
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    .header;
    font-size: 14px;
}
```

## <a name="less"></a>Less

CSS 预处理器通过使用 Node.js 来运行。要安装 Less，可通过命令提示符（-g 指“全局”）使用节点包管理器 (npm)：

```console
npm install -g less
```

如果使用 Visual Studio，则开始使用 Less 时可首先将一个或多个 Less 文件添加到项目，然后将 Gulp（或 Grunt）配置为在编译时进行处理。将一个*样式*文件夹添加到项目，然后在该文件夹中添加一个新的 Less 文件，命名为 *main.less*。

![添加 Less 文件](less-sass-fa/_static/add-less-file.png)

添加后，您的文件夹结构应如下所示：

![文件夹结构](less-sass-fa/_static/folder-structure.png)

现在你可以添加到文件中，这将编译到 CSS 并部署到的 wwwroot 文件夹 Gulp 的一些基本的样式。

修改*main.less*为包括以下内容，这将从一种基颜色创建一个简单的调色板。

```less
@base: #663333;
@background: spin(@base, 180);
@lighter: lighten(spin(@base, 5), 10%);
@lighter2: lighten(spin(@base, 10), 20%);
@darker: darken(spin(@base, -5), 10%);
@darker2: darken(spin(@base, -10), 20%);

body {
    background-color:@background;
}
.baseColor  {color:@base}
.bgLight    {color:@lighter}
.bgLight2   {color:@lighter2}
.bgDark     {color:@darker}
.bgDark2    {color:@darker2}
```

`@base` 和其他前缀为 @ 的项是变量。除 `@base` 之外，其中每一个均表示一种颜色。它们是使用颜色函数设置的：变亮、变暗和渲染。可使用“变亮”和“变暗”精确按所需改变亮度；“渲染”可按数值调节颜色（在色环范围内）。Less 是智能的处理器，可忽略未使用的变量，以便显示这些变量的工作原理以及需在何处使用它们。类 `.baseColor` 演示所生成的 CSS 文件中的每个变量的计算值。

### <a name="get-started"></a>入门

创建**npm 配置文件**(*package.json*) 在你的项目文件夹并编辑它以引用`gulp`和`gulp-less`:

```json
{
  "version": "1.0.0",
  "name": "asp.net",
  "private": true,
  "devDependencies": {
    "gulp": "3.9.1",
    "gulp-less": "3.3.0"
  }
}
```

在你的项目文件夹，或在 Visual Studio 中安装的依赖关系，请在命令提示符下**解决方案资源管理器**(**依赖项 > npm > 还原程序包**)。

```console
npm install
```

![VS 还原包](less-sass-fa/_static/restore-packages.png)

在项目文件夹中，创建**Gulp 配置文件**(*gulpfile.js*) 以定义自动的过程。  在更少，表示的文件及要运行更少的任务的顶部添加一个变量：

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less");

gulp.task("less", function () {
  return gulp.src('Styles/main.less')
    .pipe(less())
    .pipe(gulp.dest('wwwroot/css'));
});
```

打开**任务运行程序资源管理器**(**视图 > 其他 Windows > 任务运行程序资源管理器**)。 在任务之间，你应看到一个名为的新任务`less`。 你可能必须刷新窗口。

运行`less`任务，并看到类似于此处所示的输出：

![Less 任务运行程序](less-sass-fa/_static/less-task-runner.png) 

*Wwwroot/css*文件夹现在包含一个新的文件， *main.css*:

![创建主 css](less-sass-fa/_static/main-css-created.png)

打开*main.css* ，你将看到与下面类似：

```css
body {
    background-color: #336666;
}
.baseColor {
    color: #663333;
}
.bgLight {
    color: #884a44;
}
.bgLight2 {
    color: #aa6355;
}
.bgDark {
    color: #442225;
}
.bgDark2 {
    color: #221114;
}
```

添加到一个简单的 HTML 页面*wwwroot*文件夹，然后引用*main.css*若要查看操作中的调色板。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <link href="css/main.css" rel="stylesheet" />
    <title></title>
</head>
<body>
    <div>
        <div class="baseColor">BaseColor</div>
        <div class="bgLight">Light</div>
        <div class="bgLight2">Light2</div>
        <div class="bgDark">Dark</div>
        <div class="bgDark2">Dark2</div>
    </div>
</body>
</html>
```

你可以看到上旋转 180 度`@base`用于生成`@background`导致相反颜色的颜色盘`@base`:

![不太测试示例](less-sass-fa/_static/less-test-screenshot.png)

Less 还提供对嵌套规则及嵌套媒体查询的支持。例如，定义菜单等嵌套层次结构可能会生成冗长的 CSS 规则，如下所示：

```css
nav {
    height: 40px;
    width: 100%;
}
nav li {
    height: 38px;
    width: 100px;
}
nav li a:link {
    color: #000;
    text-decoration: none;
}
nav li a:visited {
    text-decoration: none;
    color: #CC3333;
}
nav li a:hover {
    text-decoration: underline;
    font-weight: bold;
}
nav li a:active {
    text-decoration: underline;
}
```

理想情况下的所有相关的样式规则将被放在一起在 CSS 文件中，但在实践中没有任何强制实施此规则约定和可能块注释除外。

使用 Less 定义这些规则时是这样的：

```less
nav {
    height: 40px;
    width: 100%;
    li {
        height: 38px;
        width: 100px;
        a {
            color: #000;
            &:link { text-decoration:none}
            &:visited { color: #CC3333; text-decoration:none}
            &:hover { text-decoration:underline; font-weight:bold}
            &:active {text-decoration:underline}
        }
    }
}
```

请注意，在此情况下，所有的从属元素`nav`包含在其作用域内。 不再父元素的任何重复 (`nav`， `li`， `a`)，并且总的行计数也已删除 （尽管某些就是将值放在第二个示例的同一行上的结果）。 它可以是非常有帮助，组织，若要查看的所有规则的给定的用户界面元素在显式限定范围内，在这种情况下设置从文件的其余部分由大括号。

`&` 语法是 Less 选择器功能，& 表示当前的父级选择器。因此，在 {...} 块中，`&` 表示 `a`标记，而 `&:link` 等效于 `a:link`。	

媒体查询在创建响应式设计时非常有用，但同时可能会极大增加 CSS 中的重复性和复杂性。通过 Less，可将媒体查询嵌套在类中，这样便无需在不同的顶级 `@media` 元素中重复使用整个类定义。例如，下面是响应式菜单的 CSS：

```css
.navigation {
    margin-top: 30%;
    width: 100%;
}
@media screen and (min-width: 40em) {
    .navigation {
        margin: 0;
    }
}
@media screen and (min-width: 62em) {
    .navigation {
        width: 960px;
        margin: 0;
    }
}
```

这可以更好地定义以秒为：

```less
.navigation {
    margin-top: 30%;
    width: 100%;
    @media screen and (min-width: 40em) {
        margin: 0;
    }
    @media screen and (min-width: 62em) {
        width: 960px;
        margin: 0;
    }
}
```

我们已经看到的 Less 的另一个功能是其对数学运算的支持，该功能允许从预定义的变量来构造样式特性。通过该功能，更新相关样式时要容易得多，因为可以修改基变量，且所有依赖值会自动更改。

CSS 文件，尤其是用于大型站点（以及在使用媒体查询的情况下）的文件，会随时间推移而逐渐变得很大，从而变得难以操作。各 Less 文件可单独定义，然后使用 `@import` 指令一并拉取。如果需要，还可使用 Less 导入单个 CSS 文件

*Mixins* 可接受参数，Less 支持 mixin 临界形式的条件逻辑，该临界以声明性方式定义特定 mixin 何时生效。Mixin 临界的一个常见用法是基于源颜色的深浅来调整颜色。如果给定一个接受颜色参数的 mixin，可使用 mixin 临界，基于该颜色来修改 mixin：

```less
.box (@color) when (lightness(@color) >= 50%) {
    background-color: #000;
}
.box (@color) when (lightness(@color) < 50%) {
    background-color: #FFF;
}
.box (@color) {
    color: @color;
}

.feature {
    .box (@base);
}
```

给定当前 `@base` 值为 `#663333`，此 Less 脚本将生成以下 CSS：

```css
.feature {
    background-color: #FFF;
    color: #663333;
}
```

Less 还提供多个其他功能，但上述介绍应已展示了此预处理语言的强大作用。

## <a name="sass"></a>Sass

Sass 与 Less 类似，也提供对许多相同功能的支持，只是语法略有不同。它使用 Ruby 而非 JavaScript 生成，因此具有不同的设置要求。原始 Sass 语言不使用花括号或分号，而是使用空白和缩进来定义作用域。第 3 版 Sass 中引入了新语法 **SCSS** ("Sassy CSS")。SCSS 与 CSS 的类似之处在于它会忽略缩进级别和空格，而使用分号和花括号。

若要安装 Sass，通常你将首先安装 Ruby （预安装在 macOS 上），，然后运行：

```console
gem install sass
```

但是，如果在运行 Visual Studio，那么开始使用 Sass 时可采用与 Less 类似的方式。打开 *package.json* 并向 `devDependencies` 添加 "gulp sass" 包：

```json
"devDependencies": {
  "gulp": "3.9.1",
  "gulp-less": "3.3.0",
  "gulp-sass": "3.1.0"
}
```

接下来，修改*gulpfile.js*添加 sass 变量和编译 Sass 文件并将结果放的 wwwroot 文件夹中的任务：

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less"),
  sass = require("gulp-sass");

// other content removed

gulp.task("sass", function () {
  return gulp.src('Styles/main2.scss')
    .pipe(sass())
    .pipe(gulp.dest('wwwroot/css'));
});
```

现在，您可以将 Sass 文件*main2.scss*到*样式*项目的根目录中的文件夹：

![添加 scss 文件](less-sass-fa/_static/add-scss-file.png)

打开*main2.scss* ，添加以下内容：

```sass
$base: #CC0000;
body {
    background-color: $base;
}
```

保存你所有文件。 现在刷新**任务运行程序资源管理器**，你看到`sass`任务。 运行它，并查找 */wwwroot/css*文件夹。 现在有了*main2.css*文件，使用以下内容：

```css
body {
    background-color: #CC0000;
}
```

Sass 支持嵌套的方式与 Less 大体相同，并具有类似的优势。可通过函数来拆分文件，并通过使用 `@import` 指令来含入文件：

```sass
@import 'anotherfile';
```

Sass 支持 mixins 同样，使用`@mixin`关键字定义它们和`@include`以便将它们，包含从如此示例所示[sass lang.com](http://sass-lang.com):

```sass
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box { @include border-radius(10px); }
```

Sass 除了 mixins，它还支持继承，的概念允许一个类，以扩展另一个。 它是从概念上讲类似于 mixin，但在更少的 CSS 代码中的结果。 它通过`@extend`关键字。 若要尝试 mixins，将以下代码添加到你*main2.scss*文件：

```sass
@mixin alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @include alert;
    border-color: green;
}

.error {
    @include alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

检查在输出*main2.css*运行之后`sass`任务中**任务运行程序资源管理器**:

```css
.success {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    border-color: green;
 }

.error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    color: red;
    border-color: red;
    font-weight: bold;
}
```

请注意所有警报 mixin 的常见属性在每个类中有重复。 Mixin 好地帮助消除重复在开发时，但它仍包含中的重复，从而导致大于必要 CSS 文件-一个潜在的性能问题很多要创建 CSS。

现在将与警报 mixin`.alert`类，并更改`@include`到`@extend`(记住来扩展`.alert`，而不`alert`):

```sass
.alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @extend .alert;
    border-color: green;
}

.error {
    @extend .alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

运行 Sass 次，并检查生成的 CSS:

```css
.alert, .success, .error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    border-color: green;
}

.error {
    color: red;
    border-color: red;
    font-weight: bold;
}
```

现在仅为根据需要多次定义属性，并更好地生成 CSS。

Sass 还包括函数和条件逻辑运算，与 Less 类似。事实上，这两种语言的功能非常相似。

## <a name="less-or-sass"></a>Less 还是 Sass？

关于 Less 与 Sass 总体而言哪种语言更好（甚或原始 Sass 与较新的 SCSS 语法哪种更好），并无定论。 可能最重要的是要**使用这些工具中的一种**，而不是以手工方式对 CSS 文件进行编码。一旦作出这样的决定，Less 和 Sass 都是不错的选择。

## <a name="font-awesome"></a>Font Awesome

除 CSS 预处理器外，另一种用于为新式 web 应用程序设置样式的好方法是 Font Awesome。Font Awesome 是一个工具包，可提供 500 多个可缩放的向量图标，这些图标可在 web 应用程序中自由使用。其最初的目的是用于 Bootstrap，但它并不依赖于该框架或任何 JavaScript 库。

若要开始使用 Font Awesome，最简单的方法是添加对其的引用，该引用使用公共内容交付网络 (CDN)：

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

你可以还将其添加到你的 Visual Studio 项目通过将它添加到"依赖关系"中*bower.json*:

```json
{
  "name": "ASP.NET",
  "private": true,
  "dependencies": {
    "bootstrap": "3.0.0",
    "jquery": "1.10.2",
    "jquery-validation": "1.11.1",
    "jquery-validation-unobtrusive": "3.2.2",
    "hammer.js": "2.0.4",
    "bootstrap-touch-carousel": "0.8.0",
    "Font-Awesome": "4.3.0"
  }
}
```

页面上具有对 Font Awesome 的引用后，可将图标添加到应用程序中，方法是向内联 HTML 元素（如 `<span>` 或 `<i>`）应用 Font Awesome 类（通常前缀为 "fa-"）。例如，可使用如下代码将图标添加到简单列表和菜单中：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <link href="lib/font-awesome/css/font-awesome.css" rel="stylesheet" />
</head>
<body>
    <ul class="fa-ul">
        <li><i class="fa fa-li fa-home"></i> Home</li>
        <li><i class="fa fa-li fa-cog"></i> Settings</li>
    </ul>
</body>
</html>
```

这将生成浏览器中的以下-请注意每个项旁边的图标：

![列表图标](less-sass-fa/_static/list-icons-screenshot.png)

你可以查看可用的图标的完整列表：

http://fontawesome.io/icons/

## <a name="summary"></a>总结

现代 web 应用程序对具有后列特点的设计的需求日益增加：响应灵敏、界面清晰、直观、流畅，可轻松在各种设备上使用。而要管理实现这些目标所需的复杂 CSS 样式表，最好的做法是使用 Less 或 Sass 等预处理器。此外，Font Awesome 等工具包可快速向文本导航菜单和按钮提供常用图标，进而提高应用程序的整体用户体验。
