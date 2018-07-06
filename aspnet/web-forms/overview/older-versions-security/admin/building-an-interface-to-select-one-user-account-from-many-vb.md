---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
title: 构建一个界面，用于从多个 (VB) 中选择一个用户帐户 |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将生成具有分页、 筛选网格的用户界面。 具体而言，我们的用户界面将包含一系列的 Linkbutton 的...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2008
ms.topic: article
ms.assetid: da53380c-a16b-41c7-a20d-24343c735c52
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
msc.type: authoredcontent
ms.openlocfilehash: ec257b09209cb1a377f1ae93b58db4469f438a46
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37373186"
---
<a name="building-an-interface-to-select-one-user-account-from-many-vb"></a>构建一个界面，用于从多个 (VB) 中选择一个用户帐户
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.12.zip)或[下载 PDF](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_vb.pdf)

> 在本教程中我们将生成具有分页、 筛选网格的用户界面。 具体而言，我们的用户界面将包含的一系列的 Linkbutton 筛选基于用户名和 GridView 控件以显示匹配的用户的起始字母对结果。 我们将开始通过列出所有 GridView 中的用户帐户。 然后，在步骤 3 中，我们将添加筛选器 Linkbutton。 步骤 4 来看待分页筛选的结果。 构造在步骤 2 到 4 的接口将在后续教程中，用于为特定用户帐户执行管理任务。


## <a name="introduction"></a>介绍

在中<a id="_msoanchor_1"> </a> [*向用户分配角色*](../roles/assigning-roles-to-users-vb.md)教程中，我们创建的管理员可以选择用户和管理其角色的基本接口。 具体而言，该接口显示下拉列表的所有用户的管理员。 此类接口适合，在存在但十几用户帐户，但难以处理针对包含数百或数千个帐户的网站。 分页、 筛选网格是具有大型用户群的网站的更适合用户界面。

在本教程中我们将生成此类的用户界面。 具体而言，我们的用户界面将包含的一系列的 Linkbutton 筛选基于用户名和 GridView 控件以显示匹配的用户的起始字母对结果。 我们将开始通过列出所有 GridView 中的用户帐户。 然后，在步骤 3 中，我们将添加筛选器 Linkbutton。 步骤 4 来看待分页筛选的结果。 构造在步骤 2 到 4 的接口将在后续教程中，用于为特定用户帐户执行管理任务。

让我们进入正题！

## <a name="step-1-adding-new-aspnet-pages"></a>步骤 1： 添加新的 ASP.NET 页面

我们将在本教程并下一步的两个检查各种与管理相关的函数和功能。 我们将需要一系列的 ASP.NET 页面实现检查在这些教程中的主题。 让我们来创建这些页面和更新的站点映射。

首先，创建一个新的文件夹在项目中名为`Administration`。 接下来，将两个新的 ASP.NET 页面添加到的文件夹中，链接与每个页面`Site.master`母版页。 命名页：

- `ManageUsers.aspx`
- `UserInformation.aspx`

此外将两个页面添加到网站的根目录：`ChangePassword.aspx`和`RecoverPassword.aspx`。

这四个页面，此时，应有两个内容控件，另一个用于每个母版页的 Contentplaceholder:`MainContent`和`LoginContent`。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample1.aspx)]

我们想要显示的主页面的默认标记`LoginContent`ContentPlaceHolder 为这些页面。 因此，删除的声明性标记`Content2`内容控件。 这样做之后，页的标记应只包含一个内容控件。

ASP.NET 页`Administration`文件夹仅供管理用户。 我们添加到中的系统管理员角色<a id="_msoanchor_2"> </a> [*创建和管理角色*](../roles/creating-and-managing-roles-vb.md)教程; 限制对这两页向此角色的访问。 若要完成此操作，添加`Web.config`的文件`Administration`文件夹并配置其`<authorization>`承认管理员角色中的用户，拒绝所有其他元素。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample2.xml)]

此时您的项目的解决方案资源管理器应类似于屏幕截图中图 1 所示。


