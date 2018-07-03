---
uid: web-pages/overview/ui-layouts-and-themes/9-working-with-images
title: 使用 ASP.NET Web Pages (Razor) 站点中的映像 |Microsoft Docs
author: tfitzmac
description: 本章展示如何添加、 显示和操作图像 （重设大小、 翻转，并添加水印） 在你的网站。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 778c4e58-4372-4d25-bab9-aec4a8d8e38d
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/9-working-with-images
msc.type: authoredcontent
ms.openlocfilehash: 32cfb9cc3c3eabcd6d724e05b85c5bf1160a39f6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362922"
---
<a name="working-with-images-in-an-aspnet-web-pages-razor-site"></a>使用 ASP.NET Web Pages (Razor) 站点中的图像
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何添加、 显示和操作图像 （重设大小、 翻转，并添加水印） 在 ASP.NET Web Pages (Razor) 的网站中。
> 
> 你将学习：
> 
> - 如何动态添加到页面的图像。
> - 如何让用户上传图像。
> - 如何调整图像大小。
> - 翻转或旋转图像的方式。
> - 如何添加水印图像。
> - 如何将图像用作水印。
> 
> 这些是 ASP.NET 编程一文中引入的功能：
> 
> - `WebImage`帮助器。
> - `Path`对象，它提供可用于操作路径和文件名的方法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 2
> - WebMatrix 2
>   
> 
> 本教程还适用于 WebMatrix 3。


<a id="Adding_an_Image"></a>
## <a name="adding-an-image-to-a-web-page-dynamically"></a>动态添加到 Web 页的图像

在开发网站时，可以向你的网站和单个页面添加图像。 您还可以让用户上传可能适用于任务，例如让他们添加个人资料照片的图像。

如果映像已在站点上可用，并且只是想要在页面上显示，则使用对应的 HTML`<img>`元素，如下：

[!code-html[Main](9-working-with-images/samples/sample1.html)]

有时，不过，您需要能够动态显示图像&#8212;，它是不知道什么图像之前的页面正在显示。

在本部分中的过程演示如何的动态用户在其中指定映像名称的列表中的图像文件名称中显示图像。 他们从下拉列表中，选择的映像的名称和时在提交页，显示他们选择的映像。

![[image]](9-working-with-images/_static/image1.jpg "ch9images 1.jpg")

1. 在 WebMatrix 中，创建新的网站。
2. 添加一个名为的新页*DynamicImage.cshtml*。
3. 在该网站的根文件夹中，添加一个新文件夹并将其命名*映像*。
4. 四个将映像添加到*映像*刚创建的文件夹。 （必须执行此操作，方便将任何图像，但它们应组合到一个页面上。）重命名图像*Photo1.jpg*， *Photo2.jpg*， *Photo3.jpg*，以及*Photo4.jpg*。 (不会使用*Photo4.jpg*在此过程中，但是您将使用它在本文后面。)
5. 验证为只读的未标记的四个映像。
6. 在页中的现有内容替换为以下：

    [!code-cshtml[Main](9-working-with-images/samples/sample2.cshtml)]

    页的正文具有下拉列表 (`<select>`元素)，名为`photoChoice`。 列表具有三个选项，并`value`每个列表选项的属性具有一个将放入映像的名称*映像*文件夹。 实质上，列表使用户可以选择一个友好名称，如&quot;照片 1&quot;，然后将传递 *.jpg*时提交页面文件名称。

    在代码中，你可以获取用户的所选内容 （即，图像文件名称） 列表中通过读取`Request["photoChoice"]`。 您首先查看是否存在所选内容根本。 如果没有，您构造组成图像的文件夹名称和用户的图像文件名称的图像的路径。 (如果您尝试构造一个路径，但没有在中为 nothing `Request["photoChoice"]`，你将收到错误。)这会导致类似下面的相对路径：

    *图像/Photo1.jpg*

    路径存储在名为变量`imagePath`，你将需要更高版本中的页。

    在正文中，此外，还有`<img>`元素用来显示用户选择的映像。 `src`属性未设置为文件的名称或 URL，像显示的静态元素。 相反，设置为`@imagePath`，这意味着它从代码中设置的路径获取其值。

    第一次该页面运行，不过，没有图像若要显示，因为用户尚未选择任何内容。 这通常就意味着`src`属性将为空，并且图像会显示为红色&quot;x&quot; （或在浏览器呈现任何内容时找不到图像）。 若要防止此情况，您将放`<img>`中的元素`if`块，可测试以查看是否`imagePath`变量中包含的任何内容。 如果用户已做出选择，`imagePath`包含的路径。 如果用户未挑选一个映像，或者如果这是首次将显示的页，`<img>`元素甚至不会呈现。
