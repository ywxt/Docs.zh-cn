---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: 迭代 3 – 添加表单验证 (VB) |Microsoft Docs
author: microsoft
description: 在第三个迭代中，我们将添加基本窗体验证。 我们阻止用户提交窗体而无法完成所需的窗体字段。 我们还验证 emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: b44aaab45f04f736e4171a43a8b24b71aaedca2f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825251"
---
<a name="iteration-3--add-form-validation-vb"></a>迭代 3 – 添加表单验证 (VB)
====================
by [Microsoft](https://github.com/microsoft)

[下载代码](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> 在第三个迭代中，我们将添加基本窗体验证。 我们阻止用户提交窗体而无法完成所需的窗体字段。 我们还验证电子邮件地址和电话号码。


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建联系人管理 ASP.NET MVC 应用程序 (VB)
  

在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。 联系人管理器应用程序，可存储联系人信息的名称，电话号码和电子邮件地址的人的列表。

我们通过多个迭代中生成应用程序。 每次迭代时，我们逐渐提高应用程序。 此多个迭代方法的目标是帮助你了解每个更改的原因。

- 迭代 1-创建应用程序。 在第一次迭代中，我们创建联系人管理器中的最简单方法可能。 我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。

- 迭代 2 – 使应用程序看上去更美观。 在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。

- 迭代 3-添加窗体验证。 在第三个迭代中，我们将添加基本窗体验证。 我们阻止用户提交窗体而无法完成所需的窗体字段。 我们还验证电子邮件地址和电话号码。

- 迭代 4-使应用程序松散耦合。 在此第四个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。 例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。

- 迭代 5 — 创建单元测试。 在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。 我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。

- 迭代 6-使用测试驱动的开发。 在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。 在此迭代中，我们将添加联系人组。

- 迭代 7-添加 Ajax 功能。 在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。


## <a name="this-iteration"></a>此迭代

在联系人管理器应用程序的此第二个迭代中，我们将添加基本窗体验证。 我们阻止用户提交联系人而无需为所需的窗体字段输入值。 我们还验证电话号码和电子邮件地址 （请参阅图 1）。


[![新建项目对话框](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)

**图 01**： 带有验证的窗体 ([单击以查看实际尺寸的图像](iteration-3-add-form-validation-vb/_static/image2.png))


在此迭代中，我们直接向控制器操作添加验证逻辑。 一般情况下，这不是将验证添加到 ASP.NET MVC 应用程序的建议的方法。 更好的方法是将应用程序的验证逻辑放在单独[服务层](http://martinfowler.com/eaaCatalog/serviceLayer.html)。 在下一个迭代中，我们将重构要使应用程序更易于维护的联系人管理器应用程序。

在此迭代中，为简便起见，我们编写验证代码的所有手动。 而不是自己编写验证代码，我们无法充分利用验证框架。 例如，可以使用 Microsoft 企业库验证应用程序块 (VAB) 要为 ASP.NET MVC 应用程序中实现验证逻辑。 若要了解有关验证应用程序块的详细信息，请参阅：

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>将验证添加到 Create 视图

让我们来首先将验证逻辑添加到 Create 视图。 幸运的是，由于我们生成的 Create 视图使用 Visual Studio，创建视图已包含的所有必要的用户界面逻辑，以显示验证消息。 在列表 1 中包含创建视图。

**代码清单 1-\Views\Contact\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

字段验证错误类用于设置样式由 Html.ValidationMessage() 帮助器呈现的输出。 输入验证错误类用于设置样式由 Html.TextBox() 帮助器呈现的文本框 （输入）。 验证摘要错误类用于设置样式呈现 Html.ValidationSummary() 帮助程序的未排序的列表。

> [!NOTE] 
> 
> 您可以修改自定义验证错误消息的外观此部分中所述的样式表类。


## <a name="adding-validation-logic-to-the-create-action"></a>添加到的验证逻辑创建操作

现在，创建视图永远不会显示验证错误消息，因为我们不编写逻辑来生成的任何消息。 为了显示验证错误消息，您需要错误消息添加到 ModelState。

> [!NOTE] 
> 
> UpdateModel() 方法将错误消息添加到 ModelState 自动错误窗体字段的值分配到属性时。 例如，如果尝试将字符串"apple"分配给接受的日期时间值的 BirthDate 属性，然后 UpdateModel() 方法向错误 ModelState。


代码清单 2 中的已修改 create （） 方法包含新的联系人插入到数据库之前会验证 Contact 类的属性的新部分。

**代码清单 2-Controllers\ContactController.vb （创建于验证）**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

验证部分会强制执行四个不同的验证规则：

- FirstName 属性必须具有的长度大于零 （和它不能只由空格）
- 姓氏属性必须具有的长度大于零 （和它不能只由空格）
- 如果电话属性具有值 （具有的长度大于 0） 则 Phone 属性必须与正则表达式匹配。
- 如果电子邮件属性具有值 （具有的长度大于 0） 则电子邮件属性必须与正则表达式匹配。

如果验证规则冲突，则将一条错误消息添加到 ModelState AddModelError() 方法的帮助。 时向 ModelState 添加一条消息，提供的属性名称和验证错误消息的文本。 Html.ValidationSummary() 和 Html.ValidationMessage() 帮助器方法的情况下，此错误消息显示在视图中。

执行验证规则后，检查 ModelState IsValid 属性。 当任何验证错误消息都已添加到 ModelState IsValid 属性返回 false。 如果验证失败，错误消息与重新创建窗体。

> [!NOTE] 
> 
> 我收到了用于验证的正则表达式存储库中的电话号码和电子邮件地址的正则表达式 [*http://regexlib.com*](http://regexlib.com)


## <a name="adding-validation-logic-to-the-edit-action"></a>将验证逻辑添加到编辑操作

Edit （） 操作更新联系人。 Edit （） 操作需要对其执行完全相同的验证作为 create （） 操作。 而不是重复相同的验证代码，我们应重构联系人控制器以便 create （） 和 edit （） 操作调用相同的验证方法。

修改后的 Contact 控制器类都包含在清单 3。 此类有一个新的 ValidateContact() 方法调用中的 create （） 和 edit （） 操作。

**代码清单 3-Controllers\ContactController.vb**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a>总结

在此迭代中，我们添加到我们的联系人管理器应用程序基本窗体验证。 我们的验证逻辑可阻止用户提交新的联系人或编辑现有联系人，无需提供的 FirstName 和 LastName 属性的值。 此外，用户必须提供有效的电话号码和电子邮件地址。

在此迭代中，我们添加验证逻辑到我们的联系人管理器应用程序中可能的最简单方法。 但是，到我们的控制器逻辑混合我们验证逻辑将创建问题对我们在长期内。 我们的应用程序将会更难维护和随着时间的推移修改。

在下一个迭代中，我们将带我们控制器重构我们的验证逻辑和数据库访问逻辑。 我们将充分利用多个软件设计原则，使我们能够创建一个更松散耦合，且更易于维护，应用程序。

> [!div class="step-by-step"]
> [上一页](iteration-2-make-the-application-look-nice-vb.md)
> [下一页](iteration-4-make-the-application-loosely-coupled-vb.md)
