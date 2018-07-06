---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: 第 6 部分： 使用数据批注的模型验证 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 6 部分介绍如何为模型 V 使用数据注释...
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: 10884f569f0f5d95517b73daab31fbd269a4726a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825948"
---
<a name="part-6-using-data-annotations-for-model-validation"></a>第 6 部分： 使用数据注释进行模型验证
====================
通过[Jon Galloway](https://github.com/jongalloway)

> MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。  
>   
> MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。  
>   
> 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 6 部分介绍如何为模型验证中使用数据注释。


我们使用我们创建和编辑窗体具有一个主要问题： 未做任何验证。 我们可以执行某些操作，如在价格字段中，保留空白的必填的字段或键入字母，我们将看到的第一个错误来自数据库。

我们可以轻松添加验证到我们的应用程序，这需要通过将数据批注添加到我们的模型类来实现。 数据批注，我们可以描述应用于模型属性，我们想要的规则和 ASP.NET MVC 将负责强制执行它们并向我们的用户显示相应的消息。

## <a name="adding-validation-to-our-album-forms"></a>向我们唱片集窗体中添加验证

我们将使用以下数据注释属性：

- **所需**– 指示该属性是必填的字段
- **DisplayName** – 定义要我们在窗体字段和验证消息使用的文本
- **StringLength** – 定义字符串字段的最大长度
- **范围**– 为数字字段提供最大和最小值
- **将绑定**– 列出要排除或包括当参数或窗体值绑定到模型属性的字段
- **ScaffoldColumn** – 允许隐藏编辑器窗体中的字段

*注意： 有关使用数据注释属性的模型验证的详细信息，请参阅上的 MSDN 文档*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)

打开唱片集类并添加以下*使用*到顶部的语句。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

接下来，更新以添加显示和验证属性，如下所示的属性。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

我们可以在那里，我们已更改为虚拟属性的流派和艺术家。 这样，若要延迟加载它们根据需要的实体框架。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

后具有这些属性添加到我们唱片集的模型，我们创建和编辑屏幕立即开始验证字段，并使用显示名称，我们已选择 (例如唱片集画面 Url 而不是 AlbumArtUrl)。 运行应用程序并浏览到 /StoreManager/Create。

![](mvc-music-store-part-6/_static/image1.png)

接下来，我们将分一些验证规则。 输入 0 的价格，然后将标题留空。 当我们单击创建按钮时，我们将看到显示验证错误消息显示哪些字段不符合验证规则我们已定义的窗体。

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a>测试客户端验证

服务器端验证是从应用程序的角度看，非常重要，因为用户可以绕过客户端验证。 但是，仅实现服务器端验证网页窗体表现出三个严重问题。

1. 用户必须等待要发布，在服务器上，验证的窗体，并且要发送到其浏览器的响应。
2. 他们会校正字段，以便它现在通过验证规则时，用户不会获得即时反馈。
3. 我们都浪费服务器资源来执行验证逻辑，而不是利用用户的浏览器。

幸运的是，ASP.NET MVC 3 基架模板具有客户端验证内置的需要说明，否则任何额外工作。

在标题字段中键入单个字母满足验证要求，以便验证消息将立即删除。

![](mvc-music-store-part-6/_static/image3.png)


> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-5.md)
> [下一页](mvc-music-store-part-7.md)
