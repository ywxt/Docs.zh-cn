---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
title: 迭代 2 – 使应用程序外表美观 (VB) |Microsoft Docs
author: microsoft
description: 在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f65cb436-e493-46fd-9608-384b27385aa1
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
msc.type: authoredcontent
ms.openlocfilehash: 7f27cbab17effc3b44649e06409893e6be09b011
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824742"
---
<a name="iteration-2--make-the-application-look-nice-vb"></a>迭代 2 – 使应用程序外表美观 (VB)
====================
by [Microsoft](https://github.com/microsoft)

[下载代码](iteration-2-make-the-application-look-nice-vb/_static/contactmanager_2_vb1.zip)

> 在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建联系人管理 ASP.NET MVC 应用程序 (VB)
  

在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。 联系人管理器应用程序使您可以存储联系人信息-名称、 电话号码和电子邮件地址-有关列表的人员。

我们通过多个迭代中生成应用程序。 每次迭代时，我们逐渐提高应用程序。 此多个迭代方法的目标是帮助你了解每个更改的原因。

- 迭代 1 – 创建应用程序。 在第一次迭代中，我们创建联系人管理器中的最简单方法可能。 我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。

- 迭代 2 – 使应用程序看上去更美观。 在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。

- 迭代 3 – 添加表单验证。 在第三个迭代中，我们将添加基本窗体验证。 我们阻止用户提交窗体而无法完成所需的窗体字段。 我们还验证电子邮件地址和电话号码。

- 迭代 4 – 使应用程序松散耦合。 在此第四个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。 例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。

- 迭代 5 — 创建单元测试。 在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。 我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。

- 迭代 6 – 使用测试驱动的开发。 在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。 在此迭代中，我们将添加联系人组。

- 迭代 7 – 添加 Ajax 功能。 在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。

## <a name="this-iteration"></a>此迭代

此迭代的目标是提高联系人管理器应用程序的外观。 目前，联系人管理器使用默认 ASP.NET MVC 视图母版页和级联样式表 （请参见图 1）。 这些不要看上去有错误，但我不想要看起来正像 ASP.NET MVC 的其他每个网站的联系人管理器。 我想要自定义文件中替换这些文件。


[![新建项目对话框](iteration-2-make-the-application-look-nice-vb/_static/image1.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image1.png)

**图 01**： 将 ASP.NET MVC 应用程序的默认外观 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-vb/_static/image2.png))


在此迭代中，我将介绍两种方法可以改进我们的应用程序的可视设计。 首先，我介绍您如何充分利用 ASP.NET MVC 设计库下载免费的 ASP.NET MVC 设计模板。 ASP.NET MVC 设计库，可创建专业的 web 应用程序不执行任何操作。

我决定不使用 ASP.NET MVC 设计库中的联系人管理器应用程序模板。 相反，我创建的专业设计公司的自定义设计。 在本教程的第二部分，我将说明我的专业设计公司创建最终的 ASP.NET MVC 设计的工作方式。

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC 设计库

ASP.NET MVC 设计库是由 Microsoft 提供的免费资源。 ASP.NET MVC 库位于以下地址：

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC 设计库托管的免费网站设计专门为使用 ASP.NET MVC 项目中创建的集合。 设计会上传由社区的成员。 库的访问者可以对他们最喜爱的设计进行投票 （请参见图 2）。


[![新建项目对话框](iteration-2-make-the-application-look-nice-vb/_static/image2.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image3.png)

**图 02**: ASP.NET MVC 设计库 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-vb/_static/image4.png))


在我撰写本教程中，在库中最受欢迎的设计是由 David Hauser 命名年 10 月的设计。 可以通过完成以下步骤来为 ASP.NET MVC 项目中使用这种设计：

1. 单击**下载**按钮 October.zip 文件下载到您的计算机。
2. 右键单击下载的 October.zip 文件，然后单击**解除阻止**按钮 （请参见图 3）。
3. 将文件提取到名为年 10 月的文件夹。
4. 从年 10 月文件夹中包含 DesignTemplate 文件夹中选择的所有文件，右键单击文件，然后选择菜单选项**复制**。
5. 右键单击 Visual Studio 解决方案资源管理器窗口中的 ContactManager 项目节点，然后选择菜单选项**粘贴**（请参阅图 4）。
6. 选择 Visual Studio 的菜单选项**编辑、 查找和替换，快速替换**和替换 *[MyProjectName]* 与*ContactManager* （请参见图 5）。


[![新建项目对话框](iteration-2-make-the-application-look-nice-vb/_static/image3.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image5.png)

**图 03**： 取消阻止文件从 web 下载 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-vb/_static/image6.png))


[![新建项目对话框](iteration-2-make-the-application-look-nice-vb/_static/image4.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image7.png)

**图 04**： 重写在解决方案资源管理器中的文件 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-vb/_static/image8.png))


[![新建项目对话框](iteration-2-make-the-application-look-nice-vb/_static/image5.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image9.png)

**图 05**: [ProjectName] 替换为 ContactManager ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-vb/_static/image10.png))


