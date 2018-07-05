---
uid: web-forms/overview/older-versions-security/roles/assigning-roles-to-users-cs
title: 将角色分配给用户 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将生成两个 ASP.NET 页，以帮助管理哪些用户属于哪些角色。 第一页将包括相应的工具来了解...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/24/2008
ms.topic: article
ms.assetid: d522639a-5aca-421e-9a76-d73f95607f57
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-security/roles/assigning-roles-to-users-cs
msc.type: authoredcontent
ms.openlocfilehash: 2f65caf132e185b381093ee1a0b5dd5400ed8434
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374135"
---
<a name="assigning-roles-to-users-c"></a>将角色分配给用户 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.10.zip)或[下载 PDF](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial10_AssigningRoles_cs.pdf)

> 在本教程中，我们将生成两个 ASP.NET 页，以帮助管理哪些用户属于哪些角色。 第一页将包括相应的工具来查看哪些用户属于给定角色特定的用户属于哪些角色和分配或从特定角色中删除特定用户的能力。 在第二页中我们将补充 CreateUserWizard 控件，以便它包含一个步骤来指定新创建的用户属于哪些角色。 这是在管理员能够创建新的用户帐户的情况下很有用。


## <a name="introduction"></a>介绍

<a id="_msoanchor_1"> </a>[前一篇教程](creating-and-managing-roles-cs.md)检查角色框架并`SqlRoleProvider`; 我们已了解如何使用`Roles`类来创建、 检索和删除角色。 除了创建和删除角色，我们需要能够将分配或从角色中删除用户。 遗憾的是，ASP.NET 不随附于任何 Web 控件，用于管理哪些用户属于哪些角色。 相反，我们必须创建我们自己的 ASP.NET 页面来管理这些关联。 值得高兴的是，添加和删除用户角色是非常简单。 `Roles`类包含多种方法来将一个或多个用户添加到一个或多个角色。

在本教程中，我们将生成两个 ASP.NET 页，以帮助管理哪些用户属于哪些角色。 第一页将包括相应的工具来查看哪些用户属于给定角色特定的用户属于哪些角色和分配或从特定角色中删除特定用户的能力。 在第二页中我们将补充 CreateUserWizard 控件，以便它包含一个步骤来指定新创建的用户属于哪些角色。 这是在管理员能够创建新的用户帐户的情况下很有用。

让我们进入正题！

## <a name="listing-what-users-belong-to-what-roles"></a>列出哪些用户属于哪些角色

首要任务对于本教程将创建 web 页，从中可为用户分配到角色。 我们考虑自己如何将用户分配到角色之前，让我们首先集中精力如何确定哪些用户属于哪些角色。 有两种方法来显示此信息:"角色"或""用户。 我们可以允许访问者可以选择一个角色，然后显示它们的所有用户属于角色 （"按角色"显示中），或者我们无法提示选择一个用户，然后显示其分配给该用户 （"按用户"显示） 的角色的访问者。

"按角色"视图都适用于情况访问者希望知道属于特定角色; 用户组访问者需要知道特定用户的角色时，"由用户"视图是理想之选。 让我们了解我们的页面包括"的 role"和"按用户"接口。

我们将首先创建"由用户"接口。 此接口将包含下拉列表和复选框的列表。 下拉列表将随系统; 中的用户组相应的复选框将枚举这些角色。 从下拉列表中选择用户将检查用户属于这些角色。 访问的页面的人可以然后选中或取消选中复选框，以添加或删除所选的用户对应的角色。

> [!NOTE]
> 使用下拉列表添加到列表的用户帐户不是网站的理想之选其中可能有数百个用户帐户。 下拉列表设计以允许用户选择一项相对较短的列表中的选项。 它很快会变得难以处理随着列表项的数量增加。 如果您正在生成将具有可能较大数量的用户帐户的网站，可能想要考虑使用一个备用用户界面，如可分页 GridView 或可筛选的接口，其中列出提示选择号的访问者，然后仅显示了其用户名以所选的字母开头的用户。


