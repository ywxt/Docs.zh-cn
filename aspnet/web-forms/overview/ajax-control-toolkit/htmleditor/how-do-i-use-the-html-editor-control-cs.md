---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: 如何使用 HTML 编辑器控件？ (C#) |Microsoft Docs
author: microsoft
description: HTMLEditor 是 ASP.NET AJAX 控件，您可以轻松地创建和编辑通过按钮在工具栏中的 HTML 内容。
ms.author: aspnetcontent
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 775cb113ea11e582806b0bd9397778cff6761940
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809402"
---
<a name="how-do-i-use-the-html-editor-control-c"></a><span data-ttu-id="e6e3e-104">如何使用 HTML 编辑器控件？</span><span class="sxs-lookup"><span data-stu-id="e6e3e-104">How do I use the HTML Editor Control?</span></span> <span data-ttu-id="e6e3e-105">(C#)</span><span class="sxs-lookup"><span data-stu-id="e6e3e-105">(C#)</span></span>
====================
<span data-ttu-id="e6e3e-106">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e6e3e-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e6e3e-107">HTMLEditor 是 ASP.NET AJAX 控件，您可以轻松地创建和编辑通过按钮在工具栏中的 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-107">HTMLEditor is an ASP.NET AJAX Control that allows you to easily create and edit HTML content via buttons in a toolbar.</span></span>


<span data-ttu-id="e6e3e-108">本教程的目的是为你提供了 AJAX 控件工具包中包含的 HTML 编辑器控件的概述。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-108">The goal of this tutorial is to provide you with an overview of the HTML Editor control included with the AJAX Control Toolkit.</span></span> <span data-ttu-id="e6e3e-109">HTML 编辑器包含可用于更改字体大小、 选择一种字体、 更改背景色、 修改的前景色，选项添加链接，添加图像，更改文本对齐方式，并执行剪切、 复制和粘贴 （见图 1） 的操作。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-109">The HTML Editor includes options for changing font size, selecting a font, changing background color, modifying the foreground color, adding links, adding images, changing text alignment, and performing cut, copy, and paste operations (see Figure 1).</span></span>


<span data-ttu-id="e6e3e-110">[![HTML 编辑器](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e6e3e-110">[![The HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="e6e3e-111">**图 01**： 使用 HTML 编辑器 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="e6e3e-111">**Figure 01**: The HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image2.png))</span></span>


<span data-ttu-id="e6e3e-112">HTML 编辑器，您可以输入使用设计模式下的内容，也可以直接输入 HTML。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-112">The HTML editor enables you to enter content using a design mode or you can enter HTML directly.</span></span> <span data-ttu-id="e6e3e-113">你还提供用于预览 HTML 内容的选项 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-113">You also are provided with the option to preview your HTML content (see Figure 2).</span></span>


<span data-ttu-id="e6e3e-114">[![设计、 HTML 和预览按钮](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e6e3e-114">[![Design, HTML, and Preview buttons](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span></span>

<span data-ttu-id="e6e3e-115">**图 02**： 设计、 HTML 和预览按钮 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="e6e3e-115">**Figure 02**: Design, HTML, and Preview buttons([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image4.png))</span></span>


<span data-ttu-id="e6e3e-116">在本教程中，您将学习如何显示 HTML 编辑器、 如何自定义工具栏按钮显示在 HTML 编辑器中，以及如何避免跨站点脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-116">In this tutorial, you learn how to display the HTML Editor, how to customize the toolbar buttons that appear in the HTML Editor, and how to avoid Cross-Site Scripting Attacks.</span></span>

## <a name="displaying-the-html-editor"></a><span data-ttu-id="e6e3e-117">显示 HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="e6e3e-117">Displaying the HTML Editor</span></span>

<span data-ttu-id="e6e3e-118">在 ASP.NET 页面中使用 HTML 编辑器之前，必须首先将 ScriptManager 控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-118">Before you can use the HTML Editor in an ASP.NET page, you must first add a ScriptManager control to the page.</span></span> <span data-ttu-id="e6e3e-119">ScriptManager 控件位于 Visual Studio/Visual Web Developer 速成版工具箱中的 AJAX 扩展选项卡下。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-119">The ScriptManager control is located beneath the AJAX Extensions tab in the Visual Studio/Visual Web Developer Express toolbox.</span></span>

<span data-ttu-id="e6e3e-120">应将 ScriptManager 控件放在之前的页的页上的任何其他控件的顶部。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-120">You should place the ScriptManager control at the top of the page before any other controls on the page.</span></span> <span data-ttu-id="e6e3e-121">例如，您可以将其放立即打开服务器端下面&lt;窗体&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-121">For example, you can place it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="e6e3e-122">HTML 编辑器控件位于与其他 AJAX 控件工具包控件工具箱中。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-122">The HTML Editor control is located in the toolbox with the rest of the AJAX Control Toolkit controls.</span></span> <span data-ttu-id="e6e3e-123">它名为编辑器控件 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-123">It is named the Editor control (see Figure 3).</span></span>


<span data-ttu-id="e6e3e-124">[![HTML 编辑器控件](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="e6e3e-124">[![The HTML Editor control](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span></span>

<span data-ttu-id="e6e3e-125">**图 03**： 使用 HTML 编辑器控件 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="e6e3e-125">**Figure 03**: The HTML Editor control([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image6.png))</span></span>


<span data-ttu-id="e6e3e-126">HTML 编辑器将拖到页后，你可以在属性表中设置其属性。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-126">After you drag the HTML Editor onto a page, you can set its properties in the property sheet.</span></span> <span data-ttu-id="e6e3e-127">例如，你通常想要设置宽度和高度属性。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-127">For example, you normally want to set the Width and Height properties.</span></span> <span data-ttu-id="e6e3e-128">代码清单 1 包含一个包含 HTML 编辑器的 ASP.NET 页面的源。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-128">Listing 1 contains the source for an ASP.NET page that contains an HTML editor.</span></span>

<span data-ttu-id="e6e3e-129">**代码清单 1-SimpleEditor.aspx**</span><span class="sxs-lookup"><span data-stu-id="e6e3e-129">**Listing 1 - SimpleEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

<span data-ttu-id="e6e3e-130">在列表 1 中的页包含的 HTML 编辑器控件、 一个按钮控件和文字控件。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-130">The page in Listing 1 contains an HTML Editor control, a Button control, and a Literal control.</span></span> <span data-ttu-id="e6e3e-131">当单击按钮时，内容的 HTML 编辑器中显示文本控件中 （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-131">When you click the button, the contents of the HTML Editor appear in the Literal control (see Figure 4).</span></span>


<span data-ttu-id="e6e3e-132">[![提交窗体使用 HTML 编辑器](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="e6e3e-132">[![Submitting a form with an HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span></span>

<span data-ttu-id="e6e3e-133">**图 04**： 提交窗体使用 HTML 编辑器 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="e6e3e-133">**Figure 04**: Submitting a form with an HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image8.png))</span></span>


<span data-ttu-id="e6e3e-134">HTML 编辑器内容属性用于检索输入到 HTML 编辑器中的 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-134">The HTML Editor Content property is used to retrieve the HTML content entered into the HTML Editor.</span></span> <span data-ttu-id="e6e3e-135">请注意，此 HTML 内容可以包含 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-135">Be aware that this HTML content can contain JavaScript.</span></span> <span data-ttu-id="e6e3e-136">在下一部分中，我们讨论了如何阻止 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-136">In the next section, we discuss how you can prevent JavaScript Injection Attacks.</span></span>

## <a name="customizing-the-html-editor-toolbar"></a><span data-ttu-id="e6e3e-137">自定义 HTML 编辑器工具栏</span><span class="sxs-lookup"><span data-stu-id="e6e3e-137">Customizing the HTML Editor Toolbar</span></span>

<span data-ttu-id="e6e3e-138">你可以自定义完全的按钮出现在编辑器中。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-138">You can customize exactly which buttons appear in the editor.</span></span> <span data-ttu-id="e6e3e-139">例如，可能想要删除 HTML 选项卡以防止用户在 HTML 编辑器切换到 HTML 模式。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-139">For example, you might want to remove the HTML tab to prevent users from switching the HTML Editor into HTML mode.</span></span> <span data-ttu-id="e6e3e-140">或者，可能想要删除字体大小下拉列表，以防止用户在论坛中创建过大文本 post 消息 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-140">Or, you might want to remove the font size dropdown list to prevent users from creating overly large text in a forum message post (see Figure 5).</span></span>


<span data-ttu-id="e6e3e-141">[![自定义 HTML 编辑器](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="e6e3e-141">[![A customized HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span></span>

<span data-ttu-id="e6e3e-142">**图 05**： 一个自定义 HTML 编辑器 ([单击以查看实际尺寸的图像](how-do-i-use-the-html-editor-control-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="e6e3e-142">**Figure 05**: A customized HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image10.png))</span></span>


<span data-ttu-id="e6e3e-143">您通过从编辑器的基类中派生新的 HTML 编辑器自定义工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-143">You customize the toolbar buttons by deriving a new HTML Editor from the base Editor class.</span></span> <span data-ttu-id="e6e3e-144">例如，代码清单 2 中的自定义编辑器仅包含粗体和斜体的工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-144">For example, the custom editor in Listing 2 only contains toolbar buttons for bold and italic.</span></span> <span data-ttu-id="e6e3e-145">已删除所有其他工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-145">All other toolbar buttons have been removed.</span></span> <span data-ttu-id="e6e3e-146">此外，HTML 选项卡已删除从编辑器的底部 （但在设计和预览选项卡仍有）。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-146">Furthermore, the HTML tab has been removed from the bottom of the editor (but the Design and Preview tabs are still there).</span></span>

<span data-ttu-id="e6e3e-147">**代码清单 2-应用\_Code\CustomEditor.cs**</span><span class="sxs-lookup"><span data-stu-id="e6e3e-147">**Listing 2 - App\_Code\CustomEditor.cs**</span></span>

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

<span data-ttu-id="e6e3e-148">必须向应用程序清单 2 中添加类\_代码文件夹，以便将自动编译的类。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-148">You must add the class in Listing 2 to your App\_Code folder so that the class will be compiled automatically.</span></span> <span data-ttu-id="e6e3e-149">如果应用\_代码文件夹中你的网站不存在，则可以只需将文件夹添加。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-149">If the App\_Code folder does not exist in your website then you can simply add the folder.</span></span>

<span data-ttu-id="e6e3e-150">创建自定义编辑器后，您可以将其添加到 ASP.NET 页面中的相同方式添加普通 HTML 编辑器 （请参阅代码清单 3）。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-150">After you create a custom editor, you can add it to an ASP.NET page in the same way as you add the normal HTML Editor (see Listing 3).</span></span>

<span data-ttu-id="e6e3e-151">**代码清单 3-ShowCustomEditor.aspx**</span><span class="sxs-lookup"><span data-stu-id="e6e3e-151">**Listing 3 - ShowCustomEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a><span data-ttu-id="e6e3e-152">避免跨站点脚本 (XSS) 攻击</span><span class="sxs-lookup"><span data-stu-id="e6e3e-152">Avoiding Cross-Site Scripting (XSS) Attacks</span></span>

<span data-ttu-id="e6e3e-153">只要您接受来自用户的输入，并且重新该输入显示在网站上，你可能会打开你受到跨站点脚本 (XSS) 攻击的网站。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-153">Whenever you accept input from a user, and redisplay that input on your website, you potentially open your website to Cross-Site Scripting (XSS) Attacks.</span></span> <span data-ttu-id="e6e3e-154">从理论上讲，恶意黑客无法提交输入重新显示时执行的 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-154">In theory, a malicious hacker could submit JavaScript code that gets executed when the input is redisplayed.</span></span> <span data-ttu-id="e6e3e-155">无法使用 JavaScript 来窃取用户密码或其他敏感信息。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-155">The JavaScript could be used to steal user passwords or other sensitive information.</span></span>

<span data-ttu-id="e6e3e-156">通常情况下，可以抵御 XSS 攻击的 HTML 编码在网页中显示之前从用户检索任何输入。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-156">Normally, you can defeat XSS attacks by HTML encoding whatever input you retrieve from a user before displaying it in a web page.</span></span> <span data-ttu-id="e6e3e-157">但是，HTML 编码的 HTML 编辑器中的输出将只对进行编码&lt;脚本&gt;标记，它还对所有 HTML 标记进行都编码。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-157">However, HTML encoding the output of the HTML Editor would not only encode &lt;script&gt; tags, it would also encode all HTML tags.</span></span> <span data-ttu-id="e6e3e-158">换而言之，就会丢失的所有格式如字体、 字体大小和背景色。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-158">In other words, you would lose all of the formatting such as the font type, font size, and background color.</span></span>

<span data-ttu-id="e6e3e-159">如果您收集的敏感信息来自您的用户-例如密码、 信用卡卡号和社会安全号码-然后应不显示未编码使用 HTML 编辑器中的用户从检索的内容。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-159">If you are collecting sensitive information from your users -- such as passwords, credit-card numbers, and social security numbers - then you should not display un-encoded content that you retrieve from a user with the HTML Editor.</span></span> <span data-ttu-id="e6e3e-160">到你的网站由受信任方，应仅在某些情况下在其中不会重新显示的 HTML 内容，或正在提交的 HTML 内容中使用 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-160">You should use the HTML Editor only in situations in which you are not redisplaying the HTML content, or the HTML content is being submitted to your website by a trusted party.</span></span>

<span data-ttu-id="e6e3e-161">例如，假设您要创建的博客应用程序。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-161">Imagine, for example, that you are creating a blog application.</span></span> <span data-ttu-id="e6e3e-162">在此情况下，最好使用 HTML 编辑器，在撰写博客文章时。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-162">In this situation, it makes sense to use the HTML Editor when composing blog posts.</span></span> <span data-ttu-id="e6e3e-163">是唯一将提交一篇博客文章的人，并且有可能可以信任自己无法提交恶意 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-163">You are the only one who submits a blog post and, presumably, you can trust yourself not to submit malicious JavaScript.</span></span> <span data-ttu-id="e6e3e-164">但是，它不难理解时要使用 HTML 编辑器允许匿名用户发表评论。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-164">However, it does not make sense to use the HTML Editor when allowing anonymous users to post comments.</span></span> <span data-ttu-id="e6e3e-165">您应在用户将提交敏感信息，如密码的情况下特别小心。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-165">You should be especially careful in situations in which users submit sensitive information such as passwords.</span></span> <span data-ttu-id="e6e3e-166">可能的恶意用户可以将发布包含适用于窃取密码右侧的 JavaScript 的注释。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-166">Potentially, a malicious user could post a comment that contains the right JavaScript for stealing a password.</span></span>

## <a name="summary"></a><span data-ttu-id="e6e3e-167">总结</span><span class="sxs-lookup"><span data-stu-id="e6e3e-167">Summary</span></span>

<span data-ttu-id="e6e3e-168">在本教程中，你已提供了 AJAX 控件工具包中包含的 HTML 编辑器控件的简要概述。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-168">In this tutorial, you were provided with a brief overview of the HTML Editor control included in the AJAX Control Toolkit.</span></span> <span data-ttu-id="e6e3e-169">您学习了如何使用 HTML 编辑器以接受来自用户的丰富内容并提交到服务器的内容。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-169">You learned how to use the HTML Editor to accept rich content from a user and submit the content to the server.</span></span> <span data-ttu-id="e6e3e-170">我们还讨论了如何自定义工具栏按钮显示的 HTML 编辑器中。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-170">We also discussed how you can customize the toolbar buttons that are displayed by the HTML Editor.</span></span> <span data-ttu-id="e6e3e-171">最后，您学习了如何使用 HTML 编辑器接受潜在的恶意输入时，避免出现跨站点脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="e6e3e-171">Finally, you learned how to avoid Cross-Site Scripting Attacks when using the HTML Editor to accept potentially malicious input.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e6e3e-172">下一篇</span><span class="sxs-lookup"><span data-stu-id="e6e3e-172">Next</span></span>](how-do-i-use-the-html-editor-control-vb.md)
