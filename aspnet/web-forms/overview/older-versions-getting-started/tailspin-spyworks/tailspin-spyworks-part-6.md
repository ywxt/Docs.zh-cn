---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 第 6 部分： ASP.NET 成员资格 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 6 部分添加 ASP.NET 成员资格。
ms.author: aspnetcontent
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: 303c1edf548db1da9ef61d94bdd8157d6afbb2e4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804415"
---
<a name="part-6-aspnet-membership"></a>第 6 部分： ASP.NET 成员资格
====================
通过[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。 它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。
> 
> 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 6 部分添加 ASP.NET 成员资格。


## <a id="_Toc260221672"></a>  使用 ASP.NET 成员资格

![](tailspin-spyworks-part-6/_static/image1.png)

单击安全

![](tailspin-spyworks-part-6/_static/image1.jpg)

请确保，我们将使用窗体身份验证。

![](tailspin-spyworks-part-6/_static/image2.jpg)

使用"创建用户"链接创建几个用户。

![](tailspin-spyworks-part-6/_static/image3.jpg)

完成后，请参阅解决方案资源管理器窗口并刷新视图。

![](tailspin-spyworks-part-6/_static/image2.png)

请注意，ASPNETDB。已创建 MDF 没问题。 此文件包含表以支持核心 ASP.NET 服务，如成员身份。

现在我们可以开始实施签出过程。

首先，创建 CheckOut.aspx 页。

CheckOut.aspx 页应仅可供已登录，因此我们会限制对访问已登录用户未登录到登录页的重定向用户的用户。

为此我们将添加以下 web.config 文件的配置节。

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

ASP.NET Web 窗体应用程序模板自动添加到 web.config 文件的身份验证部分，并建立的默认登录页。

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

我们必须修改 Login.aspx 代码隐藏文件以在用户登录时，迁移匿名的购物车。 更改的页\_加载事件，如下所示。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

然后添加如下设置的会话名称将为新登录的用户并通过我们 MyShoppingCart 类中调用 MigrateCart 方法将在购物车中的临时会话 id 更改为的用户的"LoggedIn"事件处理程序。 （在.cs 文件中实现）

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

实现 MigrateCart() 方法像这样。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

Checkout.aspx 中我们将使用 EntityDataSource 和 GridView 中我们签出页几乎与我们在我们的购物车页中。

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

请注意，我们的 GridView 控件指定"ondatabound"事件处理程序名为 MyList\_RowDataBound 因此让我们来实现此类事件处理程序。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

此方法操作可使汇总的购物车随着每个行绑定和更新 GridView 的底部行。

在此阶段我们实现了要放置的顺序的"评论"演示文稿。

让我们通过将少量的代码行添加到我们的页面处理空车方案\_加载事件：

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

当用户单击"提交"按钮时我们将执行下面的代码中的提交按钮单击事件处理程序。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

"主要内容"的订单提交过程是在我们 MyShoppingCart 类的 SubmitOrder() 方法中实现。

SubmitOrder 将：

- 在购物车中采取的所有行项，并使用它们来创建新的订单记录和相关联的 OrderDetails 记录。
- 计算发货日期。
- 清除购物车。


[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

此示例应用程序供我们将只需将两天添加到当前日期来计算发货日期。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

运行应用程序现在将允许我们要测试从开始到完成购物过程。

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-5.md)
> [下一页](tailspin-spyworks-part-7.md)