## <a name="step-1-building-the-by-user-user-interface"></a>步骤 1： 生成"按用户"用户界面

打开`UsersAndRoles.aspx`页。 在页面顶部，添加名为的标签 Web 控件`ActionStatus`并将清除其`Text`属性。 我们将使用此标签显示与此类似，所执行的操作上提供反馈，"用户 Tito 已添加到管理员角色中，"或者"用户 Jisun 已从主管角色。" 若要使这些消息凸显出来，设置标签的`CssClass`属性设置为"Important"。

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample1.aspx)]

接下来，添加以下 CSS 类定义到`Styles.css`样式表：

[!code-css[Main](assigning-roles-to-users-cs/samples/sample2.css)]

此 CSS 定义会指示浏览器显示使用的大型的红色字体的标签。 图 1 显示了 Visual Studio 设计器通过这种效果。


[![标签的 CssClass 属性会导致大型，红色字体](assigning-roles-to-users-cs/_static/image2.png)](assigning-roles-to-users-cs/_static/image1.png)

**图 1**: 标签`CssClass`属性会导致大型，红色字体 ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image3.png))


接下来，将 DropDownList 添加到页上，设置其`ID`属性设置为`UserList`，并设置其`AutoPostBack`属性设为 True。 我们将使用此 DropDownList 系统中列出的所有用户。 此 DropDownList 将绑定到的 MembershipUser 对象的集合。 因为我们希望 DropDownList 以显示 MembershipUser 对象的用户名属性 （并将其用作列表项的值），设置 DropDownList`DataTextField`和`DataValueField`为"UserName"的属性。

下面的下拉列表中，添加名为 Repeater `UsersRoleList`。 此 Repeater 将列出所有角色的系统中为一系列的复选框。 定义 Repeater 的`ItemTemplate`使用下面的声明性标记：

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample3.aspx)]

`ItemTemplate`标记包含一个名为的单个复选框 Web 控件`RoleCheckBox`。 该复选框`AutoPostBack`属性设置为 True 并`Text`属性绑定到`Container.DataItem`。 原因的数据绑定语法是`Container.DataItem`是因为角色框架将返回作为字符串数组的角色名称的列表，我们将绑定到 Repeater 此字符串数组。 为什么要使用此语法显示数组绑定到数据 Web 控件的内容的详尽描述不在本教程的范围。 有关此问题的详细信息，请参阅[标量数组绑定到数据 Web 控件](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)。

此时你"按用户"接口的声明性标记应类似以下：

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample4.aspx)]

我们现已准备好编写代码以将用户帐户添加到 DropDownList 的集和 Repeater 的角色集的绑定。 在页面的代码隐藏类中，添加一个名为`BindUsersToUserList`，另一个名为`BindRolesList`，使用以下代码：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample5.cs)]

`BindUsersToUserList`方法通过在系统中检索的所有用户帐户[`Membership.GetAllUsers`方法](https://msdn.microsoft.com/library/dy8swhya.aspx)。 这将返回[`MembershipUserCollection`对象](https://msdn.microsoft.com/library/system.web.security.membershipusercollection.aspx)，这是一系列[`MembershipUser`实例](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)。 此集合绑定到`UserList`DropDownList。 `MembershipUser`实例的集合包含的各种属性，如该构成`UserName`， `Email`， `CreationDate`，和`IsOnline`。 若要指示 DropDownList 中显示的值`UserName`属性，确保`UserList`DropDownList 的`DataTextField`和`DataValueField`属性已设置为"UserName"。

> [!NOTE]
> `Membership.GetAllUsers`方法有两个重载： 一个接受任何输入的参数并返回的所有用户，另一个使用的页索引和页大小的整数值并返回仅指定用户的子集。 当存在大量的用户帐户的可分页用户界面元素中显示时，第二个重载可以使用更高效地通过用户的页面中，因为它返回的用户帐户，而不是所有这些只是精确的子集。


`BindRolesToList`方法通过调用来启动`Roles`类的[`GetAllRoles`方法](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx)，这会返回系统中包含的角色的字符串数组。 此字符串数组，则绑定到 Repeater 中。

最后，我们需要调用这两种方法，首次加载页面时。 将以下代码添加到 `Page_Load` 事件处理程序中：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample6.cs)]

