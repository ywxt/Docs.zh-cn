---
uid: web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
title: 存储其他用户信息 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将通过构建一个非常基本的访客留言簿应用程序来回答此问题。 在此过程中，我们将查看 modeli 的不同选项...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/18/2008
ms.topic: article
ms.assetid: 1642132a-1ca5-4872-983f-ab59fc8865d3
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
msc.type: authoredcontent
ms.openlocfilehash: 201215683253afc0c6521e1bef56685d8487d7c7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398846"
---
<a name="storing-additional-user-information-c"></a>存储其他用户信息 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_08_CS.zip)或[下载 PDF](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial08_ExtraUserInfo_cs.pdf)

> 在本教程中我们将通过构建一个非常基本的访客留言簿应用程序来回答此问题。 这样，我们将看看不同的选项来建模在数据库中，用户信息，然后了解如何将此数据与成员资格框架创建的用户帐户相关联。


## <a name="introduction"></a>介绍

ASP。NET 的成员资格框架提供了一个灵活的管理用户界面。 成员资格 API 包括用于验证凭据、 检索有关当前已登录用户的信息、 创建新的用户帐户，和删除用户帐户，以及其他方法。 在成员资格框架中的每个用户帐户包含仅用于验证凭据和执行基本的用户帐户相关的任务所需的属性。 这众多的方法和属性[`MembershipUser`类](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)，该模型成员资格框架中的用户帐户。 此类具有属性，如[ `UserName` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.username.aspx)， [ `Email` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.email.aspx)，以及[ `IsLockedOut` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx)，并等方法[ `GetPassword` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.getpassword.aspx)并[ `UnlockUser` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)。

通常，应用程序需要存储其他用户信息未包含在成员资格框架。 例如，在线零售商可能需要让每个用户存储其装运和帐单地址、 付款信息、 传递首选项和联系人电话号码。 此外，在系统中的每个订单都与特定用户帐户相关联。

`MembershipUser`类不包括属性，如`PhoneNumber`或`DeliveryPreferences`或`PastOrders`。 我们因此如何跟踪所需的应用程序的用户信息并将其与成员资格框架集成？ 在本教程中我们将通过构建一个非常基本的访客留言簿应用程序来回答此问题。 这样，我们将看看不同的选项来建模在数据库中，用户信息，然后了解如何将此数据与成员资格框架创建的用户帐户相关联。 让我们进入正题！

## <a name="step-1-creating-the-guestbook-applications-data-model"></a>步骤 1： 创建访客留言簿应用程序的数据模型

有各种技术，可用来捕获数据库中的用户信息并将其与成员资格框架创建的用户帐户相关联。 为了说明了这些方法，我们将需要补充的教程的 web 应用程序，以便捕获某种类型的与用户相关数据。 (目前，应用程序的数据模型包含应用程序服务所需的表仅`SqlMembershipProvider`。)

让我们创建一个非常简单访客留言簿应用程序，其中身份验证的用户都可以发表评论。 除了存储访客留言簿注释，让我们允许每个用户存储其家乡、 主页和签名。 如果提供，用户的主城镇主页和签名会出现在他离开访客留言簿中的每个消息。

### <a name="adding-theguestbookcommentstable"></a>添加`GuestbookComments`表

为了捕获访客留言簿注释，我们需要创建一个名为的数据库表`GuestbookComments`具有类似的列`CommentId`， `Subject`， `Body`，和`CommentDate`。 我们还需要在每个记录`GuestbookComments`表引用添加注释的用户。

若要将此表添加到我们的数据库，请转到 Visual Studio 中的数据库资源管理器和向下钻取到`SecurityTutorials`数据库。 右键单击表文件夹并选择添加新表。 此时会打开一个接口，可用于定义新的表的列。


[![将新表添加到 SecurityTutorials 数据库](storing-additional-user-information-cs/_static/image2.png)](storing-additional-user-information-cs/_static/image1.png)

**图 1**： 添加一个新表格`SecurityTutorials`数据库 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image3.png))


接下来，定义`GuestbookComments`的列。 首先，通过添加一个名为列`CommentId`类型的`uniqueidentifier`。 此列将唯一地标识访客留言簿中的每个注释，因此不允许`NULL`s 并将其标记为表的主键。 而不是提供值`CommentId`每个字段`INSERT`，我们可以指示新`uniqueidentifier`值应为自动生成此字段上`INSERT`列的默认值设置为`NEWID()`。 添加此第一个字段，将其标记为主键，并设置为其默认值后, 你的屏幕应类似于屏幕截图中图 2 所示。


[![添加一个名为 CommentId 的主列](storing-additional-user-information-cs/_static/image5.png)](storing-additional-user-information-cs/_static/image4.png)

**图 2**： 添加主列命名为`CommentId`([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image6.png))


接下来，添加名为的列`Subject`类型的`nvarchar(50)`和名为的列`Body`类型的`nvarchar(MAX)`、 不允许`NULL`这两个列。 接下来，添加名为的列`CommentDate`类型的`datetime`。 不允许`NULL`s 和集`CommentDate`列的默认值为`getdate()`。

所有的就是要添加的列的每个访客留言簿注释相关联的用户帐户。 一种方法是添加名为的列`UserName`类型的`nvarchar(256)`。 这是一个合适的选择，而不使用成员资格提供程序时`SqlMembershipProvider`。 但使用时`SqlMembershipProvider`，如本系列教程，我们非常`UserName`中的列`aspnet_Users`表不能保证是唯一的。 `aspnet_Users`表的主键是`UserId`且类型`uniqueidentifier`。 因此，`GuestbookComments`表需要名为的列`UserId`类型的`uniqueidentifier`(不允许`NULL`值)。 请继续并添加此列。

> [!NOTE]
> 如中所述[ *SQL Server 中创建成员身份架构*](creating-the-membership-schema-in-sql-server-cs.md)教程中，成员资格框架为了让多个 web 应用程序使用不同的用户帐户共享相同用户存储区。 通过划分到不同的应用程序用户帐户来执行此操作。 尽管每个用户名保证是唯一的应用程序中，可能会在不同的应用程序使用相同的用户存储中使用相同的用户名。 没有复合`UNIQUE`中的约束`aspnet_Users`表`UserName`和`ApplicationId`字段，但不是一个在只需`UserName`字段。 因此，很可能 aspnet\_用户表中包含具有相同的两个 （或多个） 记录`UserName`值。 不过，还有`UNIQUE`约束`aspnet_Users`表的`UserId`字段 （因为它是主键）。 一个`UNIQUE`约束非常重要，因为没有它，我们无法建立之间的外键约束`GuestbookComments`和`aspnet_Users`表。


添加后`UserId`列中，保存对表进行单击工具栏中的保存图标。 命名新表， `GuestbookComments`。

我们有一个问题要注意与`GuestbookComments`表： 我们需要创建[外键约束](https://msdn.microsoft.com/library/ms175464.aspx)之间`GuestbookComments.UserId`列和`aspnet_Users.UserId`列。 若要实现此目的，请单击工具栏以启动外键关系对话框中的关系图标。 （或者，你可以启动此对话框中通过转到表设计器菜单并选择关系。）

单击外键关系对话框左下角中的添加按钮。 尽管我们仍需要在关系中定义参与的表，这将添加新的外键约束。


[![使用外键关系对话框中管理表的外键约束](storing-additional-user-information-cs/_static/image8.png)](storing-additional-user-information-cs/_static/image7.png)

**图 3**： 使用外键关系对话框中管理表的外键约束 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image9.png))


