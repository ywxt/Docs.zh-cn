---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 签出和使用 PayPal 付款 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: e516bcccdecce72d4fa6c705b0227ce873429e3c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386657"
---
<a name="checkout-and-payment-with-paypal"></a>签出和使用 PayPal 付款
====================
通过[Erik Reitan](https://github.com/Erikre)

[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。 Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。


本教程介绍如何修改 Wingtip Toys 示例应用程序，包括用户授权、 注册和使用 PayPal 付款。 只有登录的用户将有购买产品的授权。 ASP.NET 4.5 Web 窗体项目模板的内置用户注册功能已包含您所需的很多。 你将添加 PayPal Express 签出功能。 在本教程会使用 PayPal 开发人员测试环境，因此会不传输任何实际的资金。 在本教程结束时，将通过选择要添加到购物车中，单击签出按钮，并将数据传输到 PayPal 测试网站产品测试应用程序。 在 PayPal 测试网站上，将确认你的传送和付款信息，然后返回到本地 Wingtip Toys 示例应用程序来确认并完成购买。

该地址可伸缩性和安全性的在线购物中有多个专用化的经验丰富的第三方付款处理器。 ASP.NET 开发人员应考虑使用第三方支付解决方案在实现购物和购买解决方案之前的优点。

> [!NOTE] 
> 
> Wingtip Toys 示例应用程序设计为向 ASP.NET web 开发人员显示特定的 ASP.NET 概念和功能可用。 此示例应用程序已不适合所有可能的情况下可伸缩性和安全性方面。


## <a name="what-youll-learn"></a>你将学习：

- 如何限制对文件夹中的特定页面的访问。
- 如何从匿名的购物车创建已知的购物车。
- 如何为项目启用 SSL。
- 如何向项目添加 OAuth 提供程序。
- 如何使用 PayPal 购买产品使用 PayPal 测试环境。
- 如何显示从 PayPal 中的详细信息**DetailsView**控件。
- 如何使用从 PayPal 获取详细信息更新数据库的 Wingtip Toys 应用程序。

## <a name="adding-order-tracking"></a>添加顺序跟踪

在本教程中，将创建两个新类来从用户创建的顺序跟踪数据。 类将跟踪有关寄送信息、 采购总计和付款确认数据。

### <a name="add-the-order-and-orderdetail-model-classes"></a>添加 Order 和 OrderDetail 模型类

在本系列教程的前面定义的类别、 产品、 架构以及通过创建项目，购物车`Category`， `Product`，并`CartItem`中的类*模型*文件夹。 现在将添加两个新类定义为产品订单和订单的详细信息架构。

1. 在中**模型**文件夹中，添加一个名为的新类*Order.cs*。   
   在编辑器中显示新类文件中。
2. 默认代码替换为以下：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. 添加*OrderDetail.cs*类来*模型*文件夹。
4. 默认代码替换为以下代码：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order`和`OrderDetail`类包含的架构来定义用于购买和传送订单信息。

此外，需要更新数据库上下文类，管理的实体类并提供对数据库的数据访问。 若要执行此操作，将添加新创建的顺序并`OrderDetail`模型类到`ProductContext`类。

1. 在中**解决方案资源管理器**，找到并打开*ProductContext.cs*文件。
2. 添加到突出显示的代码*ProductContext.cs*文件如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

如以前在此教程系列中的代码中所述*ProductContext.cs*文件将添加`System.Data.Entity`命名空间，以便有权访问的实体框架的所有核心功能。 此功能包括查询、 插入、 更新和删除通过使用强类型化对象数据的功能。 在上面的代码`ProductContext`类添加到新添加的实体框架访问`Order`和`OrderDetail`类。

## <a name="adding-checkout-access"></a>添加签出访问权限

Wingtip Toys 示例应用程序允许匿名用户可以查看并将产品添加到购物车。 但是，如果匿名用户选择购买它们添加到购物车的产品，它们就必须登录到站点。 一旦他们已登录，他们可以访问受限的页面上的 Web 应用程序处理签出和购买过程。 中包含这些受限的页面*签出*的应用程序文件夹。

### <a name="add-a-checkout-folder-and-pages"></a>添加签出文件夹和页面

现在将创建*签出*文件夹，然后在其客户将看到在结帐过程中的页。 在本教程后面，你将更新这些页面。

1. 右键单击项目名称 (**Wingtip Toys**) 中**解决方案资源管理器**，然后选择**添加新文件夹**。 

    ![签出和使用 PayPal 的新文件夹的付款](checkout-and-payment-with-paypal/_static/image1.png)
2. 将新文件夹命名*签出*。
3. 右键单击*签出*文件夹，然后选择**添加**-&gt;**新项**。 

    ![签出和使用 PayPal-新项的付款](checkout-and-payment-with-paypal/_static/image2.png)
4. 随即出现“添加新项”对话框。
5. 选择**Visual C#**  - &gt; **Web**在左侧的模板组。 然后，从中间窗格中，选择**包含母版页的 Web 窗体**并将其命名*CheckoutStart.aspx*。 

    ![签出和使用 PayPal 的付款添加新项对话框](checkout-and-payment-with-paypal/_static/image3.png)
6. 与前面一样，选择*Site.Master*文件作为主页面。
7. 添加到以下的其他页面*签出*文件夹使用上述相同步骤：   

    - CheckoutReview.aspx
    - CheckoutComplete.aspx
    - CheckoutCancel.aspx
    - CheckoutError.aspx

### <a name="add-a-webconfig-file"></a>添加 Web.config 文件

通过添加一个新*Web.config*的文件*签出*文件夹中，你将能够限制对包含在文件夹中的所有页的访问。

1. 右键单击*签出*文件夹，然后选择**添加** - &gt; **新项**。  
   随即出现“添加新项”对话框。
2. 选择**Visual C#**  - &gt; **Web**在左侧的模板组。 然后，从中间窗格中，选择**Web 配置文件**，接受默认名称*Web.config*，然后选择**添加**。
3. 替换现有的 XML 中的内容*Web.config*具有以下文件：  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. 保存*Web.config*文件。

*Web.config*文件指定的 Web 应用程序的所有未知的用户必须被拒绝访问中包含的页*签出*文件夹。 但是，如果用户已注册了一个帐户，并且用户登录，则它们将是已知的用户并将有权访问中的页面*签出*文件夹。

务必要注意，ASP.NET 配置如下所示层次结构，其中每个*Web.config*文件将配置设置应用到在其所在的文件夹和所有其下的子目录。

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>为项目启用 SSL

 安全套接字层 (SSL) 是定义为允许 Web 服务器和 Web 客户端通过使用加密更安全地通信协议。 如果不使用 SSL，客户端和服务器之间发送的数据是通过物理访问网络的任何人都探查数据包。 此外，多个常见的身份验证方案是不安全通过一般 HTTP。 具体而言，基本身份验证和窗体身份验证发送未加密的凭据。 为确保安全，这些身份验证方案必须使用 SSL。 

1. 在中**解决方案资源管理器**，单击**WingtipToys**项目，然后按**F4**以显示**属性**窗口。
2. 更改**已启用 SSL**到`true`。
3. 复制**SSL URL**以便稍后使用。   
 SSL URL 将为`https://localhost:44300/`除非之前已创建 SSL 网站 （如下所示）。   
    ![项目属性](checkout-and-payment-with-paypal/_static/image4.png)
4. 在中**解决方案资源管理器**，右键单击**WingtipToys**项目，然后单击**属性**。
5. 在左侧选项卡中，单击**Web**。
6. 更改**项目 Url**若要使用**SSL URL**之前保存。   
    ![项目 Web 属性](checkout-and-payment-with-paypal/_static/image5.png)
7. 通过按保存该页**CTRL + S**。
8. 按 Ctrl+F5 运行应用程序。 Visual Studio 将显示一个选项以便您可以避免出现 SSL 警告。
9. 单击**是**以信任 IIS Express SSL 证书并继续。   
    ![IIS Express SSL 证书详细信息](checkout-and-payment-with-paypal/_static/image6.png)  
 将显示安全警告。
10. 单击**是**将证书安装到本地主机。   
    ![安全警告对话框](checkout-and-payment-with-paypal/_static/image7.png)  
 将显示在浏览器窗口。

现在可以轻松地测试 Web 应用程序使用 SSL 在本地。

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>添加 OAuth 2.0 提供程序

ASP.NET Web 窗体提供了增强的成员身份和身份验证的选项。 这些增强功能包括 OAuth。 OAuth 是一种开放协议，允许以一种简单而标准的方法，从 web、 移动和桌面应用程序的安全授权。 ASP.NET Web 窗体模板使用 OAuth 公开 Facebook、 Twitter、 Google 和 Microsoft 作为身份验证提供程序。 虽然本教程仅使用 Google 作为身份验证提供程序，你可以轻松修改代码以使用任何提供程序。 实施其他提供程序的步骤是非常类似于您将看到在本教程中的步骤。

除了身份验证，本教程还将使用角色实施授权。 你添加到这些用户`canEdit`角色将能够更改数据 （创建、 编辑或删除联系人）。

> [!NOTE] 
> 
> Windows Live 应用程序仅接受工作网站的实时 URL，因此不能用于本地网站 URL 测试登录名。


以下步骤将允许您添加 Google 身份验证提供程序。

1. 打开*应用程序\_Start\Startup.Auth.cs*文件。
2. 删除注释字符从`app.UseGoogleAuthentication()`方法以便，该方法如下所示： 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. 导航到[Google 开发人员控制台](https://console.developers.google.com/)。 您还需要在 Google 开发者电子邮件帐户 (gmail.com) 的登录。 如果你没有 Google 帐户，请选择**创建一个帐户**链接。   
   接下来，将看到**Google 开发人员控制台**。   
    ![Google 开发人员控制台](checkout-and-payment-with-paypal/_static/image8.png)
4. 单击**创建项目**按钮，然后输入项目名称和 ID （可以使用默认值）。 然后，单击**协议复选框**并**创建**按钮。  

    ![Google-新建项目](checkout-and-payment-with-paypal/_static/image9.png)

   几秒钟后将创建新项目，并在浏览器将显示新项目页。
5. 在左侧选项卡中，单击**Api&amp;身份验证**，然后单击**凭据**。
6. 单击**创建新的客户端 ID**下**OAuth**。   
   **创建客户端 ID**将显示对话框。   
    ![Google-创建客户端 ID](checkout-and-payment-with-paypal/_static/image10.png)
7. 在中**创建客户端 ID**对话框中，保留默认**Web 应用程序**为应用程序类型。
8. 设置**授权的 JavaScript 来源**之前在本教程中使用的 SSL url (`https://localhost:44300/`除非你已创建其他 SSL 项目)。   
   此 URL 是你的应用程序的原点。 对于此示例，你只需输入 localhost 测试 URL。 但是，可以输入多个 Url 以针对 localhost 和生产。
9. 设置**授权重定向 URI**所示： 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   此值是 URI ASP.NET OAuth 用户与 google OAuth 服务器进行通信。 请记住上面使用的 SSL URL (`https://localhost:44300/`除非你已创建其他 SSL 项目)。
10. 单击**创建客户端 ID**按钮。
11. 在 Google 开发人员控制台的左侧菜单中，单击**许可屏幕**菜单项，然后设置你的电子邮件地址和产品名称。 完成窗体后，单击**保存**。
12. 单击**Api**菜单项、 向下的滚动并单击**off**按钮旁边**Google + API**。   
    接受此选项将启用 Google + API。
13. 您还必须更新**Microsoft.Owin**到版本 3.0.0 的 NuGet 包。   
    从**工具**菜单中，选择**NuGet 包管理器**，然后选择**为解决方案管理 NuGet 包**。  
    从**管理 NuGet 包**窗口中，找到并更新**Microsoft.Owin**到版本 3.0.0 的包。
14. 在 Visual Studio 中，更新`UseGoogleAuthentication`方法*Startup.Auth.cs*页上通过复制和粘贴**客户端 ID**并**客户端机密**到方法。 **客户端 ID**并**客户端机密**如下所示的值是示例，它们不起作用。 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. 按**CTRL + F5**生成并运行应用程序。 单击**登录**链接。
16. 下**使用其他服务进行登录**，单击**Google**。  
    ![登录](checkout-and-payment-with-paypal/_static/image11.png)
17. 如果你需要输入你的凭据，你将重定向到 google 站点将在其中输入你的凭据。  
    ![Google-登录](checkout-and-payment-with-paypal/_static/image12.png)
18. 输入你的凭据后，系统将提示，向您刚创建的 web 应用程序授予权限。  
    ![项目默认服务帐户](checkout-and-payment-with-paypal/_static/image13.png)
19. 单击**接受**。 你将立即重定向回**注册**页**WingtipToys**应用程序可以在其中注册你的 Google 帐户。  
    ![注册你的 Google 帐户](checkout-and-payment-with-paypal/_static/image14.png)
20. 可以选择更改 Gmail 帐户使用的本地电子邮件注册名称，但你通常想要保留的默认电子邮件别名 （即，一个用于身份验证）。 单击**登录**如上所示。

### <a name="modifying-login-functionality"></a>修改登录功能

在本教程系列中先前提到过，很多用户注册功能包含在 ASP.NET Web 窗体模板中默认情况下。 现在，您将修改默认值*Login.aspx*并*Register.aspx*页面调`MigrateCart`方法。 `MigrateCart`方法将新登录的用户与匿名的购物车相关联。 通过将用户相关联并购物车，Wingtip Toys 示例应用程序将能够维护之间访问用户的购物车。

1. 在中**解决方案资源管理器**，找到并打开*帐户*文件夹。
2. 修改代码隐藏页名为*Login.aspx.cs*包括以黄色突出显示的代码，以使其显示，如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. 保存*Login.aspx.cs*文件。

现在，可以忽略没有为定义该警告`MigrateCart`方法。 你将添加它稍后在本教程中。

*Login.aspx.cs*代码隐藏文件支持登录方法。 通过检查 Login.aspx 页面，您将看到此页包括"登录"按钮，当单击触发器`LogIn`上代码隐藏的处理程序。

当`Login`方法*Login.aspx.cs*调用时，名为购物车中的新实例`usersShoppingCart`创建。 已检索到购物车 (GUID) 的 ID 并将其设置为`cartId`变量。 然后，将`MigrateCart`调用方法时，将同时传递`cartId`和登录的用户对此方法的名称。 当迁移购物车时，用于标识匿名购物车的 GUID 替换的用户名称。

还可以修改*Login.aspx.cs*代码隐藏文件来迁移购物车，当用户登录时还必须修改*Register.aspx.cs 代码隐藏文件*迁移购物车当用户创建新帐户并登录。

1. 在中*帐户*文件夹中，打开代码隐藏文件命名为*Register.aspx.cs*。
2. 通过以黄色显示，包括代码修改代码隐藏文件，以使其显示，如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. 保存*Register.aspx.cs*文件。 再次重申，有关忽略该警告`MigrateCart`方法。

请注意，在代码中所用的`CreateUser_Click`事件处理程序中使用的代码非常相似`LogIn`方法。 当用户注册或登录到站点，调用`MigrateCart`方法将发生。

## <a name="migrating-the-shopping-cart"></a>迁移购物车

现在，已更新的登录名和注册过程，您可以添加代码以迁移购物车使用`MigrateCart`方法。

1. 在中**解决方案资源管理器**，找到*逻辑*文件夹，然后打开*ShoppingCartActions.cs*类文件。
2. 添加代码以对现有代码中的黄色突出显示*ShoppingCartActions.cs*文件，以便中的代码*ShoppingCartActions.cs*文件将出现，如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

`MigrateCart`方法使用现有 cartId 来查找用户的购物车。 接下来，代码循环访问所有购物车商品，并将替换`CartId`属性 (如指定的`CartItem`架构) 的登录的用户名称。

### <a name="updating-the-database-connection"></a>正在更新数据库连接

如果您按照本教程使用**预生成**Wingtip Toys 示例应用程序，则必须重新创建默认成员资格数据库。 通过修改默认连接字符串，成员资格数据库创建为的下次运行应用程序。

1. 打开*Web.config*根目录下的项目文件。
2. 更新的默认连接字符串，以使其显示，如下所示：   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>将集成 PayPal

PayPal 是接受付款网上商店通过基于 web 的计费平台。 接下来，本教程介绍如何将 PayPal 的 Express 签出功能集成到你的应用程序。 快速签出，客户可使用 PayPal 支付他们添加到购物车的项。

### <a name="create-paylpal-test-accounts"></a>创建 PaylPal 测试帐户

若要使用 PayPal 测试环境，必须创建并验证开发人员测试帐户。 开发人员测试帐户将用于创建购买者测试帐户和卖方测试帐户。 开发人员测试帐户凭据还将允许 Wingtip Toys 示例应用程序访问 PayPal 测试环境。

1. 在浏览器中，导航到 PayPal 开发人员测试站点：   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. 如果您没有 PayPal 开发人员帐户，通过单击创建新的帐户**注册**并按照步骤注册。 如果你有现有的 PayPal 开发人员帐户，单击登录**日志中**。 你将需要你 PayPal 的开发人员帐户来测试本教程后面的 Wingtip Toys 示例应用程序。
3. 如果您只需为 PayPal 开发人员帐户注册，可能需要验证你使用 PayPal 的 PayPal 开发人员帐户。 可以通过 PayPal 发送到电子邮件帐户的步骤来验证你的帐户。 验证你 PayPal 的开发人员帐户后，请重新登录到 PayPal 开发人员测试站点。
4. 您需要创建一个 PayPal buyer 测试帐户，如果已没有 PayPal 开发者帐户登录到 PayPal 开发人员站点后有一个。 若要创建购买者测试帐户，在 PayPal 网站，请单击**应用程序**选项卡，然后单击**沙盒帐户**。   
 **沙盒测试帐户**页所示。   

    > [!NOTE] 
    > 
    > PayPal 开发人员网站已经提供了一个商家测试帐户。

    ![签出和使用 PayPal 的沙盒测试帐户付款](checkout-and-payment-with-paypal/_static/image15.png)
5. 在沙盒测试的帐户页上，单击**创建帐户**。
6. 上**创建测试帐户**页上选择是购买者测试帐户电子邮件和你选择的密码。   

    > [!NOTE] 
    > 
    > 你将需要购买者电子邮件地址和密码以测试本教程末尾的 Wingtip Toys 示例应用程序。

    ![签出和使用 PayPal 的沙盒测试帐户付款](checkout-and-payment-with-paypal/_static/image16.png)
7. 通过单击创建购买者测试帐户**创建帐户**按钮。  
 **沙盒测试帐户**显示页。 

    ![签出和使用 PayPal-PaylPal 帐户付款](checkout-and-payment-with-paypal/_static/image17.png)
8. 上**沙盒测试帐户**页上，单击**主持人**电子邮件帐户。  
    **配置文件**并**通知**显示选项。
9. 选择**配置文件**选项，然后单击**API 凭据**若要查看 API 商家测试帐户的凭据。
10. 将测试 API 凭据复制到记事本。

您需要显示经典测试 API 凭据 （用户名、 密码和签名） 进行 API 调用从 Wingtip Toys 示例应用程序测试环境 PayPal。 您将在下一步中添加凭据。

### <a name="add-paypal-class-and-api-credentials"></a>添加 PayPal 类和 API 凭据

会将大部分 PayPal 代码到单个类。 此类包含用于与 PayPal 进行通信的方法。 此外，您将向此类添加 PayPal 凭据。

1. 在 Visual Studio 中 Wingtip Toys 示例应用程序中，右键单击**逻辑**文件夹，然后选择**添加** - &gt; **新项**。   
   随即出现“添加新项”对话框。
2. 下**Visual C#** 从**已安装**左侧窗格中，选择**代码**。
3. 在中间窗格中，选择**类**。 此新类命名**PayPalFunctions.cs**。
4. 单击 **添加**。  
   在编辑器中显示新类文件中。
5. 默认代码替换为以下代码：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. 添加，以便能够进行函数调用到 PayPal 测试环境显示在本教程前面的商户 API 凭据 （用户名、 密码和签名）。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> 在此示例应用程序都只需将凭据添加到 C# 文件 (.cs)。 但是，在实施解决方案，应考虑加密你的配置文件中的凭据。


NVPAPICaller 类包含大多数 PayPal 功能。 类中的代码提供了进行一次测试从 PayPal 测试环境购买所需的方法。 以下三个 PayPal 函数用于进行购买：

- `SetExpressCheckout` 函数
- `GetExpressCheckoutDetails` 函数
- `DoExpressCheckoutPayment` 函数

`ShortcutExpressCheckout`方法从购物车和调用收集测试采购信息和产品详细信息`SetExpressCheckout`PayPal 函数。 `GetCheckoutDetails`方法确认采购详细信息，并调用`GetExpressCheckoutDetails`PayPal 函数进行测试购买之前。 `DoCheckoutPayment`方法通过调用来完成测试环境中的测试购买`DoExpressCheckoutPayment`PayPal 函数。 剩余代码支持的 PayPal 方法和过程，如编码字符串、 解码字符串、 数组、 处理和确定凭据。

> [!NOTE] 
> 
> PayPal 可以包括可选采购详细信息，根据[PayPal 的 API 规范](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)。 通过扩展 Wingtip Toys 示例应用程序中的代码，可以包括本地化的详细信息、 产品说明、 税务、 客户服务电话号码，以及许多其他可选字段。


请注意，将返回并取消 Url 中指定的**ShortcutExpressCheckout**方法使用的端口号。

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

Visual Web Developer 运行时使用 SSL 的 web 项目，通常端口 44300 用于 web 服务器。 如上所示，端口号是 44300。 当您运行该应用程序时，可以看到不同的端口号。 本教程结束时，端口号必须正确设置代码中，以便可以成功运行 Wingtip Toys 示例应用程序。 本教程的下一节介绍了如何检索本地主机端口号和更新 PayPal 类。

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>更新 PayPal 类中的 LocalHost 端口号

Wingtip Toys 示例应用程序通过导航到 PayPal 测试站点，并返回到 Wingtip Toys 示例应用程序的本地实例购买产品。 若要有 PayPal 返回到正确的 URL，需要指定的端口号的本地运行示例应用程序中上面提到的 PayPal 代码。

1. 右键单击项目名称 (**WingtipToys**) 中**解决方案资源管理器**，然后选择**属性**。
2. 在左侧列中，选择**Web**选项卡。
3. 检索中的端口号**项目 Url**框。
4. 如果需要更新`returnURL`并`cancelURL`PayPal 类中 (`NVPAPICaller`) 中*PayPalFunctions.cs*文件以使用 web 应用程序的端口号：   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

现在已添加的代码将与本地 Web 应用程序的预期的端口匹配。 PayPal 将能够在本地计算机上返回到正确的 URL。

### <a name="add-the-paypal-checkout-button"></a>添加 PayPal 签出按钮

现在，主要的 PayPal 功能已添加到示例应用程序，您可以开始添加标记和调用这些函数所需的代码。 首先，必须添加该用户将看到购物车页的签出按钮。

1. 打开*ShoppingCart.aspx*文件。
2. 滚动到文件的底部，找到`<!--Checkout Placeholder -->`注释。
3. 替换与注释`ImageButton`控件，以便注册的标记替换，如下所示：  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. 在中*ShoppingCart.aspx.cs*文件，之后`UpdateBtn_Click`事件处理程序中的该文件末尾附近添加`CheckOutBtn_Click`事件处理程序：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. 另外，请在*ShoppingCart.aspx.cs*文件中，添加对引用`CheckoutBtn`，以便引用新的图像按钮，如下所示：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. 将所做的更改保存到这两*ShoppingCart.aspx*文件并*ShoppingCart.aspx.cs*文件。
7. 从菜单中选择**调试**-&gt;**生成 WingtipToys**。  
   将重新生成该项目与新添加**ImageButton**控件。

### <a name="send-purchase-details-to-paypal"></a>将采购详细信息发送到 PayPal

当用户单击**签出**购物车页上的按钮 (*ShoppingCart.aspx*)，它们将开始购买过程。 下面的代码调用购买产品所需的第一个 PayPal 函数。

1. 从*签出*文件夹中，打开代码隐藏文件命名为*CheckoutStart.aspx.cs*。   
   请确保打开代码隐藏文件。
2. 将现有代码替换为以下代码：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

当应用程序的用户单击**签出**按钮在购物车页上，浏览器将导航到*CheckoutStart.aspx*页。 当*CheckoutStart.aspx*页上的负载，`ShortcutExpressCheckout`调用方法。 此时，用户会传输到 PayPal 测试 web 站点。 PayPal 站点上用户输入其 PayPal 凭据、 查看购买详细信息，接受 PayPal 协议并返回到 Wingtip Toys 示例应用程序在其中`ShortcutExpressCheckout`方法完成。 当`ShortcutExpressCheckout`方法完成后，它会为用户重定向*CheckoutReview.aspx*页中指定`ShortcutExpressCheckout`方法。 这允许用户查看订单详细信息从 Wingtip Toys 示例应用程序中。

### <a name="review-order-details"></a>查看订单详细信息

从 PayPal、 返回之后*CheckoutReview.aspx* Wingtip Toys 示例应用程序中的页显示订单详细信息。 此页面允许用户在购买产品前应查看订单详细信息。 *CheckoutReview.aspx*必须按如下所示创建页：

1. 在中*签出*文件夹中，打开名为页*CheckoutReview.aspx*。
2. 使用以下内容替换现有标记：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. 打开名为的代码隐藏页*CheckoutReview.aspx.cs*和现有代码替换为以下：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

**DetailsView**控件用于显示尚未从 PayPal 返回的订单详细信息。 此外，上面的代码将订单详细信息保存到 Wingtip Toys 数据库作为`OrderDetail`对象。 当用户单击**Complete Order**按钮，将被重定向到*CheckoutComplete.aspx*页。

> [!NOTE] 
> 
> **提示**
> 
> 中的标记*CheckoutReview.aspx*页上，注意`<ItemStyle>`标记用于更改中的项的样式**DetailsView**靠近页面底部的控件。 通过查看中的页**设计视图**(通过选择**设计**在 Visual Studio 左下角)，然后选择**DetailsView**控件，然后选择**智能标记**(在顶部的箭头图标右侧的控件)，你将能够看到**DetailsView 任务**。
> 
> ![签出和使用 PayPal 的付款编辑字段](checkout-and-payment-with-paypal/_static/image18.png)
> 
> 通过选择**编辑字段**，则**字段**对话框将出现。 在此对话框中，可以轻松控制的可视属性，如**ItemStyle**的**DetailsView**控件。
> 
> ![签出和付款使用 PayPal 的字段对话框](checkout-and-payment-with-paypal/_static/image19.png)


### <a name="complete-purchase"></a>完成购买

*CheckoutComplete.aspx*页从 PayPal 进行购买。 如上所述，用户必须单击**Complete Order**按钮之前应用程序将导航到*CheckoutComplete.aspx*页。

1. 在中*签出*文件夹中，打开名为页*CheckoutComplete.aspx*。
2. 使用以下内容替换现有标记：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. 打开名为的代码隐藏页*CheckoutComplete.aspx.cs*和现有代码替换为以下：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

当*CheckoutComplete.aspx*加载页面时，`DoCheckoutPayment`调用方法。 如前文所述，`DoCheckoutPayment`方法完成从 PayPal 测试环境购买。 PayPal 完成订单的采购*CheckoutComplete.aspx*页上显示的付款事务`ID`到购买者。

### <a name="handle-cancel-purchase"></a>句柄取消购买

如果用户决定取消购买，它们将会转向*CheckoutCancel.aspx*页上，他们将看到已取消其顺序。

1. 打开名为的页*CheckoutCancel.aspx*中*签出*文件夹。
2. 使用以下内容替换现有标记：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>处理购买错误

在购买过程中的错误将由*CheckoutError.aspx*页。 代码隐藏*CheckoutStart.aspx*页上， *CheckoutReview.aspx*页上，并且*CheckoutComplete.aspx*页面将每个重定向到*CheckoutError.aspx*页上，如果发生错误。

1. 打开名为的页*CheckoutError.aspx*中*签出*文件夹。
2. 使用以下内容替换现有标记：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

*CheckoutError.aspx*签出过程中发生错误会显示包含错误详细信息页面。

## <a name="running-the-application"></a>运行应用程序

运行应用程序若要了解如何购买产品。 请注意，你将在运行中 PayPal 测试环境。 要交换没有实际的资金。

1. 请确保所有文件保存在 Visual Studio。
2. 打开 Web 浏览器并导航到[ https://developer.paypal.com ](https://developer.paypal.com/)。
3. 使用你在本教程前面创建的 PayPal 开发人员帐户登录。  
   对于 PayPal 的开发人员沙箱，您需要在登录[ https://developer.paypal.com ](https://developer.paypal.com/)测试快速签出。 这仅适用于 PayPal 的沙盒测试，不适用于 PayPal 的实时环境。
4. 在 Visual Studio 中，按**F5**运行 Wingtip Toys 示例应用程序。  
   重新生成数据库后，浏览器将打开并显示*Default.aspx*页。
5. 通过选择产品类别，例如"汽车"，然后单击将三个不同的产品添加到购物车**添加到购物车**旁边的每个产品。  
   购物车将显示所选的产品。
6. 单击**PayPal**签出的按钮。 

    ![签出和使用 PayPal 的付款放入购物车](checkout-and-payment-with-paypal/_static/image20.png)

   正在签出将要求您具有 Wingtip Toys 示例应用程序的用户帐户。
7. 单击**Google**在能够使用现有的 gmail.com 电子邮件帐户进行登录页的右侧的链接。  
   如果还没有 gmail.com 帐户，可以创建一个用于测试目的[www.gmail.com](https://www.gmail.com/)。 此外可以通过单击"注册"使用标准的本地帐户。 

    ![签出和付款使用 PayPal-登录](checkout-and-payment-with-paypal/_static/image21.png)
8. 使用你的 gmail 帐户和密码登录。 

    ![签出和使用 PayPal 的 Gmail 登录付款](checkout-and-payment-with-paypal/_static/image22.png)
9. 单击**登录**按钮以注册你的 gmail 帐户与您 Wingtip Toys 示例应用程序的用户名称。 

    ![签出和使用 PayPal 的注册帐户付款](checkout-and-payment-with-paypal/_static/image23.png)
10. PayPal 测试站点，添加你**buyer**电子邮件地址和在本教程前面创建的密码，然后单击**Log In**按钮。 

    ![签出和使用 PayPal 的 PayPal 登录付款](checkout-and-payment-with-paypal/_static/image24.png)
11. 同意 PayPal 策略，单击**同意并继续**按钮。  
    请注意，此页仅显示第一次使用此 PayPal 帐户。 再次请注意，这是一个测试帐户，交换任何真实的货币交易。 

    ![签出和 PayPal-PayPal 策略与付款](checkout-and-payment-with-paypal/_static/image25.png)
12. 查看订单信息在测试环境查看页并单击 PayPal**继续**。 

    ![签出和付款使用 PayPal-查看信息](checkout-and-payment-with-paypal/_static/image26.png)
13. 上*CheckoutReview.aspx*页上，验证订单金额并查看生成的寄送地址。 然后，单击**Complete Order**按钮。 

    ![签出和使用 PayPal 的顺序查看付款](checkout-and-payment-with-paypal/_static/image27.png)
14. **CheckoutComplete.aspx**页将显示的付款事务 id。 

    ![签出和使用 PayPal-签出完整的付款](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>查看数据库

通过运行应用程序后查看 Wingtip Toys 示例应用程序数据库中更新后的数据，可以看到该应用程序已成功记录在购买的产品。

您可以检查中包含的数据*Wingtiptoys.mdf*使用的数据库文件**数据库资源管理器**窗口 (**服务器资源管理器**Visual Studio 窗口中的) 一样前面在本系列教程。

1. 如果仍打开，请关闭浏览器窗口。
2. 在 Visual Studio 中，选择**显示所有文件**顶部的图标**解决方案资源管理器**来，你可以展开**应用\_数据**文件夹。
3. 展开**应用程序\_数据**文件夹。  
 可能需要选择**显示所有文件**的文件夹图标。
4. 右键单击*Wingtiptoys.mdf*数据库文件，然后选择**打开**。  
    **服务器资源管理器**显示。
5. 展开**表**文件夹。
6. 右键单击**订单**表，然后选择**显示表数据**。  
 **订单**显示表。
7. 审阅**PaymentTransactionID**列以确认成功的事务。 

    ![签出和使用 PayPal-查看数据库的付款](checkout-and-payment-with-paypal/_static/image29.png)
8. 关闭**订单**表窗口。
9. 在服务器资源管理器中右键单击**OrderDetails**表，然后选择**显示表数据**。
10. 审阅`OrderId`并`Username`中的值**OrderDetails**表。 请注意，这些值与匹配`OrderId`并`Username`中包含的值**订单**表。
11. 关闭**OrderDetails**表窗口。
12. 右键单击 Wingtip Toys 数据库文件 (*Wingtiptoys.mdf*)，然后选择**关闭连接**。
13. 如果没有看到**解决方案资源管理器**窗口中，单击**解决方案资源管理器**底部**服务器资源管理器**窗口以显示**解决方案资源管理器**试。

## <a name="summary"></a>总结

在本教程中添加订单和订单详细信息架构来跟踪在购买的产品。 您还集成 PayPal 功能到 Wingtip Toys 示例应用程序。

## <a name="additional-resources"></a>其他资源

[ASP.NET 配置概述](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[包含成员资格、 OAuth 和 SQL 数据库的安全的 ASP.NET Web 窗体应用部署到 Azure 应用服务](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure-免费试用版](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>免责声明

本教程包含示例代码。 此类的示例代码"按原样"提供，而无需任何种类的担保。 相应地，Microsoft 不保证准确性、 完整性或示例代码的质量。 你同意的示例代码使用您自己承担。 在任何情况下下，Microsoft 对给您以任何方式的内容，包括但不是限于任何错误或遗漏的任何示例代码、 内容，或任何丢失或损坏产生的任何示例代码使用任何任何的类型示例代码。 在此通知并据此同意进行赔偿、 保存 Microsoft 使从和针对所有丢失、 丢失、 受伤或任何的损坏类型的包括但不限于，那些由 occasioned 或因其他营销材料都在发布时，声明传输、 使用或依赖于包括但不是限于表示其中的视图。

> [!div class="step-by-step"]
> [上一页](shopping-cart.md)
> [下一页](membership-and-administration.md)
