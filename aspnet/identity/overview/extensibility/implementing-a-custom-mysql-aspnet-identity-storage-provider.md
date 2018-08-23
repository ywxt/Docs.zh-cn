---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: 实现自定义 MySQL ASP.NET 标识存储提供程序 |Microsoft Docs
author: raquelsa
description: ASP.NET 标识是一个可扩展的系统，这样就可以创建自己的存储提供程序并将其插入到你的应用程序而无需重新处理应用...
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 358b1a3b7277f21c63a1d395f2a5fce79bbe0d56
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834554"
---
<a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a>实现自定义 MySQL ASP.NET 标识存储提供程序
====================
通过[Raquel Soares De Almeida](https://github.com/raquelsa)， [Suhas Joshi](https://github.com/suhasj)， [Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET 标识是一个可扩展的系统，这样就可以创建自己的存储提供程序并将其插入到你的应用程序而无需重新使用该应用程序。 本主题介绍如何创建 ASP.NET 标识的 MySQL 存储提供程序。 有关创建自定义存储提供程序的概述，请参阅[概述的自定义存储提供程序的 ASP.NET 标识](overview-of-custom-storage-providers-for-aspnet-identity.md)。
> 
> 若要完成本教程，必须具有 Visual Studio 2013 Update 2。
> 
> 本教程将：
> 
> - 演示如何在 Azure 上创建 MySQL 数据库实例。
> - 演示如何使用 MySQL 客户端工具 (MySQL Workbench) 来创建表和管理在 Azure 上的远程数据库。
> - 显示如何使用我们在 MVC 应用程序项目的自定义实现替换默认 ASP.NET 标识存储实现。
> 
> 本教程中原本编写 Raquel Soares De Almeida 和 Rick Anderson ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )。 示例项目已针对标识 2.0 更新通过 Suhas Joshi。 Tom FitzMacken 标识 2.0 更新主题。


## <a name="download-completed-project"></a>下载已完成项目

在本教程结束时，将您的 MVC 应用程序项目与 ASP.NET 标识使用 Azure 上托管的 MySQL 数据库。

您可以下载的已完成的 MySQL 存储提供程序的[AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/)。

## <a name="the-steps-you-will-perform"></a>将执行的步骤

在本教程中，你将：

1. 在 Azure 上创建 MySQL 数据库
2. 在 MySQL 中创建 ASP.NET 标识表
3. 创建 MVC 应用程序并将其配置为使用 MySQL 提供程序
4. 运行应用

本主题不涉及 ASP.NET 标识的体系结构实现客户存储提供程序时必须做出的决定。 该信息，请参阅[概述的自定义存储提供程序的 ASP.NET 标识](overview-of-custom-storage-providers-for-aspnet-identity.md)。

## <a name="review-mysql-storage-provider-classes"></a>查看 MySQL 存储提供程序类

之前跳转到创建的 MySQL 存储提供程序的步骤，让我们看看组成的存储提供程序的类。 你将需要管理的数据库操作的类和应用程序来管理用户和角色从调用的类。

### <a name="storage-classes"></a>存储类