[![四个新的网页和 Web.config 文件已添加到网站](building-an-interface-to-select-one-user-account-from-many-vb/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image1.png)

**图 1**： 四个新页面和一个`Web.config`文件已添加到网站 ([单击以查看实际尺寸的图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image3.png))


最后，更新站点图 (`Web.sitemap`) 包含在进入`ManageUsers.aspx`页。 添加以下 XML 之后`<siteMapNode>`我们添加了有关角色的教程。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample3.xml)]

使用更新的站点映射，请访问通过浏览器的站点。 如图 2 所示，在左侧的导航窗格现在为管理教程包括项。


[![站点图包括一个标题为用户管理的节点](building-an-interface-to-select-one-user-account-from-many-vb/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image4.png)

**图 2**： 站点图包括节点标题为的用户管理 ([单击以查看实际尺寸的图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image6.png))


## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>步骤 2： 列出在 GridView 中的所有用户帐户

本教程中我们最终目标是创建一个分页、 筛选网格，通过该管理员可以选择要管理的用户帐户。 让我们首先列出*所有*GridView 中的用户。 完成此操作，我们将添加筛选和分页界面和功能。

打开`ManageUsers.aspx`页中`Administration`文件夹并添加一个 GridView，设置其`ID`到`UserAccounts`一会儿，我们将编写代码以将用户帐户的组绑定到 GridView 使用`Membership`类的`GetAllUsers`方法。 如之前教程中所述`GetAllUsers`方法将返回`MembershipUserCollection`对象，它是集合的`MembershipUser`对象。 每个`MembershipUser`集合中包含属性，如`UserName`， `Email`， `IsApproved`，依次类推。

为了 GridView 中显示所需的用户帐户信息，请设置 GridView`AutoGenerateColumns`属性设置为 False，并添加有关 BoundFields `UserName`， `Email`，和`Comment`属性和为 CheckBoxFields `IsApproved`，`IsLockedOut`，和`IsOnline`属性。 通过该控件声明性标记或字段对话框中，可以应用此配置。 图 3 显示的屏幕截图的字段对话框的自动生成字段复选框已取消选中并添加并配置 BoundFields 和 CheckBoxFields 后。


[![将三个 BoundFields 和三个 CheckBoxFields 添加到 GridView](building-an-interface-to-select-one-user-account-from-many-vb/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image7.png)

**图 3**： 添加三个 BoundFields 和三个 CheckBoxFields 到 GridView ([单击以查看实际尺寸的图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image9.png))


在配置后你 GridView，请确保其声明性标记类似于以下：

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample4.aspx)]

接下来，我们需要编写代码，将用户帐户绑定到 GridView。 创建一个名为方法`BindUserAccounts`若要执行此任务，然后调用它从`Page_Load`上第一次的页面访问事件处理程序。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample5.vb)]

请花费片刻时间来测试通过浏览器页面。 如图 4 所示， `UserAccounts` GridView 用户名、 电子邮件地址和所有用户的其他相关帐户信息列出了系统中。


[![用户帐户已列出 GridView 中](building-an-interface-to-select-one-user-account-from-many-vb/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image10.png)

**图 4**: GridView 中列出的用户帐户 ([单击以查看实际尺寸的图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image12.png))


## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>步骤 3： 筛选结果的第一个字母的用户名

目前`UserAccounts`GridView 显示*所有*的用户帐户。 对于包含数百或数千个用户帐户的网站，因此务必该用户能够迅速缩小显示的帐户。 这可以通过添加到页筛选 Linkbutton。 让我们向页面添加 27 Linkbutton： 一个标题为所有以及一个 LinkButton 的字母表中的每个字母。 如果访问者单击所有 LinkButton，GridView 将显示的所有用户。 如果他们单击特定字母时，将显示只有其用户名以所选的字母开头的用户。

我们的第一个任务是添加 27 LinkButton 控件。 一种方法就是以声明方式，创建的 27 Linkbutton 一次一个。 更灵活的方法是使用具有的 Repeater 控件`ItemTemplate`，它呈现 LinkButton 并且然后将筛选选项绑定到作为 Repeater`String`数组。

通过将 Repeater 控件添加到上述页面开始`UserAccounts`GridView。 设置 Repeater`ID`属性设置为`FilteringUI`配置转发器的模板，以便其`ItemTemplate`呈现 LinkButton 其`Text`和`CommandName`属性绑定到当前数组元素。 中可以看到<a id="_msoanchor_3"> </a> [*向用户分配角色*](../roles/assigning-roles-to-users-vb.md)教程中，可以使用完成这`Container.DataItem`数据绑定语法。 使用 Repeater 的`SeparatorTemplate`以显示每个链接之间的竖直线。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample6.aspx)]

