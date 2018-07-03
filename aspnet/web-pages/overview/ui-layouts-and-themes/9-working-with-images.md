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
<a name="working-with-images-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="a2678-103">使用 ASP.NET Web Pages (Razor) 站点中的图像</span><span class="sxs-lookup"><span data-stu-id="a2678-103">Working with Images in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="a2678-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a2678-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a2678-105">本文介绍如何添加、 显示和操作图像 （重设大小、 翻转，并添加水印） 在 ASP.NET Web Pages (Razor) 的网站中。</span><span class="sxs-lookup"><span data-stu-id="a2678-105">This article shows you how to add, display, and manipulate images (resize, flip, and add watermarks) in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="a2678-106">你将学习：</span><span class="sxs-lookup"><span data-stu-id="a2678-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="a2678-107">如何动态添加到页面的图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-107">How to add an image to a page dynamically.</span></span>
> - <span data-ttu-id="a2678-108">如何让用户上传图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-108">How to let users upload an image.</span></span>
> - <span data-ttu-id="a2678-109">如何调整图像大小。</span><span class="sxs-lookup"><span data-stu-id="a2678-109">How to resize an image.</span></span>
> - <span data-ttu-id="a2678-110">翻转或旋转图像的方式。</span><span class="sxs-lookup"><span data-stu-id="a2678-110">How to flip or rotate an image.</span></span>
> - <span data-ttu-id="a2678-111">如何添加水印图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-111">How to add a watermark to an image.</span></span>
> - <span data-ttu-id="a2678-112">如何将图像用作水印。</span><span class="sxs-lookup"><span data-stu-id="a2678-112">How to use an image as a watermark.</span></span>
> 
> <span data-ttu-id="a2678-113">这些是 ASP.NET 编程一文中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="a2678-113">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="a2678-114">`WebImage`帮助器。</span><span class="sxs-lookup"><span data-stu-id="a2678-114">The `WebImage` helper.</span></span>
> - <span data-ttu-id="a2678-115">`Path`对象，它提供可用于操作路径和文件名的方法。</span><span class="sxs-lookup"><span data-stu-id="a2678-115">The `Path` object, which provides methods that let you manipulate path and file names.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a2678-116">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="a2678-116">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a2678-117">ASP.NET 网页 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="a2678-117">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="a2678-118">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="a2678-118">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="a2678-119">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="a2678-119">This tutorial also works with WebMatrix 3.</span></span>


<a id="Adding_an_Image"></a>
## <a name="adding-an-image-to-a-web-page-dynamically"></a><span data-ttu-id="a2678-120">动态添加到 Web 页的图像</span><span class="sxs-lookup"><span data-stu-id="a2678-120">Adding an Image to a Web Page Dynamically</span></span>

<span data-ttu-id="a2678-121">在开发网站时，可以向你的网站和单个页面添加图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-121">You can add images to your website and to individual pages while you're developing the website.</span></span> <span data-ttu-id="a2678-122">您还可以让用户上传可能适用于任务，例如让他们添加个人资料照片的图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-122">You can also let users upload images, which might be useful for tasks like letting them add a profile photo.</span></span>

<span data-ttu-id="a2678-123">如果映像已在站点上可用，并且只是想要在页面上显示，则使用对应的 HTML`<img>`元素，如下：</span><span class="sxs-lookup"><span data-stu-id="a2678-123">If an image is already available on your site and you just want to display it on a page, you use an HTML `<img>` element like this:</span></span>

[!code-html[Main](9-working-with-images/samples/sample1.html)]

<span data-ttu-id="a2678-124">有时，不过，您需要能够动态显示图像&#8212;，它是不知道什么图像之前的页面正在显示。</span><span class="sxs-lookup"><span data-stu-id="a2678-124">Sometimes, though, you need to be able to display images dynamically &#8212; that is, you don't know what image to display until the page is running.</span></span>

<span data-ttu-id="a2678-125">在本部分中的过程演示如何的动态用户在其中指定映像名称的列表中的图像文件名称中显示图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-125">The procedure in this section shows how to display an image on the fly where users specify the image file name from a list of image names.</span></span> <span data-ttu-id="a2678-126">他们从下拉列表中，选择的映像的名称和时在提交页，显示他们选择的映像。</span><span class="sxs-lookup"><span data-stu-id="a2678-126">They select the name of the image from a drop-down list, and when they submit the page, the image they selected is displayed.</span></span>

<span data-ttu-id="a2678-127">![[image]](9-working-with-images/_static/image1.jpg "ch9images 1.jpg")</span><span class="sxs-lookup"><span data-stu-id="a2678-127">![[image]](9-working-with-images/_static/image1.jpg "ch9images-1.jpg")</span></span>

