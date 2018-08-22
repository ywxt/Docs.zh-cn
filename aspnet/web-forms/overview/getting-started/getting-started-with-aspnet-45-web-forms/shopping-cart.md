---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: 购物车 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: 2823970144e6dce4a3a9f4d28dabfabe9fe053d6
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825079"
---
<a name="shopping-cart"></a>购物车
====================
通过[Erik Reitan](https://github.com/Erikre)

[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。 Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。


本教程介绍将购物车添加到 Wingtip Toys 示例 ASP.NET Web 窗体应用程序所需的业务逻辑。 本教程基于上一教程"显示数据的项和详细信息"，而是 Wingtip Toy 存储教程系列的一部分。 完成本教程后，对示例应用的用户将能够添加、 删除和修改在其购物车中的产品。

## <a name="what-youll-learn"></a>你将学习：

1. 如何创建 web 应用程序的购物车。
2. 如何使用户能够将项添加到购物车。
3. How to add [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction)控件来显示购物车详细信息。
4. 如何计算和显示订单总计。
5. 如何删除和更新购物车中的项目。
6. 如何包括购物车计数器。

## <a name="code-features-in-this-tutorial"></a>在本教程中的代码功能：

1. 实体框架代码优先
2. 数据注释
3. 强类型数据控件
4. 模型绑定

## <a name="creating-a-shopping-cart"></a>创建购物车

前面在本系列教程，您可以添加页面和代码，以查看数据库中的产品数据。 在本教程中，你将创建购物车管理产品的用户有兴趣购买。 用户将能够浏览并将项添加到购物车，即使它们未注册或登录。 若要管理购物车访问，你会将用户分配一个唯一`ID`首次使用全局唯一标识符 (GUID)，当用户访问购物车。 将存储此`ID`使用 ASP.NET 会话状态。

> [!NOTE] 
> 
> ASP.NET 会话状态是很方便地存储在用户离开站点将到期的特定于用户的信息。 虽然不恰当使用会话状态的可能较大的站点上会影响性能，打造出色会话状态适用于演示目的的使用。 Wingtip Toys 示例项目演示如何使用会话状态而无需外部提供程序，其中会话状态是存储的进程内托管站点的 web 服务器上。 提供应用程序的多个实例的大型站点或不同服务器运行的应用程序的多个实例的站点，请考虑使用**Windows Azure 缓存服务**。 此缓存服务提供的分布式缓存服务的外部 web 站点且解决了使用进程内会话状态的问题。 有关详细信息，请参阅[如何将 ASP.NET 会话状态与 Windows Azure Web Sites](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider)。


### <a name="add-cartitem-as-a-model-class"></a>将 CartItem 添加为 Model 类

通过创建在本系列教程的前面定义的类别和产品数据的架构`Category`并`Product`中的类*模型*文件夹。 现在，添加了新类来定义购物车的架构。 稍后在本教程中，你将添加用于处理对数据访问类`CartItem`表。 此类将提供用于添加、 删除和更新购物车中的项目的业务逻辑。

1. 右键单击*模型*文件夹，然后选择**添加** - &gt; **新项**。 

    ![购物车-新项](shopping-cart/_static/image1.png)
2. 随即出现“添加新项”对话框。 选择**代码**，然后选择**类**。 

    ![购物车中的添加新项对话框](shopping-cart/_static/image2.png)
3. 此新类命名*CartItem.cs*。
4. 单击 **添加**。  
   在编辑器中显示新类文件中。
5. 默认代码替换为以下代码：   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

`CartItem`类包含将定义每个用户添加到购物车产品的架构。 此类是类似于您在本系列教程前面创建的其他架构类。 按照约定，Entity Framework Code First 期望的主键`CartItem`表将`CartItemId`或`ID`。 但是，代码将使用数据批注覆盖默认行为`[Key]`属性。 `Key` ItemId 属性特性指定`ItemID`属性是主键。

`CartId`属性指定`ID`与要购买的项相关联的用户。 将添加代码以创建此用户`ID`当用户访问购物车。 这`ID`也将存储为 ASP.NET 会话变量。

### <a name="update-the-product-context"></a>更新产品上下文

除了添加`CartItem`类，您将需要更新数据库上下文类，管理的实体类并提供对数据库的数据访问。 若要执行此操作，您将添加新创建`CartItem`模型类到`ProductContext`类。

1. 在中**解决方案资源管理器**，找到并打开*ProductContext.cs*文件中*模型*文件夹。
2. 添加到突出显示的代码*ProductContext.cs*文件，如下所示：  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

如以前在此教程系列中的代码中所述*ProductContext.cs*文件将添加`System.Data.Entity`命名空间，以便有权访问的实体框架的所有核心功能。 此功能包括查询、 插入、 更新和删除通过使用强类型化对象数据的功能。 `ProductContext`类将访问权限添加到新添加`CartItem`的模型。

### <a name="managing-the-shopping-cart-business-logic"></a>管理购物车业务逻辑

接下来，将创建`ShoppingCart`中的新类*逻辑*文件夹。 `ShoppingCart`类处理的数据访问`CartItem`表。 类还将包括业务逻辑，可添加、 删除和更新购物车中的项。

您将添加的购物车逻辑将包含的功能来管理以下操作：

1. 将项添加到购物车
2. 从购物车中删除项
3. 获取购物车 ID
4. 正在从购物车检索项目
5. 合计购物车商品的量
6. 正在更新购物车数据

购物车页 (*ShoppingCart.aspx*) 并且将一起使用的购物车类来访问购物车数据。 购物车页将显示用户将添加到购物车的所有项。 除了购物车页和类，你将创建一个页 (*AddToCart.aspx*) 若要将产品添加到购物车。 您还将添加到代码*ProductList.aspx*页和*ProductDetails.aspx*将提供一个指向页*AddToCart.aspx*页上，以便用户可以添加放入购物车产品。

下图显示了当用户将产品添加到购物车时出现的基本过程。

![购物车-将添加到购物车](shopping-cart/_static/image3.png)

当用户单击**添加到购物车**任一链接*ProductList.aspx*页或*ProductDetails.aspx*页上，应用程序将导航到*AddToCart.aspx*页，然后自动向*ShoppingCart.aspx*页。 *AddToCart.aspx*页将购物车类中调用方法来向购物车添加选择产品。 *ShoppingCart.aspx*页将显示已添加到购物车的产品。

#### <a name="creating-the-shopping-cart-class"></a>创建购物车类

`ShoppingCart`类将添加到应用程序中单独的文件夹，以便将模型 （模型文件夹）、 页面 （根文件夹） 和逻辑 （逻辑文件夹） 之间的明显区别。

1. 在中**解决方案资源管理器**，右键单击**WingtipToys**项目，然后选择**添加**-&gt;**新文件夹**. 将新文件夹命名*逻辑*。
2. 右键单击*逻辑*文件夹，然后选择**添加** - &gt; **新项**。
3. 添加名为的新类文件*ShoppingCartActions.cs*。
4. 默认代码替换为以下代码：   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

`AddToCart`方法使单个产品要基于的产品在购物车包含`ID`。 产品添加到购物车中，或如果购物车已包含该产品的项，递增数量。

`GetCartId`方法返回在购物车`ID`用户。 购物车`ID`用于跟踪用户已在其购物车中的项。 如果用户不具有现有购物车`ID`，新车`ID`为其创建。 如果用户作为已注册用户，在购物车登录`ID`设置为其用户名称。 但是，如果用户未登录，在购物车`ID`设置为唯一值 (GUID)。 GUID 可确保为每个用户，基于在会话上创建该只有一个购物车。

`GetCartItems`方法返回的购物车商品的用户列表。 稍后在本教程中，你将看到模型绑定用于显示购物车使用中的购物车项`GetCartItems`方法。

### <a name="creating-the-add-to-cart-functionality"></a>创建到车添加功能

前面曾提到，您将创建一个名为处理页*AddToCart.aspx*将用于将新产品添加到用户的购物车。 此页将调用`AddToCart`中的方法`ShoppingCart`刚创建的类。 *AddToCart.aspx*页将期望的产品`ID`传递给它。 此产品`ID`调用时将使用`AddToCart`中的方法`ShoppingCart`类。

> [!NOTE] 
> 
> 您将修改代码隐藏 (*AddToCart.aspx.cs*) 的此页上，不是在页面 UI (*AddToCart.aspx*)。


#### <a name="to-create-the-add-to-cart-functionality"></a>若要创建添加车功能：

1. 在中**解决方案资源管理器**，右键单击**WingtipToys**项目，然后单击**添加** - &gt; **新项**。  
   随即出现“添加新项”对话框。
2. 将标准的新页 （Web 窗体） 添加到名为应用程序*AddToCart.aspx*。 

    ![购物车-添加 Web 窗体](shopping-cart/_static/image4.png)
3. 在中**解决方案资源管理器**，右键单击*AddToCart.aspx*页，然后单击**查看代码**。 *AddToCart.aspx.cs*在编辑器中打开代码隐藏文件。
4. 中的现有代码替换*AddToCart.aspx.cs*以下的代码隐藏：   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

当*AddToCart.aspx*加载页面时，该产品`ID`检索查询字符串中。 接下来，创建购物车类的实例并用于调用`AddToCart`在本教程前面部分添加的方法。 `AddToCart`中包含的方法*ShoppingCartActions.cs*文件中，包括逻辑，用于将所选的产品添加到购物车或递增的所选产品的产品数量。 如果尚未添加到购物车产品，产品添加到`CartItem`数据库表。 如果已添加到购物车产品，用户将添加同一产品的其他项中递增的产品数量`CartItem`表。 最后，页面将重定向回到*ShoppingCart.aspx*将添加下一步，其中用户会看到在购物车中的项的更新的列表中的页。

如前面所述，用户`ID`用于标识与特定用户关联的产品。 这`ID`添加到中的行`CartItem`表每次用户将产品添加到购物车。

### <a name="creating-the-shopping-cart-ui"></a>创建购物车 UI

*ShoppingCart.aspx*页将显示用户添加到购物车的产品。 它还将提供添加、 删除和更新购物车中的项的功能。

1. 在中**解决方案资源管理器**，右键单击**WingtipToys**，单击**添加** - &gt; **新项**。  
   随即出现“添加新项”对话框。
2. 添加新页面 （Web 窗体），通过选择包含一个母版页**使用母版页的 Web 窗体**。 命名新页面*ShoppingCart.aspx*。
3. 选择**Site.Master**附加到新创建的母版页 *.aspx*页。
4. 在中*ShoppingCart.aspx*页上，将现有标记替换为以下标记：   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

*ShoppingCart.aspx*页包含**GridView**控件命名为`CartList`。 此控件使用模型绑定将购物车数据绑定到数据库中**GridView**控件。 当您将设置`ItemType`的属性**GridView**控件，数据绑定表达式`Item`现已推出将成为强类型化的控件和控件的标记。 如本系列教程前面所述，可以选择的详细信息`Item`对象使用 IntelliSense。 若要配置数据控件，以使用模型绑定选择数据，请设置`SelectMethod`控件的属性。 在上面的标记中，您设置`SelectMethod`若要使用 GetShoppingCartItems 方法可返回一系列`CartItem`对象。 **GridView**数据控件在页生命周期中的适当时间调用方法，并自动将绑定返回的数据。 `GetShoppingCartItems`仍将添加的方法。

#### <a name="retrieving-the-shopping-cart-items"></a>检索购物车商品

接下来，您将代码添加到*ShoppingCart.aspx.cs*隐藏代码检索并填充购物车 UI。

1. 在中**解决方案资源管理器**，右键单击*ShoppingCart.aspx*页，然后单击**查看代码**。 *ShoppingCart.aspx.cs*在编辑器中打开代码隐藏文件。
2. 将现有代码替换为以下代码：  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

如前面所述`GridView`数据控件调用`GetShoppingCartItems`方法在适当的时间在页生命周期并自动将绑定返回的数据。 `GetShoppingCartItems`方法创建的一个实例`ShoppingCartActions`对象。 然后，代码使用该实例在购物车中返回的项，通过调用`GetCartItems`方法。

### <a name="adding-products-to-the-shopping-cart"></a>将产品添加到购物车

当任一*ProductList.aspx*或*ProductDetails.aspx*显示页面，用户将能够将产品添加到购物车使用的链接。 当他们单击链接时，该应用程序导航到名为处理页面*AddToCart.aspx*。 *AddToCart.aspx*页将调用`AddToCart`中的方法`ShoppingCart`在本教程前面部分添加的类。

现在，您将添加**添加到购物车**指向同时*ProductList.aspx*页并*ProductDetails.aspx*页。 此链接将包括该产品`ID`从数据库中检索的。

1. 在中**解决方案资源管理器**，找到并打开名为的页*ProductList.aspx*。
2. 添加到的黄色突出显示的标记*ProductList.aspx*页上，以便整个页面显示，如下所示：  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a>测试购物车

运行应用程序，请参阅如何将产品添加到购物车。

1. 按 **F5** 运行该应用程序。  
 项目重新创建数据库后，浏览器将打开并显示*Default.aspx*页。
2. 选择**汽车**类别导航菜单中。  
 *ProductList.aspx*显示仅"Cars"类别中包含的产品显示页。 

    ![购物车的汽车](shopping-cart/_static/image5.png)
3. 单击**添加到购物车**链接旁边的第一个产品列出 (转换 car)。   
 *ShoppingCart.aspx*显示页面时，在您的购物车中显示所选内容。 

    ![购物车的购物车](shopping-cart/_static/image6.png)
4. 选择查看其他产品**平面**类别导航菜单中。
5. 单击**添加到购物车**旁边列出的第一个产品的链接。  
 *ShoppingCart.aspx*页显示与其他项。
6. 关闭浏览器。

### <a name="calculating-and-displaying-the-order-total"></a>计算和显示订单总计

除了将产品添加到购物车中，您将添加`GetTotal`方法`ShoppingCart`类，并在购物车页中显示订单总金额。

1. 在中**解决方案资源管理器**，打开*ShoppingCartActions.cs*文件中*逻辑*文件夹。
2. 添加以下`GetTotal`方法用到的黄色突出显示`ShoppingCart`类，以便此类显示，如下所示：   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

首先，`GetTotal`方法获取用户的购物车中的 ID。 然后该方法获取购物车总数乘以每个产品在购物车中列出的产品数量的产品价格。

> [!NOTE] 
> 
> 上面的代码中使用可以为 null 的类型"`int?`"。 可以为 null 的类型可以表示为基础类型的也以 null 值的所有值。 有关详细信息，请参阅[使用可以为 Null 的类型](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx)。


### <a name="modify-the-shopping-cart-display"></a>修改购物车显示

接下来将修改的代码*ShoppingCart.aspx*页面以调`GetTotal`方法，并显示总*ShoppingCart.aspx*页上加载页面时。

1. 在中**解决方案资源管理器**，右键单击*ShoppingCart.aspx*页，然后选择**查看代码**。
2. 在中*ShoppingCart.aspx.cs*文件中，更新`Page_Load`通过添加以下代码以黄色突出显示的处理程序：   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

当*ShoppingCart.aspx*加载页面，它将加载购物车对象，然后通过调用中检索的购物车总额`GetTotal`方法的`ShoppingCart`类。 购物车是否为空，该结果被显示消息。

### <a name="testing-the-shopping-cart-total"></a>测试的购物车总额

运行应用程序现在，请参阅如何您可以不只将产品加入购物车，但您可以看到购物车总额。

1. 按 **F5** 运行该应用程序。  
 在浏览器将打开并显示*Default.aspx*页。
2. 选择**汽车**类别导航菜单中。
3. 单击**添加到购物车**旁边的第一个产品的链接。   
 *ShoppingCart.aspx*页中显示订单总计。 

    ![购物车的购物车总计](shopping-cart/_static/image7.png)
4. 将一些其他产品 （例如，平面） 添加到购物车。
5. *ShoppingCart.aspx*页中显示已添加的所有产品更新的总数。 

    ![购物车的多个产品](shopping-cart/_static/image8.png)
6. 通过关闭浏览器窗口中停止正在运行的应用。

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a>将更新和签出按钮添加到购物车

若要允许用户修改购物车，你将添加**更新**按钮和一个**签出**购物车页的按钮。 **签出**直到更高版本中本系列教程不使用按钮。

1. 在中**解决方案资源管理器**，打开*ShoppingCart.aspx* web 应用程序项目的根目录中的页。
2. 若要添加**更新**按钮并**签出**按钮*ShoppingCart.aspx*页上，添加到的现有标记的黄色突出显示的标记，如中所示以下代码：   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

当用户单击**更新**按钮，`UpdateBtn_Click`将调用事件处理程序。 此事件处理程序将调用将在下一步添加的代码。

接下来，你可以更新中包含的代码*ShoppingCart.aspx.cs*文件，以遍历车商品并调用`RemoveItem`和`UpdateItem`方法。

1. 在中**解决方案资源管理器**，打开*ShoppingCart.aspx.cs* web 应用程序项目的根目录中的文件。
2. 添加以下代码部分用到的黄色突出显示*ShoppingCart.aspx.cs*文件：   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

当用户单击**更新**按钮*ShoppingCart.aspx*页上，调用 UpdateCartItems 方法。 UpdateCartItems 方法获取在购物车中的每个项的更新的值。 然后，UpdateCartItems 方法调用`UpdateShoppingCartDatabase`方法 （添加和下一步中所述） 以添加或从购物车中删除项目。 更新数据库以反映放入购物车中，更新后**GridView**购物车页上通过调用更新控件`DataBind`方法**GridView**。 此外，订单总金额购物车页上的将更新以反映更新的项列表。

### <a name="updating-and-removing-shopping-cart-items"></a>更新和删除购物车商品

上*ShoppingCart.aspx*页中，可以看到已添加控件更新项的数量和删除项。 现在，添加将使处理这些控件的代码。

1. 在中**解决方案资源管理器**，打开*ShoppingCartActions.cs*文件中*逻辑*文件夹。
2. 添加以下代码以到黄色突出显示*ShoppingCartActions.cs*类文件：   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

`UpdateShoppingCartDatabase`方法，从调用`UpdateCartItems`方法*ShoppingCart.aspx.cs*页上，包含用于更新或从购物车中删除项目的逻辑。 `UpdateShoppingCartDatabase`方法循环访问购物车列表中的所有行。 如果已标记的购物车项被删除，或者数量为小于 1，`RemoveItem`调用方法。 否则，购物车项检查的更新时`UpdateItem`调用方法。 已删除或更新购物车项后，在保存数据库更改。

`ShoppingCartUpdates`结构用来保存所有购物车商品。 `UpdateShoppingCartDatabase`方法使用`ShoppingCartUpdates`结构，以确定任何一项需要更新或删除。

在下一步的教程中，您将使用`EmptyCart`方法清除购物车后购买产品。 但现在，您将使用`GetCount`刚添加到方法*ShoppingCartActions.cs*文件以确定购物车中有多少项。

### <a name="adding-a-shopping-cart-counter"></a>添加购物车计数器

若要允许用户查看购物车中的项总数，您将添加到计数器*Site.Master*页。 此计数器也将作为放入购物车的链接。

1. 在中**解决方案资源管理器**，打开*Site.Master*页。
2. 通过添加购物车计数器链接，因此，它按如下所示显示黄色再到导航部分中所示修改标记：  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. 接下来，更新的代码隐藏*Site.Master.cs*文件添加，如下所示以黄色突出显示的代码：  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

页面呈现为 HTML 之前,`Page_PreRender`引发事件。 在中`Page_PreRender`处理程序，购物车的总计数由调用`GetCount`方法。 返回的值添加到`cartCount`的标记中包含的跨度*Site.Master*页。 `<span>`标记使要正确呈现的内部元素。 该站点的任何页显示时，将显示购物车总额。 用户还可以单击以显示购物车的购物车总额。

## <a name="testing-the-completed-shopping-cart"></a>测试已完成的购物车

可以在购物车中运行应用程序现在以查看如何添加、 删除和更新的项。 购物车总额将反映在购物车中的所有项的总成本。

1. 按 **F5** 运行该应用程序。  
 在浏览器将打开并显示*Default.aspx*页。
2. 选择**汽车**类别导航菜单中。
3. 单击**添加到购物车**旁边的第一个产品的链接。   
 *ShoppingCart.aspx*页中显示订单总计。
4. 选择**平面**类别导航菜单中。
5. 单击**添加到购物车**旁边的第一个产品的链接。
6. 第一项的数量设置为 3 的购物车中并选择**删除项**第二个项的复选框。<a id="a"></a>
7. 单击**更新**按钮来更新购物车页并显示新的订单总计。 

    ![购物车的购物车更新](shopping-cart/_static/image9.png)

## <a name="summary"></a>总结

在本教程中，您创建了购物车的 Wingtip Toys Web 窗体示例应用程序。 在本教程期间你已使用 Entity Framework Code First、 数据批注、 强类型的数据控件和模型绑定。

购物车支持添加、 删除和更新用户已经选择购买的项。 除了实现购物车功能，已了解如何显示在购物车商品**GridView**控制并计算订单总计。

## <a name="addition-information"></a>其他信息

[ASP.NET 会话状态概述](https://msdn.microsoft.com/library/ms178581.aspx)

> [!div class="step-by-step"]
> [上一页](display_data_items_and_details.md)
> [下一页](checkout-and-payment-with-paypal.md)
