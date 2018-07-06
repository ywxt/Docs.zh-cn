---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
title: 迭代 7 – 添加 Ajax 功能 (VB) |Microsoft Docs
author: microsoft
description: 在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: f640e063-150e-453d-8cfc-7e54a6ce0f1e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
msc.type: authoredcontent
ms.openlocfilehash: f5ea425c69dec803bfbdcb9f319a1d24e816bcf7
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37840127"
---
<a name="iteration-7--add-ajax-functionality-vb"></a>迭代 7 – 添加 Ajax 功能 (VB)
====================
by [Microsoft](https://github.com/microsoft)

[下载代码](iteration-7-add-ajax-functionality-vb/_static/contactmanager_7_vb1.zip)

> 在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建联系人管理 ASP.NET MVC 应用程序 (VB)
  

在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。 联系人管理器应用程序，可存储联系人信息的名称，电话号码和电子邮件地址的人的列表。

我们通过多个迭代中生成应用程序。 每次迭代时，我们逐渐提高应用程序。 此多个迭代方法的目标是帮助你了解每个更改的原因。

- 迭代 1-创建应用程序。 在第一次迭代中，我们创建联系人管理器中的最简单方法可能。 我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。

- 迭代 2 – 使应用程序看上去更美观。 在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。

- 迭代 3-添加窗体验证。 在第三个迭代中，我们将添加基本窗体验证。 我们阻止用户提交窗体而无法完成所需的窗体字段。 我们还验证电子邮件地址和电话号码。

- 迭代 4-使应用程序松散耦合。 在此第三个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。 例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。

- 迭代 5 — 创建单元测试。 在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。 我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。

- 迭代 6-使用测试驱动的开发。 在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。 在此迭代中，我们将添加联系人组。

- 迭代 7-添加 Ajax 功能。 在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。

## <a name="this-iteration"></a>此迭代

在此迭代的联系人管理器应用程序中，我们将重构应用程序以充分利用 Ajax。 通过利用 Ajax，我们使我们的应用程序响应速度更快。 我们可以避免当我们需要更新某些区域在页面中的呈现整个页面。

我们将重构索引视图，以便我们不需要重新显示整个页面，只要有人选择新联系人组。 相反，当某人单击联系人组时，我们将只需更新的联系人列表并保留单独的页的其余部分。

我们还将更改我们删除链接的工作原理的方式。 而不是显示一个单独的确认页面，我们将显示一个 JavaScript 确认对话框。 如果您确认要删除联系人，则对要从数据库中删除联系人记录的服务器执行 HTTP DELETE 操作。

此外，我们将利用 jQuery 将动画效果添加到我们的索引视图。 正在从服务器提取新的联系人列表时，我们将显示动画。

最后，我们将利用 ASP.NET AJAX framework 支持管理浏览器历史记录。 每当我们执行的 Ajax 调用以更新联系人列表，我们将创建历史时间点。 这样一来，在浏览器向后和向前按钮将起作用。

## <a name="why-use-ajax"></a>为何使用 Ajax？

使用 Ajax 具有诸多优点。 首先，将 Ajax 功能添加到应用程序导致更好的用户体验。 在普通的 web 应用程序中，整个页面必须为回发到服务器每个用户执行的操作的时间。 每当执行的操作，浏览器锁和用户必须等待，直到提取并重新显示整个页面。

这将是在桌面应用程序的情况下不能接受体验。 但是，一直以来，我们一直与在 web 应用程序的情况下此不良用户体验因为我们不知道我们能做任何越好。 我们认为它是 web 应用程序的限制时，实际上，它只是我们想象力的限制。

在 Ajax 应用程序，您不需要停止只是为了将更新页面，使用户体验。 相反，您可以在后台更新页面执行的异步请求。 您不 t 强制用户等待获取更新的页的一部分时。

通过利用 Ajax，您还可以提高应用程序的性能。 请考虑联系人管理器应用程序的工作原理现在不具有 Ajax 功能。 当您单击联系人组时，则必须重新显示整个索引视图。 必须从数据库服务器检索的联系人列表和联系人组的列表。 所有这些数据必须是通过线缆从 web 服务器传递到 web 浏览器。

我们将 Ajax 功能添加到我们的应用程序后，但是，我们可以避免在用户单击联系人组时重新显示整个页面。 我们不再需要获取数据库中联系人的组。 我们也不需要通过网络推送整个索引视图。 通过利用 Ajax，我们减少我们的数据库服务器必须执行的工作量和我们减少所需的应用程序的网络流量的量。

## <a name="don-t-be-afraid-of-ajax"></a>不要将担心的 Ajax

一些开发人员避免使用 Ajax，因为他们担心低级浏览器。 他们想要确保其 web 应用程序不支持 JavaScript 的浏览器进行访问时仍将起作用。 由于 Ajax 依赖于 JavaScript，一些开发人员避免使用 Ajax。

但是，如果你非常小心有关如何实现 Ajax，则可生成适用于上级和下层浏览器应用程序。 我们的联系人管理器应用程序将使用支持 JavaScript 的浏览器和浏览器不这样做。

如果联系人管理器应用程序使用支持 JavaScript 的浏览器，然后将具有更好的用户体验。 例如，当您单击联系人组时，将更新仅显示联系人的页面的区域。

另一方面，如果您使用的浏览器不支持 JavaScript （或已禁用 JavaScript） 的联系人管理器应用程序，然后将具有略有不太理想的用户体验。 例如，当单击联系人组时，整个索引视图必须为回发到浏览器以显示匹配的联系人列表。

## <a name="adding-the-required-javascript-files"></a>添加所需的 JavaScript 文件

我们将需要使用三个 JavaScript 文件将 Ajax 功能添加到我们的应用程序。 所有这三个这些文件包含在新的 ASP.NET MVC 应用程序的 Scripts 文件夹中。

如果你打算在应用程序中的多个页中使用 Ajax 然后最好在应用程序的视图主页面中包含所需的 JavaScript 文件。 这样一来，JavaScript 文件将在所有应用程序中的页面中自动都包含。

添加以下 JavaScript 包括内部&lt;head&gt;视图母版页的标记：

[!code-html[Main](iteration-7-add-ajax-functionality-vb/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>重构要使用 Ajax 的索引视图

让我们来首先修改索引视图，以便显示联系人的视图的区域，仅单击联系人组更新。 图 1 中的红色框包含我们想要更新的区域。


[![更新仅联系人](iteration-7-add-ajax-functionality-vb/_static/image1.jpg)](iteration-7-add-ajax-functionality-vb/_static/image1.png)

**图 01**： 更新仅联系人 ([单击以查看实际尺寸的图像](iteration-7-add-ajax-functionality-vb/_static/image2.png))


第一步是视图的将我们想要以异步方式更新到单独的部分 （视图用户控件） 的一部分。 显示的联系人的索引视图的一部分已被移动到在列表 1 中部分。

**代码清单 1-Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample2.aspx)]

请注意，在列表 1 中部分包含与索引视图不同的模型。 *Inherits*属性中&lt;%@ 页 %&gt;指令指定分部继承 ViewUserControl&lt;组&gt;类。

列表 2 中包含更新的索引视图。

**代码清单 2-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample3.aspx)]