接下来，单击右侧的"表和列规范"行中的省略号图标。 这将启动表和列对话框，从中我们可以指定主键表和列和外的键列从`GuestbookComments`表。 具体而言，选择`aspnet_Users`并`UserId`作为主键表和列，并`UserId`从`GuestbookComments`表作为外键列 （请参阅图 4）。 在定义的主键和外键表和列之后, 单击确定以返回到外键关系对话框中。


[![建立外键约束之间 aspnet_Users 和 GuesbookComments 表](storing-additional-user-information-cs/_static/image11.png)](storing-additional-user-information-cs/_static/image10.png)

**图 4**: 外键约束之间建立`aspnet_Users`并`GuesbookComments`表 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image12.png))


此时已建立的外键约束。 是否存在此约束可确保[关系完整性](http://en.wikipedia.org/wiki/Referential_integrity)之间通过确保永远不会将存在引用不存在的用户帐户的访客留言簿项的两个表。 默认情况下，如果那里相应的子记录要删除的父记录将不允许的外键约束。 也就是说，如果用户发出一个或多个访客留言簿注释，然后我们尝试删除该用户帐户，删除将失败，除非他访客留言簿注释会最先删除。

外键约束可以配置为删除父记录时自动删除关联的子记录。 换而言之，我们可以设置该外键约束，以便删除其用户帐户时，会自动删除用户的留言簿条目。 若要实现此目的，展开"INSERT 和 UPDATE 规范"部分，并将"删除规则"属性设置为 Cascade。


[![配置为级联删除的外键约束](storing-additional-user-information-cs/_static/image14.png)](storing-additional-user-information-cs/_static/image13.png)

**图 5**： 配置为级联删除外键约束 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image15.png))


若要保存的外键约束，请单击关闭按钮退出外键关系。 然后单击保存图标以保存对表和此工具栏中的关系。

### <a name="storing-the-users-home-town-homepage-and-signature"></a>存储用户的主页城镇、 主页和签名

`GuestbookComments`表说明了如何存储用户帐户与共享一个对多关系的信息。 每个用户帐户可能具有任意数目的关联的注释，因为此关系是通过创建一个表以保存包含列链接到特定用户返回每个注释的注释集建模。 使用时`SqlMembershipProvider`，通过创建一个名为列最建立此链接`UserId`类型的`uniqueidentifier`和此列之间的外键约束和`aspnet_Users.UserId`。

我们现在需要将三个列与用于存储用户的主城镇、 主页和签名，它将显示在自己的访客留言簿建议每个用户帐户相关联。 有多种不同方法来实现此目的：

- <strong>添加新的列</strong><strong>`aspnet_Users`</strong><strong>或</strong><strong>`aspnet_Membership`</strong><strong>表。</strong> 我不会建议这种方法，因为它修改所用架构`SqlMembershipProvider`。 此决策可能会回来言词您这个过程中。 例如，如果 ASP.NET 的未来版本使用不同时`SqlMembershipProvider`架构。 Microsoft 可能包括一个工具，可将 ASP.NET 2.0 迁移`SqlMembershipProvider`到新的架构，但如果您已修改 ASP.NET 2.0 数据`SqlMembershipProvider`架构，这种转换不可能。

- **使用 ASP。NET 的配置文件框架定义主城镇、 主页和签名的配置文件属性。** ASP.NET 包括一个配置文件框架，用于存储其他特定于用户的数据。 成员资格框架，如配置文件框架构建提供程序模型之上。 .NET Framework 附带`SqlProfileProvider`都在 SQL Server 数据库中存储配置文件数据。 事实上，我们的数据库已使用的表`SqlProfileProvider`(`aspnet_Profile`)，如时我们添加了应用程序服务后重新添加它<a id="_msoanchor_2"> </a> [*在 SQL 中创建成员身份架构服务器*](creating-the-membership-schema-in-sql-server-cs.md)教程。   
  配置文件框架的主要优点是，它允许开发人员定义中的配置文件属性`Web.config`– 没有代码需要写入序列化到和从基础数据存储区的配置文件数据。 简单地说，是极其简便的方式来定义一组配置文件属性并在代码中使用它们。 但是，个人资料系统会留下很多以将所需的谈到版本控制，因此，如果其中期望新特定于用户的属性添加在更高版本时或现有功能，可删除或修改，则可能不是配置文件框架的应用程序 最佳选项。 此外，`SqlProfileProvider`以高度非规范化的方式，使其下一步，几乎不可能直接对配置文件数据 （例如，多少用户拥有 New York 家庭城镇） 运行查询存储的配置文件属性。   
  配置文件框架的详细信息，请在本教程末尾查阅"进一步读数"部分。

- <strong>将这三列添加到数据库中的新表并建立此表之间的一对一关系并</strong><strong>`aspnet_Users`</strong><strong>。</strong> 这种方法涉及到比使用配置文件框架的更多工作，但在如何在数据库中建模的其他用户属性的最大灵活性。 这是我们将在本教程中使用的选项。

我们将创建一个名为的新表`UserProfiles`以保存家庭城镇、 主页，并为每个用户的签名。 右键单击数据库资源管理器窗口中的表文件夹并选择创建新表。 命名的第一列`UserId`并将其类型设置为`uniqueidentifier`。 不允许`NULL`值，并将标记为主键列。 接下来，添加名为的列：`HomeTown`类型的`nvarchar(50)`;`HomepageUrl`类型的`nvarchar(100)`; 和类型的签名`nvarchar(500)`。 这三列的每个可接受`NULL`值。


[![创建在 UserProfiles 表](storing-additional-user-information-cs/_static/image17.png)](storing-additional-user-information-cs/_static/image16.png)

**图 6**： 创建`UserProfiles`表 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image18.png))


保存该表并将其命名为`UserProfiles`。 最后，建立之间的外键约束`UserProfiles`表的`UserId`字段和`aspnet_Users.UserId`字段。 正如我们之间的外键约束与做`GuestbookComments`和`aspnet_Users`表，有级联删除此约束。 由于`UserId`字段中`UserProfiles`是主数据库密钥，这可确保将中的多个记录`UserProfiles`每个用户帐户的表。 这种关系称为为一对一。

现在，我们已创建的数据模型，我们就可以使用它。 步骤 2 和 3 中将探讨如何当前登录的用户可以查看和编辑其家庭的城镇、 主页和签名信息。 在步骤 4 中，我们将创建经过身份验证的用户可以提交访客留言簿的新评论并查看现有的接口。

## <a name="step-2-displaying-the-users-home-town-homepage-and-signature"></a>步骤 2： 显示用户的主页城镇、 主页和签名

