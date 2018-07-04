---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
title: 成员身份和管理 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 732a2316-e49f-4f72-becd-0cd72f14457e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
msc.type: authoredcontent
ms.openlocfilehash: 58eda260ccf2d0f237aaade65017760ed87a8c4f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368293"
---
<a name="membership-and-administration"></a>成员身份和管理
====================
通过[Erik Reitan](https://github.com/Erikre)

[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。 Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。


本教程演示如何更新 Wingtip Toys 示例应用程序来添加自定义角色并使用 ASP.NET 标识。 它还演示如何实现具有自定义角色的用户可以从中添加和从网站中删除产品的管理页。

[ASP.NET 标识](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)是用于生成 ASP.NET web 应用程序的成员身份系统，可在 ASP.NET 4.5。 在 Visual Studio 2013 Web 窗体项目模板，以及为模板中使用 ASP.NET 标识[ASP.NET MVC](../../../../mvc/index.md)， [ASP.NET Web API](../../../../web-api/index.md)，和[ASP.NET 单页面应用程序](../../../../single-page-application/index.md). 此外专门可以安装在与空 Web 应用程序启动时使用 NuGet 的 ASP.NET 标识系统。 但是，在本系列教程中使用**Web 窗体**projecttemplate，其中包括 ASP.NET 标识系统。 ASP.NET 标识，可以轻松地将特定于用户的配置文件数据与应用程序数据集成。 此外，ASP.NET 标识，可在应用程序中选择的用户配置文件的持久性模型。 你可以将数据存储在 SQL Server 数据库或其他数据存储，包括*NoSQL*数据存储 Windows Azure 存储表等。

本教程基于 Wingtip Toys 教程系列中标题为"签出和支付与 PayPal"上一教程。

## <a name="what-youll-learn"></a>你将学习：

- 如何使用代码将自定义角色和用户添加到应用程序。
- 如何限制对管理文件夹和页的访问。
- 如何提供属于自定义角色的用户的导航。
- 如何使用模型绑定来填充[DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx)与产品类别的控件。
- 如何将文件上传到 web 应用程序通过[FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx)控件。
- 如何使用验证控件来实施输入的验证。
- 如何添加和删除从应用程序的产品。

## <a name="these-features-are-included-in-the-tutorial"></a>在本教程中包括这些功能：

- ASP.NET 标识
- 配置和授权
- 模型绑定
- 非介入式验证

ASP.NET Web 窗体提供了成员资格功能。 通过使用默认模板，您有可以立即使用应用程序运行时的内置成员资格功能。 本教程演示如何使用 ASP.NET 标识添加自定义角色，并将用户分配给该角色。 您将学习如何限制对管理文件夹的访问。 对管理文件夹，允许具有自定义角色的用户添加和删除产品，以及预览产品，在添加完后，将添加一个页面。

## <a name="adding-a-custom-role"></a>添加自定义角色

使用 ASP.NET 标识，可以添加自定义角色，并将用户分配给该角色使用的代码。

1. 在中**解决方案资源管理器**，右键单击*逻辑*文件夹并创建一个新类。
2. 将新类命名*RoleActions.cs*。
3. 修改代码，以使其显示，如下所示：  

    [!code-csharp[Main](membership-and-administration/samples/sample1.cs?highlight=8)]
4. 在中**解决方案资源管理器**，打开*Global.asax.cs*文件。
5. 修改*Global.asax.cs*文件添加代码以黄色突出显示，以使其显示，如下所示：  

    [!code-csharp[Main](membership-and-administration/samples/sample2.cs?highlight=11,26-28)]
6. 请注意，`AddUserAndRole`以红色下划线标记。 双击 AddUserAndRole 代码。  
   将带有下划线字母"A"突出显示方法的开头。
7. 悬停在字母"A"，然后单击用户界面，使你可以生成方法存根`AddUserAndRole`方法。 

    ![成员资格和 Advministration-生成方法存根 （stub）](membership-and-administration/_static/image1.png)
8. 单击标题为的选项：  
    `Generate method stub for "AddUserAndRole" in "WingtipToys.Logic.RoleActions"`
9. 打开*RoleActions.cs*文件从*逻辑*文件夹。  
   `AddUserAndRole`方法已添加到类文件。
10. 修改*RoleActions.cs*通过删除文件`NotImplementedeException`并添加以黄色突出显示的代码，以使其显示，如下所示：  

    [!code-csharp[Main](membership-and-administration/samples/sample3.cs?highlight=5-7,15-51)]

上面的代码首先建立成员资格数据库的数据库上下文。 成员资格数据库还存储为 *.mdf*中的文件*应用\_数据*文件夹。 你将能够查看此数据库后的第一个用户已登录到此 web 应用程序。 

> [!NOTE] 
> 
> 如果你希望存储成员资格数据以及产品的数据，可以考虑使用的相同**DbContext**用于将产品数据存储在上面的代码。


 *内部*关键字是类型 （如类） 和类型成员 （如方法或属性） 的访问修饰符。 内部类型或成员是只能在同一程序集中包含的文件中访问 *(.dll*文件)。 当生成应用程序，程序集文件 *(.dll*) 创建，其中包含运行应用程序时执行的代码。 

一个`RoleStore`对象，它提供角色管理，将根据创建的数据库上下文。

> [!NOTE] 
> 
> 请注意，当`RoleStore`创建对象时使用泛型`IdentityRole`类型。 这意味着`RoleStore`仅允许包含`IdentityRole`对象。 此外通过使用泛型，在内存中的资源的更好地处理。


下一步，`RoleManager`对象，会根据创建`RoleStore`刚创建的对象。 `RoleManager`对象公开与角色相关 API 可用于自动将更改保存到`RoleStore`。 `RoleManager`仅允许包含`IdentityRole`对象，因为该代码使用`<IdentityRole>`泛型类型。

在调用`RoleExists`方法，以确定是否存在成员资格数据库中的"canEdit"角色。 如果不是这样，您创建的角色。

创建`UserManager`似乎比复杂对象`RoleManager`控制，但是它是几乎相同。 它只是上一个行，而不是几个进行编码。 在这里，您传递的参数作为包含在括号中的新对象实例化。

接下来通过创建一个新创建的"canEditUser"用户`ApplicationUser`对象。 然后，如果您已成功创建用户，你将用户添加到新角色。

> [!NOTE] 
> 
> 稍后在本系列教程中，"ASP.NET 错误处理"本教程中，将更新错误处理。


下次启动应用程序，将作为名为应用程序的"canEdit"角色添加名为"canEditUser"的用户。 更高版本在本教程中，你将登录为"canEditUser"用户以显示将在本教程过程中添加的其他功能。 有关 ASP.NET 标识的 API 详细信息，请参阅[Microsoft.AspNet.Identity Namespace](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx)。 有关初始化 ASP.NET 标识系统的其他详细信息，请参阅[AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs)。

### <a name="restricting-access-to-the-administration-page"></a>限制对管理页的访问

Wingtip Toys 示例应用程序允许匿名用户和登录的用户可以查看和购买产品。 但是，有自定义"canEdit"角色的登录的用户可以访问受限的页面才能添加和删除产品。

#### <a name="add-an-administration-folder-and-page"></a>添加管理文件夹和页面

接下来，将创建名为的文件夹*管理员*"canEditUser"用户属于自定义角色的 Wingtip Toys 示例应用程序。

1. 右键单击项目名称 (**Wingtip Toys**) 中**解决方案资源管理器**，然后选择**添加** - &gt; **的新文件夹**.
2. 将新文件夹命名*管理员*。
3. 右键单击*管理员*文件夹，然后选择**添加** - &gt; **新项**。   
   随即出现“添加新项”对话框。
4. 选择<strong>Visual C#</strong> - &gt; <strong>Web</strong>在左侧的模板组。 从中间列表中选择<strong>包含母版页的 Web 窗体</strong>，其命名<em>AdminPage.aspx</em><strong>，</strong> ，然后选择<strong>添加</strong>。
5. 选择*Site.Master*另存为母版页文件，然后选择**确定**。

#### <a name="add-a-webconfig-file"></a>添加 Web.config 文件

通过添加*Web.config*的文件*管理员*文件夹中，您可以限制对访问该文件夹中包含的页。

1. 右键单击*管理员*文件夹，然后选择**添加** - &gt; **新项**。  
   随即出现“添加新项”对话框。
2. 从 Visual C# web 模板列表中选择<strong>Web 配置文件</strong>从中间列表中，接受默认名称<em>Web.config</em><strong>，</strong> ，然后选择<strong>添加</strong>。
3. 替换现有的 XML 中的内容*Web.config*具有以下文件：  

    [!code-xml[Main](membership-and-administration/samples/sample4.xml)]

保存*Web.config*文件。 *Web.config*文件指定仅属于"canEdit"角色的应用程序的用户才能访问中包含页*管理员*文件夹。

### <a name="including-custom-role-navigation"></a>包括自定义角色导航

若要启用自定义"canEdit"角色的用户可以导航到应用程序的管理部分，必须添加一个链接到*Site.Master*页。 只有属于"canEdit"角色的用户将能看到**管理员**链接，然后访问管理部分。

1. 在解决方案资源管理器，找到并打开*Site.Master*页。
2. 若要创建用户的"canEdit"角色链接，请将添加到以下的未排序列表的黄色突出显示的标记`<ul>`元素，以便列表显示为如下所示：  

    [!code-html[Main](membership-and-administration/samples/sample5.html?highlight=2-3)]
3. 打开*Site.Master.cs*文件。 请**管理员**链接仅对"canEditUser"用户添加到的黄色突出显示的代码可见`Page_Load`处理程序。 `Page_Load`处理程序将出现，如下所示：   

    [!code-csharp[Main](membership-and-administration/samples/sample6.cs?highlight=3-6)]

当页面加载时，代码将检查是否已登录的用户具有的"canEdit"角色。 如果用户属于"canEdit"角色，其中包含指向的 span 元素*AdminPage.aspx*页 （并因此在范围内的链接） 变为可见。

### <a name="enabling-product-administration"></a>启用产品管理

到目前为止，已创建"canEdit"角色，并添加"canEditUser"用户、 管理文件夹和管理页。 已设置为管理文件夹和页的访问权限，并已添加到应用程序的"canEdit"角色的用户的导航链接。 接下来，将添加到标记*AdminPage.aspx*页上，并为代码*AdminPage.aspx.cs*将启用"canEdit"角色的用户添加和删除产品的代码隐藏文件。

1. 在中**解决方案资源管理器**，打开*AdminPage.aspx*从文件*管理员*文件夹。
2. 使用以下内容替换现有标记：  

    [!code-aspx[Main](membership-and-administration/samples/sample7.aspx)]
3. 接下来，打开*AdminPage.aspx.cs*代码隐藏文件，请右键单击*AdminPage.aspx* ，然后单击**查看代码**。
4. 中的现有代码替换*AdminPage.aspx.cs*代码隐藏文件中的使用以下代码：  

    [!code-csharp[Main](membership-and-administration/samples/sample8.cs)]

在代码中的输入*AdminPage.aspx.cs*代码隐藏文件中，一个名为类`AddProducts`执行将产品添加到数据库的实际工作。 此类尚不存在，这样就会立即创建。

1. 在中**解决方案资源管理器**，右键单击*逻辑*文件夹，然后选择**添加** - &gt; **新项**。   
   随即出现“添加新项”对话框。
2. 选择**Visual C#**  - &gt; **代码**在左侧的模板组。 然后，选择**类**从中间列表并将其命名*AddProducts.cs*。   
   显示新类文件中。
3. 将现有代码替换为以下代码：  

    [!code-csharp[Main](membership-and-administration/samples/sample9.cs)]

*AdminPage.aspx*页允许用户属于"canEdit"角色添加和删除产品。 添加一个新的产品，有关该产品的详细信息证，然后输入到数据库。 新的产品是立即可供所有用户的 web 应用程序。

#### <a name="unobtrusive-validation"></a>非介入式验证

用户在提供的产品详细信息*AdminPage.aspx*通过验证控件对页面进行验证 (`RequiredFieldValidator`和`RegularExpressionValidator`)。 这些控件将自动使用非介入式验证。 非介入式验证允许 JavaScript 用于客户端验证逻辑，这意味着页面不需要到服务器，以验证某个行程的验证控件。 默认情况下，非介入式验证包含在*Web.config*文件基于以下配置设置：

[!code-xml[Main](membership-and-administration/samples/sample10.xml)]

#### <a name="regular-expressions"></a>正则表达式

上的产品价格*AdminPage.aspx*使用验证页**RegularExpressionValidator**控件。 此控件验证是否关联的输入控件 （"AddProductPrice"文本框） 的值与指定的正则表达式模式匹配。 正则表达式模式匹配表示法，可用于快速查找和匹配特定的字符模式。 **RegularExpressionValidator**控件包含一个名为属性`ValidationExpression`，其中包含用于验证价格输入，如下所示的正则表达式：

[!code-aspx[Main](membership-and-administration/samples/sample11.aspx)]

#### <a name="fileupload-control"></a>FileUpload 控件

添加输入和验证控件中，除了**FileUpload**控制对*AdminPage.aspx*页。 此控件提供了将文件上传的能力。 在这种情况下，你仅允许将上传的图像文件。 在代码隐藏文件 (*AdminPage.aspx.cs*)，当`AddProductButton`单击时，代码将检查`HasFile`属性**FileUpload**控件。 如果控件具有一个文件，并且如果允许文件类型 （基于文件扩展名），则将图像保存到*映像*文件夹并*缩略图图像/* 的应用程序文件夹。

#### <a name="model-binding"></a>模型绑定

在本系列教程的前面使用模型绑定来填充**ListView**控件， **FormsView**控件， **GridView**控件，和一个**DetailView**控件。 在本教程中，您使用模型绑定来填充**DropDownList**的产品类别的列表控件。

添加到的标记*AdminPage.aspx*文件包含**DropDownList**控件调用`DropDownAddCategory`:

[!code-aspx[Main](membership-and-administration/samples/sample12.aspx)]

使用模型绑定来填充此**DropDownList**通过设置`ItemType`属性和`SelectMethod`属性。 `ItemType`属性指定您使用`WingtipToys.Models.Category`键入填充该控件时。 通过创建定义在开始本系列教程的此类型`Category`类 （如下所示）。 `Category`类位于*模型*内的文件夹*Category.cs*文件。

[!code-csharp[Main](membership-and-administration/samples/sample13.cs)]

`SelectMethod`的属性**DropDownList**控制指定您使用`GetCategories`方法 （如下所示），它是包含在代码隐藏文件 (*AdminPage.aspx.cs*)。

[!code-csharp[Main](membership-and-administration/samples/sample14.cs)]

此方法指定`IQueryable`接口用于针对查询的计算结果`Category`类型。 返回的值用于填充**DropDownList**中页的标记 (*AdminPage.aspx*)。

通过设置指定列表中的每个项的显示文本`DataTextField`属性。 `DataTextField`属性使用`CategoryName`的`Category`类 （如上所示） 以显示在每个类别**DropDownList**控件。 在中选择一项时传递的实际值**DropDownList**控制基于`DataValueField`属性。 `DataValueField`属性设置为`CategoryID`中定义`Category`类 （如上所示）。

### <a name="how-the-application-will-work"></a>如何在应用程序

属于"canEdit"角色的用户首次导航到页面时`DropDownAddCategory` **DropDownList**上文所述填充控件。 `DropDownRemoveProduct` **DropDownList**还与产品使用相同的方法填充控件。 属于"canEdit"角色的用户选择的类别类型，并添加产品详细信息 (**名称**，**说明**，**价格**，和**映像文件**). 当用户属于"canEdit"角色单击**添加产品**按钮，`AddProductButton_Click`触发事件处理程序。 `AddProductButton_Click`事件处理程序位于代码隐藏文件中 (*AdminPage.aspx.cs*) 会检查以确保它与允许的文件类型相匹配的图像文件 *(.gif*， *.png*， *.jpeg*，或 *.jpg*)。 然后，该图像文件保存到 Wingtip Toys 示例应用程序的文件夹中。 接下来，将新产品添加到数据库。 若要完成添加一个新的产品的新实例`AddProducts`创建类并将其命名为产品。 `AddProducts`类具有一个名为方法`AddProduct`，和产品对象将调用此方法以将产品添加到数据库。

[!code-csharp[Main](membership-and-administration/samples/sample15.cs)]

如果成功，该代码将新产品添加到数据库，使用查询字符串值加载该页`ProductAction=add`。

[!code-csharp[Main](membership-and-administration/samples/sample16.cs)]

当页面重新加载时，在 URL 中包含查询字符串。 通过重新加载该页面，属于"canEdit"角色的用户可以立即查看中的更新**DropDownList**上的控件*AdminPage.aspx*页。 此外，通过包括使用 URL 查询字符串，页可以显示一条成功消息向用户属于"canEdit"角色。

当*AdminPage.aspx*页上重新加载，`Page_Load`调用事件。

[!code-csharp[Main](membership-and-administration/samples/sample17.cs)]

`Page_Load`事件处理程序检查查询字符串值，并确定是否显示一条成功消息。

## <a name="running-the-application"></a>运行应用程序

可以在购物车中运行应用程序现在以查看如何添加、 删除和更新的项。 购物车总额将反映在购物车中的所有项的总成本。

1. 在解决方案资源管理器，按**F5**运行 Wingtip Toys 示例应用程序。  
   在浏览器将打开并显示*Default.aspx*页。
2. 单击**登录**在页面顶部的链接。 

    ![成员身份和管理的登录链接](membership-and-administration/_static/image2.png)

   *Login.aspx*显示页。
3. 使用以下用户名和密码：  
   用户名： canEditUser@wingtiptoys.com  
   密码： Pa $$ word1 

    ![成员身份和管理的登录页](membership-and-administration/_static/image3.png)
4. 单击**登录**靠近页面底部的按钮。
5. 在下一步的页的顶部，选择**管理员**链接以导航到*AdminPage.aspx*页。 

    ![成员身份和管理-管理员链接](membership-and-administration/_static/image4.png)
6. 若要测试输入的验证，请单击**添加产品**按钮而不添加任何产品的详细信息。 

    ![成员身份和管理-管理员页](membership-and-administration/_static/image5.png)

   请注意，显示必填的字段消息。
7. 添加一个新产品的详细信息，然后单击**添加产品**按钮。 

    ![成员身份和管理-添加产品](membership-and-administration/_static/image6.png)
8. 选择**产品**添加从顶部导航菜单上，若要查看新的产品。 

    ![成员身份和管理-显示新产品](membership-and-administration/_static/image7.png)
9. 单击**管理员**链接以返回到管理页。
10. 在中**删除产品**部分中的页上，选择你在中添加的新产品**DropDownListBox**。
11. 单击**删除产品**按钮可以删除从应用程序的新产品。 

    ![成员身份和管理-删除产品](membership-and-administration/_static/image8.png)
12. 选择**产品**确认已删除了该产品在顶部导航菜单中。
13. 单击**注销**存在管理模式。   
    请注意，不再显示在顶部导航窗格**管理员**菜单项。

## <a name="summary"></a>总结

在本教程中，添加了自定义角色和用户属于自定义角色，对受限访问权限管理文件夹和页上，并提供属于自定义角色的用户的导航。 使用模型绑定来填充**DropDownList**控件的数据。 您实现**FileUpload**控件和验证控件。 此外，介绍了如何添加和从数据库中删除产品。 在下一步的教程中，您将了解如何实现 ASP.NET 路由。

## <a name="additional-resources"></a>其他资源

[Web.config 的 authorization 元素](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)  
[ASP.NET 标识](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)  
[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET Web 窗体应用部署到 Azure 网站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure-免费试用版](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [上一页](checkout-and-payment-with-paypal.md)
> [下一页](url-routing.md)