1. <span data-ttu-id="a2678-128">在 WebMatrix 中，创建新的网站。</span><span class="sxs-lookup"><span data-stu-id="a2678-128">In WebMatrix, create a new website.</span></span>
2. <span data-ttu-id="a2678-129">添加一个名为的新页*DynamicImage.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a2678-129">Add a new page named *DynamicImage.cshtml*.</span></span>
3. <span data-ttu-id="a2678-130">在该网站的根文件夹中，添加一个新文件夹并将其命名*映像*。</span><span class="sxs-lookup"><span data-stu-id="a2678-130">In the root folder of the website, add a new folder and name it *images*.</span></span>
4. <span data-ttu-id="a2678-131">四个将映像添加到*映像*刚创建的文件夹。</span><span class="sxs-lookup"><span data-stu-id="a2678-131">Add four images to the *images* folder you just created.</span></span> <span data-ttu-id="a2678-132">（必须执行此操作，方便将任何图像，但它们应组合到一个页面上。）重命名图像*Photo1.jpg*， *Photo2.jpg*， *Photo3.jpg*，以及*Photo4.jpg*。</span><span class="sxs-lookup"><span data-stu-id="a2678-132">(Any images you have handy will do, but they should fit onto a page.) Rename the images *Photo1.jpg*, *Photo2.jpg*, *Photo3.jpg*, and *Photo4.jpg*.</span></span> <span data-ttu-id="a2678-133">(不会使用*Photo4.jpg*在此过程中，但是您将使用它在本文后面。)</span><span class="sxs-lookup"><span data-stu-id="a2678-133">(You won't use *Photo4.jpg* in this procedure, but you'll use it later in the article.)</span></span>
5. <span data-ttu-id="a2678-134">验证为只读的未标记的四个映像。</span><span class="sxs-lookup"><span data-stu-id="a2678-134">Verify that the four images are not marked as read-only.</span></span>
6. <span data-ttu-id="a2678-135">在页中的现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="a2678-135">Replace the existing content in the page with the following:</span></span>

    [!code-cshtml[Main](9-working-with-images/samples/sample2.cshtml)]

    <span data-ttu-id="a2678-136">页的正文具有下拉列表 (`<select>`元素)，名为`photoChoice`。</span><span class="sxs-lookup"><span data-stu-id="a2678-136">The body of the page has a drop-down list (a `<select>` element) that's named `photoChoice`.</span></span> <span data-ttu-id="a2678-137">列表具有三个选项，并`value`每个列表选项的属性具有一个将放入映像的名称*映像*文件夹。</span><span class="sxs-lookup"><span data-stu-id="a2678-137">The list has three options, and the `value` attribute of each list option has the name of one of the images that you put in the *images* folder.</span></span> <span data-ttu-id="a2678-138">实质上，列表使用户可以选择一个友好名称，如&quot;照片 1&quot;，然后将传递 *.jpg*时提交页面文件名称。</span><span class="sxs-lookup"><span data-stu-id="a2678-138">Essentially, the list lets the user select a friendly name like &quot;Photo 1&quot;, and it then passes the *.jpg* file name when the page is submitted.</span></span>

    <span data-ttu-id="a2678-139">在代码中，你可以获取用户的所选内容 （即，图像文件名称） 列表中通过读取`Request["photoChoice"]`。</span><span class="sxs-lookup"><span data-stu-id="a2678-139">In the code, you can get the user's selection (in other words, the image file name) from the list by reading `Request["photoChoice"]`.</span></span> <span data-ttu-id="a2678-140">您首先查看是否存在所选内容根本。</span><span class="sxs-lookup"><span data-stu-id="a2678-140">You first see if there's a selection at all.</span></span> <span data-ttu-id="a2678-141">如果没有，您构造组成图像的文件夹名称和用户的图像文件名称的图像的路径。</span><span class="sxs-lookup"><span data-stu-id="a2678-141">If there is, you construct a path for the image that consists of the name of the folder for the images and the user's image file name.</span></span> <span data-ttu-id="a2678-142">(如果您尝试构造一个路径，但没有在中为 nothing `Request["photoChoice"]`，你将收到错误。)这会导致类似下面的相对路径：</span><span class="sxs-lookup"><span data-stu-id="a2678-142">(If you tried to construct a path but there was nothing in `Request["photoChoice"]`, you'd get an error.) This results in a relative path like this:</span></span>

    <span data-ttu-id="a2678-143">*图像/Photo1.jpg*</span><span class="sxs-lookup"><span data-stu-id="a2678-143">*images/Photo1.jpg*</span></span>

    <span data-ttu-id="a2678-144">路径存储在名为变量`imagePath`，你将需要更高版本中的页。</span><span class="sxs-lookup"><span data-stu-id="a2678-144">The path is stored in variable named `imagePath` that you'll need later in the page.</span></span>

    <span data-ttu-id="a2678-145">在正文中，此外，还有`<img>`元素用来显示用户选择的映像。</span><span class="sxs-lookup"><span data-stu-id="a2678-145">In the body, there's also an `<img>` element that's used to display the image that the user picked.</span></span> <span data-ttu-id="a2678-146">`src`属性未设置为文件的名称或 URL，像显示的静态元素。</span><span class="sxs-lookup"><span data-stu-id="a2678-146">The `src` attribute isn't set to a file name or URL, like you'd do to display a static element.</span></span> <span data-ttu-id="a2678-147">相反，设置为`@imagePath`，这意味着它从代码中设置的路径获取其值。</span><span class="sxs-lookup"><span data-stu-id="a2678-147">Instead, it's set to `@imagePath`, meaning that it gets its value from the path you set in code.</span></span>

    <span data-ttu-id="a2678-148">第一次该页面运行，不过，没有图像若要显示，因为用户尚未选择任何内容。</span><span class="sxs-lookup"><span data-stu-id="a2678-148">The first time that the page runs, though, there's no image to display, because the user hasn't selected anything.</span></span> <span data-ttu-id="a2678-149">这通常就意味着`src`属性将为空，并且图像会显示为红色&quot;x&quot; （或在浏览器呈现任何内容时找不到图像）。</span><span class="sxs-lookup"><span data-stu-id="a2678-149">This would normally mean that the `src` attribute would be empty and the image would show up as a red &quot;x&quot; (or whatever the browser renders when it can't find an image).</span></span> <span data-ttu-id="a2678-150">若要防止此情况，您将放`<img>`中的元素`if`块，可测试以查看是否`imagePath`变量中包含的任何内容。</span><span class="sxs-lookup"><span data-stu-id="a2678-150">To prevent this, you put the `<img>` element in an `if` block that tests to see whether the `imagePath` variable has anything in it.</span></span> <span data-ttu-id="a2678-151">如果用户已做出选择，`imagePath`包含的路径。</span><span class="sxs-lookup"><span data-stu-id="a2678-151">If the user made a selection, `imagePath` contains the path.</span></span> <span data-ttu-id="a2678-152">如果用户未挑选一个映像，或者如果这是首次将显示的页，`<img>`元素甚至不会呈现。</span><span class="sxs-lookup"><span data-stu-id="a2678-152">If the user didn't pick an image or if this is the first time the page is displayed, the `<img>` element isn't even rendered.</span></span>
7. <span data-ttu-id="a2678-153">保存该文件并在浏览器中运行此页。</span><span class="sxs-lookup"><span data-stu-id="a2678-153">Save the file and run the page in a browser.</span></span> <span data-ttu-id="a2678-154">(请确保的页中选择**文件**工作区之前运行它。)</span><span class="sxs-lookup"><span data-stu-id="a2678-154">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
8. <span data-ttu-id="a2678-155">从下拉列表中选择一个映像，然后单击**示例图像**。</span><span class="sxs-lookup"><span data-stu-id="a2678-155">Select an image from the drop-down list and then click **Sample Image**.</span></span> <span data-ttu-id="a2678-156">请确保您看到的不同选择不同的映像。</span><span class="sxs-lookup"><span data-stu-id="a2678-156">Make sure that you see different images for different choices.</span></span>

<a id="Uploading_an_Image"></a>
## <a name="uploading-an-image"></a><span data-ttu-id="a2678-157">上传图像</span><span class="sxs-lookup"><span data-stu-id="a2678-157">Uploading an Image</span></span>

<span data-ttu-id="a2678-158">前面的示例演示如何动态显示图像，但它仅适用于已在网站的映像。</span><span class="sxs-lookup"><span data-stu-id="a2678-158">The previous example showed you how to display an image dynamically, but it worked only with images that were already on your website.</span></span> <span data-ttu-id="a2678-159">此过程说明如何以使用户可以上传的映像，然后在页面显示。</span><span class="sxs-lookup"><span data-stu-id="a2678-159">This procedure shows how to let users upload an image, which is then displayed on the page.</span></span> <span data-ttu-id="a2678-160">在 ASP.NET 中，您可以操作上使用动态映像`WebImage`帮助程序，有方法，可用于创建、 处理和保存图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-160">In ASP.NET, you can manipulate images on the fly using the `WebImage` helper, which has methods that let you create, manipulate, and save images.</span></span> <span data-ttu-id="a2678-161">`WebImage`帮助器支持所有常见 web 图像文件的类型，包括 *.jpg*， *.png*，并且 *.bmp*。</span><span class="sxs-lookup"><span data-stu-id="a2678-161">The `WebImage` helper supports all the common web image file types, including *.jpg*, *.png*, and *.bmp*.</span></span> <span data-ttu-id="a2678-162">在整篇文章中，将使用 *.jpg*映像，但你可以使用任何图像类型。</span><span class="sxs-lookup"><span data-stu-id="a2678-162">Throughout this article, you'll use *.jpg* images, but you can use any of the image types.</span></span>

<span data-ttu-id="a2678-163">![[image]](9-working-with-images/_static/image2.jpg "ch9images 2.jpg")</span><span class="sxs-lookup"><span data-stu-id="a2678-163">![[image]](9-working-with-images/_static/image2.jpg "ch9images-2.jpg")</span></span>

1. <span data-ttu-id="a2678-164">添加一个新页面并将其命名*UploadImage.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a2678-164">Add a new page and name it *UploadImage.cshtml*.</span></span>
2. <span data-ttu-id="a2678-165">在页中的现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="a2678-165">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample3.cshtml)]

    <span data-ttu-id="a2678-166">具有文本正文`<input type="file">`元素，它使用户可以选择要上载的文件。</span><span class="sxs-lookup"><span data-stu-id="a2678-166">The body of the text has an `<input type="file">` element, which lets users select a file to upload.</span></span> <span data-ttu-id="a2678-167">在单击时**提交**，他们选择的文件和窗体提交。</span><span class="sxs-lookup"><span data-stu-id="a2678-167">When they click **Submit**, the file they picked is submitted along with the form.</span></span>

    <span data-ttu-id="a2678-168">若要获取上传的映像，请使用`WebImage`帮助程序，有各种有用的方法，用于处理图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-168">To get the uploaded image, you use the `WebImage` helper, which has all sorts of useful methods for working with images.</span></span> <span data-ttu-id="a2678-169">具体而言，使用`WebImage.GetImageFromRequest`以获取上传的图像 （如果有） 并将其存储在一个名为变量`photo`。</span><span class="sxs-lookup"><span data-stu-id="a2678-169">Specifically, you use `WebImage.GetImageFromRequest` to get the uploaded image (if any) and store it in a variable named `photo`.</span></span>

    <span data-ttu-id="a2678-170">在此示例中的工作很多涉及获取和设置文件和路径名称。</span><span class="sxs-lookup"><span data-stu-id="a2678-170">A lot of the work in this example involves getting and setting file and path names.</span></span> <span data-ttu-id="a2678-171">问题是你想要获取用户上传，图像的名称 （和只是名称），然后创建要用于存储映像的新路径。</span><span class="sxs-lookup"><span data-stu-id="a2678-171">The issue is that you want to get the name (and just the name) of the image that the user uploaded, and then create a new path for where you're going to store the image.</span></span> <span data-ttu-id="a2678-172">因为用户可能无法上传具有相同名称的多个映像，使用少量额外代码以创建唯一的名称，并确保用户不会覆盖现有的图片。</span><span class="sxs-lookup"><span data-stu-id="a2678-172">Because users could potentially upload multiple images that have the same name, you use a bit of extra code to create unique names and make sure that users don't overwrite existing pictures.</span></span>

    <span data-ttu-id="a2678-173">如果实际上已上载图像 (测试`if (photo != null)`)，从图像的获取映像名称`FileName`属性。</span><span class="sxs-lookup"><span data-stu-id="a2678-173">If an image actually has been uploaded (the test `if (photo != null)`), you get the image name from the image's `FileName` property.</span></span> <span data-ttu-id="a2678-174">当用户上传图像，`FileName`包含用户的原始名称，其中包括从用户的计算机的路径。</span><span class="sxs-lookup"><span data-stu-id="a2678-174">When the user uploads the image, `FileName` contains the user's original name, which includes the path from the user's computer.</span></span> <span data-ttu-id="a2678-175">它可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="a2678-175">It might look like this:</span></span>

    <span data-ttu-id="a2678-176">*C:\Users\Joe\Pictures\SamplePhoto1.jpg*</span><span class="sxs-lookup"><span data-stu-id="a2678-176">*C:\Users\Joe\Pictures\SamplePhoto1.jpg*</span></span>

    <span data-ttu-id="a2678-177">您不希望所有该路径信息，但&#8212;只是想实际文件名称 (*SamplePhoto1.jpg*)。</span><span class="sxs-lookup"><span data-stu-id="a2678-177">You don't want all that path information, though &#8212; you just want the actual file name (*SamplePhoto1.jpg*).</span></span> <span data-ttu-id="a2678-178">可以去除使用的只是从路径文件`Path.GetFileName`方法，如下：</span><span class="sxs-lookup"><span data-stu-id="a2678-178">You can strip out just the file from a path by using the `Path.GetFileName` method, like this:</span></span>

    [!code-csharp[Main](9-working-with-images/samples/sample4.cs)]

    <span data-ttu-id="a2678-179">然后，通过将 GUID 添加到原始名称创建新的唯一文件名。</span><span class="sxs-lookup"><span data-stu-id="a2678-179">You then create a new unique file name by adding a GUID to the original name.</span></span> <span data-ttu-id="a2678-180">(有关 Guid 的详细信息，请参阅[有关 Guid](#SB_AboutGUIDs)这篇文章中更高版本。)然后您构造可用于将图像保存的完整路径。</span><span class="sxs-lookup"><span data-stu-id="a2678-180">(For more about GUIDs, see [About GUIDs](#SB_AboutGUIDs) later in this article.) Then you construct a complete path that you can use to save the image.</span></span> <span data-ttu-id="a2678-181">在保存路径由新的文件名、 文件夹 （映像） 和当前的网站位置。</span><span class="sxs-lookup"><span data-stu-id="a2678-181">The save path is made up of the new file name, the folder (images), and the current website location.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a2678-182">为你的代码来保存文件的顺序*映像*文件夹中，应用程序需要读写该文件夹的权限。</span><span class="sxs-lookup"><span data-stu-id="a2678-182">In order for your code to save files in the *images* folder, the application needs read-write permissions for that folder.</span></span> <span data-ttu-id="a2678-183">在开发计算机上这不是通常出现问题。</span><span class="sxs-lookup"><span data-stu-id="a2678-183">On your development computer this is not typically an issue.</span></span> <span data-ttu-id="a2678-184">但是，当将您的网站发布到宿主提供程序的 web 服务器，您可能需要显式设置这些权限。</span><span class="sxs-lookup"><span data-stu-id="a2678-184">However, when you publish your site to a hosting provider's web server, you might need to explicitly set those permissions.</span></span> <span data-ttu-id="a2678-185">如果托管提供商的服务器上运行此代码，并出现错误，请与宿主提供程序中，若要了解如何设置这些权限。</span><span class="sxs-lookup"><span data-stu-id="a2678-185">If you run this code on a hosting provider's server and get errors, check with the hosting provider to find out how to set those permissions.</span></span>

    <span data-ttu-id="a2678-186">最后，将传递在保存路径`Save`方法的`WebImage`帮助器。</span><span class="sxs-lookup"><span data-stu-id="a2678-186">Finally, you pass the save path to the `Save` method of the `WebImage` helper.</span></span> <span data-ttu-id="a2678-187">这会存储上传的图像采用新名称。</span><span class="sxs-lookup"><span data-stu-id="a2678-187">This stores the uploaded image under its new name.</span></span> <span data-ttu-id="a2678-188">保存方法如下所示： `photo.Save(@"~\" + imagePath)`。</span><span class="sxs-lookup"><span data-stu-id="a2678-188">The save method looks like this: `photo.Save(@"~\" + imagePath)`.</span></span> <span data-ttu-id="a2678-189">完整路径追加到`@"~\"`，这是当前的网站位置。</span><span class="sxs-lookup"><span data-stu-id="a2678-189">The complete path is appended to `@"~\"`, which is the current website location.</span></span> <span data-ttu-id="a2678-190">(有关`~`运算符，请参阅[ASP.NET Web 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths)。)</span><span class="sxs-lookup"><span data-stu-id="a2678-190">(For information about the `~` operator, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths).)</span></span>

    <span data-ttu-id="a2678-191">在上一示例中，页的正文包含`<img>`元素显示图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-191">As in the previous example, the body of the page contains an `<img>` element to display the image.</span></span> <span data-ttu-id="a2678-192">如果`imagePath`已设置`<img>`呈现元素并将其`src`属性设置为`imagePath`值。</span><span class="sxs-lookup"><span data-stu-id="a2678-192">If `imagePath` has been set, the `<img>` element is rendered and its `src` attribute is set to the `imagePath` value.</span></span>
3. <span data-ttu-id="a2678-193">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="a2678-193">Run the page in a browser.</span></span>
4. <span data-ttu-id="a2678-194">上传图像，并确保它在页中显示。</span><span class="sxs-lookup"><span data-stu-id="a2678-194">Upload an image and make sure it's displayed in the page.</span></span>
5. <span data-ttu-id="a2678-195">在你的站点，打开*映像*文件夹。</span><span class="sxs-lookup"><span data-stu-id="a2678-195">In your site, open the *images* folder.</span></span> <span data-ttu-id="a2678-196">你看到了其文件名外观如下所示，添加新文件::</span><span class="sxs-lookup"><span data-stu-id="a2678-196">You see that a new file has been added whose file name looks something like this::</span></span> 

    <span data-ttu-id="a2678-197">*45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto.png*</span><span class="sxs-lookup"><span data-stu-id="a2678-197">*45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto.png*</span></span>

    <span data-ttu-id="a2678-198">这是使用 GUID 作为名称前缀上载的映像。</span><span class="sxs-lookup"><span data-stu-id="a2678-198">This is the image that you uploaded with a GUID prefixed to the name.</span></span> <span data-ttu-id="a2678-199">(你自己的文件将具有不同的 GUID，可能命名为类似不同于*MyPhoto.png*。)</span><span class="sxs-lookup"><span data-stu-id="a2678-199">(Your own file will have a different GUID and probably is named something different than *MyPhoto.png*.)</span></span>

> [!TIP] 
> 
> <a id="SB_AboutGUIDs"></a>
> ### <a name="about-guids"></a><span data-ttu-id="a2678-200">有关 Guid</span><span class="sxs-lookup"><span data-stu-id="a2678-200">About GUIDs</span></span>
> 
> <span data-ttu-id="a2678-201">GUID (全局唯一 ID) 是一个标识符，通常以如下格式呈现： `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`。</span><span class="sxs-lookup"><span data-stu-id="a2678-201">A GUID (globally-unique ID) is an identifier that's usually rendered in a format like this: `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`.</span></span> <span data-ttu-id="a2678-202">数字和字母 （从 A 到 F) 存在差异的每个 GUID，但它们都遵循使用组 8-4-4-4-12 个字符的模式。</span><span class="sxs-lookup"><span data-stu-id="a2678-202">The numbers and letters (from A-F) differ for each GUID, but they all follow the pattern of using groups of 8-4-4-4-12 characters.</span></span> <span data-ttu-id="a2678-203">（从技术上讲，GUID 是一个 16 字节 128 位数字。）当您需要一个 GUID 时，可以调用专门为您生成一个 GUID 的代码。</span><span class="sxs-lookup"><span data-stu-id="a2678-203">(Technically, a GUID is a 16-byte/128-bit number.) When you need a GUID, you can call specialized code that generates a GUID for you.</span></span> <span data-ttu-id="a2678-204">Guid 背后的理念是，之间的数很大的规模 (3.4 x 10<sup>38</sup>)，用于生成它的算法，得到数几乎能保证是一种类型之一。</span><span class="sxs-lookup"><span data-stu-id="a2678-204">The idea behind GUIDs is that between the enormous size of the number (3.4 x 10<sup>38</sup>) and the algorithm for generating it, the resulting number is virtually guaranteed to be one of a kind.</span></span> <span data-ttu-id="a2678-205">因此，Guid 是好办法时必须保证不会两次使用相同的名称生成操作的名称。</span><span class="sxs-lookup"><span data-stu-id="a2678-205">GUIDs therefore are a good way to generate names for things when you must guarantee that you won't use the same name twice.</span></span> <span data-ttu-id="a2678-206">缺点，当然，是，Guid 并不特别是用户友好，因此他们趋向于仅在代码中使用名称时使用。</span><span class="sxs-lookup"><span data-stu-id="a2678-206">The downside, of course, is that GUIDs aren't particularly user friendly, so they tend to be used when the name is used only in code.</span></span>


<a id="Resizing_an_Image"></a>
## <a name="resizing-an-image"></a><span data-ttu-id="a2678-207">调整图像的大小</span><span class="sxs-lookup"><span data-stu-id="a2678-207">Resizing an Image</span></span>

<span data-ttu-id="a2678-208">如果你的网站接受来自用户的图像，您可能想要调整图像大小之前显示或将其保存。</span><span class="sxs-lookup"><span data-stu-id="a2678-208">If your website accepts images from a user, you might want to resize the images before you display or save them.</span></span> <span data-ttu-id="a2678-209">您可以再次使用`WebImage`的此帮助器。</span><span class="sxs-lookup"><span data-stu-id="a2678-209">You can again use the `WebImage` helper for this.</span></span>

<span data-ttu-id="a2678-210">此过程说明如何调整已上传的图像创建缩略图，然后在网站中保存缩略图和原始图像大小。</span><span class="sxs-lookup"><span data-stu-id="a2678-210">This procedure shows how to resize an uploaded image to create a thumbnail and then save the thumbnail and original image in the website.</span></span> <span data-ttu-id="a2678-211">在页面上显示缩略图，并使用超链接将用户重定向到尺寸的图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-211">You display the thumbnail on the page and use a hyperlink to redirect users to the full-sized image.</span></span>

<span data-ttu-id="a2678-212">![[image]](9-working-with-images/_static/image3.jpg "ch9images 3.jpg")</span><span class="sxs-lookup"><span data-stu-id="a2678-212">![[image]](9-working-with-images/_static/image3.jpg "ch9images-3.jpg")</span></span>

1. <span data-ttu-id="a2678-213">添加一个名为的新页*Thumbnail.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a2678-213">Add a new page named *Thumbnail.cshtml*.</span></span>
2. <span data-ttu-id="a2678-214">在中*映像*文件夹中，创建一个名为子*thumbs*。</span><span class="sxs-lookup"><span data-stu-id="a2678-214">In the *images* folder, create a subfolder named *thumbs*.</span></span>
3. <span data-ttu-id="a2678-215">在页中的现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="a2678-215">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample5.cshtml)]

    <span data-ttu-id="a2678-216">此代码是上一示例中类似于代码。</span><span class="sxs-lookup"><span data-stu-id="a2678-216">This code is similar to the code from the previous example.</span></span> <span data-ttu-id="a2678-217">不同之处是，此代码将图像保存两次，一次通常一次后创建缩略图图像的副本。</span><span class="sxs-lookup"><span data-stu-id="a2678-217">The difference is that this code saves the image twice, once normally and once after you create a thumbnail copy of the image.</span></span> <span data-ttu-id="a2678-218">首先获取上传的映像并将其保存在*映像*文件夹。</span><span class="sxs-lookup"><span data-stu-id="a2678-218">First you get the uploaded image and save it in the *images* folder.</span></span> <span data-ttu-id="a2678-219">然后构建新的缩略图的路径。</span><span class="sxs-lookup"><span data-stu-id="a2678-219">You then construct a new path for the thumbnail image.</span></span> <span data-ttu-id="a2678-220">若要实际创建缩略图，请调用`WebImage`帮助者`Resize`方法来创建一个 60 像素由 60 像素的图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-220">To actually create the thumbnail, you call the `WebImage` helper's `Resize` method to create a 60-pixel by 60-pixel image.</span></span> <span data-ttu-id="a2678-221">该示例演示如何保留纵横比，以及如何可以防止图像被放大 （如果新大小实际上会使映像更大）。</span><span class="sxs-lookup"><span data-stu-id="a2678-221">The example shows how you preserve the aspect ratio and how you can prevent the image from being enlarged (in case the new size would actually make the image larger).</span></span> <span data-ttu-id="a2678-222">调整大小的图像则保存在*thumbs*子文件夹。</span><span class="sxs-lookup"><span data-stu-id="a2678-222">The resized image is then saved in the *thumbs* subfolder.</span></span>

    <span data-ttu-id="a2678-223">在结束标记时，使用相同`<img>`具有动态元素`src`已了解在前面的示例有条件地显示的图像的属性。</span><span class="sxs-lookup"><span data-stu-id="a2678-223">At the end of the markup, you use the same `<img>` element with the dynamic `src` attribute that you've seen in the previous examples to conditionally show the image.</span></span> <span data-ttu-id="a2678-224">在这种情况下，您显示缩略图。</span><span class="sxs-lookup"><span data-stu-id="a2678-224">In this case, you display the thumbnail.</span></span> <span data-ttu-id="a2678-225">此外使用`<a>`元素来创建大版本的映像的超链接。</span><span class="sxs-lookup"><span data-stu-id="a2678-225">You also use an `<a>` element to create a hyperlink to the big version of the image.</span></span> <span data-ttu-id="a2678-226">如同`src`的属性`<img>`元素，设置`href`的属性`<a>`动态地为任何内容中的元素`imagePath`。</span><span class="sxs-lookup"><span data-stu-id="a2678-226">As with the `src` attribute of the `<img>` element, you set the `href` attribute of the `<a>` element dynamically to whatever is in `imagePath`.</span></span> <span data-ttu-id="a2678-227">若要确保该路径可以正常运行以 URL 形式，可以传递`imagePath`到`Html.AttributeEncode`方法，后者将在路径中的保留的字符转换为确定在 URL 中的字符。</span><span class="sxs-lookup"><span data-stu-id="a2678-227">To make sure that the path can work as a URL, you pass `imagePath` to the `Html.AttributeEncode` method, which converts reserved characters in the path to characters that are ok in a URL.</span></span>