有两件事，您会注意到有关清单 2 中更新的视图。 首先，注意到的所有内容移到分部替换 Html.RenderPartial() 调用。 Html.RenderPartial() 方法称为索引视图首次请求以便显示联系人的初始设置时。

其次，请注意，用于显示联系人组 Html.ActionLink() 已替换为 Ajax.ActionLink()。 使用以下参数调用 Ajax.ActionLink():

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample4.aspx)]

第一个参数表示要显示的链接的文本、 第二个参数表示路由值和第三个参数表示的 Ajax 选项。 在这种情况下，我们使用 UpdateTargetId Ajax 选项指向 HTML &lt;div&gt;我们想要在 Ajax 请求完成后更新的标记。 我们想要更新&lt;div&gt;新联系人列表的标记。

请联系控制器的更新的 index （） 方法包含在清单 3。

**代码清单 3-Controllers\ContactController.vb （Index 方法）**

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample5.vb)]

更新后的 index （） 操作有条件地返回两个条件之一。 如果由 Ajax 请求调用 index （） 操作控制器返回部分。 否则，index （） 操作返回整个视图。

请注意，index （） 操作不需要返回尽可能多的数据时调用的 Ajax 请求。 在正常的请求的上下文中，索引操作返回的所有联系人组和所选联系人组的列表。 在 Ajax 请求的上下文，index （） 操作返回只为所选的组。 Ajax 意味着数据库服务器上的工作较少。