7. 保存该文件并在浏览器中运行此页。 (请确保的页中选择**文件**工作区之前运行它。)
8. 从下拉列表中选择一个映像，然后单击**示例图像**。 请确保您看到的不同选择不同的映像。

<a id="Uploading_an_Image"></a>
## <a name="uploading-an-image"></a>上传图像

前面的示例演示如何动态显示图像，但它仅适用于已在网站的映像。 此过程说明如何以使用户可以上传的映像，然后在页面显示。 在 ASP.NET 中，您可以操作上使用动态映像`WebImage`帮助程序，有方法，可用于创建、 处理和保存图像。 `WebImage`帮助器支持所有常见 web 图像文件的类型，包括 *.jpg*， *.png*，并且 *.bmp*。 在整篇文章中，将使用 *.jpg*映像，但你可以使用任何图像类型。

![[image]](9-working-with-images/_static/image2.jpg "ch9images 2.jpg")

1. 添加一个新页面并将其命名*UploadImage.cshtml*。
2. 在页中的现有内容替换为以下： 

    [!code-cshtml[Main](9-working-with-images/samples/sample3.cshtml)]

    具有文本正文`<input type="file">`元素，它使用户可以选择要上载的文件。 在单击时**提交**，他们选择的文件和窗体提交。

    若要获取上传的映像，请使用`WebImage`帮助程序，有各种有用的方法，用于处理图像。 具体而言，使用`WebImage.GetImageFromRequest`以获取上传的图像 （如果有） 并将其存储在一个名为变量`photo`。

    在此示例中的工作很多涉及获取和设置文件和路径名称。 问题是你想要获取用户上传，图像的名称 （和只是名称），然后创建要用于存储映像的新路径。 因为用户可能无法上传具有相同名称的多个映像，使用少量额外代码以创建唯一的名称，并确保用户不会覆盖现有的图片。

    如果实际上已上载图像 (测试`if (photo != null)`)，从图像的获取映像名称`FileName`属性。 当用户上传图像，`FileName`包含用户的原始名称，其中包括从用户的计算机的路径。 它可能如下所示：

    *C:\Users\Joe\Pictures\SamplePhoto1.jpg*

    您不希望所有该路径信息，但&#8212;只是想实际文件名称 (*SamplePhoto1.jpg*)。 可以去除使用的只是从路径文件`Path.GetFileName`方法，如下：

    [!code-csharp[Main](9-working-with-images/samples/sample4.cs)]

    然后，通过将 GUID 添加到原始名称创建新的唯一文件名。 (有关 Guid 的详细信息，请参阅[有关 Guid](#SB_AboutGUIDs)这篇文章中更高版本。)然后您构造可用于将图像保存的完整路径。 在保存路径由新的文件名、 文件夹 （映像） 和当前的网站位置。

    > [!NOTE]
    > 为你的代码来保存文件的顺序*映像*文件夹中，应用程序需要读写该文件夹的权限。 在开发计算机上这不是通常出现问题。 但是，当将您的网站发布到宿主提供程序的 web 服务器，您可能需要显式设置这些权限。 如果托管提供商的服务器上运行此代码，并出现错误，请与宿主提供程序中，若要了解如何设置这些权限。

    最后，将传递在保存路径`Save`方法的`WebImage`帮助器。 这会存储上传的图像采用新名称。 保存方法如下所示： `photo.Save(@"~\" + imagePath)`。 完整路径追加到`@"~\"`，这是当前的网站位置。 (有关`~`运算符，请参阅[ASP.NET Web 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths)。)

    在上一示例中，页的正文包含`<img>`元素显示图像。 如果`imagePath`已设置`<img>`呈现元素并将其`src`属性设置为`imagePath`值。
3. 在浏览器中运行页。
4. 上传图像，并确保它在页中显示。
5. 在你的站点，打开*映像*文件夹。 你看到了其文件名外观如下所示，添加新文件:: 

    *45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto.png*

    这是使用 GUID 作为名称前缀上载的映像。 (你自己的文件将具有不同的 GUID，可能命名为类似不同于*MyPhoto.png*。)

> [!TIP] 
> 
> <a id="SB_AboutGUIDs"></a>
> ### <a name="about-guids"></a>有关 Guid
> 
> GUID (全局唯一 ID) 是一个标识符，通常以如下格式呈现： `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`。 数字和字母 （从 A 到 F) 存在差异的每个 GUID，但它们都遵循使用组 8-4-4-4-12 个字符的模式。 （从技术上讲，GUID 是一个 16 字节 128 位数字。）当您需要一个 GUID 时，可以调用专门为您生成一个 GUID 的代码。 Guid 背后的理念是，之间的数很大的规模 (3.4 x 10<sup>38</sup>)，用于生成它的算法，得到数几乎能保证是一种类型之一。 因此，Guid 是好办法时必须保证不会两次使用相同的名称生成操作的名称。 缺点，当然，是，Guid 并不特别是用户友好，因此他们趋向于仅在代码中使用名称时使用。


<a id="Resizing_an_Image"></a>
## <a name="resizing-an-image"></a>调整图像的大小

如果你的网站接受来自用户的图像，您可能想要调整图像大小之前显示或将其保存。 您可以再次使用`WebImage`的此帮助器。

此过程说明如何调整已上传的图像创建缩略图，然后在网站中保存缩略图和原始图像大小。 在页面上显示缩略图，并使用超链接将用户重定向到尺寸的图像。

![[image]](9-working-with-images/_static/image3.jpg "ch9images 3.jpg")

1. 添加一个名为的新页*Thumbnail.cshtml*。
2. 在中*映像*文件夹中，创建一个名为子*thumbs*。
3. 在页中的现有内容替换为以下： 

    [!code-cshtml[Main](9-working-with-images/samples/sample5.cshtml)]

    此代码是上一示例中类似于代码。 不同之处是，此代码将图像保存两次，一次通常一次后创建缩略图图像的副本。 首先获取上传的映像并将其保存在*映像*文件夹。 然后构建新的缩略图的路径。 若要实际创建缩略图，请调用`WebImage`帮助者`Resize`方法来创建一个 60 像素由 60 像素的图像。 该示例演示如何保留纵横比，以及如何可以防止图像被放大 （如果新大小实际上会使映像更大）。 调整大小的图像则保存在*thumbs*子文件夹。

    在结束标记时，使用相同`<img>`具有动态元素`src`已了解在前面的示例有条件地显示的图像的属性。 在这种情况下，您显示缩略图。 此外使用`<a>`元素来创建大版本的映像的超链接。 如同`src`的属性`<img>`元素，设置`href`的属性`<a>`动态地为任何内容中的元素`imagePath`。 若要确保该路径可以正常运行以 URL 形式，可以传递`imagePath`到`Html.AttributeEncode`方法，后者将在路径中的保留的字符转换为确定在 URL 中的字符。
4. 在浏览器中运行页。
5. 上传照片并验证显示缩略图。
6. 单击要查看原尺寸图像的缩略图。
7. 在中*映像*并*缩略图图像/*，请注意，已添加新文件。

<a id="Rotating_and_Flipping"></a>
## <a name="rotating-and-flipping-an-image"></a>旋转和翻转图像

`WebImage`帮助器还允许您翻转和旋转图像。 此过程说明如何从服务器获取图像，（垂直） 上下翻转图像，保存该文件，然后在页面上显示翻转的图像。 在此示例中，您只需使用你已在服务器的文件 (*Photo2.jpg*)。 在实际的应用程序，可能会翻转图像动态，像前面的示例中一样获取其名称。

![[image]](9-working-with-images/_static/image4.jpg "ch9images 4.jpg")

1. 添加一个名为的新页*FlipImage.cshtml*。
2. 在页中的现有内容替换为以下： 

    [!code-cshtml[Main](9-working-with-images/samples/sample6.cshtml)]

    该代码使用`WebImage`帮助者从服务器获取图像。 创建使用相同的方法来保存图像，前面的示例中使用的图像的路径并将该路径传递时创建图像使用`WebImage`:

    [!code-javascript[Main](9-working-with-images/samples/sample7.js)]

    如果找到的图像，则构造新路径和文件名的名称，像前面的示例中一样。 若要翻转图像，请调用`FlipVertical`方法，然后再次保存该图像。

    图像时再次显示的页上通过使用`<img>`具有元素`src`属性设置为`imagePath`。
3. 在浏览器中运行页。 此图像可查看*Photo2.jpg*正面朝下所示。
4. 请刷新页面或请求页上再次看到图像类型为翻转的右侧向上又。

若要旋转图像，您可以使用相同的代码，不同之处在于而不是调用`FlipVertical`或`FlipHorizontal`，则调用`RotateLeft`或`RotateRight`。

<a id="Adding_a_Watermark"></a>
## <a name="adding-a-watermark-to-an-image"></a>向图像添加水印

当将映像添加到你的网站时，你可能想要将水印添加到映像，然后将其保存，或在页面上显示。 人们经常使用水印，将版权信息添加到映像，或将播发其业务名称。

![[image]](9-working-with-images/_static/image5.jpg "ch9images 5.jpg")

1. 添加一个名为的新页*Watermark.cshtml*。
2. 在页中的现有内容替换为以下： 

    [!code-cshtml[Main](9-working-with-images/samples/sample8.cshtml)]

    此代码就像中的代码*FlipImage.cshtml*前面的页 (尽管这次使用*Photo3.jpg*文件)。 若要添加水印，则调用`WebImage`帮助者`AddTextWatermark`方法之前保存的图像。 在调用`AddTextWatermark`，将文本&quot;我水印&quot;、 将字体颜色设置为黄色，并设置为 Arial 字体系列。 (尽管它不显示在这里，`WebImage`帮助程序，您还可以指定不透明度、 字体系列和字体大小和水印文本的位置。)保存图像时它不必须是只读的。

    如您所见之前，图像显示在页上通过使用`<img>`元素的 src 属性设置为`@imagePath`。
3. 在浏览器中运行页。 请注意右下角的图像，文本"My 水印"。

<a id="Using_an_Image_as_a_Watermark"></a>
## <a name="using-an-image-as-a-watermark"></a>将图像用作水印

而不是使用文本的水印，可以使用另一个映像。 人们有时使用公司徽标之类的映像作为水印，或它们而不是文本中使用水印图像的版权信息。

![[image]](9-working-with-images/_static/image6.jpg "ch9images 6.jpg")

1. 添加一个名为的新页*ImageWatermark.cshtml*。
2. 添加到图像*映像*文件夹，可以用作徽标，并且重命名图像*MyCompanyLogo.jpg*。 此图像应是您所见清楚如果设置为 80 像素宽和高 20 像素的图像。
3. 在页中的现有内容替换为以下： 

    [!code-cshtml[Main](9-working-with-images/samples/sample9.cshtml)]

    这是在前面的示例中的代码的另一个变体。 在这种情况下，调用`AddImageWatermark`将水印图像添加到目标映像 (*Photo3.jpg*) 保存图像之前。 当您调用`AddImageWatermark`，其宽度设置为 80 像素，高度为 20 像素。 *MyCompanyLogo.jpg*图像水平按居中对齐和垂直方向上的目标映像底部对齐。 不透明度设置为 100%和填充设置为 10 像素。 如果水印图像大于目标映像，不会发生。 如果水印图像大于目标图像并设置为零的图像水印的填充，则忽略水印。

    如前面一样，显示图像使用`<img>`元素，并动态`src`属性。
4. 在浏览器中运行页。 请注意，水印图像显示在主映像的底部。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源


[在 ASP.NET Web Pages 站点中使用文件](https://go.microsoft.com/fwlink/?LinkId=202896)

[编程使用 Razor 语法的 ASP.NET 网页简介](https://go.microsoft.com/fwlink/?LinkID=251587)