有多种方式以允许当前登录的用户可以查看和编辑其家庭的城镇、 主页和签名信息。 我们可以手动创建用户界面使用文本框和标签控件，或者我们可以使用一种数据 Web 控件，如 DetailsView 控件。 若要执行的数据库`SELECT`和`UPDATE`语句我们可以编写 ADO.NET 代码在我们的页面代码隐藏类中，或者，或者，使用声明性的方法与 SqlDataSource。 理想情况下我们的应用程序将包含分层体系结构，我们可以调用以编程方式从页面的代码隐藏类或以声明方式通过对象数据源控件。

由于本系列教程着重于窗体身份验证、 授权、 用户帐户和角色，将不会有这些不同的数据访问选项或分层体系结构为何通过直接执行 SQL 语句是首选的全面讨论从 ASP.NET 页中。 我将引导完成使用 DetailsView 和 SqlDataSource – 最快且最简单选项 – 但当然，要讨论的概念可应用于备用 Web 控件和数据访问逻辑。 有关如何使用 ASP.NET 中的数据的详细信息，请参阅我*[使用 ASP.NET 2.0 中的数据](../../data-access/index.md)* 系列教程。

打开`AdditionalUserInfo.aspx`页中`Membership`文件夹并将的 DetailsView 控件添加到页上，设置其`ID`属性设置为`UserProfile`并清除其`Width`和`Height`属性。 展开 DetailsView 的智能标记，并选择将其绑定到新的数据源控件。 这将启动数据源配置向导 （请参阅图 7）。 第一步会要求您指定的数据源类型。 由于我们要直接连接到`SecurityTutorials`数据库，则选择数据库图标，指定`ID`作为`UserProfileDataSource`。


[![添加名为 UserProfileDataSource 新 SqlDataSource 控件](storing-additional-user-information-cs/_static/image20.png)](storing-additional-user-information-cs/_static/image19.png)

**图 7**： 添加新 SqlDataSource 控件命名`UserProfileDataSource`([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image21.png))


下一个屏幕会提示输入要使用的数据库。 我们已定义中的连接字符串`Web.config`为`SecurityTutorials`数据库。 此连接字符串名称 – `SecurityTutorialsConnectionString` – 应出现在下拉列表中。 选择此选项，然后单击下一步。


[![从下拉列表中选择 SecurityTutorialsConnectionString](storing-additional-user-information-cs/_static/image23.png)](storing-additional-user-information-cs/_static/image22.png)

**图 8**： 选择`SecurityTutorialsConnectionString`从下拉列表 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image24.png))


后续屏幕要求我们指定的表和查询的列。 选择`UserProfiles`表从下拉列表，并检查的所有列。


[![自带的所有列将从在 UserProfiles 表](storing-additional-user-information-cs/_static/image26.png)](storing-additional-user-information-cs/_static/image25.png)

**图 9**： 将返回所有的中的列`UserProfiles`表 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image27.png))


图 9 返回中的当前查询*所有*中记录的`UserProfiles`，但我们只是对当前登录的用户的记录。 若要添加`WHERE`子句中，单击`WHERE`按钮以打开添加`WHERE`子句对话框 （请参阅图 10）。 在此处可以选择要作为筛选依据的列、 运算符和筛选器参数的源。 选择`UserId`作为列并选择"="与运算符。

遗憾的是没有任何内置参数源将返回当前登录的用户的`UserId`值。 我们将需要以编程方式获取此值。 因此，设置为"None、 单击添加按钮以添加参数，然后单击确定的源下拉列表。


[![上 UserId 列添加筛选器参数](storing-additional-user-information-cs/_static/image29.png)](storing-additional-user-information-cs/_static/image28.png)

**图 10**： 上添加筛选器参数`UserId`列 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image30.png))


单击确定后您将返回到图 9 中所示的屏幕。 这一次，但是，在屏幕底部的 SQL 查询应包括`WHERE`子句。 单击下一步以转到"测试查询"屏幕。 您可以在此处运行的查询，并查看结果。 单击完成以完成向导。

完成之后数据源配置向导，Visual Studio 创建 SqlDataSource 控件根据在向导中指定的设置。 此外，它将 BoundFields 手动添加到每个列返回的 SqlDataSource 的 DetailsView `SelectCommand`。 无需显示`UserId`字段中 DetailsView，因为用户无需知道此值。 可以直接从 DetailsView 控件声明性标记中删除此字段，或单击"编辑字段"链接从其智能标记。

此时页面的声明性标记应类似于下面：

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample1.aspx)]

我们需要以编程方式设置 SqlDataSource 控件`UserId`参数对当前登录用户的`UserId`之前选择的数据。 这可以通过为 SqlDataSource 创建事件处理程序来实现`Selecting`那里事件并添加以下代码：

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample2.cs)]

上面的代码首先会通过调用获取对当前登录用户的引用`Membership`类的`GetUser`方法。 这将返回`MembershipUser`对象，其`ProviderUserKey`属性包含`UserId`。 `UserId`值然后分配给 SqlDataSource`@UserId`参数。

> [!NOTE]
> `Membership.GetUser()`方法将返回有关当前已登录用户的信息。 如果匿名用户访问的页面，它将返回值为`null`。 在这种情况下，这将导致`NullReferenceException`代码尝试读取时在下一行`ProviderUserKey`属性。 当然，我们无需担心`Membership.GetUser()`返回`null`中的值`AdditionalUserInfo.aspx`页，因为我们在上一教程中配置 URL 授权，以便只有经过身份验证的用户无法访问此文件夹中的 ASP.NET 资源。 如果需要访问有关允许进行匿名访问的页面中的当前登录用户的信息，请务必检查非`null MembershipUser`对象返回从`GetUser()`方法，然后才能引用它的属性。


如果您访问`AdditionalUserInfo.aspx`页上通过浏览器则将看到一个空白页，因为我们尚未添加到任何行`UserProfiles`表。 在步骤 6 中我们将介绍如何自定义 CreateUserWizard 控件可自动将添加到一个新行`UserProfiles`表时创建一个新的用户帐户。 现在，但是，我们将需要手动创建一条记录表中。

导航到 Visual Studio 中的数据库资源管理器并展开表文件夹。 右键单击`aspnet_Users`表并选择"显示表数据"以查看表中的记录; 执行相同的操作`UserProfiles`表。 图 11 显示了这些结果时垂直平铺。 在我的数据库中当前有`aspnet_Users`Bruce、 Fred，和 Tito，记录但中的没有记录`UserProfiles`表。


[![显示 aspnet_Users 的内容和 UserProfiles 表](storing-additional-user-information-cs/_static/image32.png)](storing-additional-user-information-cs/_static/image31.png)

**图 11**： 内容`aspnet_Users`并`UserProfiles`将显示表 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image33.png))


添加到新的记录`UserProfiles`通过手动输入的值中的表`HomeTown`， `HomepageUrl`，和`Signature`字段。 获取一个有效的最简单办法`UserId`中的新值`UserProfiles`记录是选择`UserId`字段中的特定用户帐户从`aspnet_Users`表，复制并将其粘贴到`UserId`字段中`UserProfiles`。 图 12 显示了`UserProfiles`表后为 Bruce 添加一条新记录。


[![记录有关 Bruce 已添加到 UserProfiles](storing-additional-user-information-cs/_static/image35.png)](storing-additional-user-information-cs/_static/image34.png)

