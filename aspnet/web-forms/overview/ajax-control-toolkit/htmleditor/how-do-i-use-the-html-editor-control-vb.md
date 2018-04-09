---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: 如何使用 HTML 编辑器控件？ (VB) | Microsoft Docs
author: microsoft
description: HTMLEditor 是 ASP.NET AJAX 控件，您可以轻松地创建和编辑通过在工具栏中的按钮的 HTML 内容。
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 4833949a54fa9ae12eaf7b596a5fe1ddfd1f7b7a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="how-do-i-use-the-html-editor-control-vb"></a><span data-ttu-id="a6458-104">如何使用 HTML 编辑器控件？</span><span class="sxs-lookup"><span data-stu-id="a6458-104">How do I use the HTML Editor Control?</span></span> <span data-ttu-id="a6458-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="a6458-105">(VB)</span></span>
====================
<span data-ttu-id="a6458-106">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a6458-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="a6458-107">HTMLEditor 是 ASP.NET AJAX 控件，您可以轻松地创建和编辑通过在工具栏中的按钮的 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="a6458-107">HTMLEditor is an ASP.NET AJAX Control that allows you to easily create and edit HTML content via buttons in a toolbar.</span></span>


<span data-ttu-id="a6458-108">本教程旨在为你提供附带 AJAX 控件工具包的 HTML 编辑器控件的概述。</span><span class="sxs-lookup"><span data-stu-id="a6458-108">The goal of this tutorial is to provide you with an overview of the HTML Editor control included with the AJAX Control Toolkit.</span></span> <span data-ttu-id="a6458-109">HTML 编辑器包括更改字体大小、 选择一种字体、 更改背景色、 修改的前景色，选项添加链接，添加图像，更改文本对齐方式，并执行剪切、 复制和粘贴的操作 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="a6458-109">The HTML Editor includes options for changing font size, selecting a font, changing background color, modifying the foreground color, adding links, adding images, changing text alignment, and performing cut, copy, and paste operations (see Figure 1).</span></span>