若要填充此 Repeater 具有所需的筛选选项，创建一个名为方法`BindFilteringUI`。 请务必调用此方法从`Page_Load`上第一次的页面加载事件处理程序。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample7.vb)]

此方法为中的元素指定的筛选选项`String`数组`filterOptions`Repeater 将数组中每个元素，用于呈现使用 LinkButton 其`Text`和`CommandName`属性分配给数组的值元素。

图 5 显示了`ManageUsers.aspx`页面的浏览器查看时。


[![Repeater 列出了 27 筛选 Linkbutton](building-an-interface-to-select-one-user-account-from-many-vb/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image13.png)

**图 5**: Repeater 列出了 27 筛选 Linkbutton ([单击以查看实际尺寸的图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image15.png))


> [!NOTE]
> 用户名可能开始任何字符，包括数字和标点符号。 若要查看这些帐户，管理员将需要使用所有 LinkButton 选项。 或者，可以添加 LinkButton 返回以数字开头的所有用户帐户。 我将此当作练习留给读者。


单击任意筛选 Linkbutton 导致回发并引发 Repeater 的`ItemCommand`事件，但有在网格中的任何更改，因为我们尚未为编写任何代码来筛选结果。 `Membership`类包括[`FindUsersByName`方法](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx)返回其用户名与指定的搜索模式匹配这些用户帐户。 我们可以使用此方法以检索其用户名与指定的字母开头的那些用户帐户`CommandName`筛选 LinkButton 被单击。

通过更新开始`ManageUser.aspx`页面的代码隐藏类以使其包括一个名为属性`UsernameToMatch`此属性在回发之间保持用户名筛选器字符串：

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample8.vb)]

`UsernameToMatch`属性将其分配到其值存储`ViewState`使用 UsernameToMatch 的键的集合。 当读取此属性的值时，它会检查以查看是否存在某个值在`ViewState`集合; 如果不正确，则返回默认值为空字符串。 `UsernameToMatch`属性表现出一种常见模式，即持久保存一个值，以查看状态，以便在回发之间保留对该属性的任何更改。 此模式的详细信息，请阅读[Understanding ASP.NET View State](https://msdn.microsoftn-us/library/ms972976.aspx)。

接下来，更新`BindUserAccounts`方法的调用以代替`Membership.GetAllUsers`，它将调用`Membership.FindUsersByName`，并传递的值中`UsernameToMatch`追加 SQL 通配符字符开头的属性 %。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample9.vb)]

若要显示其用户名以字母 A 开头的那些用户，请设置`UsernameToMatch`属性设置为一个，然后调用`BindUserAccounts`这将导致调用`Membership.FindUsersByName("A%")`，这将返回所有用户的用户名开头 a。 同样，返回*所有*用户，将分配到一个空字符串`UsernameToMatch`属性，以便`BindUserAccounts`方法将调用`Membership.FindUsersByName("%")`，从而返回所有用户帐户。

为 Repeater 的创建事件处理程序`ItemCommand`事件。 单击某一筛选器 Linkbutton 时; 时将引发此事件它传递已单击的 LinkButton`CommandName`通过值`RepeaterCommandEventArgs`对象。 我们需要将相应的值赋给`UsernameToMatch`属性，然后调用`BindUserAccounts`方法。 如果`CommandName`为 All，将分配到一个空字符串`UsernameToMatch`，以便显示所有用户帐户。 否则，将分配`CommandName`值设为 `UsernameToMatch`

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample10.vb)]

利用此代码，测试筛选功能。 当首次访问页面时，显示所有用户帐户 （回头查看图 5）。 单击 LinkButton 导致回发，并筛选结果，显示以 A 开头这些用户帐户。