**图 12**: A 记录添加到`UserProfiles`为 Bruce ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image36.png))


返回到`AdditionalUserInfo.aspx`页上，以 Bruce 身份登录。 如图 13 所示，会显示 Bruce 的设置。


[![当前访问用户是所示。 他设置](storing-additional-user-information-cs/_static/image38.png)](storing-additional-user-information-cs/_static/image37.png)

**图 13**: 当前访问用户是所示。 他设置 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image39.png))


> [!NOTE]
> 手动添加中的记录`UserProfiles`表为每个成员资格用户。 在步骤 6 中我们将介绍如何自定义 CreateUserWizard 控件可自动将添加到一个新行`UserProfiles`表时创建一个新的用户帐户。


## <a name="step-3-allowing-the-user-to-edit-his-home-town-homepage-and-signature"></a>步骤 3： 允许用户编辑他的主页城镇、 主页和签名

当前登录的用户现在可以查看其家乡、 主页和签名设置，但它们尚不能修改它们。 让我们更新 DetailsView 控件，以便可以编辑数据。

我们需要做的第一件事是添加`UpdateCommand`SqlDataSource，用于指定`UPDATE`要执行的语句以及其对应的参数。 选择 SqlDataSource，并从属性窗口中，单击要打开命令和参数编辑器对话框中的 UpdateQuery 属性旁边的省略号。 输入以下`UPDATE`到文本框的语句：

[!code-sql[Main](storing-additional-user-information-cs/samples/sample3.sql)]

接下来，单击"刷新参数"按钮，将创建 SqlDataSource 控件中的参数`UpdateParameters`集合中的参数的每个`UPDATE`语句。 保留所有参数集的源为无，然后单击确定按钮以完成对话框。


[![指定 SqlDataSource UpdateCommand 和 UpdateParameters](storing-additional-user-information-cs/_static/image41.png)](storing-additional-user-information-cs/_static/image40.png)

**图 14**： 指定 SqlDataSource`UpdateCommand`并`UpdateParameters`([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image42.png))


由于添加了内容我们做 SqlDataSource 控件，DetailsView 控件现在支持编辑。 在 DetailsView 的智能标记中，选中"启用编辑"复选框。 这将添加到控件的 CommandField`Fields`集合，其`ShowEditButton`属性设置为 True。 在 DetailsView 显示在只读模式和更新和取消按钮时显示在编辑模式时，这会使编辑按钮。 不需要用户单击编辑，不过，我们可以 DetailsView 呈现"始终可编辑"状态中通过设置 DetailsView 控件[`DefaultMode`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode.aspx)到`Edit`。

这些更改，DetailsView 控件的声明性标记应类似于下面：

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample4.aspx)]

请注意添加的 CommandField 和`DefaultMode`属性。

继续操作并测试通过浏览器的此页。 使用具有相应的记录中的用户访问时`UserProfiles`，可编辑界面中显示的用户的设置。


[![在 DetailsView 呈现一个可编辑接口](storing-additional-user-information-cs/_static/image44.png)](storing-additional-user-information-cs/_static/image43.png)

**图 15**: DetailsView 呈现一个可编辑的接口 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image45.png))


请尝试更改这些值并单击更新按钮。 它会显示像没有任何反应。 没有为在回发和值保存到数据库，但没有保存发生任何可视反馈。

若要解决此问题，返回到 Visual Studio，并添加 DetailsView 上方的一个标签控件。 设置其`ID`到`SettingsUpdatedMessage`，将其`Text`属性设置为"已更新您的设置"，并将其`Visible`并`EnableViewState`属性设置为`false`。

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample5.aspx)]

我们需要显示`SettingsUpdatedMessage`标记每次更新 DetailsView 时。 若要实现此目的，创建一个事件处理程序 DetailsView`ItemUpdated`事件，并添加以下代码：

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample6.cs)]

返回到`AdditionalUserInfo.aspx`逐页浏览器查看和更新数据。 这次，将显示有用的状态消息。


[![一条短消息是更新显示时设置](storing-additional-user-information-cs/_static/image47.png)](storing-additional-user-information-cs/_static/image46.png)

**图 16**： 更新的设置时，显示短消息 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image48.png))


> [!NOTE]
> DetailsView 控件的编辑界面使许多需要改进。 它使用标准大小的文本框，但签名字段可能是多行文本框。 RegularExpressionValidator 应该用于确保主页 URL，如果输入，以"http://"或"https://"开头。 此外，由于 DetailsView 控件具有其`DefaultMode`属性设置为`Edit`，取消按钮不会执行任何操作。 它应是删除或，单击时，将用户重定向到其他页面上 (如`~/Default.aspx`)。 我将这些增强功能作为练习留给读者。


### <a name="adding-a-link-to-theadditionaluserinfoaspxpage-in-the-master-page"></a>添加一个指向`AdditionalUserInfo.aspx`母版页中的页

目前，该网站不提供任何指向`AdditionalUserInfo.aspx`页。 若要访问它的唯一方法是直接在浏览器地址栏中输入该页面的 URL。 让我们将链接添加到中的此页面`Site.master`母版页。

回想一下母版页包含 LoginView Web 控件在其`LoginContent`ContentPlaceHolder 为经过身份验证和匿名访问者将显示不同的标记。 更新 LoginView 控件`LoggedInTemplate`可包括指向链接`AdditionalUserInfo.aspx`页。 以后进行这些更改 LoginView 控件的声明性标记看起来应类似于下面：

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample7.aspx)]

请注意添加`lnkUpdateSettings`超链接控件到`LoggedInTemplate`。 与此链接后，身份验证的用户可以快速跳转到页后，可以查看和修改其家庭的城镇、 主页和签名设置。

## <a name="step-4-adding-new-guestbook-comments"></a>步骤 4： 添加新访客留言簿注释

`Guestbook.aspx`页，身份验证的用户可以查看访客留言簿和发表评论。 让我们开始创建要添加新访客留言簿注释的接口。

打开`Guestbook.aspx`页在 Visual Studio 中，构造包含两个 TextBox 控件、 新注释的使用者和其主体的用户界面。 设置第一个文本框控件的`ID`属性设置为`Subject`并将其`Columns`为 40 的属性; 设置的秒`ID`到`Body`，将其`TextMode`到`MultiLine`，并将其`Width`和`Rows`为"95%"和 8 中，属性分别。 若要完成的用户界面，添加名为的 Button Web 控件`PostCommentButton`并设置其`Text`属性设置为"发表您的评论"。

由于每个访客留言簿注释要求主题和正文，请为每个文本框添加一个 RequiredFieldValidator。 设置`ValidationGroup`属性的这些控件，以便"EnterComment"; 同样，设置`PostCommentButton`控件的`ValidationGroup`属性设置为"EnterComment"。 有关 ASP 的详细信息。NET 的验证控件，请查看[在 ASP.NET 中的窗体验证](http://www.4guysfromrolla.com/webtech/090200-1.shtml)，[仔细分析 ASP.NET 2.0 中的验证控件](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)，并[验证服务器控件教程](http://www.w3schools.com/aspnet/aspnet_refvalidationcontrols.asp)上[W3Schools](http://www.w3schools.com/)。

以后创建的用户界面页面的声明性标记看起来应类似于以下内容：

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample8.aspx)]

