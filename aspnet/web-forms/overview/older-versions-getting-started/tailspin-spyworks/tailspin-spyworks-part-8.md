---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 第 8 部分： 最终页、 异常处理和结论 |Microsoft 文档
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 8 部分将添加一个联系人页面，页面上和异常有关...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: f82294aab0616012393cf3e10f932f6d1ad0cdb6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30886266"
---
<a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="c9b8c-104">第 8 部分： 最终页、 异常处理和结论</span><span class="sxs-lookup"><span data-stu-id="c9b8c-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>
====================
<span data-ttu-id="c9b8c-105">通过[Joe stagner 将](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="c9b8c-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="c9b8c-106">Tailspin Spyworks 演示创建在.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="c9b8c-107">它演示如何使用 ASP.NET 4 中出色的新功能构建在线商店，包括购物、 结帐和管理关闭。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="c9b8c-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="c9b8c-109">第 8 部分添加联系人页，有关页上和异常处理。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="c9b8c-110">这是序列结束。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-110">This is the conclusion of the series.</span></span>


## <a id="_Toc260221680"></a>  <span data-ttu-id="c9b8c-111">联系人页 （从 ASP.NET 发送电子邮件）</span><span class="sxs-lookup"><span data-stu-id="c9b8c-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="c9b8c-112">创建一个名为 ContactUs.aspx 的新页</span><span class="sxs-lookup"><span data-stu-id="c9b8c-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="c9b8c-113">使用设计器，创建以下形式采用特殊的注释，以包括 ToolkitScriptManager 和从 AjaxdControlToolkit 编辑器控件。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxdControlToolkit.</span></span> <span data-ttu-id="c9b8c-114">.</span><span class="sxs-lookup"><span data-stu-id="c9b8c-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="c9b8c-115">双击"提交"按钮以在代码隐藏文件中生成一个 click 事件处理程序和实现方法以作为电子邮件发送的联系信息。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="c9b8c-116">此代码要求你的 web.config 文件包含指定要用于发送邮件的 SMTP 服务器的配置节中的条目。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>  <span data-ttu-id="c9b8c-117">有关页面</span><span class="sxs-lookup"><span data-stu-id="c9b8c-117">About Page</span></span>

<span data-ttu-id="c9b8c-118">创建一个名为 AboutUs.aspx 页并添加任何您喜欢的内容。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a>  <span data-ttu-id="c9b8c-119">全局异常处理程序</span><span class="sxs-lookup"><span data-stu-id="c9b8c-119">Global Exception Handler</span></span>

<span data-ttu-id="c9b8c-120">最后，在整个应用程序中，我们具有引发异常并且没有出现未预见的情况下，冷还在我们的 web 应用程序中的原因的未经处理的异常。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="c9b8c-121">我们永远不希望显示给网站访问者未经处理的异常。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="c9b8c-122">除了正在可怕的用户体验未经处理的异常也可以是安全问题。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="c9b8c-123">若要解决此问题，我们将实现全局异常处理程序。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="c9b8c-124">若要执行此操作，打开 Global.asax 文件，并请注意以下预生成的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="c9b8c-125">添加代码以实现应用程序\_，如下所示的错误处理程序。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="c9b8c-126">然后添加一个名为到解决方案的 Error.aspx 页，并添加此标记代码段。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="c9b8c-127">现在，在页\_从请求对象加载事件处理程序提取错误消息。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>  <span data-ttu-id="c9b8c-128">结论</span><span class="sxs-lookup"><span data-stu-id="c9b8c-128">Conclusion</span></span>

<span data-ttu-id="c9b8c-129">我们已了解，ASP.NET WebForms 便于对来创建复杂的网站和数据库访问，成员身份，AJAX 等。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="c9b8c-130">非常快速。</span><span class="sxs-lookup"><span data-stu-id="c9b8c-130">pretty quickly.</span></span>

<span data-ttu-id="c9b8c-131">希望本教程已授予所需若要开始构建应用程序的你自己 ASP.NET WebForms 工具 ！</span><span class="sxs-lookup"><span data-stu-id="c9b8c-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c9b8c-132">上一篇</span><span class="sxs-lookup"><span data-stu-id="c9b8c-132">Previous</span></span>](tailspin-spyworks-part-7.md)