<span data-ttu-id="a6458-110">[![HTML 编辑器](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a6458-110">[![The HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="a6458-111">**图 01**: HTML 编辑器 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="a6458-111">**Figure 01**: The HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image2.png))</span></span>


<span data-ttu-id="a6458-112">HTML 编辑器使您能够输入使用设计模式下的内容，也可以直接输入 HTML。</span><span class="sxs-lookup"><span data-stu-id="a6458-112">The HTML editor enables you to enter content using a design mode or you can enter HTML directly.</span></span> <span data-ttu-id="a6458-113">你还附带了用于预览 HTML 内容的选项 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="a6458-113">You also are provided with the option to preview your HTML content (see Figure 2).</span></span>


<span data-ttu-id="a6458-114">[![设计、 HTML 和预览按钮](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="a6458-114">[![Design, HTML, and Preview buttons](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)</span></span>

<span data-ttu-id="a6458-115">**图 02**： 设计、 HTML 和预览按钮 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="a6458-115">**Figure 02**: Design, HTML, and Preview buttons([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image4.png))</span></span>


<span data-ttu-id="a6458-116">在本教程中，你将学习如何显示 HTML 编辑器，如何自定义工具栏按钮显示在 HTML 编辑器中，以及如何避免跨站点脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="a6458-116">In this tutorial, you learn how to display the HTML Editor, how to customize the toolbar buttons that appear in the HTML Editor, and how to avoid Cross-Site Scripting Attacks.</span></span>

## <a name="displaying-the-html-editor"></a><span data-ttu-id="a6458-117">显示 HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="a6458-117">Displaying the HTML Editor</span></span>

<span data-ttu-id="a6458-118">你可以在 ASP.NET 页中使用 HTML 编辑器之前，首先必须将 ScriptManager 控件添加到页面中。</span><span class="sxs-lookup"><span data-stu-id="a6458-118">Before you can use the HTML Editor in an ASP.NET page, you must first add a ScriptManager control to the page.</span></span> <span data-ttu-id="a6458-119">ScriptManager 控件位于下 Visual Studio/Visual Web Developer Express 工具箱中的 AJAX Extensions 选项卡。</span><span class="sxs-lookup"><span data-stu-id="a6458-119">The ScriptManager control is located beneath the AJAX Extensions tab in the Visual Studio/Visual Web Developer Express toolbox.</span></span>

<span data-ttu-id="a6458-120">应将 ScriptManager 控件放在之前页面上的任何其他控件的页面的顶部。</span><span class="sxs-lookup"><span data-stu-id="a6458-120">You should place the ScriptManager control at the top of the page before any other controls on the page.</span></span> <span data-ttu-id="a6458-121">例如，可以将它立即打开服务器端下面&lt;窗体&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="a6458-121">For example, you can place it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="a6458-122">HTML 编辑器控件位于工具箱中与 AJAX 控件工具包控件的其余部分。</span><span class="sxs-lookup"><span data-stu-id="a6458-122">The HTML Editor control is located in the toolbox with the rest of the AJAX Control Toolkit controls.</span></span> <span data-ttu-id="a6458-123">它名为编辑器控件 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="a6458-123">It is named the Editor control (see Figure 3).</span></span>


<span data-ttu-id="a6458-124">[![HTML 编辑器控件](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="a6458-124">[![The HTML Editor control](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)</span></span>

<span data-ttu-id="a6458-125">**图 03**: HTML 编辑器控件 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="a6458-125">**Figure 03**: The HTML Editor control([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image6.png))</span></span>


<span data-ttu-id="a6458-126">HTML 编辑器拖到页面上后，你可以在属性表中设置其属性。</span><span class="sxs-lookup"><span data-stu-id="a6458-126">After you drag the HTML Editor onto a page, you can set its properties in the property sheet.</span></span> <span data-ttu-id="a6458-127">例如，你通常想要设置宽度和高度属性。</span><span class="sxs-lookup"><span data-stu-id="a6458-127">For example, you normally want to set the Width and Height properties.</span></span> <span data-ttu-id="a6458-128">列表 1 包含 ASP.NET 页包含 HTML 编辑器源。</span><span class="sxs-lookup"><span data-stu-id="a6458-128">Listing 1 contains the source for an ASP.NET page that contains an HTML editor.</span></span>

<span data-ttu-id="a6458-129">**列表 1-SimpleEditor.aspx**</span><span class="sxs-lookup"><span data-stu-id="a6458-129">**Listing 1 - SimpleEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

<span data-ttu-id="a6458-130">列表 1 中的页面包含的 HTML 编辑器控件，按钮控件和文本控件。</span><span class="sxs-lookup"><span data-stu-id="a6458-130">The page in Listing 1 contains an HTML Editor control, a Button control, and a Literal control.</span></span> <span data-ttu-id="a6458-131">文本控件中单击按钮时，显示的 HTML 编辑器中的内容 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="a6458-131">When you click the button, the contents of the HTML Editor appear in the Literal control (see Figure 4).</span></span>


<span data-ttu-id="a6458-132">[![提交窗体使用 HTML 编辑器](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="a6458-132">[![Submitting a form with an HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)</span></span>

<span data-ttu-id="a6458-133">**图 04**： 提交窗体使用 HTML 编辑器 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="a6458-133">**Figure 04**: Submitting a form with an HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image8.png))</span></span>


<span data-ttu-id="a6458-134">HTML 编辑器 Content 属性用于检索输入到 HTML 编辑器中的 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="a6458-134">The HTML Editor Content property is used to retrieve the HTML content entered into the HTML Editor.</span></span> <span data-ttu-id="a6458-135">请注意，此 HTML 内容可以包含 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="a6458-135">Be aware that this HTML content can contain JavaScript.</span></span> <span data-ttu-id="a6458-136">在下一部分中，我们将讨论如何阻止 JavaScript 注入式攻击。</span><span class="sxs-lookup"><span data-stu-id="a6458-136">In the next section, we discuss how you can prevent JavaScript Injection Attacks.</span></span>

## <a name="customizing-the-html-editor-toolbar"></a><span data-ttu-id="a6458-137">自定义 HTML 编辑器工具栏</span><span class="sxs-lookup"><span data-stu-id="a6458-137">Customizing the HTML Editor Toolbar</span></span>

<span data-ttu-id="a6458-138">你可以自定义完全哪些按钮出现在编辑器中。</span><span class="sxs-lookup"><span data-stu-id="a6458-138">You can customize exactly which buttons appear in the editor.</span></span> <span data-ttu-id="a6458-139">例如，你可能想要删除 HTML 选项卡，以防止用户 HTML 编辑器切换到 HTML 模式。</span><span class="sxs-lookup"><span data-stu-id="a6458-139">For example, you might want to remove the HTML tab to prevent users from switching the HTML Editor into HTML mode.</span></span> <span data-ttu-id="a6458-140">或者，你可能想要删除要阻止用户在论坛中创建过大的文本的字体大小下拉列表 post 消息 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="a6458-140">Or, you might want to remove the font size dropdown list to prevent users from creating overly large text in a forum message post (see Figure 5).</span></span>


<span data-ttu-id="a6458-141">[![自定义的 HTML 编辑器](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="a6458-141">[![A customized HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)</span></span>

<span data-ttu-id="a6458-142">**图 05**： 一个自定义 HTML 编辑器 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="a6458-142">**Figure 05**: A customized HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image10.png))</span></span>


<span data-ttu-id="a6458-143">你通过派生自的基类的编辑器的新的 HTML 编辑器自定义工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="a6458-143">You customize the toolbar buttons by deriving a new HTML Editor from the base Editor class.</span></span> <span data-ttu-id="a6458-144">例如，清单 2 中的自定义编辑器仅包含加粗和倾斜的工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="a6458-144">For example, the custom editor in Listing 2 only contains toolbar buttons for bold and italic.</span></span> <span data-ttu-id="a6458-145">已删除所有其他工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="a6458-145">All other toolbar buttons have been removed.</span></span> <span data-ttu-id="a6458-146">此外，HTML 选项卡已从底部的编辑器中 （但设计和预览选项卡仍有）。</span><span class="sxs-lookup"><span data-stu-id="a6458-146">Furthermore, the HTML tab has been removed from the bottom of the editor (but the Design and Preview tabs are still there).</span></span>

<span data-ttu-id="a6458-147">**Listing 2 - App\_Code\CustomEditor.vb**</span><span class="sxs-lookup"><span data-stu-id="a6458-147">**Listing 2 - App\_Code\CustomEditor.vb**</span></span>

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

<span data-ttu-id="a6458-148">必须向您的应用程序中列出 2 中添加类\_代码文件夹，以便将自动编译的类。</span><span class="sxs-lookup"><span data-stu-id="a6458-148">You must add the class in Listing 2 to your App\_Code folder so that the class will be compiled automatically.</span></span> <span data-ttu-id="a6458-149">如果应用程序\_代码文件夹中你的网站不存在，则可以只需将文件夹添加。</span><span class="sxs-lookup"><span data-stu-id="a6458-149">If the App\_Code folder does not exist in your website then you can simply add the folder.</span></span>

<span data-ttu-id="a6458-150">创建自定义编辑器后，你可以将其添加到 ASP.NET 页相同的方式添加正常 HTML 编辑器中 （请参阅列出 3）。</span><span class="sxs-lookup"><span data-stu-id="a6458-150">After you create a custom editor, you can add it to an ASP.NET page in the same way as you add the normal HTML Editor (see Listing 3).</span></span>

<span data-ttu-id="a6458-151">**列出 3-ShowCustomEditor.aspx**</span><span class="sxs-lookup"><span data-stu-id="a6458-151">**Listing 3 - ShowCustomEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a><span data-ttu-id="a6458-152">避免跨站点脚本 (XSS) 攻击</span><span class="sxs-lookup"><span data-stu-id="a6458-152">Avoiding Cross-Site Scripting (XSS) Attacks</span></span>

<span data-ttu-id="a6458-153">无论何时你接受来自用户的输入，并重新该输入显示在网站上，你可能打开你受到跨站点脚本 (XSS) 攻击的网站。</span><span class="sxs-lookup"><span data-stu-id="a6458-153">Whenever you accept input from a user, and redisplay that input on your website, you potentially open your website to Cross-Site Scripting (XSS) Attacks.</span></span> <span data-ttu-id="a6458-154">从理论上讲，恶意黑客无法提交时将重新显示输入获取执行的 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="a6458-154">In theory, a malicious hacker could submit JavaScript code that gets executed when the input is redisplayed.</span></span> <span data-ttu-id="a6458-155">JavaScript 无法用于窃取用户密码或其他敏感信息。</span><span class="sxs-lookup"><span data-stu-id="a6458-155">The JavaScript could be used to steal user passwords or other sensitive information.</span></span>

<span data-ttu-id="a6458-156">通常情况下，你可以抵消被 HTML 编码显示在 web 页前从用户检索任何输入 XSS 攻击。</span><span class="sxs-lookup"><span data-stu-id="a6458-156">Normally, you can defeat XSS attacks by HTML encoding whatever input you retrieve from a user before displaying it in a web page.</span></span> <span data-ttu-id="a6458-157">但是，HTML 编码输出的 HTML 编辑器中将不仅编码&lt;脚本&gt;标记，它还对所有的 HTML 标记进行编码。</span><span class="sxs-lookup"><span data-stu-id="a6458-157">However, HTML encoding the output of the HTML Editor would not only encode &lt;script&gt; tags, it would also encode all HTML tags.</span></span> <span data-ttu-id="a6458-158">换而言之，你都将丢失的所有格式如字体类型、 字体大小和背景色。</span><span class="sxs-lookup"><span data-stu-id="a6458-158">In other words, you would lose all of the formatting such as the font type, font size, and background color.</span></span>

<span data-ttu-id="a6458-159">如果你正在从你的用户-如密码、 信用卡卡号和社会保障号-收集敏感信息然后应不显示来自用户使用 HTML 编辑器中检索的未编码内容。</span><span class="sxs-lookup"><span data-stu-id="a6458-159">If you are collecting sensitive information from your users -- such as passwords, credit-card numbers, and social security numbers - then you should not display un-encoded content that you retrieve from a user with the HTML Editor.</span></span> <span data-ttu-id="a6458-160">到你的网站由受信任方，应仅在不重新显示 HTML 内容，或提交所使用的 HTML 内容中使用 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="a6458-160">You should use the HTML Editor only in situations in which you are not redisplaying the HTML content, or the HTML content is being submitted to your website by a trusted party.</span></span>

<span data-ttu-id="a6458-161">例如，假设你要创建一个博客的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a6458-161">Imagine, for example, that you are creating a blog application.</span></span> <span data-ttu-id="a6458-162">在此情况下，它有意义时要使用 HTML 编辑器撰写的博客文章。</span><span class="sxs-lookup"><span data-stu-id="a6458-162">In this situation, it makes sense to use the HTML Editor when composing blog posts.</span></span> <span data-ttu-id="a6458-163">是唯一提交博客文章的人，并有可能信任自己无法提交恶意 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="a6458-163">You are the only one who submits a blog post and, presumably, you can trust yourself not to submit malicious JavaScript.</span></span> <span data-ttu-id="a6458-164">但是，它没有意义时要使用 HTML 编辑器允许匿名用户发表评论。</span><span class="sxs-lookup"><span data-stu-id="a6458-164">However, it does not make sense to use the HTML Editor when allowing anonymous users to post comments.</span></span> <span data-ttu-id="a6458-165">你应在用户将提交密码等敏感信息的情况下特别小心。</span><span class="sxs-lookup"><span data-stu-id="a6458-165">You should be especially careful in situations in which users submit sensitive information such as passwords.</span></span> <span data-ttu-id="a6458-166">可能的恶意用户可以将发布包含右 JavaScript 的窃取密码的注释。</span><span class="sxs-lookup"><span data-stu-id="a6458-166">Potentially, a malicious user could post a comment that contains the right JavaScript for stealing a password.</span></span>

## <a name="summary"></a><span data-ttu-id="a6458-167">总结</span><span class="sxs-lookup"><span data-stu-id="a6458-167">Summary</span></span>

<span data-ttu-id="a6458-168">在本教程中，你已提供包括 AJAX 控件工具包中的 HTML 编辑器控件的简要概述。</span><span class="sxs-lookup"><span data-stu-id="a6458-168">In this tutorial, you were provided with a brief overview of the HTML Editor control included in the AJAX Control Toolkit.</span></span> <span data-ttu-id="a6458-169">您学习了如何使用 HTML 编辑器接受来自用户的丰富内容并将其提交到服务器的内容。</span><span class="sxs-lookup"><span data-stu-id="a6458-169">You learned how to use the HTML Editor to accept rich content from a user and submit the content to the server.</span></span> <span data-ttu-id="a6458-170">我们还讨论了如何自定义工具栏按钮显示由 HTML 编辑器中。</span><span class="sxs-lookup"><span data-stu-id="a6458-170">We also discussed how you can customize the toolbar buttons that are displayed by the HTML Editor.</span></span> <span data-ttu-id="a6458-171">最后，您学习了如何避免跨站点脚本攻击时使用 HTML 编辑器接受潜在的恶意输入。</span><span class="sxs-lookup"><span data-stu-id="a6458-171">Finally, you learned how to avoid Cross-Site Scripting Attacks when using the HTML Editor to accept potentially malicious input.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a6458-172">上一篇</span><span class="sxs-lookup"><span data-stu-id="a6458-172">Previous</span></span>](how-do-i-use-the-html-editor-control-cs.md)