我们已修改的索引视图在上级和下层浏览器的情况下适用。 如果单击联系人组，并在浏览器支持 JavaScript，然后更新只有包含的联系人列表的视图的区域。 如果，但是，你的浏览器不支持 JavaScript，然后更新整个视图。


我们已更新的索引视图都有一个问题。 当单击联系人组时，不突出显示所选的组。 由于在 Ajax 请求期间更新的区域之外显示的组的列表，不会不获取突出显示正确的组。 我们将在下一节中修复此问题。


## <a name="adding-jquery-animation-effects"></a>添加 jQuery 动画效果

通常情况下，当单击网页中的链接时，可以使用浏览器进度栏来检测在浏览器主动提取更新的内容。 在执行时 Ajax 请求，另一方面，浏览器进度栏不显示任何进度。 这可以让用户紧张。 如何知道是否已冻结在浏览器？

有几种方法，您可以指示用户正在执行的 Ajax 请求时执行工作。 一种方法是显示一个简单的动画。 例如，您可以淡出区域时 Ajax 请求开始，并在请求完成时淡入的区域中。

我们将使用 jQuery 库包含在 Microsoft ASP.NET MVC 框架，若要创建的动画效果。 列表 4 中包含更新的索引视图。

**列表 4-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample6.aspx)]

请注意，更新的索引视图包含三个新的 JavaScript 函数。 前两个函数使用 jQuery 淡出和淡入的联系人列表中，单击新联系人组时。 第三个函数中出现错误 （例如，网络超时） 显示一条错误消息时 Ajax 请求结果。

第一个函数还负责的突出显示所选的组。 一个类 = 所选的属性添加到单击的元素的父元素 （LI 元素）。 同样，jQuery 使得可以轻松选择正确的元素和添加的 CSS 类。

这些脚本已绑定到 Ajax.ActionLink() AjaxOptions 参数的帮助的组链接。 更新的 Ajax.ActionLink() 方法调用如下所示：

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>添加浏览器历史记录支持

通常情况下，单击更新页的链接，将更新你的浏览器历史记录。 这样一来，可以单击浏览器后退按钮在时间中返回移动到页面的以前的状态。 例如，如果您单击的好友联系人组，然后单击业务联系人组，可以单击浏览器后退按钮时要导航到页面的状态的好友联系人组选择。

遗憾的是，执行 Ajax 请求不会更新浏览器历史记录自动。 如果单击联系人组，并使用 Ajax 请求检索匹配的联系人的列表，则不会更新浏览器历史记录。 浏览器的后退按钮不能用于向后定位到联系人组选择新联系人组后。

如果你希望用户能够使用浏览器返回按钮执行 Ajax 请求后，然后需要执行更多工作。 您需要充分利用在 ASP.NET AJAX Framework 中构建的浏览器历史记录管理功能。

ASP.NET AJAX 浏览器历史记录，您需要做三件事：

1. 通过浏览器历史记录 enableBrowserHistory 属性设置为 true。
2. 通过调用 addHistoryPoint() 方法的视图状态更改时，将保存历史时间点。
3. 引发导航事件时，重新构造的视图状态。

列表 5 中包含更新的索引视图。

**列表 5-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample8.aspx)]

列表 5 中 pageInit() 函数中启用了浏览器历史记录。 PageInit() 函数还用于设置导航事件的事件处理程序。 浏览器前进或后退按钮会导致的页后，可以更改状态时，将引发导航事件。