[![使用筛选的 Linkbutton 来显示其用户名以某些字母开头的用户](building-an-interface-to-select-one-user-account-from-many-vb/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image16.png)

**图 6**： 使用筛选 Linkbutton 来显示这些用户其用户名以特定字母开头 ([单击以查看实际尺寸的图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image18.png))


## <a name="step-4-updating-the-gridview-to-use-paging"></a>步骤 4： 更新 GridView，其中使用的分页

图 5 和 6 中所示 GridView 列出了从返回的记录的所有`FindUsersByName`方法。 如果有数百或数千个用户帐户这可以查看的所有帐户 （如单击所有 LinkButton 时或当最初访问页面时都是如此） 时导致信息过载。 为了帮助更易于管理的块中存在的用户帐户，让我们配置 GridView，其中每次显示 10 个用户帐户。

GridView 控件提供了两种类型的分页：

- **默认分页**-容易实现，但效率低下。 简单地说，默认值分页 GridView 期望*所有*从其数据源的记录。 然后仅显示记录的相应页。
- **自定义分页**-需要更多工作来实现，但比默认分页因为使用自定义分页数据源返回只精确的可显示的记录集更高效。

分页浏览几千条记录时，可以极大地默认和自定义分页的性能差异。 由于我们要构建假定此接口可能是数百或数千个用户帐户，让我们使用自定义分页。

> [!NOTE]
> 有关默认和自定义分页，以及实现自定义分页所面临的挑战之间的区别的更深入讨论，请参阅[有效地分页通过大容量数据的](https://asp.net/learn/data-access/tutorial-25-vb.aspx)。 默认和自定义分页的性能差异一些分析，请参阅[结合使用 ASP.NET 和 SQL Server 2005 中的自定义分页](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)。


若要实现自定义分页我们首先需要某些机制，通过其检索 GridView 显示的记录的精确的子集。 值得高兴的是`Membership`类的`FindUsersByName`方法具有重载方法，可用于指定的页索引和页大小，并返回在记录该范围内这些用户帐户。

具体而言，此重载具有以下签名： [ `FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)` ](https://msdn.microsoft.com/library/fa5st8b2.aspx)。

*PageIndex*参数指定要返回; 用户帐户的页*pageSize*指示每页显示的记录数。 *Totalrecords 信息*参数是`ByRef`参数，它在用户存储区返回的总用户帐户数。

> [!NOTE]
> 返回的数据`FindUsersByName`按 username; 不能自定义排序条件。


GridView 可以配置为使用自定义分页，但仅当绑定到对象数据源控件。 要实现自定义分页的 ObjectDataSource 控件，它需要两个方法： 一个传递给起始行索引和记录，若要显示，最大数目，并返回该范围内; 内的记录的精确子集和通过分页所返回的记录总数的方法。 `FindUsersByName`重载接受的页索引和页面大小，并返回通过记录总数`ByRef`参数。 因此，此处接口不匹配。

一种方法就是创建代理类公开的接口 ObjectDataSource 期望，并在内部调用`FindUsersByName`方法。 另一种方法-，另一个我们将对此项目使用的是创建我们自己分页接口，并使用，而不是 GridView 的内置分页界面。

### <a name="creating-a-first-previous-next-last-paging-interface"></a>创建第一个上, 一条、 下一步，最后一个分页界面

让我们构建第一个、 上一步、 下一步，与最后一个 Linkbutton 分页界面。 第一个 LinkButton，单击时，将用户转到第一页数据，而上一步将返回与他联系到前一页。 同样地下, 一步和上一次将用户移到下一步和最后一页中，分别。 添加下面的四个 LinkButton 控件`UserAccounts`GridView。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample11.aspx)]

接下来，创建一个事件处理程序的 LinkButton 的每个`Click`事件。

图 7 显示了四个 Linkbutton 时通过 Visual Web Developer 设计视图查看。


[![接下来，添加第一个、 上一个、 和最后一个 Linkbutton 下 GridView](building-an-interface-to-select-one-user-account-from-many-vb/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image19.png)

**图 7**： 添加第一个、 上一步、 下一步，和最后一个 Linkbutton 下方的 GridView ([单击以查看实际尺寸的图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image21.png))


### <a name="keeping-track-of-the-current-page-index"></a>跟踪的当前页索引

当用户第一次访问`ManageUsers.aspx`页或单击任一筛选按钮，我们想要在 GridView 中显示数据的第一页。 当用户单击其中一个导航 Linkbutton 时，但是，我们需要更新的页索引。 若要维护的页索引和要每页显示的记录数，添加到页面的代码隐藏类的以下两个属性：

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample12.vb)]