用户界面完成后，我们的下一个任务是插入新记录到`GuestbookComments`表`PostCommentButton`单击。 这可以通过多种方式实现： 我们可以编写 ADO.NET 代码中的按钮`Click`事件处理程序; 我们可以将 SqlDataSource 控件添加到页，配置其`InsertCommand`，，然后调用其`Insert`方法从`Click`事件处理程序;或者，我们可以生成负责插入新访客留言簿注释，中间层，调用此功能从`Click`事件处理程序。 由于我们在步骤 3 中使用 SqlDataSource，让我们此处使用的 ADO.NET 代码。

> [!NOTE]
> 用来以编程方式访问数据从 Microsoft SQL Server 数据库的 ADO.NET 类位于`System.Data.SqlClient`命名空间。 可能需要将此命名空间导入页面的代码隐藏类 (即， `using System.Data.SqlClient;`)。


创建事件处理程序`PostCommentButton`的`Click`事件，并添加以下代码：

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample9.cs)]

`Click`事件处理程序首先会检查该用户提供的数据是否有效。 如果不是这样，插入记录之前就存在的事件处理程序。 假设所提供的数据是否有效，当前登录的用户`UserId`检索值并将其存储在`currentUserId`本地变量。 需要此值，因为我们必须提供`UserId`值时插入到记录`GuestbookComments`。

接下来，连接字符串为`SecurityTutorials`从数据库检索`Web.config`和`INSERT`指定 SQL 语句。 一个`SqlConnection`对象然后创建并打开。 下一步，`SqlCommand`构造对象和参数的值中使用`INSERT`分配查询。 `INSERT`然后执行语句和连接关闭。 在事件处理程序末尾`Subject`并`Body`文本框`Text`属性，以便不会在回发之间保留用户的值会清除。

请继续并查看此页在浏览器中测试。 因为此页处于`Membership`文件夹不能由匿名访问者访问。 因此，需要第一次登录 （如果还没有）。 输入一个值`Subject`并`Body`文本框，单击`PostCommentButton`按钮。 这将导致新记录添加到`GuestbookComments`。 在回发时，从文本框擦除的主题和正文提供。

单击后`PostCommentButton`有按钮是不可视反馈的注释已添加到访客留言簿。 我们仍需要更新此页显示现有访客留言簿注释，我们将在步骤 5 中执行操作。 一旦我们完成此操作，刚添加的注释将显示在列表中的注释，提供足够的可视反馈。 现在，确认访客留言簿注释已通过检查的内容保存`GuestbookComments`表。

图 17 显示了的内容`GuestbookComments`表后都没有这两个注释。


[![可以看到 GuestbookComments 表中的访客留言簿注释](storing-additional-user-information-cs/_static/image50.png)](storing-additional-user-information-cs/_static/image49.png)

**图 17**： 您所见中的访客留言簿注释`GuestbookComments`表 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image51.png))


> [!NOTE]
> 如果用户尝试插入访客留言簿注释可能包含危险标记 – 例如 HTML – ASP.NET 将引发`HttpRequestValidationException`。 若要了解有关此异常，引发原因，以及如何允许用户提交具有潜在危险值的详细信息，请查阅[请求验证白皮书](../../../../whitepapers/request-validation.md)。


## <a name="step-5-listing-the-existing-guestbook-comments"></a>步骤 5： 列出现有的访客留言簿注释

除了使用户访问的注释，`Guestbook.aspx`页还应该能够查看访客留言簿的现有注释。 若要完成此操作，将添加一个名为 ListView 控件`CommentList`到页面底部。

> [!NOTE]
> ListView 控件是刚刚接触 ASP.NET 3.5 版。 这被为了在非常可自定义和灵活布局中，显示的项的列表，但仍提供内置编辑、 插入、 删除、 分页和排序功能，如 GridView。 如果使用的 ASP.NET 2.0，您将需要改为使用 DataList 或 Repeater 控件。 使用 ListView 的详细信息，请参阅[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章[asp: ListView 控件](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)，和我的文章[与 ListView 控件显示数据](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)。


打开 ListView 的智能标记，并从选择数据源下拉列表，请将控件绑定到新的数据源。 步骤 2 中可以看到，这将启动数据源配置向导。 选择数据库图标，将命名生成 SqlDataSource `CommentsDataSource`，单击确定。 接下来，选择`SecurityTutorialsConnectionString`连接字符串从下拉列表，并单击下一步。

此时在步骤 2 中我们指定查询的数据选择`UserProfiles`表从下拉列表并选择要返回的列 （回头查看图 9）。 这一次，但是，我们想要创建一条 SQL 语句不只从记录会提取`GuestbookComments`，但还注释器的家庭城镇、 主页、 签名和用户名。 因此，选择"指定自定义 SQL 语句或存储的过程"单选按钮，然后单击下一步。

此时会弹出"定义自定义语句或存储过程"屏幕。 单击查询生成器按钮以图形方式生成查询。 查询生成器首先会提示我们指定我们想要从查询的表。 选择`GuestbookComments`， `UserProfiles`，和`aspnet_Users`表并单击确定。 这会将所有三个表添加到设计图面。 由于没有彼此之间的外键约束`GuestbookComments`， `UserProfiles`，并`aspnet_Users`表，查询生成器会自动`JOIN`s 这些表。

剩下的就是以指定要返回的列。 从`GuestbookComments`表选择`Subject`， `Body`，和`CommentDate`列; 返回`HomeTown`， `HomepageUrl`，以及`Signature`中的列`UserProfiles`表;，然后返回`UserName`从`aspnet_Users`. 此外，添加"`ORDER BY CommentDate DESC`"到末尾`SELECT`查询，以便首先返回最新文章。 做出这些选择后，查询生成器界面应类似于屏幕快照中图 18。


[![将构造的查询联接 GuestbookComments、 UserProfiles 和 aspnet_Users 表](storing-additional-user-information-cs/_static/image53.png)](storing-additional-user-information-cs/_static/image52.png)

**图 18**: 构造查询`JOIN`s `GuestbookComments`， `UserProfiles`，并`aspnet_Users`表 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image54.png))


单击确定以关闭查询生成器窗口并返回到"定义自定义语句或存储过程"屏幕。 单击转到"测试查询"屏幕上，您可以通过单击测试查询按钮查看查询结果旁边。 在准备就绪时，单击完成以完成配置数据源向导。

当我们完成步骤 2，关联的 DetailsView 控件中的配置数据源向导`Fields`集合已更新为包括每一列返回 BoundField `SelectCommand`。 ListView，但是，保持不变;我们仍需要定义其布局。 通过其声明性标记或从其智能标记中的"配置 ListView"选项，可以手动构造 ListView 的布局。 我通常更喜欢手动，定义标记，但使用无论何种方式是最自然。

我最终使用以下`LayoutTemplate`， `ItemTemplate`，和`ItemSeparatorTemplate`我 ListView 控件：

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample10.aspx)]

