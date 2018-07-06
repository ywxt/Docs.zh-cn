---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: 在 ASP.NET 网页中创建一致布局页 (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 若要使之更高效，以创建你的站点的 web 页面，可以创建可重用内容 （如页眉和页脚） 为您的网站和你 c 块...
ms.author: aspnetcontent
ms.date: 03/10/2014
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: d27cdc70417f380d596f4d07384a615586427643
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821209"
---
<a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a>在 ASP.NET Web Pages (Razor) 站点中创建一致布局
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET Web Pages (Razor) 的网站中使用布局页中，创建可重用块的内容 （如页眉和页脚），在站点中创建的所有页面一致的外观。
> 
> **你将学习：** 
> 
> - 如何创建可重用基块的内容，如页眉和页脚。
> - 如何在你使用的布局的站点中创建的所有页面一致的外观。
> - 如何将数据在运行时传递给布局页。
> 
> 下面是在本文中引入的 ASP.NET 功能：
> 
> - 内容块，是包含 HTML 格式的内容插入多个页面中的文件。
> - 布局页中，这是页面，其中包含可由网站页面上共享的 HTML 格式的内容。
> - `RenderPage`， `RenderBody`，和`RenderSection`告诉 ASP.NET 在何处插入页面元素的方法。
> - `PageData`使您能够共享内容块和布局页之间的数据的字典。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 3
>   
> 
> 本教程还适用于 ASP.NET Web Pages 2。


## <a name="about-layout-pages"></a>有关布局页

许多网站具有每个页面中，如页眉和页脚或告知用户，他们在登录框显示的内容。 ASP.NET 允许您使用内容块可以包含文本、 标记和代码，就像常规的网页创建一个单独的文件。 然后可以在想要显示的信息的站点上的其他页中插入内容块。 这样无需复制并粘贴到每个页面的相同的内容。 创建此类的常见内容还可以更轻松地更新你的站点。 如果需要更改的内容、 仅更新单个文件，并且所做的更改将反映无处不在已插入内容。

下图显示了如何将内容阻止工作。 在浏览器请求页面从 web 服务器时，ASP.NET 在点插入内容块其中`RenderPage`主页面中调用方法。 已完成 （合并） 页然后发送到浏览器。

![显示如何 RenderPage 方法将一个引用的页插入到当前页的概念关系图。](3-creating-a-consistent-look/_static/image1.jpg)

在此过程中，你将创建引用两个内容块 （页眉和页脚），它们位于单独的文件中的页。 在你的站点中的任意页面中，可以使用这些相同的内容块。 完成后，会显示如下页：

![是在运行包括对 RenderPage 方法的调用的页面在浏览器中显示一个页面的屏幕截图。](3-creating-a-consistent-look/_static/image2.jpg)

1. 在你的网站的根文件夹中，创建名为的文件*Index.cshtml*。
2. 使用以下内容替换现有标记：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. 在根文件夹中，创建名为的文件夹*共享*。

    > [!NOTE]
    > 它是常见的做法在名为的文件夹中的 web 页间共享的文件存储*共享*。
4. 在中*共享*文件夹中，创建名为的文件 *\_Header.cshtml*。
5. 使用以下内容替换任何现有内容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    请注意，文件名称是 *\_Header.cshtml*，以下划线 (\_) 作为前缀。 ASP.NET 不会向浏览器发送一个页面，如果其名称以下划线开头。 这可以防止用户请求 （无意或有意） 这些页面直接。 它是一个好办法使用名称页中，具有内容块的一条下划线，因为你确实不希望用户能够请求这些页&#8212;它们严格存在要插入到其他页面。
6. 在中*共享*文件夹中，创建名为的文件 *\_Footer.cshtml*和替换为以下内容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. 在中*Index.cshtml*页上，添加到两个调用`RenderPage`方法，如下所示：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    这显示了如何将内容块插入到网页。 在调用`RenderPage`方法并将其传递你想要在该点插入其内容的文件的名称。 在这里，要插入的内容 *\_Header.cshtml*并 *\_Footer.cshtml*文件到*Index.cshtml*文件。
8. 运行*Index.cshtml*页在浏览器中。 (在 WebMatrix 中，在**文件**工作区中，右键单击该文件，然后选择**浏览器中启动**。)
9. 在浏览器中查看页面源文件。 (例如，在 Internet Explorer 中，右键单击页上，然后单击**查看源**。)

    这可以查看发送到浏览器，将索引页面标记与内容块相结合的 web 页面标记。 下面的示例演示为呈现的页面源文件*Index.cshtml*。 对调用`RenderPage`插入到*Index.cshtml*已被替换为页眉和页脚文件的实际内容。

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a>创建一致外观使用布局页

到目前为止您已了解很容易地包含在多个页相同的内容。 创建一致外观为站点的更多结构化的方法是使用布局页。 布局页定义 web 页的结构，但不包含任何实际内容。 创建布局页后，可以创建包含的内容，然后将其链接到布局页的网页。 这些页面显示时，它们将格式化根据布局页。 （在这个意义上说，布局页充当一种在其他页中定义的内容的模板。）

布局页就像任何 HTML 页面，只不过它包含调用`RenderBody`方法。 位置`RenderBody`从内容页的信息将包含布局页中的方法确定。

下图显示了如何在内容页面，并在运行时以生成已完成的 web 页面组合在布局页。 在浏览器请求的内容页面。 内容页中，指定布局页后，可以使用页面的结构有代码。 在布局页中，将内容插入点处其中`RenderBody`调用方法。 内容块还可以插入到布局页通过调用`RenderPage`方法，在上一部分中采用的方式。 完成 web 页时，它是发送到浏览器。

![是在运行包括对 RenderBody 方法的调用的页面在浏览器中显示一个页面的屏幕截图。](3-creating-a-consistent-look/_static/image3.jpg)

以下过程演示如何创建网页并链接到它的内容页面的布局。

1. 在中*共享*您的网站的文件夹中创建名为的文件 *\_Layout1.cshtml*。
2. 使用以下内容替换任何现有内容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    您使用`RenderPage`布局页可用于插入内容块中的方法。 布局页面可以包含仅调用一个`RenderBody`方法。
3. 在中*共享*文件夹中，创建名为的文件 *\_Header2.cshtml*和任何现有内容替换为以下代码：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. 在根文件夹中，创建一个新文件夹并将其命名*样式*。
5. 在中*样式*文件夹中，创建名为的文件*Site.css*并添加以下样式定义：

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    这些样式定义目前仅用于显示如何对布局页面使用样式表。 如果需要，可以定义您自己对这些元素的样式。
6. 在根文件夹中，创建名为的文件*Content1.cshtml*和任何现有内容替换为以下代码：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    这是一个将使用布局页的页面。 在页面顶部的代码块指示要用于设置此内容的格式的布局页。
7. 运行*Content1.cshtml*在浏览器中。 在呈现的页面将使用的格式和样式表中定义 *\_Layout1.cshtml*中定义的文本 （内容） 和*Content1.cshtml*。

    ![[image]](3-creating-a-consistent-look/_static/image4.jpg)

    可以重复步骤 6 以创建然后可以共享相同的布局页的其他内容页面。

    > [!NOTE]
    > 您可以设置你的站点，以便可以自动使用的文件夹中的所有内容页面的相同的布局页。 有关详细信息，请参阅[自定义网站的行为为 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906)。

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a>具有多个内容部分的设计布局页

内容页面可以包含多个部分，这很有用，如果你想要使用具有多个区域具有可更换部件内容的布局。 在内容页，您为每个部分指定唯一名称。 (默认部分保持未命名。)在布局页中，您将添加`RenderBody`方法可指定未命名 （默认值） 部分应显示位置。 然后添加单独`RenderSection`方法中，以便单独呈现命名的部分。

下图显示了 ASP.NET 如何处理分为多个部分的内容。 在内容页中的部分块中包含每个命名的节。 (它们命名`Header`和`List`在示例中。)框架将插入点处的布局页内容部分其中`RenderSection`调用方法。 未命名 （默认值） 部分会在该点处插入其中`RenderBody`如上文所调用方法。

![显示如何 RenderSection 方法将引用部分插入到当前页的概念关系图。](3-creating-a-consistent-look/_static/image5.jpg)

此过程演示如何创建具有多个内容部分的内容页以及使用支持多个内容区域的布局页的呈现方式。

1. 在中*共享*文件夹中，创建名为的文件 *\_Layout2.cshtml*。
2. 使用以下内容替换任何现有内容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    您使用`RenderSection`方法以呈现的标头和列表部分。
3. 在根文件夹中，创建名为的文件*Content2.cshtml*和任何现有内容替换为以下代码：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    本页内容包含在页面顶部的代码块。 每个命名的部分包含在部分块。 页的其余部分包含的默认 （未命名） 的内容部分。
4. 运行*Content2.cshtml*在浏览器中。

    ![是在运行包括对 RenderSection 方法的调用的页面在浏览器中显示一个页面的屏幕截图。](3-creating-a-consistent-look/_static/image6.jpg)

## <a name="making-content-sections-optional"></a>使内容部分可选

通常情况下，在内容页面中创建的部分必须匹配在布局页中定义的部分。 如果发生以下任一情况，你会遇到错误：

- 内容页包含已在布局页面中的没有相应部分的部分。
- 布局页包含没有任何内容的部分。
- 布局页包括尝试多次呈现相同的部分的方法调用。

但是，可以通过声明部分为可选中布局页来重写此行为的指定部分。 这可以定义多个内容页面，可以共享布局页，但可能或可能不具有特定部分的内容。

1. 打开*Content2.cshtml*并删除以下部分：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. 保存页面，然后在浏览器中运行它。 显示一条错误消息，因为内容页面上不提供布局页，即标头部分中定义的部分的内容。

    ![显示如果运行某个页面，则会发生该错误的屏幕截图调用 RenderSection 方法但未提供的相应部分。](3-creating-a-consistent-look/_static/image7.jpg)
3. 在中*共享*文件夹中，打开 *\_Layout2.cshtml*页上，并将以下代码行：

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    替换为以下代码：

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    或者，可以使用以下代码块，它将生成相同的结果替换上的一行代码：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. 运行*Content2.cshtml*再次浏览器中的页。 （如果您仍然可以在浏览器中打开此页，则可以只需刷新它。）这一次页面显示与没有错误，即使它具有无标头。

## <a name="passing-data-to-layout-pages"></a>将数据传递给布局页

你可能需要在布局页面中引用的内容页中定义的数据。 如果是这样，您需要将数据从内容页传递到布局页。 例如，你可能想要显示的用户的登录状态，或者可能想要显示或隐藏根据用户输入的内容区域。

若要将数据从内容页传递到布局页中，您可以将值放入`PageData`内容页的属性。 `PageData`属性是包含你想要在页面之间传递的数据的名称/值对的集合。 在布局页中，便可以读取的值`PageData`属性。

下面是另一个关系图。 此示例显示如何使用 ASP.NET`PageData`属性将值从内容页传递到布局页。 当 ASP.NET 开始构建 web 页时，它会创建`PageData`集合。 在内容页，编写代码以将数据放入`PageData`集合。 中的值以`PageData`通过内容页中的其他部分或其他内容块，也可以访问集合。

![演示如何填充 PageData 字典并将该信息传递给布局页的内容页面的概念图。](3-creating-a-consistent-look/_static/image8.jpg)

以下过程演示如何将数据从内容页传递到布局页。 页运行时，它会显示一个按钮，使用户可以隐藏或显示在布局页中定义的列表。 当用户单击按钮时，它设置一个 true/false （布尔值） 值`PageData`属性。 布局页读取该值，，和如果为 false，将隐藏列表。 值还用于在内容页中确定是否显示**隐藏列表**按钮或**显示列表**按钮。

![[image]](3-creating-a-consistent-look/_static/image9.jpg)

1. 在根文件夹中，创建名为的文件*Content3.cshtml*和任何现有内容替换为以下代码：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    代码将存储中的数据的两份`PageData`属性&#8212;网页和 true 或 false 以指定是否显示列表的标题。

    请注意，ASP.NET 允许您放入有条件地使用代码块的页面的 HTML 标记。 例如，`if/else`块的页的正文中确定哪个窗体，具体取决于是否显示`PageData["ShowList"]`设置为 true。
2. 在中*共享*文件夹中，创建名为的文件 *\_Layout3.cshtml*和任何现有内容替换为以下代码：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    布局页包括中的表达式`<title>`获取从的标题值的元素`PageData`属性。 它还使用`ShowList`的值`PageData`属性来确定是否显示列表内容块。
3. 在中*共享*文件夹中，创建名为的文件 *\_List.cshtml*和任何现有内容替换为以下代码：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. 运行*Content3.cshtml*页在浏览器中。 在左侧和右侧的页上可见的列表将显示的页和一个**隐藏列表**底部的按钮。

    ![显示包含列表和一个按钮，显示隐藏列表页屏幕截图。](3-creating-a-consistent-look/_static/image10.jpg)
5. 单击**隐藏列表**。 列表会消失，按钮将变为**显示列表**。

    ![显示不包含列表和一个按钮，显示显示列表页屏幕截图。](3-creating-a-consistent-look/_static/image11.jpg)
6. 单击**显示列表**按钮和列表会再次显示。

## <a name="additional-resources"></a>其他资源


[为 ASP.NET 网页自定义站点范围的行为](https://go.microsoft.com/fwlink/?LinkId=202906)