利用此代码，请花费片刻时间访问通过浏览器; 页面屏幕应类似于图 2。 所有用户帐户被填充下拉列表中，，在其中，每个角色显示为一个复选框。 因为我们设置`AutoPostBack`属性的 DropDownList 和复选框为 True，则更改所选的用户或选中或取消选中角色导致回发。 但是，因为我们尚未编写代码来处理这些操作，不执行任何操作。 例如，我们将介绍以下两个部分中的这些任务。


[![页面显示的用户和角色](assigning-roles-to-users-cs/_static/image5.png)](assigning-roles-to-users-cs/_static/image4.png)

**图 2**: 页上显示的用户和角色 ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image6.png))


### <a name="checking-the-roles-the-selected-user-belongs-to"></a>检查这些角色所选的用户归属的

首次加载页面，或访问者从下拉列表中选择新用户，我们需要更新`UsersRoleList`的复选框，以便仅当选定的用户属于该角色检查一个给定的角色的复选框。 若要实现此目的，创建一个名为方法`CheckRolesForSelectedUser`使用以下代码：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample7.cs)]

上面的代码首先会确定所选的用户是谁。 然后，它使用角色类的[`GetRolesForUser(userName)`方法](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx)返回角色作为一个字符串数组，指定的用户的组。 接下来，枚举 Repeater 的项和每个项的`RoleCheckBox`复选框以编程方式引用。 仅当它对应于该角色包含在选中该复选框`selectedUsersRoles`字符串数组。

> [!NOTE]
> `selectedUserRoles.Contains<string>(...)`语法将无法编译，如果您使用的 ASP.NET 2.0 版。 `Contains<string>`方法属于[LINQ 库](http://en.wikipedia.org/wiki/Language_Integrated_Query)，这是 ASP.NET 3.5 中新增。 如果您仍在使用 ASP.NET 2.0 版中，使用[`Array.IndexOf<string>`方法](https://msdn.microsoft.com/library/eha9t187.aspx)相反。


`CheckRolesForSelectedUser`方法需要两种情况下调用： 首次加载页面时，只要`UserList`DropDownList 的所选的索引更改。 因此，调用此方法从`Page_Load`事件处理程序 (调用后`BindUsersToUserList`和`BindRolesToList`)。 此外，为 DropDownList 的创建事件处理程序`SelectedIndexChanged`事件，并从中调用此方法。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample8.cs)]

利用此代码，可以通过浏览器页进行测试。 但是，由于`UsersAndRoles.aspx`页当前不具备的功能，若要将用户分配到角色，没有用户的角色。 我们将创建将用户分配到角色的那样，因此可以相信我所说，此代码有效，并验证这一点更高版本，接口或可以手动添加用户到角色的方法是插入记录到`aspnet_UsersInRoles`为了测试此 functi 表现在 onality。

### <a name="assigning-and-removing-users-from-roles"></a>分配或从角色删除用户

访问者时选中或取消选中中的复选框`UsersRoleList`Repeater 我们需要添加或删除选定的用户从相应的角色。 复选框的`AutoPostBack`属性当前设置为 True，这会导致回发，只要 Repeater 中的复选框是选中或取消选中。 简单地说，我们需要创建一个事件处理程序的复选框的`CheckChanged`事件。 由于该复选框，在 Repeater 控件中，我们需要手动添加事件处理程序管道。 首先将事件处理程序添加到代码隐藏类作为`protected`方法，如下所示：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample9.cs)]

我们将返回为此事件处理程序在一段时间中编写代码。 但首先让我们来完成的事件处理管道。 从 Repeater 中的复选框`ItemTemplate`，添加`OnCheckedChanged="RoleCheckBox_CheckChanged"`。 此语法绑定`RoleCheckBox_CheckChanged`事件处理程序`RoleCheckBox`的`CheckedChanged`事件。

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample10.aspx)]