`LayoutTemplate`定义的标记发出的控件，而`ItemTemplate`呈现 SqlDataSource 所返回每个项。 `ItemTemplate`的所得的标记将置于`LayoutTemplate`的`itemPlaceholder`控件。 除了`itemPlaceholder`，则`LayoutTemplate`包括限制为显示每个页面 （默认值） 的 10 个访客留言簿注释 ListView 的 DataPager 控件和呈现分页界面。

我`ItemTemplate`显示在每个访客留言簿注释的使用者`<h4>`使用以下主题位于正文的元素。 请注意显示正文所用的语法采用返回的数据`Eval("Body")`数据绑定语句，将其转换为一个字符串，并替换其中的换行符使用`<br />`元素。 此转换需要才能显示输入提交注释，因为 html 忽略空格时换行。 下面以斜体显示，用户的家乡，他的主页、 日期和时间进行注释，以及添加注释的人员的用户名的链接后跟正文显示用户的签名。

花点时间查看通过浏览器页面。 应会看到添加到此处显示的步骤 5 中访客留言簿的注释。


[![Guestbook.aspx 现在显示访客留言簿的备注](storing-additional-user-information-cs/_static/image56.png)](storing-additional-user-information-cs/_static/image55.png)

**图 19**:`Guestbook.aspx`现在显示访客留言簿的备注 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image57.png))


请尝试将新的注释添加到访客留言簿。 单击时`PostCommentButton`按钮页回发和注释添加到数据库，但 ListView 控件将不更新以显示新的注释。 这可通过以下任一方法来解决：

- 正在更新`PostCommentButton`按钮的`Click`事件处理程序，使其调用 ListView 控件的`DataBind()`方法之后将新的注释插入到数据库，或
- 设置 ListView 控件的`EnableViewState`属性设置为`false`。 这种方法有效，因为通过禁用控件的视图状态，它必须重新绑定到基础数据在每次回发。

教程的网站可从本教程说明了这两种技术。 ListView 控件的`EnableViewState`属性设置为`false`并以编程方式重新绑定到 ListView 的数据所需的代码存在`Click`事件处理程序，但已被注释掉。

> [!NOTE]
> 当前`AdditionalUserInfo.aspx`页允许用户查看和编辑其家庭的城镇、 主页和签名设置。 可能会令人高兴更新`AdditionalUserInfo.aspx`以显示已登录用户的访客留言簿注释中。 也就是说，除了检查和修改她的信息，用户可以访问`AdditionalUserInfo.aspx`页以查看哪些访客留言簿注释她由在过去。 我将此作为练习留给感读取器。


## <a name="step-6-customizing-the-createuserwizard-control-to-include-an-interface-for-the-home-town-homepage-and-signature"></a>步骤 6： 自定义 CreateUserWizard 控件以包含主页城镇、 主页和签名的接口

`SELECT`使用的查询`Guestbook.aspx`页上使用`INNER JOIN`组合之间的相关的记录`GuestbookComments`， `UserProfiles`，并`aspnet_Users`表。 如果在具有任何记录的用户`UserProfiles`访客留言簿一个注释，注释不会显示在 ListView，因为`INNER JOIN`仅返回`GuestbookComments`记录中的匹配记录时`UserProfiles`和`aspnet_Users`。 如果用户不具有一条记录可以在步骤 3 中看到`UserProfiles`她无法查看或编辑在她设置`AdditionalUserInfo.aspx`页。

不用说，由于我们的设计的决策非常重要的成员身份系统中每个用户帐户具有匹配记录中`UserProfiles`表。 我们想要为相应的记录添加到`UserProfiles`只要 CreateUserWizard 通过创建新的成员资格用户帐户。

如中所述[*创建用户帐户*](creating-user-accounts-cs.md)教程中，新的成员资格用户帐户创建 CreateUserWizard 控件后引发其[`CreatedUser`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx). 我们可以创建此事件的事件处理程序中，对于刚创建的用户，获取用户 Id，然后插入到的记录`UserProfiles`使用的默认值表`HomeTown`， `HomepageUrl`，和`Signature`列。 更重要的是，则可以通过自定义 CreateUserWizard 控件的界面，以包括其他文本框提示用户输入这些值。

让我们先看看如何将添加到一个新行`UserProfiles`表中`CreatedUser`事件处理程序替换默认值。 接下来，我们将了解如何自定义 CreateUserWizard 控件的用户界面，以包括其他窗体字段，以收集新用户的主城镇、 主页和签名。

### <a name="adding-a-default-row-touserprofiles"></a>添加到默认行`UserProfiles`

在中[*创建用户帐户*](creating-user-accounts-cs.md)教程，我们添加到了 CreateUserWizard 控件`CreatingUserAccounts.aspx`页`Membership`文件夹。 为了获得 CreateUserWizard 控件添加到记录`UserProfiles`表用户帐户创建后，我们需要更新 CreateUserWizard 控件的功能。 而不是进行这些更改`CreatingUserAccounts.aspx`页上，让我们改为添加到新的 CreateUserWizard 控件`EnhancedCreateUserWizard.aspx`页上，并为本教程那里进行的修改。

打开`EnhancedCreateUserWizard.aspx`页上，在 Visual Studio 中并从工具箱拖到页面上拖动 CreateUserWizard 控件。 设置 CreateUserWizard 控件`ID`属性设置为`NewUserWizard`。 如中所述<a id="_msoanchor_5"> </a> [*创建用户帐户*](creating-user-accounts-cs.md)教程，CreateUserWizard 的默认用户界面将提示所需的信息的访问者。 后提供此信息，该控件在内部创建新的用户帐户在成员资格框架中，一切都不需要我们无需编写一行代码。

CreateUserWizard 控件在其工作流期间引发事件的数。 访问者提供的请求信息并提交表单后，最初会触发 CreateUserWizard 控件及其[`CreatingUser`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)。 如果在创建过程中，问题[`CreateUserError`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx)激发; 但是，如果已成功创建用户，则[`CreatedUser`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)引发。 在中<a id="_msoanchor_6"> </a> [*创建用户帐户*](creating-user-accounts-cs.md)教程中，我们创建的事件处理程序`CreatingUser`事件，以确保提供的用户名不包含任何前导或尾随空格，且这些用户名未不显示任何位置在密码。

若要添加中的某一行`UserProfiles`表对于刚创建的用户，我们需要创建的事件处理程序`CreatedUser`事件。 按时间`CreatedUser`已触发事件，已在成员资格框架，使我们能够检索帐户的用户 Id 值中创建的用户帐户。

创建事件处理程序`NewUserWizard`的`CreatedUser`事件，并添加以下代码：

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample11.cs)]

上述代码才会通过检索刚添加的用户帐户的用户 Id。 这通过使用实现`Membership.GetUser(username)`方法以返回有关特定用户，然后使用信息`ProviderUserKey`要检索其用户 Id 属性。 用户在 CreateUserWizard 控件中输入的用户名是可通过其[`UserName`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)。