像`UsernameToMatch`属性，`PageIndex`属性保持其视图状态的值。 只读的`PageSize`属性返回 10 的硬编码值。 我邀请感的读取器来更新此属性，以使用相同的模式`PageIndex`，然后以增加`ManageUsers.aspx`页上，以便访问的页面的人员可以指定多少个用户帐户以显示每个页上。

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>检索只是当前页的记录，更新页索引，并启用和禁用分页界面 Linkbutton

使用就地分页接口和`PageIndex`和`PageSize`添加属性，我们已准备好更新`BindUserAccounts`方法，以便使用相应`FindUsersByName`重载。 此外，我们需要将此方法启用或禁用分页界面，具体取决于要显示哪些页。 在查看数据的第一页时，应禁用第一个和上一步链接;查看最后一页时，应禁用下一步和最后一次。

使用以下代码更新 `BindUserAccounts` 方法：

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample13.vb)]

请注意，通过的最后一个参数确定正在通过用寻呼发送的记录总数`FindUsersByName`方法。 返回指定的页的用户帐户后，四个 Linkbutton 可以启用或禁用，具体取决于是否正在查看数据的第一个或最后一页。

最后一步是编写代码的四个 Linkbutton`Click`事件处理程序。 这些事件处理程序需要更新`PageIndex`属性，然后重新绑定到通过调用 GridView 数据`BindUserAccounts`第一个、 上一步，和下一步的事件处理程序是非常简单。 `Click`最后一个 LinkButton，事件处理程序，但稍微有些复杂因为我们需要确定多少条记录显示以确定最后一页索引。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample14.vb)]

图 8 和 9 在操作中展示的自定义分页界面。 图 8 显示了`ManageUsers.aspx`页上查看所有用户帐户的数据的第一页时。 请注意，仅有 10 的 13 帐户会显示。 单击下一步或最后一个链接会导致回发时，更新`PageIndex`为 1，第二页的用户帐户添加到网格中的绑定 （请参阅图 9）。


[![显示第一个 10 用户帐户](building-an-interface-to-select-one-user-account-from-many-vb/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image22.png)

**图 8**： 显示第一个 10 用户帐户 ([单击以查看实际尺寸的图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image24.png))


[![单击下一步链接显示用户帐户的第二的页](building-an-interface-to-select-one-user-account-from-many-vb/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image25.png)

**图 9**： 单击下一步链接显示的第二个页面的用户帐户 ([单击以查看实际尺寸的图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image27.png))


## <a name="summary"></a>总结

管理员通常需要从帐户列表中选择用户。 在前面的教程探讨了使用下拉列表填充用户，但这种方法可伸缩性差。 在本教程中我们探讨了更好的选择： 分页 GridView 中显示其结果的可筛选接口。 与此用户界面，管理员可以快速高效地找到并选择在千位之间的一个用户帐户。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [在 ASP.NET 中使用 SQL Server 2005 的自定义分页](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [通过大量的数据有效分页](https://asp.net/learn/data-access/tutorial-25-vb.aspx)
- [滚动你自己的网站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>关于作者

自 1998 年以来，Scott Mitchell，多部 asp/ASP.NET 书籍的作者及 4GuysFromRolla.com 的已从事 Microsoft Web 技术工作。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是 *[Sams Teach 自己 ASP.NET 2.0 24 小时内](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在达到 Scott [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Alicja Maziarz。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行

> [!div class="step-by-step"]
> [上一页](unlocking-and-approving-user-accounts-cs.md)
> [下一页](recovering-and-changing-passwords-vb.md)