最后一项任务是完成`RoleCheckBox_CheckChanged`事件处理程序。 我们需要通过引用引发事件，因为可以告诉我们哪些角色已选中还是通过取消选中此复选框实例的复选框控件开始其`Text`和`Checked`属性。 使用此信息，以及用户名的所选用户，我们中添加或删除用户通过角色`Roles`类的[ `AddUserToRole` ](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx)或[`RemoveUserFromRole`方法](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample11.cs)]

上面的代码以编程方式引用引发事件，可通过该复选框`sender`输入的参数。 如果选中此复选框，则会将所选的用户添加到指定角色，否则为会从角色中删除。 在任一情况下，`ActionStatus`标签显示一条消息，汇总只需执行的操作。

请花费片刻时间来查看此页，通过浏览器测试。 选择用户 Tito，然后将 Tito 添加到管理员和在监督器角色。


[![Tito 已添加到管理员和在监督器角色](assigning-roles-to-users-cs/_static/image8.png)](assigning-roles-to-users-cs/_static/image7.png)

**图 3**: Tito 已添加到管理员和主管角色 ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image9.png))


接下来，从下拉列表中选择用户 Bruce。 没有为在回发和 Repeater 的复选框会更新通过`CheckRolesForSelectedUser`。 由于 Bruce 尚不属于任何角色，两个复选框的未选中状态。 接下来，将 Bruce 添加到在监督器角色。


[![Bruce 已添加到在监督器角色](assigning-roles-to-users-cs/_static/image11.png)](assigning-roles-to-users-cs/_static/image10.png)

**图 4**: Bruce 已添加到主管角色 ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image12.png))


若要进一步验证的功能`CheckRolesForSelectedUser`方法中，选择一个 Tito 或 Bruce 以外的用户。 请注意如何复选框的未自动选中，表示它们确实不属于任何角色。 返回到 Tito。 应检查管理员和在监督器复选框。

## <a name="step-2-building-the-by-roles-user-interface"></a>步骤 2： 生成"的角色"用户界面

现在我们已完成"的用户"接口，并准备好开始处理"的角色"接口。 "按角色"接口会提示用户从下拉列表选择一个角色，然后显示属于该角色的 GridView 中的用户组。

添加到另一个 DropDownList 控件`UsersAndRoles.aspx`页。 将此某个的 Repeater 控件下方，将其命名`RoleList`，并设置其`AutoPostBack`属性设为 True。 下方，添加一个 GridView 并将其命名`RolesUserList`。 此 GridView 将列出属于所选角色的用户。 设置 GridView`AutoGenerateColumns`属性设置为 False，向网格添加 TemplateField`Columns`集合，并设置其`HeaderText`属性设置为"用户"。 定义 TemplateField `ItemTemplate` ，以便显示数据绑定表达式的值`Container.DataItem`中`Text`属性的一个名为标签`UserNameLabel`。

添加并配置 GridView 之后, 你"按角色"接口的声明性标记应类似于下面：

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample12.aspx)]

我们需要填充`RoleList`DropDownList 与系统中的角色集。 若要完成此操作，更新`BindRolesToList`方法，这就是绑定以便通过返回的字符串数组`Roles.GetAllRoles`方法`RolesList`DropDownList (以及`UsersRoleList`Repeater)。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample13.cs)]

中的最后两行`BindRolesToList`方法已添加要绑定到的角色集`RoleList`DropDownList 控件。 图 5 显示了最终结果时的浏览器 – 使用系统的角色填充下拉列表查看。


[![角色显示在 RoleList DropDownList](assigning-roles-to-users-cs/_static/image14.png)](assigning-roles-to-users-cs/_static/image13.png)

**图 5**: 角色显示在`RoleList`DropDownList ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image15.png))


### <a name="displaying-the-users-that-belong-to-the-selected-role"></a>显示属于所选角色的用户

