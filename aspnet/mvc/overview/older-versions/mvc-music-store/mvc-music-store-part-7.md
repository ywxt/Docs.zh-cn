---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 第 7 部分： 成员身份和授权 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 7 部分介绍了成员身份和授权。
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/13/2010
ms.topic: article
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: 41b17315cbe1f6d93001a736bc24bf003df24061
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393165"
---
<a name="part-7-membership-and-authorization"></a>第 7 部分： 成员身份和授权
====================
通过[Jon Galloway](https://github.com/jongalloway)

> MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。  
>   
> MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。  
>   
> 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 7 部分介绍了成员身份和授权。


Store Manager 控制器是当前访问我们的站点的任何人都可访问。 让我们更改此设置以限制对网站管理员的权限。

## <a name="adding-the-accountcontroller-and-views"></a>添加 AccountController 和视图

完整的 ASP.NET MVC 3 Web 应用程序模板和 ASP.NET MVC 3 空 Web 应用程序模板之间的一个区别是空的模板不包括帐户控制器。 我们将通过复制几个文件从完整的 ASP.NET MVC 3 Web 应用程序模板创建新的 ASP.NET MVC 应用程序来添加帐户控制器。

创建新的 ASP.NET MVC 应用程序使用完整的 ASP.NET MVC 3 Web 应用程序模板并将以下文件复制到项目中的同一个目录：

1. 在 Controllers 目录中复制 AccountController.cs
2. 在 Models 目录中复制 AccountModels
3. 创建 Views 目录帐户目录并复制中的所有四个视图

更改控制器和模型类的命名空间，以便它们开头 MvcMusicStore。 AccountController 类应使用 MvcMusicStore.Controllers 命名空间，并且 AccountModels 类应使用 MvcMusicStore.Models 命名空间。

*注意： 这些文件也是从中我们复制站点设计文件在本教程开始 MvcMusicStore Assets.zip 下载中提供的。成员资格文件位于代码目录中。*

更新后的解决方案应如以下所示：

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a>添加了管理用户与 ASP.NET 配置网站

我们要求在我们的网站授权之前，我们将需要创建具有访问权限的用户。 若要创建的用户的最简单方法是使用内置的 ASP.NET 配置网站。

通过单击以下解决方案资源管理器中的图标启动 ASP.NET 配置网站。

![](mvc-music-store-part-7/_static/image2.png)

这将启动配置网站。 单击主屏幕上的安全选项卡，然后单击"启用角色"中的链接，在屏幕的中心。

![](mvc-music-store-part-7/_static/image3.png)

单击"创建或管理角色"链接。

![](mvc-music-store-part-7/_static/image4.png)

输入"管理员"角色名称，然后按添加角色按钮。

![](mvc-music-store-part-7/_static/image5.png)

单击后退按钮，然后单击左侧和右侧的创建用户链接。

![](mvc-music-store-part-7/_static/image6.png)

填写用户信息字段在左侧使用以下信息：

| **字段** | **值** |
| --- | --- |
| **用户名** | 管理员 |
| **密码** | password123 ！ |
| **确认密码** | password123 ！ |
| **电子邮件** | （也适用任何电子邮件地址） |
| **安全提示问题** | （任意） |
| **安全提示问题的答案** | （任意） |

*注意： 当然可以使用您希望的任何密码。默认密码安全设置需要 7 个字符长，并且包含一个非字母数字字符的密码。*

选择此用户的管理员角色，然后单击创建用户按钮。

![](mvc-music-store-part-7/_static/image7.png)

此时，应看到一条消息指出已成功创建用户。

![](mvc-music-store-part-7/_static/image8.png)

现在可以关闭浏览器窗口。

## <a name="role-based-authorization"></a>基于角色的授权

现在我们可以使用 [Authorize] 特性，指定用户必须管理员角色才能访问类中的任何控制器操作 StoreManagerController 限制访问。

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

*注意： 可以放置 [Authorize] 特性，以及在控制器类级别上的特定操作方法。*

现在浏览到 /StoreManager 会出现一个登录对话框：

![](mvc-music-store-part-7/_static/image9.png)

登录后使用这个新的管理员帐户，我们可以转到唱片集编辑屏幕之前。

> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-6.md)
> [下一页](mvc-music-store-part-8.md)