接下来，从检索连接字符串`Web.config`和`INSERT`指定语句。 所需的 ADO.NET 对象进行实例化和执行此命令。 该代码将分配[ `DBNull` ](https://msdn.microsoft.com/library/system.dbnull.aspx)实例向`@HomeTown`， `@HomepageUrl`，和`@Signature`参数，插入数据库的影响`NULL`值`HomeTown`， `HomepageUrl`，和`Signature`字段。

请访问`EnhancedCreateUserWizard.aspx`通过浏览器页并创建新的用户帐户。 之后执行此操作，返回到 Visual Studio 和检查的内容`aspnet_Users`和`UserProfiles`表 （例如，我们回到在图 12 中所做的那样）。 应会看到在新的用户帐户`aspnet_Users`和相应`UserProfiles`行 (与`NULL`值为`HomeTown`， `HomepageUrl`，并`Signature`)。


[![添加了新的用户帐户和 UserProfiles 记录](storing-additional-user-information-cs/_static/image59.png)](storing-additional-user-information-cs/_static/image58.png)

**图 20**: 新的用户帐户和`UserProfiles`已添加记录 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image60.png))


访问者已提供其新的帐户信息并单击"创建用户"按钮，创建用户帐户并添加一行之后`UserProfiles`表。 CreateUserWizard 然后显示其`CompleteWizardStep`，后者将显示一条成功消息和继续按钮。 单击继续按钮会导致回发，但不执行任何操作，这样用户就可以收到`EnhancedCreateUserWizard.aspx`页。

我们可以指定要向用户发送到通过 CreateUserWizard 控件的单击继续按钮时的 URL [ `ContinueDestinationPageUrl`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)。 设置`ContinueDestinationPageUrl`属性设置为"~ / Membership/AdditionalUserInfo.aspx"。 这会转到新用户`AdditionalUserInfo.aspx`，其中他们可以查看和更新其设置。

### <a name="customizing-the-createuserwizards-interface-to-prompt-for-the-new-users-home-town-homepage-and-signature"></a>自定义 CreateUserWizard 的界面为提示输入新用户的主页城镇、 主页和签名

CreateUserWizard 控件的默认接口足以满足简单帐户创建方案需要从中收集用户名、 密码和电子邮件等唯一核心用户帐户信息。 但是，如果我们想要提示输入访问者创建她的帐户时输入其家乡、 主页和签名？ 可以自定义 CreateUserWizard 控件的界面以收集其他信息在注册，并可能在使用此信息`CreatedUser`事件处理程序以将更多记录插入到基础数据库。

CreateUserWizard 控件扩展了 ASP.NET 向导控件，它是允许页面开发人员可以定义一系列有序的控件`WizardSteps`。 向导控件呈现到活动步骤，并提供了一个允许访问者浏览这些步骤的导航界面。 向导控件非常适合于长任务拆分成几个简短的步骤。 有关向导控件的详细信息，请参阅[使用 ASP.NET 2.0 向导控件创建一个分步的用户界面](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)。

CreateUserWizard 控件的默认标记定义了两个`WizardSteps`:`CreateUserWizardStep`和`CompleteWizardStep`。

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample12.aspx)]

第一个`WizardStep`， `CreateUserWizardStep`，呈现提示输入用户名、 密码、 电子邮件和等等的界面。 访问者提供此信息并单击"创建用户"后，她会显示`CompleteWizardStep`，其中显示成功消息和继续按钮。

若要自定义 CreateUserWizard 控件的界面，以便包括其他窗体的字段，我们可以：

- <strong>创建一个或多个新</strong><strong>`WizardStep`</strong><strong>s 以包含附加用户界面元素</strong>。 若要添加一个新`WizardStep`CreateUserWizard，请单击"添加/删除`WizardSteps`"链接以启动其智能标记`WizardStep`集合编辑器。 从此处可以添加、 删除或重新排序向导中的步骤。 这是我们将在本教程使用的方法。

- <strong>将转换</strong><strong>`CreateUserWizardStep`</strong><strong>到一个可编辑</strong><strong>`WizardStep`</strong><strong>。</strong> 这将替换`CreateUserWizardStep`使用等效`WizardStep`其标记定义匹配的用户界面`CreateUserWizardStep`' s。 通过将转换`CreateUserWizardStep`到`WizardStep`我们可以重新定位控件或将附加用户界面元素添加到此步骤。 要转换`CreateUserWizardStep`或`CompleteWizardStep`到一个可编辑`WizardStep`，单击"自定义创建用户跳转"或"自定义完成步骤"链接从控件的智能标记。

- **使用上述两个选项的某种组合。**

需要记住的重要一点是 CreateUserWizard 控件执行其用户帐户创建过程，在单击"创建用户"按钮时其`CreateUserWizardStep`。 如果有其他并不重要`WizardStep`之后的 s`CreateUserWizardStep`与否。

添加自定义时`WizardStep`于 CreateUserWizard 控件，以收集其他用户输入自定义`WizardStep`之前或之后可以放置`CreateUserWizardStep`。 如果它出现时前`CreateUserWizardStep`额外用户输入从自定义的收集然后`WizardStep`适用于`CreatedUser`事件处理程序。 但是，如果自定义`WizardStep`之后`CreateUserWizardStep`然后按时间自定义`WizardStep`将显示已创建了新的用户帐户和`CreatedUser`已触发事件。

图 21 显示了工作流时，添加`WizardStep`位于`CreateUserWizardStep`。 由于其他用户信息收集时`CreatedUser`事件触发时，我们只需是更新`CreatedUser`事件处理程序以检索这些输入并将其用于`INSERT`语句的参数值 （而非`DBNull.Value`).


[![当其他 WizardStep 之前 CreateUserWizardStep 时 CreateUserWizard 工作流](storing-additional-user-information-cs/_static/image62.png)](storing-additional-user-information-cs/_static/image61.png)

**图 21**: CreateUserWizard 工作流时其他`WizardStep`Precedes `CreateUserWizardStep` ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image63.png))


如果自定义`WizardStep`放置*后* `CreateUserWizardStep`，但是，创建用户帐户过程发生在用户有机会进入她的家庭城镇、 主页或签名之前。 在这种情况下，需要如图 22 所示插入到数据库后创建的用户帐户，此附加信息。


[![CreateUserWizard 工作流时在 CreateUserWizardStep 后出现其他 WizardStep](storing-additional-user-information-cs/_static/image65.png)](storing-additional-user-information-cs/_static/image64.png)

**图 22**: CreateUserWizard 工作流时其他`WizardStep`出现后`CreateUserWizardStep`([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image66.png))


图 22 所示的工作流等待要插入到一条记录`UserProfiles`第 2 步完成后表格中，直到。 如果访问者在步骤 1 后关闭其浏览器，但是，我们将已经达到了一种状态的用户帐户已创建，但没有记录已添加到`UserProfiles`。 一个解决方法是拥有 a 记录`NULL`或默认值插入到`UserProfiles`中`CreatedUser`（这在步骤 1 后会激发） 的事件处理程序和更新此记录后步骤 2 完成。 这可确保`UserProfiles`记录将添加的用户帐户，即使在用户退出注册过程中途。

对于本教程让我们创建一个新`WizardStep`之后将发生这种情况`CreateUserWizardStep`之前`CompleteWizardStep`。 让我们首先获取 WizardStep 中的放置和配置，然后我们将看一下代码。