首次加载页面时，或从选择的新角色时`RoleList`下拉列表中，我们需要显示属于该角色在 GridView 中的用户的列表。 创建一个名为方法`DisplayUsersBelongingToRole`使用以下代码：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample14.cs)]

此方法开始时获取从所选的角色`RoleList`DropDownList。 然后，它使用[`Roles.GetUsersInRole(roleName)`方法](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx)检索属于该角色的用户的用户名的字符串数组。 然后，此数组绑定到`RolesUserList`GridView。

此方法需要在两种情况下调用： 和最初加载页面时中的所选的角色`RoleList`DropDownList 的更改。 因此，更新`Page_Load`事件处理程序，以便在调用后调用此方法`CheckRolesForSelectedUser`。 接下来，创建的事件处理程序`RoleList`的`SelectedIndexChanged`事件，并太从中调用此方法。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample15.cs)]

利用此代码， `RolesUserList` GridView 应显示那些属于所选角色的用户。 如图 6 所示，在监督器角色都包含两个成员： Bruce 和 Tito。


[![GridView 列出了这些属于所选角色的用户](assigning-roles-to-users-cs/_static/image17.png)](assigning-roles-to-users-cs/_static/image16.png)

**图 6**: GridView 列出了这些用户的属于所选角色 ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image18.png))


### <a name="removing-users-from-the-selected-role"></a>从所选角色中删除用户

让我们来增强`RolesUserList`GridView，使之包含的列的"删除"按钮。 单击特定用户的"删除"按钮将其从该角色中删除。

首先删除按钮字段添加到 GridView。 将此字段显示为字段最左侧，并更改其`DeleteText`属性从"删除"（默认值） 为"删除"。


[![添加](assigning-roles-to-users-cs/_static/image20.png)](assigning-roles-to-users-cs/_static/image19.png)

**图 7**： 将"删除"按钮添加到 GridView ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image21.png))


单击"删除"按钮时，才会回发和 GridView`RowDeleting`引发事件。 我们需要创建此事件的事件处理程序和编写代码，从所选角色中删除用户。 创建事件处理程序，并添加以下代码：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample16.cs)]

代码首先会确定所选的角色名称。 然后，它以编程方式引用`UserNameLabel`控件从其"删除"按钮被单击以确定要删除的用户的用户名的行。 然后通过调用在角色中删除用户`Roles.RemoveUserFromRole`方法。 `RolesUserList` GridView 然后被刷新，并且通过显示一条消息`ActionStatus`标签控件。

> [!NOTE]
> "删除"按钮不需要任何种类的来自用户的确认之前从角色中删除用户。 我邀请您添加某一级别的用户进行确认。 若要确认某项操作的最简单方法之一是通过客户端的确认对话框。 有关此技术的详细信息，请参阅[删除时添加客户端确认](https://asp.net/learn/data-access/tutorial-42-cs.aspx)。


图 8 在监督器组中删除用户 Tito 后显示的页。


[![唉，Tito 不再负责管理](assigning-roles-to-users-cs/_static/image23.png)](assigning-roles-to-users-cs/_static/image22.png)

**图 8**： 唉，Tito 不再负责管理 ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image24.png))


### <a name="adding-new-users-to-the-selected-role"></a>将新用户添加到所选角色

从所选角色中删除用户，以及到此页的访问者也应该能够将用户添加到所选角色。 将用户添加到所选角色的最佳接口取决于你预期获得的用户帐户数。 如果你的网站将容纳几几十个用户帐户或更少，您可以在此处使用 DropDownList。 可能有数千个用户帐户，如果你想要包括允许的访问者可以逐页查看的帐户，搜索特定帐户，或筛选以某种其他方式的用户帐户的用户界面。

此页让我们使用在系统中工作而不考虑用户帐户数的接口非常简单。 也就是说，我们将使用文本框中，提示她想要添加到所选角色的用户的用户名中的类型的访问者。 如果存在具有该名称没有用户，或者如果用户已是角色的成员，我们将显示一条消息中的`ActionStatus`标签。 但是，如果用户存在，并且不是角色的成员，我们将添加到角色并刷新该网格。