4. <span data-ttu-id="a2678-228">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="a2678-228">Run the page in a browser.</span></span>
5. <span data-ttu-id="a2678-229">上传照片并验证显示缩略图。</span><span class="sxs-lookup"><span data-stu-id="a2678-229">Upload a photo and verify that the thumbnail is shown.</span></span>
6. <span data-ttu-id="a2678-230">单击要查看原尺寸图像的缩略图。</span><span class="sxs-lookup"><span data-stu-id="a2678-230">Click the thumbnail to see the full-size image.</span></span>
7. <span data-ttu-id="a2678-231">在中*映像*并*缩略图图像/*，请注意，已添加新文件。</span><span class="sxs-lookup"><span data-stu-id="a2678-231">In the *images* and *images/thumbs*, note that new files have been added.</span></span>

<a id="Rotating_and_Flipping"></a>
## <a name="rotating-and-flipping-an-image"></a><span data-ttu-id="a2678-232">旋转和翻转图像</span><span class="sxs-lookup"><span data-stu-id="a2678-232">Rotating and Flipping an Image</span></span>

<span data-ttu-id="a2678-233">`WebImage`帮助器还允许您翻转和旋转图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-233">The `WebImage` helper also lets you flip and rotate images.</span></span> <span data-ttu-id="a2678-234">此过程说明如何从服务器获取图像，（垂直） 上下翻转图像，保存该文件，然后在页面上显示翻转的图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-234">This procedure shows how to get an image from the server, flip the image upside down (vertically), save it, and then display the flipped image on the page.</span></span> <span data-ttu-id="a2678-235">在此示例中，您只需使用你已在服务器的文件 (*Photo2.jpg*)。</span><span class="sxs-lookup"><span data-stu-id="a2678-235">In this example, you're just using a file you already have on the server (*Photo2.jpg*).</span></span> <span data-ttu-id="a2678-236">在实际的应用程序，可能会翻转图像动态，像前面的示例中一样获取其名称。</span><span class="sxs-lookup"><span data-stu-id="a2678-236">In a real application, you'd probably flip an image whose name you get dynamically, like you did in previous examples.</span></span>

<span data-ttu-id="a2678-237">![[image]](9-working-with-images/_static/image4.jpg "ch9images 4.jpg")</span><span class="sxs-lookup"><span data-stu-id="a2678-237">![[image]](9-working-with-images/_static/image4.jpg "ch9images-4.jpg")</span></span>

1. <span data-ttu-id="a2678-238">添加一个名为的新页*FlipImage.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a2678-238">Add a new page named *FlipImage.cshtml*.</span></span>
2. <span data-ttu-id="a2678-239">在页中的现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="a2678-239">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample6.cshtml)]

    <span data-ttu-id="a2678-240">该代码使用`WebImage`帮助者从服务器获取图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-240">The code uses the `WebImage` helper to get an image from the server.</span></span> <span data-ttu-id="a2678-241">创建使用相同的方法来保存图像，前面的示例中使用的图像的路径并将该路径传递时创建图像使用`WebImage`:</span><span class="sxs-lookup"><span data-stu-id="a2678-241">You create the path to the image using the same technique you used in earlier examples for saving images, and you pass that path when you create an image using `WebImage`:</span></span>

    [!code-javascript[Main](9-working-with-images/samples/sample7.js)]

    <span data-ttu-id="a2678-242">如果找到的图像，则构造新路径和文件名的名称，像前面的示例中一样。</span><span class="sxs-lookup"><span data-stu-id="a2678-242">If an image is found, you construct a new path and file name, like you did in earlier examples.</span></span> <span data-ttu-id="a2678-243">若要翻转图像，请调用`FlipVertical`方法，然后再次保存该图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-243">To flip the image, you call the `FlipVertical` method, and then you save the image again.</span></span>

    <span data-ttu-id="a2678-244">图像时再次显示的页上通过使用`<img>`具有元素`src`属性设置为`imagePath`。</span><span class="sxs-lookup"><span data-stu-id="a2678-244">The image is again displayed on the page by using the `<img>` element with the `src` attribute set to `imagePath`.</span></span>
3. <span data-ttu-id="a2678-245">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="a2678-245">Run the page in a browser.</span></span> <span data-ttu-id="a2678-246">此图像可查看*Photo2.jpg*正面朝下所示。</span><span class="sxs-lookup"><span data-stu-id="a2678-246">The image for *Photo2.jpg* is shown upside down.</span></span>
4. <span data-ttu-id="a2678-247">请刷新页面或请求页上再次看到图像类型为翻转的右侧向上又。</span><span class="sxs-lookup"><span data-stu-id="a2678-247">Refresh the page or request the page again to see the image is flipped right side up again.</span></span>

<span data-ttu-id="a2678-248">若要旋转图像，您可以使用相同的代码，不同之处在于而不是调用`FlipVertical`或`FlipHorizontal`，则调用`RotateLeft`或`RotateRight`。</span><span class="sxs-lookup"><span data-stu-id="a2678-248">To rotate an image, you use the same code, except that instead of calling the `FlipVertical` or `FlipHorizontal`, you call `RotateLeft` or `RotateRight`.</span></span>

<a id="Adding_a_Watermark"></a>
## <a name="adding-a-watermark-to-an-image"></a><span data-ttu-id="a2678-249">向图像添加水印</span><span class="sxs-lookup"><span data-stu-id="a2678-249">Adding a Watermark to an Image</span></span>

<span data-ttu-id="a2678-250">当将映像添加到你的网站时，你可能想要将水印添加到映像，然后将其保存，或在页面上显示。</span><span class="sxs-lookup"><span data-stu-id="a2678-250">When you add images to your website, you might want to add a watermark to the image before you save it or display it on a page.</span></span> <span data-ttu-id="a2678-251">人们经常使用水印，将版权信息添加到映像，或将播发其业务名称。</span><span class="sxs-lookup"><span data-stu-id="a2678-251">People often use watermarks to add copyright information to an image or to advertise their business name.</span></span>

<span data-ttu-id="a2678-252">![[image]](9-working-with-images/_static/image5.jpg "ch9images 5.jpg")</span><span class="sxs-lookup"><span data-stu-id="a2678-252">![[image]](9-working-with-images/_static/image5.jpg "ch9images-5.jpg")</span></span>

1. <span data-ttu-id="a2678-253">添加一个名为的新页*Watermark.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a2678-253">Add a new page named *Watermark.cshtml*.</span></span>
2. <span data-ttu-id="a2678-254">在页中的现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="a2678-254">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample8.cshtml)]

    <span data-ttu-id="a2678-255">此代码就像中的代码*FlipImage.cshtml*前面的页 (尽管这次使用*Photo3.jpg*文件)。</span><span class="sxs-lookup"><span data-stu-id="a2678-255">This code is like the code in the *FlipImage.cshtml* page from earlier (although this time it uses the *Photo3.jpg* file).</span></span> <span data-ttu-id="a2678-256">若要添加水印，则调用`WebImage`帮助者`AddTextWatermark`方法之前保存的图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-256">To add the watermark, you call the `WebImage` helper's `AddTextWatermark` method before you save the image.</span></span> <span data-ttu-id="a2678-257">在调用`AddTextWatermark`，将文本&quot;我水印&quot;、 将字体颜色设置为黄色，并设置为 Arial 字体系列。</span><span class="sxs-lookup"><span data-stu-id="a2678-257">In the call to `AddTextWatermark`, you pass the text &quot;My Watermark&quot;, set the font color to yellow, and set the font family to Arial.</span></span> <span data-ttu-id="a2678-258">(尽管它不显示在这里，`WebImage`帮助程序，您还可以指定不透明度、 字体系列和字体大小和水印文本的位置。)保存图像时它不必须是只读的。</span><span class="sxs-lookup"><span data-stu-id="a2678-258">(Although it's not shown here, the `WebImage` helper also lets you specify opacity, font family and font size, and the position of the watermark text.) When you save the image it must not be read-only.</span></span>

    <span data-ttu-id="a2678-259">如您所见之前，图像显示在页上通过使用`<img>`元素的 src 属性设置为`@imagePath`。</span><span class="sxs-lookup"><span data-stu-id="a2678-259">As you've seen before, the image is displayed on the page by using the `<img>` element with the src attribute set to `@imagePath`.</span></span>
3. <span data-ttu-id="a2678-260">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="a2678-260">Run the page in a browser.</span></span> <span data-ttu-id="a2678-261">请注意右下角的图像，文本"My 水印"。</span><span class="sxs-lookup"><span data-stu-id="a2678-261">Notice the text "My Watermark" at the bottom-right corner of the image.</span></span>

<a id="Using_an_Image_as_a_Watermark"></a>
## <a name="using-an-image-as-a-watermark"></a><span data-ttu-id="a2678-262">将图像用作水印</span><span class="sxs-lookup"><span data-stu-id="a2678-262">Using an Image As a Watermark</span></span>

<span data-ttu-id="a2678-263">而不是使用文本的水印，可以使用另一个映像。</span><span class="sxs-lookup"><span data-stu-id="a2678-263">Instead of using text for a watermark, you can use another image.</span></span> <span data-ttu-id="a2678-264">人们有时使用公司徽标之类的映像作为水印，或它们而不是文本中使用水印图像的版权信息。</span><span class="sxs-lookup"><span data-stu-id="a2678-264">People sometimes use images like a company logo as a watermark, or they use a watermark image instead of text for copyright information.</span></span>

<span data-ttu-id="a2678-265">![[image]](9-working-with-images/_static/image6.jpg "ch9images 6.jpg")</span><span class="sxs-lookup"><span data-stu-id="a2678-265">![[image]](9-working-with-images/_static/image6.jpg "ch9images-6.jpg")</span></span>

1. <span data-ttu-id="a2678-266">添加一个名为的新页*ImageWatermark.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a2678-266">Add a new page named *ImageWatermark.cshtml*.</span></span>
2. <span data-ttu-id="a2678-267">添加到图像*映像*文件夹，可以用作徽标，并且重命名图像*MyCompanyLogo.jpg*。</span><span class="sxs-lookup"><span data-stu-id="a2678-267">Add an image to the *images* folder that you can use as a logo, and rename the image *MyCompanyLogo.jpg*.</span></span> <span data-ttu-id="a2678-268">此图像应是您所见清楚如果设置为 80 像素宽和高 20 像素的图像。</span><span class="sxs-lookup"><span data-stu-id="a2678-268">This image should be an image that you can see clearly when it's set to 80 pixels wide and 20 pixels high.</span></span>
3. <span data-ttu-id="a2678-269">在页中的现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="a2678-269">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample9.cshtml)]

    <span data-ttu-id="a2678-270">这是在前面的示例中的代码的另一个变体。</span><span class="sxs-lookup"><span data-stu-id="a2678-270">This is another variation on the code from earlier examples.</span></span> <span data-ttu-id="a2678-271">在这种情况下，调用`AddImageWatermark`将水印图像添加到目标映像 (*Photo3.jpg*) 保存图像之前。</span><span class="sxs-lookup"><span data-stu-id="a2678-271">In this case, you call `AddImageWatermark` to add the watermark image to the target image (*Photo3.jpg*) before you save the image.</span></span> <span data-ttu-id="a2678-272">当您调用`AddImageWatermark`，其宽度设置为 80 像素，高度为 20 像素。</span><span class="sxs-lookup"><span data-stu-id="a2678-272">When you call `AddImageWatermark`, you set its width to 80 pixels and the height to 20 pixels.</span></span> <span data-ttu-id="a2678-273">*MyCompanyLogo.jpg*图像水平按居中对齐和垂直方向上的目标映像底部对齐。</span><span class="sxs-lookup"><span data-stu-id="a2678-273">The *MyCompanyLogo.jpg* image is horizontally aligned in the center and vertically aligned at the bottom of the target image.</span></span> <span data-ttu-id="a2678-274">不透明度设置为 100%和填充设置为 10 像素。</span><span class="sxs-lookup"><span data-stu-id="a2678-274">The opacity is set to 100% and the padding is set to 10 pixels.</span></span> <span data-ttu-id="a2678-275">如果水印图像大于目标映像，不会发生。</span><span class="sxs-lookup"><span data-stu-id="a2678-275">If the watermark image is bigger than the target image, nothing will happen.</span></span> <span data-ttu-id="a2678-276">如果水印图像大于目标图像并设置为零的图像水印的填充，则忽略水印。</span><span class="sxs-lookup"><span data-stu-id="a2678-276">If the watermark image is bigger than the target image and you set the padding for the image watermark to zero, the watermark is ignored.</span></span>

    <span data-ttu-id="a2678-277">如前面一样，显示图像使用`<img>`元素，并动态`src`属性。</span><span class="sxs-lookup"><span data-stu-id="a2678-277">As before, you display the image using the `<img>` element and a dynamic `src` attribute.</span></span>
4. <span data-ttu-id="a2678-278">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="a2678-278">Run the page in a browser.</span></span> <span data-ttu-id="a2678-279">请注意，水印图像显示在主映像的底部。</span><span class="sxs-lookup"><span data-stu-id="a2678-279">Notice that the watermark image appears at the bottom of the main image.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="a2678-280">其他资源</span><span class="sxs-lookup"><span data-stu-id="a2678-280">Additional Resources</span></span>


[<span data-ttu-id="a2678-281">在 ASP.NET Web Pages 站点中使用文件</span><span class="sxs-lookup"><span data-stu-id="a2678-281">Working with Files in an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkId=202896)

[<span data-ttu-id="a2678-282">编程使用 Razor 语法的 ASP.NET 网页简介</span><span class="sxs-lookup"><span data-stu-id="a2678-282">Introduction to ASP.NET Web Pages Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=251587)