- [IdentityUser](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -包含用户的属性。
- [UserStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserStore.cs) -包含用于添加、 更新或检索用户的操作。
- [IdentityRole](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -包含角色的属性。
- [RoleStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleStore.cs) -包含用于添加、 删除、 更新和检索角色的操作。

### <a name="data-access-layer-classes"></a>数据访问层类

对于此示例中，数据访问层类包含 SQL 语句使用表;但是，在代码中你可能想要使用如 Entity Framework 或 NHibernate 的对象关系映射 (ORM)。 具体而言，你的应用程序可能会遇到性能不佳而无需包括延迟加载和缓存对象是 ORM。 有关详细信息，请参阅[而无需实体框架的 ASP.NET 标识 2.0？](https://aspnetidentity.codeplex.com/discussions/561828)

- [MySQLDatabase](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -包含 MySQL 数据库连接和执行数据库操作的方法。 UserStore 和 RoleStore 被同时实例化此类的实例。
- [RoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleTable.cs) -包含用于存储角色的表的数据库操作。
- [UserClaimsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -包含用于存储用户声明的表的数据库操作。
- [UserLoginsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -包含用于存储用户登录信息的表的数据库操作。
- [UserRoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -包含用于存储到了哪些角色分配的用户的表的数据库操作。
- [数据库](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserTable.cs)-包含用于存储用户的表的数据库操作。

## <a name="create-a-mysql-database-instance-on-azure"></a>在 Azure 上创建 MySQL 数据库实例

1. 登录到 [Azure 门户](https://manage.windowsazure.com/)。
2. 单击 **+ 新建**底部的页上，并选择**存储区**。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. 在中**Choose 和外接程序**向导中，选择**ClearDB MySQL 数据库**，然后单击右下角的对话框中的下一步箭头。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. 保留默认值**免费**计划和更改**名称**到**IdentityMySQLDatabase**。 选择离你最近的区域，然后单击下一步箭头。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. 单击复选标记以完成创建数据库。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. 创建数据库后，你可以管理从**外接程序**在管理门户中的选项卡。   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. 可以通过单击获取数据库连接信息**连接信息**页的底部。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. 通过单击复制按钮来复制连接字符串并将其保存，因此，可以使用在 MVC 应用程序中更高版本。   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a>在 MySQL 数据库中创建 ASP.NET 标识表

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a>安装 MySQL Workbench 工具，以连接和管理 MySQL 数据库

1. 安装**MySQL Workbench**工具从[MySQL 下载页](http://dev.mysql.com/downloads/windows/installer/)
2. 启动该应用程序，并添加单击**MySQLConnections +** 按钮以添加新的连接。 使用从前面在本教程中创建的 Azure MySQL 数据库复制的连接字符串数据。
3. 建立连接后，打开一个新**查询**选项卡，将从命令粘贴[MySQLIdentity.sql](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)到查询和执行它，以创建数据库表。
4. 现在，已创建的所有 ASP.NET 标识必要表上，如下所示，在 Azure 上托管的 MySQL 数据库。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a>从模板创建 MVC 应用程序项目，并将其配置为使用 MySQL 提供程序

如果需要请安装[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) Update 2。

### <a name="download-the-aspnetidentitymysql-project-from-codeplex"></a>从 CodePlex 下载 ASP.NET.Identity.MySQL 项目

1. 浏览到存储库 URL [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/)。
2. 下载的源代码。
3. 将.zip 文件提取到本地文件夹。
4. 打开 AspNet.Identity.MySQL 解决方案并生成它。

### <a name="create-a-new-mvc-application-project-from-template"></a>从模板创建新的 MVC 应用程序项目

1. 右键单击**AspNet.Identity.MySQL**解决方案并**添加**，**新项目**
2. 在中**添加新项目**对话框中，选择**Visual C#** 在左侧，然后**Web** ，然后选择**ASP.NET Web 应用程序**。 将项目命名**IdentityMySQLDemo**; 然后单击确定。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. 在**新建 ASP.NET 项目**对话框中，选择 MVC 模板中的使用默认选项 (包括**单个用户帐户**作为身份验证方法)，单击**确定**.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)
4. 在解决方案资源管理器，右键单击 IdentityMySQLDemo 项目并选择**管理 NuGet 包**。 在搜索文本框对话框，键入**Identity.EntityFramework**。 在结果列表中选择此包，然后单击**卸载**。 系统将提示您若要卸载依赖项包 EntityFramework。 单击是我们将不再会在此应用程序上的此包。
5. 右键单击 IdentityMySQLDemo 项目中，选择**外**，**的引用、 解决方案、 项目中;** 选择 AspNet.Identity.MySQL 项目，然后单击**确定**。
6. 在 IdentityMySQLDemo 项目中，替换为对所有引用  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   替换为  
     `using AspNet.Identity.MySQL;`
7. 在 IdentityModels.cs，设置**ApplicationDbContext**为派生**MySqlDatabase** ，包括采用一个参数与该连接名称构造函数。  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. 打开 IdentityConfig.cs 文件。 在中**ApplicationUserManager.Create**方法中，将为以下代码实例化 UserManager:  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. 打开 web.config 文件并将 DefaultConnection 字符串替换此项突出显示的值替换为上一步骤中创建的 MySQL 数据库的连接字符串：  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a>运行应用并连接到 MySQL 数据库

1. 右键单击**IdentityMySQLDemo**项目，然后选择**设为启动项目**
2. 按**Ctrl + F5**生成并运行应用程序。
3. 单击**注册**页面顶部的选项卡。
4. 输入新用户名和密码，然后单击**注册**。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. 新用户立即注册并登录。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. 返回到 MySQL Workbench 工具并检查**IdentityMySQLDatabase**表的内容。 检查条目的用户表，如注册新用户。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a>后续步骤

有关如何启用此应用上的其他身份验证方法的详细信息，请参阅[创建 ASP.NET MVC 5 应用程序使用 Facebook 和 Google OAuth2 和 OpenID 登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。

若要了解如何将你的数据库与 OAuth 集成以及如何设置角色以限制用户访问应用，请参阅[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 5 应用部署到 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。