添加一个文本框和按钮下方 GridView。 设置文本框的`ID`到`UserNameToAddToRole`并设置按钮的`ID`并`Text`属性设置为`AddUserToRoleButton`和"添加用户到角色"，分别。

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample17.aspx)]

接下来，创建`Click`事件处理程序`AddUserToRoleButton`并添加以下代码：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample18.cs)]

中的代码大部分`Click`事件处理程序执行各种验证检查。 它可确保访问者提供中的用户名`UserNameToAddToRole`文本框中，该用户在系统中，存在并且已不属于所选角色。 如果任一检查失败，相应的消息将显示在`ActionStatus`和退出事件处理程序。 如果所有检查都通过，将用户添加到通过角色`Roles.AddUserToRole`方法。 之后，文本框中的`Text`清除属性、 刷新 GridView，和`ActionStatus`标签显示一条消息，该值指示指定的用户已成功添加到所选角色。

> [!NOTE]
> 若要确保不已属于所选角色指定的用户，我们使用[`Roles.IsUserInRole(userName, roleName)`方法](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)，它返回一个布尔值，该值指示是否*用户名*属于*roleName*。 我们将使用此方法在再次<a id="_msoanchor_2"> </a>[下一教程](role-based-authorization-cs.md)当我们查看基于角色的授权。


访问通过浏览器页面，然后选择从主管角色`RoleList`DropDownList。 请尝试输入无效的用户名 – 你应看到一条消息说明用户不存在系统中。


[![不能将不存在的用户添加到角色](assigning-roles-to-users-cs/_static/image26.png)](assigning-roles-to-users-cs/_static/image25.png)

**图 9**： 不能将非存在的用户添加到角色 ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image27.png))


现在，尝试添加的有效用户。 继续操作并将 Tito 重新添加到在监督器角色。


[![Tito 是再一次监督程序 ！](assigning-roles-to-users-cs/_static/image29.png)](assigning-roles-to-users-cs/_static/image28.png)

**图 10**: Tito 是再一次监督程序 ！  ([单击此项可查看原尺寸图像](assigning-roles-to-users-cs/_static/image30.png))


## <a name="step-3-cross-updating-the-by-user-and-by-role-interfaces"></a>步骤 3： 跨更新"用户"和"的角色"接口

`UsersAndRoles.aspx`页提供了用于管理用户和角色的两个不同接口。 目前，这两个接口互相独立地处理，因此，在一个接口中所做的更改将不会立即反映在其他。 例如，假设到页面的访问者选择的主管角色`RoleList`下拉列表中，其中列出 Bruce 和 Tito 了作为其成员。 接下来，访问者选择从 Tito`UserList`下拉列表中，它检查中的管理员和监督复选框`UsersRoleList`Repeater。 如果访问者然后取消选中从 Repeater 监督者角色，从在监督器角色中删除 Tito 但是"的角色"界面中不会反映这种修改。 GridView 仍会显示 Tito 视为在监督器角色的成员。

若要修复此，我们需要只要角色是 checked 或 unchecked 从刷新 GridView `UsersRoleList` Repeater。 同样，我们需要刷新 Repeater，每当用户删除或从"按角色"接口添加到角色。

在"按用户"界面 Repeater 刷新通过调用`CheckRolesForSelectedUser`方法。 "按角色"接口可以中修改`RolesUserList`GridView`RowDeleting`事件处理程序和`AddUserToRoleButton`按钮的`Click`事件处理程序。 因此，我们需要调用`CheckRolesForSelectedUser`从每个这些方法的方法。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample19.cs)]

同样，通过调用刷新"的角色"界面中 GridView`DisplayUsersBelongingToRole`方法和"按用户"接口通过修改`RoleCheckBox_CheckChanged`事件处理程序。 因此，我们需要调用`DisplayUsersBelongingToRole`来自此事件处理程序方法。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample20.cs)]