从 CreateUserWizard 控件的智能标记，选择"添加/删除`WizardStep`s"，这会打开`WizardStep`集合编辑器对话框。 添加一个新`WizardStep`，并设置其`ID`到`UserSettings`，将其`Title`到"设置"并将其`StepType`到`Step`。 然后确定其位置，以便之后涉及`CreateUserWizardStep`（"注册新帐户的"） 和之前`CompleteWizardStep`（"已完成"），如图 23 中所示。


[![将新 WizardStep 添加到 CreateUserWizard 控件](storing-additional-user-information-cs/_static/image68.png)](storing-additional-user-information-cs/_static/image67.png)

**图 23**： 添加新`WizardStep`到 CreateUserWizard 控件 ([单击以查看实际尺寸的图像](storing-additional-user-information-cs/_static/image69.png))


单击确定以关闭`WizardStep`集合编辑器对话框。 新`WizardStep`CreateUserWizard 控件的已更新的声明性标记众多：

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample13.aspx)]

请注意新`<asp:WizardStep>`元素。 我们需要添加要收集新用户的主城镇、 主页和此处签名的用户界面。 声明性语法中或通过设计器，可以输入此内容。 若要使用设计器，请从智能标记以查看在设计器中的步中的下拉列表中选择"应用设置"步骤。

> [!NOTE]
> 选择通过智能标记的下拉列表的步骤更新 CreateUserWizard 控件[`ActiveStepIndex`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.activestepindex.aspx)，它指定起始步骤的索引。 因此，如果你使用此下拉列表以编辑在设计器中的"设置"步骤，请务必将其设置回"符号注册新帐户"，以便当用户首次访问时显示此步骤`EnhancedCreateUserWizard.aspx`页。


创建包含三个文本框控件分别命名为"应用设置"步骤中的用户界面`HomeTown`， `HomepageUrl`，和`Signature`。 以后构造此接口，CreateUserWizard 的声明性标记看起来应类似于下面：

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample14.aspx)]

请继续并访问本页可通过浏览器并创建新的用户帐户，指定主城镇、 主页和签名值。 完成后`CreateUserWizardStep`在成员资格框架中创建的用户帐户和`CreatedUser`事件处理程序将运行，也就是添加新行`UserProfiles`，但与数据库`NULL`值`HomeTown`， `HomepageUrl`，和`Signature`. 永远不会使用主城镇、 主页和签名为输入的值。 最终结果是与新的用户帐户`UserProfiles`记录其`HomeTown`， `HomepageUrl`，和`Signature`字段尚未指定。

我们需要采用用户输入的家庭城镇、 honepage 和签名值并更新相应的"设置"步骤后执行代码`UserProfiles`记录。 每次用户在向导中的步骤之间移动控件，该向导[`ActiveStepChanged`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.activestepchanged.aspx)激发。 我们可以创建此事件和更新的事件处理程序`UserProfiles`表时在"设置"步骤未完成。

有关 CreateUserWizard 添加事件处理程序`ActiveStepChanged`事件，并添加以下代码：

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample15.cs)]

上面的代码首先会确定如果我们只是已达到"完成"步骤。 由于在"设置"步骤之后立即发生"已完成"步骤，然后访问者到达时"完成"单步意味着她刚刚完成的"应用设置"步骤。

在这种情况下，我们需要以编程方式引用中的文本框控件`UserSettings WizardStep`。 这通过先使用实现`FindControl`方法以编程方式引用`UserSettings WizardStep`，，然后再次引用在文本框内`WizardStep`。 一旦已引用文本框后，我们已准备好执行`UPDATE`语句。 `UPDATE`语句具有相同数量的参数作为`INSERT`中的语句`CreatedUser`事件处理程序，但此处我们使用的用户提供的主城镇、 主页和签名值。

在位置在此事件处理程序，请访问`EnhancedCreateUserWizard.aspx`通过浏览器页并创建新的用户帐户指定为家庭城镇、 主页和签名的值。 创建新帐户后，应重定向到`AdditionalUserInfo.aspx`页上，其中显示的只是输入家庭城镇、 主页和签名信息。

> [!NOTE]
> 我们的网站当前具有两个访问者可以从中创建新的帐户的页面：`CreatingUserAccounts.aspx`和`EnhancedCreateUserWizard.aspx`。 网站的站点地图和登录页指向`CreatingUserAccounts.aspx`页上，但`CreatingUserAccounts.aspx`页面不会提示用户输入其家庭的城镇、 主页和签名信息并不会添加到相应行`UserProfiles`。 因此，更新`CreatingUserAccounts.aspx`页上，以便提供此功能或更新站点地图和登录页面，以引用`EnhancedCreateUserWizard.aspx`而不是`CreatingUserAccounts.aspx`。 如果选择后一种选择，请务必更新`Membership`文件夹的`Web.config`文件以允许匿名用户访问`EnhancedCreateUserWizard.aspx`页。


## <a name="summary"></a>总结

在本教程中我们介绍了用于与成员资格框架中的用户帐户相关的数据进行建模的技术。 具体而言，我们介绍了建模与用户帐户，以及共享的一对一关系的数据共享一个对多关系的实体。 此外，我们已了解如何这相关的信息可以显示、 插入和更新使用 SqlDataSource 控件，而其他一些示例使用 ADO.NET 代码。

本教程中完成我们研究用户帐户。 开始下一教程，我们将把注意力转向角色。 在接下来几个教程，我们将查看角色框架中，请参阅如何创建新角色，如何将角色分配给用户，如何来确定哪些角色用户所属，以及如何应用基于角色的授权。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [访问和更新 ASP.NET 2.0 中的数据](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 2.0 向导控件](https://weblogs.asp.net/scottgu/archive/2006/02/21/438732.aspx)
- [使用 ASP.NET 2.0 向导控件中创建分步的用户界面](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [创建自定义数据源控件参数](http://aspnet.4guysfromrolla.com/articles/110106-1.aspx)
- [自定义 CreateUserWizard 控件](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)
- [在 DetailsView 控件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/detailsview.aspx)
- [使用 ListView 控件显示数据](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [仔细分析 ASP.NET 2.0 中的验证控件](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)
- [编辑插入和删除数据](../../data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)
- [在 ASP.NET 中的窗体验证](http://www.4guysfromrolla.com/webtech/090200-1.shtml)
- [正在收集自定义用户注册信息](https://weblogs.asp.net/scottgu/archive/2006/07/05/Tip_2F00_Trick_3A00_-Gathering-Custom-User-Registration-Information.aspx)
- [ASP.NET 2.0 中的配置文件](http://www.odetocode.com/Articles/440.aspx)
- [Asp: ListView 控件](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)
- [用户配置文件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/profile/default.aspx)

### <a name="about-the-author"></a>关于作者

自 1998 年以来，Scott Mitchell，多部 asp/ASP.NET 书籍的作者及 4GuysFromRolla.com 的已从事 Microsoft Web 技术工作。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是 *[Sams Teach 自己 ASP.NET 2.0 24 小时内](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在达到 Scott [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢...

很多有用的审阅者已评审本系列教程。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)。

> [!div class="step-by-step"]
> [上一页](user-based-authorization-cs.md)
> [下一页](creating-the-membership-schema-in-sql-server-vb.md)