单击联系人组时，被调用 beginContactList() 方法。 此方法通过调用 addHistoryPoint() 方法来创建新的历史时间点。 单击联系人组的 id 添加到历史记录。

从联系人组链接的 expando 属性中检索组 id。 使用以下调用 Ajax.ActionLink() 呈现链接。

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample9.aspx)]

最后一个参数传递给 Ajax.ActionLink() 将添加一个名为 groupid （小写的 XHTML 兼容性） 链接到的 expando 属性。

当用户遇到回浏览器或前进按钮时，引发导航事件，并调用 navigate() 方法。 此方法会更新以匹配到浏览器历史记录点传递给 navigate 方法相对应的页的状态在页中显示的联系人。

## <a name="performing-ajax-deletes"></a>执行 Ajax 删除

目前，若要删除联系人，您需要单击删除链接上，然后单击删除确认页中显示删除按钮 （请参见图 2）。 这看起来好像很多的页请求来执行简单删除的数据库记录。


[![删除确认页](iteration-7-add-ajax-functionality-vb/_static/image2.jpg)](iteration-7-add-ajax-functionality-vb/_static/image3.png)

**图 02**: 删除确认页 ([单击以查看实际尺寸的图像](iteration-7-add-ajax-functionality-vb/_static/image4.png))


很容易就跳过删除确认页面并直接从索引视图中删除联系人。 由于采用这种方法打开到安全漏洞的应用程序，应避免心。 一般情况下，don t 想要调用的 web 应用程序状态修改操作时执行的 HTTP GET 操作。 在执行 delete 时，你想要执行 HTTP POST，或者更确切地说，HTTP DELETE 操作。

删除链接包含在部分联系人列表。 列表 6 中包含的部分 ContactList 更新的版本。

**代码清单 6-Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample10.aspx)]

删除链接呈现并对 Ajax.ImageActionLink() 方法的以下调用：

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample11.aspx)]

> [!NOTE] 
> 
> Ajax.ImageActionLink() 不是 ASP.NET MVC 框架的标准组成部分。 Ajax.ImageActionLink() 是 Contact Manager 项目中包含自定义帮助器方法。


AjaxOptions 参数具有两个属性。 首先，确认属性用于显示一个弹出窗口 JavaScript 确认对话框。 其次，HttpMethod 属性用于执行 HTTP DELETE 操作。

列表 7 包含已添加到联系人控制器的新 AjaxDelete() 操作。

**列表 7-Controllers\ContactController.vb (AjaxDelete)**   

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample12.vb)]

AjaxDelete() 操作是使用 AcceptVerbs 属性进行修饰。 此属性会阻止调用除了任何 HTTP 操作而不是 HTTP DELETE 操作的操作。 具体而言，不能调用此操作使用 HTTP GET。

删除数据库记录后，您需要显示更新的联系人列表不包含已删除的记录。 AjaxDelete() 方法返回部分 ContactList 和更新的联系人列表。

## <a name="summary"></a>总结

在此迭代中，我们添加 Ajax 功能到我们的联系人管理器应用程序。 我们使用 Ajax 来提高响应能力和我们的应用程序的性能。

首先，我们重构索引视图，以便单击联系人组不会更新整个视图。 相反，单击联系人组仅可更新联系人的列表。

接下来，我们使用 jQuery 动画效果淡出和淡入的联系人列表。 将动画添加到 Ajax 应用程序可以用于为浏览器进度栏的等效项的应用程序的用户提供。

我们还添加到我们的 Ajax 应用程序的浏览器历史记录支持。 我们已启用的用户单击浏览器返回并转发按钮可以更改索引视图的状态。

最后，我们创建支持 HTTP DELETE 操作的删除链接。 通过执行 Ajax 删除，我们使用户能够删除数据库记录，而无需用户请求额外的删除确认页面。

> [!div class="step-by-step"]
> [上一篇](iteration-6-use-test-driven-development-vb.md)