这些细微的代码更改，"按用户"和"按角色"接口现在正确地跨更新。 若要验证这一点，请访问通过浏览器页面，并选择 Tito 和在监督器从`UserList`和`RoleList`Dropdownlist，分别。 请注意用于从"按用户"界面中 Repeater Tito 取消选中在监督器角色，如 Tito 会自动删除从"按角色"界面中 GridView。 将添加 Tito 回主管角色从"按角色"接口会自动重新检查"由用户"接口中的主管复选框。

## <a name="step-4-customizing-the-createuserwizard-to-include-a-specify-roles-step"></a>步骤 4： 自定义 CreateUserWizard 包括"指定角色"的步骤

在中<a id="_msoanchor_3"> </a> [*创建用户帐户*](../membership/creating-user-accounts-cs.md)教程中我们已了解如何使用 CreateUserWizard Web 控件来提供用于创建新的用户帐户的接口。 CreateUserWizard 控件可以采用两种方式之一：

- 作为一种方式为在站点上创建其自己的用户帐户的访问者和
- 作为一种方式创建新的帐户管理员

在第一个用例，访问者进入这个网站并填写 CreateUserWizard，以便在网站注册以输入他们的信息。 在第二种情况下，管理员将为其他人创建新帐户。

通过某些其他人的管理员创建帐户后，可能会有帮助，可允许管理员指定新的用户帐户所属的哪些角色。 在中<a id="_msoanchor_4"> </a> [*存储**其他用户信息*](../membership/storing-additional-user-information-cs.md)我们已了解如何通过添加其他自定义 CreateUserWizard 教程`WizardSteps`. 让我们看看如何将一个额外的步骤添加到 CreateUserWizard，以指定新用户的角色。

打开`CreateUserWizardWithRoles.aspx`页上，添加名为的 CreateUserWizard 控件`RegisterUserWithRoles`。 设置控件的`ContinueDestinationPageUrl`属性设置为"~ / Default.aspx"。 由于这里的思路是，管理员使用此 CreateUserWizard 控件来创建新的用户帐户，设置控件的`LoginCreatedUser`属性设置为 False。 这`LoginCreatedUser`属性指定是否以刚创建的用户自动登录访问者和默认为 True。 我们将其设置为 False 则因为管理员创建新帐户时我们想要使他自己以身份登录。

接下来，选择"添加/删除`WizardSteps`..."选项从 CreateUserWizard 的智能标记，然后添加一个新`WizardStep`，并设置其`ID`到`SpecifyRolesStep`。 移动`SpecifyRolesStep WizardStep`，以便它出现在"符号注册新帐户"步骤中，但在"完成"步骤之前。 设置`WizardStep`的`Title`属性设置为"指定的角色"其`StepType`属性设置为`Step`，并将其`AllowReturn`属性设置为 False。


[![添加](assigning-roles-to-users-cs/_static/image32.png)](assigning-roles-to-users-cs/_static/image31.png)

**图 11**： 添加"指定角色"`WizardStep`到 CreateUserWizard ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image33.png))


此更改后 CreateUserWizard 的声明性标记应如下所示：

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample21.aspx)]

在"指定角色" `WizardStep`，添加名为 CheckBoxList `RoleList`。 此 CheckBoxList 将列出可用的角色启用访问的页面的人员，以检查新创建的用户属于哪些角色。

我们仍然面临着两个编码任务： 首先，我们必须填充`RoleList`CheckBoxList 系统; 中的角色与第二，我们需要将创建的用户添加到所选角色中，当用户从"指定的角色"步骤移动到"已完成"步骤。 我们可以完成的第一个任务`Page_Load`事件处理程序。 下面的代码以编程方式引用`RoleList`复选框在第一天访问网页，并对其绑定在系统中的角色。

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample22.cs)]

上面的代码应该很熟悉。 在中<a id="_msoanchor_5"> </a> [*存储**其他用户信息*](../membership/storing-additional-user-information-cs.md)教程中我们使用了两个`FindControl`语句，以引用 Web 控件从自定义内`WizardStep`。 并将角色绑定到 CheckBoxList 的代码已在本教程前面从中获取。