完成这些步骤后，web 应用程序将使用新的设计。 图 6 中的页说明了与年 10 月设计 Contact Manager 应用程序的外观。


[![新建项目对话框](iteration-2-make-the-application-look-nice-vb/_static/image6.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image11.png)

**图 06**： 使用年 10 月模板 ContactManager ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-vb/_static/image12.png))


## <a name="creating-a-custom-aspnet-mvc-design"></a>创建自定义 ASP.NET MVC 设计

ASP.NET MVC 设计库具有不同的设计样式的不错的选择。 库提供了一种轻松的方法，以自定义 ASP.NET MVC 应用程序的外观。 而且，当然，库已大优点是完全免费。

但是，您可能需要创建你的网站的完全唯一设计。 在这种情况下，最好使用网站设计公司。 我决定采用此方法的联系人管理器应用程序的设计。

我压缩了联系人管理器从迭代 #1 并发送到设计公司的项目。 它们不归 Visual Studio （感到难为情它们 ！），但该无效 t 出现问题。 他们就能够从免费下载 Microsoft Visual Web Developer [ https://www.asp.net ](https://www.asp.net)网站，然后打开 Visual Web Developer 中的联系人管理器应用程序。 在几天，它们必须生成图 7 中的设计。


[![新建项目对话框](iteration-2-make-the-application-look-nice-vb/_static/image7.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image13.png)

**图 07**: ASP.NET MVC 联系人管理器中设计 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-vb/_static/image14.png))


新的设计包括两个主要文件： 新的级联样式表文件和新视图母版页文件。 视图母版页包含布局和共享的内容的 ASP.NET MVC 应用程序中的视图。 例如，视图母版页包括标头、 导航选项卡和页脚显示在图 7。 我使用从设计公司中，新的 Site.Master 文件覆盖现有 Site.Master 视图母版页中的 Views\Shared 文件夹

设计公司还创建了新的级联样式表和的图像集。 我的内容文件夹中放置了这些新文件，并覆盖现有 Site.css 文件。 应将所有静态内容放在内容文件夹中。

请注意，新设计的联系人管理器中包含图像编辑和删除联系人。 联系人的 HTML 表中每个联系人旁边出现的编辑和删除映像。

最初，这些链接在呈现的 HTML。此类 ActionLink() 帮助程序：

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample1.aspx)]

Html.ActionLink() 方法不支持 （方法 HTML 编码的链接文本出于安全原因） 的映像。 因此，我可以对 Html.ActionLink() 调用替换到 Url.Action() 如下调用：

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample2.aspx)]

Html.ActionLink() 方法将呈现整个 HTML 超链接。 Url.Action() 方法，但是，呈现只是不带 URL &lt;&gt;标记。

此外，请注意，新的设计包括选定和未选定的选项卡。 例如，在图 8**创建新的联系人**选择选项卡和**我的联系人**不选择选项卡。


[![新建项目对话框](iteration-2-make-the-application-look-nice-vb/_static/image8.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image15.png)

**图 08**： 选中和取消选中选项卡 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-vb/_static/image16.png))


若要支持呈现选定和未选定的选项卡，我创建了名为 MenuItemHelper 的自定义 HTML 帮助程序。 此帮助器方法将呈现任一&lt;li&gt;标记或&lt;l i 类 ="所选"&gt;具体取决于当前的控制器和操作是否对应于传递给帮助者的控制器和操作名称的标记。 MenuItemHelper 的代码包含在列表 1 中。

**代码清单 1 – Helpers\MenuItemHelper.vb**

[!code-vb[Main](iteration-2-make-the-application-look-nice-vb/samples/sample3.vb)]

MenuItemHelper TagBuilder 类在内部用于生成&lt;li&gt; HTML 标记。 TagBuilder 类是无论何时需要新的 HTML 标记生成可以使用一个非常有用的实用工具类。 它包括用于添加属性、 添加 CSS 类、 生成 Id，和修改标记的方法内部 HTML。

## <a name="summary"></a>总结

在此迭代中，我们改进了 ASP.NET MVC 应用程序的可视设计。 首先，已引入到 ASP.NET MVC 设计库。 您学习了如何从 ASP.NET MVC 设计库，可以使用 ASP.NET MVC 应用程序中下载免费的设计模板。

接下来，我们讨论了如何通过修改默认级联样式表文件和母版视图页文件创建自定义设计。 为了支持新的设计，我们需要对我们的联系人管理器应用程序进行少量更改。 例如，我们添加了名为显示选定和未选定的选项卡 MenuItemHelper 的新 HTML 帮助程序。

在下一个迭代中，我们将探讨的验证非常重要的主题。 以便用户不能创建新的联系人，无需首先提供所需的值，例如一个人 s 名和姓，我们将验证代码添加到我们的应用程序。

> [!div class="step-by-step"]
> [上一页](iteration-1-create-the-application-vb.md)
> [下一页](iteration-3-add-form-validation-vb.md)
