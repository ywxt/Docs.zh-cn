---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 第 8 部分： 最终页面、 异常处理和结论 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 8 部分添加一个联系人页，有关页和异常...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f1d855e157f6a58995d301a793e660925767fb4
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37380248"
---
<a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="5ddf9-104">第 8 部分： 最终页面、 异常处理和结论</span><span class="sxs-lookup"><span data-stu-id="5ddf9-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>
====================
<span data-ttu-id="5ddf9-105">通过[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="5ddf9-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="5ddf9-106">Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="5ddf9-107">它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="5ddf9-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="5ddf9-109">第 8 部分将添加联系人的页上，有关页和异常处理。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="5ddf9-110">这是系列教程的结论。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-110">This is the conclusion of the series.</span></span>


## <a id="_Toc260221680"></a>  <span data-ttu-id="5ddf9-111">请联系页 （从 ASP.NET 发送电子邮件）</span><span class="sxs-lookup"><span data-stu-id="5ddf9-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="5ddf9-112">创建一个名为 ContactUs.aspx 的新页</span><span class="sxs-lookup"><span data-stu-id="5ddf9-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="5ddf9-113">使用设计器，创建以下形式采用特殊的注释，以包括 ToolkitScriptManager 和从 AjaxdControlToolkit 编辑器控件。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxdControlToolkit.</span></span> <span data-ttu-id="5ddf9-114">.</span><span class="sxs-lookup"><span data-stu-id="5ddf9-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="5ddf9-115">双击"提交"按钮以在代码隐藏文件中生成一个 click 事件处理程序并实现为一封电子邮件发送的联系信息的方法。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="5ddf9-116">此代码需要在 web.config 文件包含指定要用于发送邮件的 SMTP 服务器的配置节中的条目。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>  <span data-ttu-id="5ddf9-117">有关页</span><span class="sxs-lookup"><span data-stu-id="5ddf9-117">About Page</span></span>

<span data-ttu-id="5ddf9-118">创建一个名为 AboutUs.aspx 页并添加您喜欢的任何内容。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a>  <span data-ttu-id="5ddf9-119">全局异常处理程序</span><span class="sxs-lookup"><span data-stu-id="5ddf9-119">Global Exception Handler</span></span>

<span data-ttu-id="5ddf9-120">最后，整个应用程序中，我们已引发异常并且未预见情况下，冷还可在 web 应用程序中导致未经处理的异常。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="5ddf9-121">我们永远不会想要显示给网站访问者未经处理的异常。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="5ddf9-122">除了可怕的用户体验未经处理的异常也可以是安全问题。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="5ddf9-123">若要解决此问题，我们将实现全局异常处理程序。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="5ddf9-124">若要执行此操作，打开 Global.asax 文件，并请注意以下预生成的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="5ddf9-125">添加代码以实现应用程序\_，如下所示的错误处理程序。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="5ddf9-126">然后添加一个名为到解决方案的 Error.aspx 页并添加此标记片段。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="5ddf9-127">现在，在页面\_从请求对象中加载事件处理程序提取的错误消息。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>  <span data-ttu-id="5ddf9-128">结论</span><span class="sxs-lookup"><span data-stu-id="5ddf9-128">Conclusion</span></span>

<span data-ttu-id="5ddf9-129">我们所见，ASP.NET WebForms 可以轻松创建复杂的网站具有数据库访问，成员身份，AJAX，等等。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="5ddf9-130">很快就会变。</span><span class="sxs-lookup"><span data-stu-id="5ddf9-130">pretty quickly.</span></span>

<span data-ttu-id="5ddf9-131">希望本教程提供若要开始构建你自己的 ASP.NET WebForms 应用程序所需的工具 ！</span><span class="sxs-lookup"><span data-stu-id="5ddf9-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5ddf9-132">上一篇</span><span class="sxs-lookup"><span data-stu-id="5ddf9-132">Previous</span></span>](tailspin-spyworks-part-7.md)