若要执行的第二个编程任务，我们需要知道"指定的角色"步骤已在已完成。 回想一下，CreateUserWizard 具有`ActiveStepChanged`访问者从某一步导航到另一个每次触发的事件。 此处我们可以确定用户是否已达到"完成"步骤中;如果是这样，我们需要将用户添加到所选角色。

创建事件处理程序`ActiveStepChanged`事件，并添加以下代码：

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample23.cs)]

如果用户只是已达到"已完成"步骤，事件处理程序的项进行枚举`RoleList`CheckBoxList 和刚创建的用户分配给所选角色。

访问本页可通过浏览器。 CreateUserWizard 的第一步是标准的"符号注册新帐户"步骤，该对话框提示输入新用户的用户名、 密码、 电子邮件和其他重要信息。 输入要创建一个名为 Wanda 的新用户的信息。


[![创建名为 Wanda 的新用户](assigning-roles-to-users-cs/_static/image35.png)](assigning-roles-to-users-cs/_static/image34.png)

**图 12**： 创建新的用户名为 Wanda ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image36.png))


单击"创建用户"按钮。 在内部调用 CreateUserWizard`Membership.CreateUser`方法，创建新用户帐户，然后将前进到下一步"指定角色。" 此处列出的系统角色。 检查在监督器复选框，然后单击下一步。


[![使 Wanda 在监督器角色的成员](assigning-roles-to-users-cs/_static/image38.png)](assigning-roles-to-users-cs/_static/image37.png)

**图 13**： 使 Wanda 在监督器角色的成员 ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image39.png))


单击下一步会导致回发和更新`ActiveStep`到"已完成"步骤。 在`ActiveStepChanged`事件处理程序的最近创建的用户帐户分配给在监督器角色。 若要验证这一点，返回到`UsersAndRoles.aspx`页上，选择在监督器从`RoleList`DropDownList。 如图 14 所示，在监督器现在由组成的三个用户： Bruce、 Tito 和 Wanda。


[![Bruce、 Tito 和 Wanda 是所有主管](assigning-roles-to-users-cs/_static/image41.png)](assigning-roles-to-users-cs/_static/image40.png)

**图 14**: Bruce、 Tito 和 Wanda 是所有监督器 ([单击以查看实际尺寸的图像](assigning-roles-to-users-cs/_static/image42.png))


## <a name="summary"></a>总结

角色框架提供了用于检索有关特定用户的角色和方法来确定哪些用户属于指定角色信息的方法。 此外，有多种方法来添加和删除一个或多个用户到一个或多个角色。 在本教程中我们主要介绍这些方法的两个：`AddUserToRole`和`RemoveUserFromRole`。 有其他变体旨在将多个用户添加到单个角色，并将多个角色分配给单个用户。

本教程还包括一看扩展 CreateUserWizard 控件以包含`WizardStep`指定新建的用户的角色。 此类步骤可以帮助管理员简化创建新用户的用户帐户的过程。

现在我们已了解如何创建和删除角色以及如何添加和删除角色的用户。 但我们还未以看看应用基于角色的授权。 在中<a id="_msoanchor_6"> </a>[以下教程](role-based-authorization-cs.md)我们将了解基于角色的角色定义 URL 授权规则以及如何基于当前登录的用户的角色来限制页级别的功能。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 网站管理工具概述](https://msdn.microsoft.com/library/ms228053.aspx)
- [正在检查 ASP。NET 的成员资格、 角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [滚动你自己的网站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>关于作者

自 1998 年以来，Scott Mitchell，多部 asp/ASP.NET 书籍的作者及 4GuysFromRolla.com 的已从事 Microsoft Web 技术工作。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是 *[Sams Teach 自己 ASP.NET 2.0 24 小时内](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在达到 Scott [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢...

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](creating-and-managing-roles-cs.md)
> [下一页](role-based-authorization-cs.md)
