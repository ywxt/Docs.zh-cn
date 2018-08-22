---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: ASP.NET 标识： 使用 MySQL 存储通过 EntityFramework MySQL 提供程序 (C#) |Microsoft Docs
author: maumar
description: 本教程演示如何将 ASP.NET 标识的默认数据存储机制 EntityFramework （SQL 客户端提供程序） 替换为使用 MySQL 签约...
ms.author: riande
ms.date: 12/10/2013
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: 3856b40b31a3deb6ad1c6c5d2cd678e183f012d7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826617"
---
<a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a><span data-ttu-id="787cf-103">ASP.NET 标识： 使用 EntityFramework MySQL 提供程序 (C#) 使用 MySQL 存储</span><span class="sxs-lookup"><span data-stu-id="787cf-103">ASP.NET Identity: Using MySQL Storage with an EntityFramework MySQL Provider (C#)</span></span>
====================
<span data-ttu-id="787cf-104">通过[Maurycy Markowski](https://github.com/maumar)， [Raquel Soares De Almeida](https://github.com/raquelsa)， [Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="787cf-104">by [Maurycy Markowski](https://github.com/maumar), [Raquel Soares De Almeida](https://github.com/raquelsa), [Robert McMurray](https://github.com/rmcmurray)</span></span>

> <span data-ttu-id="787cf-105">本教程演示如何替换的默认数据存储机制[ **ASP.NET 标识**](introduction-to-aspnet-identity.md) EntityFramework （SQL 客户端提供程序） 使用 MySQL 提供程序使用。</span><span class="sxs-lookup"><span data-stu-id="787cf-105">This tutorial shows you how to replace the default data storage mechanism for [**ASP.NET Identity**](introduction-to-aspnet-identity.md) with EntityFramework (SQL client provider) with a MySQL provider.</span></span>


<span data-ttu-id="787cf-106">本教程中，将涵盖以下主题：</span><span class="sxs-lookup"><span data-stu-id="787cf-106">The following topics will be covered in this tutorial:</span></span>

- <span data-ttu-id="787cf-107">在 Azure 上创建 MySQL 数据库</span><span class="sxs-lookup"><span data-stu-id="787cf-107">Creating a MySQL database on Azure</span></span>
- <span data-ttu-id="787cf-108">创建 MVC 应用程序使用 Visual Studio 2013 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="787cf-108">Creating an MVC application using Visual Studio 2013 MVC template</span></span>
- <span data-ttu-id="787cf-109">配置 EntityFramework 以使用 MySQL 数据库提供程序</span><span class="sxs-lookup"><span data-stu-id="787cf-109">Configuring EntityFramework to work with a MySQL database provider</span></span>
- <span data-ttu-id="787cf-110">运行应用程序以验证结果</span><span class="sxs-lookup"><span data-stu-id="787cf-110">Running the application to verify the results</span></span>

<span data-ttu-id="787cf-111">在本教程结束时，会创建 MVC 应用程序与 ASP.NET 标识存储，使用在 Azure 中托管的 MySQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="787cf-111">At the end of this tutorial, you will have an MVC application with the ASP.NET Identity store that is using a MySQL database that is hosted in Azure.</span></span>

## <a name="creating-a-mysql-database-instance-on-azure"></a><span data-ttu-id="787cf-112">在 Azure 上创建 MySQL 数据库实例</span><span class="sxs-lookup"><span data-stu-id="787cf-112">Creating a MySQL database instance on Azure</span></span>

1. <span data-ttu-id="787cf-113">登录到 [Azure 门户](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="787cf-113">Log in to the [Azure Portal](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409).</span></span>
2. <span data-ttu-id="787cf-114">单击**新建**底部的页上，并选择**存储区**:</span><span class="sxs-lookup"><span data-stu-id="787cf-114">Click **NEW** at the bottom of the page, and then select **STORE**:</span></span>  
  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. <span data-ttu-id="787cf-115">在中**Choose 和外接程序**向导中，选择**ClearDB MySQL 数据库**，然后单击**下一步**框架底部的箭头：</span><span class="sxs-lookup"><span data-stu-id="787cf-115">In the **Choose and Add-on** wizard, select **ClearDB MySQL Database**, and then click the **Next** arrow at the bottom of the frame:</span></span>  
  
   <span data-ttu-id="787cf-116">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-116">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-117">]</span><span class="sxs-lookup"><span data-stu-id="787cf-117">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)
4. <span data-ttu-id="787cf-118">保留默认值**免费**计划，更改**名称**到**IdentityMySQLDatabase**，选择离你，最近的区域，然后单击**下一步**框架底部的箭头：</span><span class="sxs-lookup"><span data-stu-id="787cf-118">Keep the default **Free** plan, change the **NAME** to **IdentityMySQLDatabase**, select the region that is nearest to you, and then click the **Next** arrow at the bottom of the frame:</span></span>  
  
   <span data-ttu-id="787cf-119">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-119">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-120">]</span><span class="sxs-lookup"><span data-stu-id="787cf-120">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)
5. <span data-ttu-id="787cf-121">单击**采购**复选标记以完成创建数据库。</span><span class="sxs-lookup"><span data-stu-id="787cf-121">Click the **PURCHASE** checkmark to complete the database creation.</span></span>  
  
   <span data-ttu-id="787cf-122">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-122">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-123">]</span><span class="sxs-lookup"><span data-stu-id="787cf-123">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)
6. <span data-ttu-id="787cf-124">创建数据库后，你可以管理从**外接程序**在管理门户中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="787cf-124">After your database has been created, you can manage it from the **ADD-ONS** tab in the management portal.</span></span> <span data-ttu-id="787cf-125">若要检索你的数据库的连接信息，请单击**连接信息**页的底部：</span><span class="sxs-lookup"><span data-stu-id="787cf-125">To retrieve the connection information for your database, click **CONNECTION INFO** at the bottom of the page:</span></span>  
  
   <span data-ttu-id="787cf-126">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-126">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-127">]</span><span class="sxs-lookup"><span data-stu-id="787cf-127">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)
7. <span data-ttu-id="787cf-128">通过单击通过复制按钮来复制连接字符串**CONNECTIONSTRING**字段并将其保存; 您将稍后在本教程中此信息用于 MVC 应用程序：</span><span class="sxs-lookup"><span data-stu-id="787cf-128">Copy the connection string by clicking on the copy button by the **CONNECTIONSTRING** field and save it; you will use this information later in this tutorial for your MVC application:</span></span>  
  
   <span data-ttu-id="787cf-129">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-129">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-130">]</span><span class="sxs-lookup"><span data-stu-id="787cf-130">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)

## <a name="creating-an-mvc-application-project"></a><span data-ttu-id="787cf-131">创建 MVC 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="787cf-131">Creating an MVC application project</span></span>

<span data-ttu-id="787cf-132">若要完成本教程的此部分中的步骤，您将首先需要安装[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="787cf-132">To complete the steps in this section of the tutorial, you will first need to install [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="787cf-133">后安装 Visual Studio 后，使用以下步骤创建新的 MVC 应用程序项目：</span><span class="sxs-lookup"><span data-stu-id="787cf-133">Once Visual Studio has been installed, use the following steps to create a new MVC application project:</span></span>

1. <span data-ttu-id="787cf-134">打开 Visual Studio 2103。</span><span class="sxs-lookup"><span data-stu-id="787cf-134">Open Visual Studio 2103.</span></span>
2. <span data-ttu-id="787cf-135">单击**新的项目**从**启动**页上，也可以单击**文件**菜单，然后**新项目**:</span><span class="sxs-lookup"><span data-stu-id="787cf-135">Click **New Project** from the **Start** page, or you can click the **File** menu and then **New Project**:</span></span>  
  
   <span data-ttu-id="787cf-136">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-136">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-137">]</span><span class="sxs-lookup"><span data-stu-id="787cf-137">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)
3. <span data-ttu-id="787cf-138">时**新的项目**对话框中，展开**Visual C#** 在模板列表中，然后单击**Web**，然后选择**ASP.NET Web 应用程序**.</span><span class="sxs-lookup"><span data-stu-id="787cf-138">When the **New Project** dialog box is displayed, expand **Visual C#** in the list of templates, then click **Web**, and select **ASP.NET Web Application**.</span></span> <span data-ttu-id="787cf-139">将项目命名**IdentityMySQLDemo** ，然后单击**确定**:</span><span class="sxs-lookup"><span data-stu-id="787cf-139">Name your project **IdentityMySQLDemo** and then click **OK**:</span></span>  
  
   <span data-ttu-id="787cf-140">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-140">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-141">]</span><span class="sxs-lookup"><span data-stu-id="787cf-141">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)
4. <span data-ttu-id="787cf-142">在中**新建 ASP.NET 项目**对话框中，选择**MVC** templatewith 默认选项; 这会配置**单个用户帐户**作为身份验证方法。</span><span class="sxs-lookup"><span data-stu-id="787cf-142">In the **New ASP.NET Project** dialog, select the **MVC** templatewith the default options; this will configure **Individual User Accounts** as the authentication method.</span></span> <span data-ttu-id="787cf-143">单击“确定”：</span><span class="sxs-lookup"><span data-stu-id="787cf-143">Click **OK**:</span></span>  
  
   <span data-ttu-id="787cf-144">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-144">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-145">]</span><span class="sxs-lookup"><span data-stu-id="787cf-145">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a><span data-ttu-id="787cf-146">配置 EntityFramework 以使用 MySQL 数据库</span><span class="sxs-lookup"><span data-stu-id="787cf-146">Configure EntityFramework to work with a MySQL database</span></span>

### <a name="update-the-entity-framework-assembly-for-your-project"></a><span data-ttu-id="787cf-147">更新你的项目的实体框架程序集</span><span class="sxs-lookup"><span data-stu-id="787cf-147">Update the Entity Framework assembly for your project</span></span>

<span data-ttu-id="787cf-148">从 Visual Studio 2013 模板创建的 MVC 应用程序包含对引用[EntityFramework 6.0.0](http://www.nuget.org/packages/EntityFramework)包，但那里具有已对其发布以来该程序集的更新，其中包含大量性能改进。</span><span class="sxs-lookup"><span data-stu-id="787cf-148">The MVC application that was created from the Visual Studio 2013 template contains a reference to the [EntityFramework 6.0.0](http://www.nuget.org/packages/EntityFramework) package, but there have been updates to that assembly since its release which contain significant performance improvements.</span></span> <span data-ttu-id="787cf-149">若要在应用程序中使用这些最新的更新，使用以下步骤。</span><span class="sxs-lookup"><span data-stu-id="787cf-149">In order to use these latest updates in your application, use the following steps.</span></span>

1. <span data-ttu-id="787cf-150">在 Visual Studio 2013 中打开你的 MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="787cf-150">Open your MVC project in Visual Studio 2013.</span></span>
2. <span data-ttu-id="787cf-151">单击**工具**，然后单击**库程序包管理器**，然后单击**程序包管理器控制台**:</span><span class="sxs-lookup"><span data-stu-id="787cf-151">Click **TOOLS**, then click **Library Package Manager**, and then click **Package Manager Console**:</span></span>  
  
   <span data-ttu-id="787cf-152">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-152">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-153">]</span><span class="sxs-lookup"><span data-stu-id="787cf-153">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)
3. <span data-ttu-id="787cf-154">**程序包管理器控制台**会在 Visual Studio 的下半部分中显示。</span><span class="sxs-lookup"><span data-stu-id="787cf-154">The **Package Manager Console** will appear in the bottom section of Visual Studio.</span></span> <span data-ttu-id="787cf-155">类型&quot;**更新 EntityFramework** &quot;然后按 Enter:</span><span class="sxs-lookup"><span data-stu-id="787cf-155">Type &quot;**Update-Package EntityFramework**&quot; and press Enter:</span></span>  
  
   <span data-ttu-id="787cf-156">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-156">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-157">]</span><span class="sxs-lookup"><span data-stu-id="787cf-157">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)

### <a name="install-the-mysql-provider-for-entityframework"></a><span data-ttu-id="787cf-158">安装 EntityFramework MySQL 提供程序</span><span class="sxs-lookup"><span data-stu-id="787cf-158">Install the MySQL provider for EntityFramework</span></span>

<span data-ttu-id="787cf-159">为了使 EntityFramework 以连接到 MySQL 数据库，您需要安装 MySQL 提供程序。</span><span class="sxs-lookup"><span data-stu-id="787cf-159">In order for EntityFramework to connect to MySQL database, you need to install a MySQL provider.</span></span> <span data-ttu-id="787cf-160">为此，请打开**程序包管理器控制台**并键入&quot;**安装包 MySql.Data.Entity-Pre**&quot;，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="787cf-160">To do so, open the **Package Manager Console** and type &quot;**Install-Package MySql.Data.Entity -Pre**&quot;, and then press Enter.</span></span>

> [!NOTE]
> <span data-ttu-id="787cf-161">这是预发行版本的程序集，并且这种情况下它可能包含 bug。</span><span class="sxs-lookup"><span data-stu-id="787cf-161">This is a pre-release version of the assembly, and as such it may contain bugs.</span></span> <span data-ttu-id="787cf-162">不应在生产环境中使用预发行版本的提供程序。</span><span class="sxs-lookup"><span data-stu-id="787cf-162">You should not use a pre-release version of the provider in production.</span></span>


<span data-ttu-id="787cf-163">[单击下图以将其展开。]</span><span class="sxs-lookup"><span data-stu-id="787cf-163">[Click the following image to expand it.]</span></span>  
  
[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a><span data-ttu-id="787cf-164">你的应用程序的 Web.config 文件进行项目配置更改</span><span class="sxs-lookup"><span data-stu-id="787cf-164">Making project configuration changes to the Web.config file for your application</span></span>

<span data-ttu-id="787cf-165">在本部分中，您将配置实体框架使用刚安装的 MySQL 提供程序，注册 MySQL 提供程序工厂，并从 Azure 添加你的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="787cf-165">In this section you will configure the Entity Framework to use the MySQL provider that you just installed, register the MySQL provider factory, and add your connection string from Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="787cf-166">下面的示例包含 MySql.Data.dll 特定程序集版本。</span><span class="sxs-lookup"><span data-stu-id="787cf-166">The following examples contain a specific assembly version for MySql.Data.dll.</span></span> <span data-ttu-id="787cf-167">如果程序集版本更改，需要修改使用正确版本的合适配置设置。</span><span class="sxs-lookup"><span data-stu-id="787cf-167">If the assembly version changes, you will need to modify the appropriate configuration settings with the correct version.</span></span>


1. <span data-ttu-id="787cf-168">在 Visual Studio 2013 中打开你的项目的 Web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="787cf-168">Open the Web.config file for your project in Visual Studio 2013.</span></span>
2. <span data-ttu-id="787cf-169">找到用于实体框架定义的默认数据库提供程序和工厂的以下配置设置：</span><span class="sxs-lookup"><span data-stu-id="787cf-169">Locate the following configuration settings, which define the default database provider and factory for the Entity Framework:</span></span>

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. <span data-ttu-id="787cf-170">这些配置设置替换为以下内容，他们将配置实体框架，以使用 MySQL 提供程序：</span><span class="sxs-lookup"><span data-stu-id="787cf-170">Replace those configuration settings with the following, which will configure the Entity Framework to use the MySQL provider:</span></span> 

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. <span data-ttu-id="787cf-171">找到&lt;connectionStrings&gt;部分并替换为以下代码，将定义在 Azure 托管的 MySQL 数据库的连接字符串 (请注意，还从更改 providerName 值时原始）：</span><span class="sxs-lookup"><span data-stu-id="787cf-171">Locate the &lt;connectionStrings&gt; section and replace it with the following code, which will define the connection string for your MySQL database that is hosted on Azure (note that providerName value has also been changed from the original):</span></span>

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a><span data-ttu-id="787cf-172">添加自定义的 MigrationHistory 上下文</span><span class="sxs-lookup"><span data-stu-id="787cf-172">Adding custom MigrationHistory context</span></span>

<span data-ttu-id="787cf-173">使用实体框架 Code First **MigrationHistory**表来跟踪模型更改并确保数据库架构和概念性架构之间的一致性。</span><span class="sxs-lookup"><span data-stu-id="787cf-173">Entity Framework Code First uses a **MigrationHistory** table to keep track of model changes and to ensure the consistency between the database schema and conceptual schema.</span></span> <span data-ttu-id="787cf-174">但是，此表不适用于 MySQL 默认情况下由于太大的主键。</span><span class="sxs-lookup"><span data-stu-id="787cf-174">However, this table does not work for MySQL by default because the primary key is too large.</span></span> <span data-ttu-id="787cf-175">若要纠正这种情况下，你将需要压缩该表的密钥大小。</span><span class="sxs-lookup"><span data-stu-id="787cf-175">To remedy this situation, you will need to shrink the key size for that table.</span></span> <span data-ttu-id="787cf-176">为此，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="787cf-176">To do so, use the following steps:</span></span>

1. <span data-ttu-id="787cf-177">此表的架构信息中捕获**HistoryContext**，可修改任何其他**DbContext**。</span><span class="sxs-lookup"><span data-stu-id="787cf-177">The schema information for this table is captured in a **HistoryContext**, which can be modified as any other **DbContext**.</span></span> <span data-ttu-id="787cf-178">若要执行此操作，添加名为的新类文件**MySqlHistoryContext.cs**到项目中，并将其内容替换为下面的代码：</span><span class="sxs-lookup"><span data-stu-id="787cf-178">To do so, add a new class file named **MySqlHistoryContext.cs** to the project, and replace its contents with the following code:</span></span>

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. <span data-ttu-id="787cf-179">接下来需要配置要使用修改后的实体框架**HistoryContext**，而不是默认值。</span><span class="sxs-lookup"><span data-stu-id="787cf-179">Next you will need to configure Entity Framework to use the modified **HistoryContext**, rather than default one.</span></span> <span data-ttu-id="787cf-180">这可以通过利用基于代码的配置功能。</span><span class="sxs-lookup"><span data-stu-id="787cf-180">This can be done by leveraging code-based configuration features.</span></span> <span data-ttu-id="787cf-181">若要执行此操作，添加名为的新类文件**MySqlConfiguration.cs**到你的项目，并将其内容为：</span><span class="sxs-lookup"><span data-stu-id="787cf-181">To do so, add new class file named **MySqlConfiguration.cs** to your project and replace its contents with:</span></span>

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a><span data-ttu-id="787cf-182">创建的自定义 EntityFramework 初始值设定项 ApplicationDbContext</span><span class="sxs-lookup"><span data-stu-id="787cf-182">Creating a custom EntityFramework initializer for ApplicationDbContext</span></span>

<span data-ttu-id="787cf-183">在本教程中精选的 MySQL 提供程序当前不支持实体框架迁移，因此将需要使用模型初始值设定项来连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="787cf-183">The MySQL provider that is featured in this tutorial does not currently support Entity Framework migrations, so you will need to use model initializers in order to connect to the database.</span></span> <span data-ttu-id="787cf-184">由于本教程在 Azure 上使用 MySQL 实例，需要创建自定义的实体框架初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="787cf-184">Because this tutorial is using a MySQL instance on Azure, you will need to create a custom Entity Framework initializer.</span></span>

> [!NOTE]
> <span data-ttu-id="787cf-185">如果要连接到 Azure 或如果您使用的是在本地托管的数据库上的 SQL Server 实例，则不需要此步骤。</span><span class="sxs-lookup"><span data-stu-id="787cf-185">This step is not required if you are connecting to a SQL Server instance on Azure or if you are using a database that is hosted on premises.</span></span>


<span data-ttu-id="787cf-186">若要创建用于 MySQL 的自定义实体框架初始值设定项，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="787cf-186">To create a custom Entity Framework initializer for MySQL, use the following steps:</span></span>

1. <span data-ttu-id="787cf-187">添加名为的新类文件**MySqlInitializer.cs**到项目中，并替换它是用下面的代码的内容：</span><span class="sxs-lookup"><span data-stu-id="787cf-187">Add a new class file named **MySqlInitializer.cs** to the project, and replace it's contents with the following code:</span></span> 

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. <span data-ttu-id="787cf-188">打开**IdentityModels.cs**项目，它位于文件**模型**目录，并将其内容替换以下：</span><span class="sxs-lookup"><span data-stu-id="787cf-188">Open the **IdentityModels.cs** file for your project, which is located in the **Models** directory, and replace it's contents with the following:</span></span> 

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a><span data-ttu-id="787cf-189">运行应用程序和验证数据库</span><span class="sxs-lookup"><span data-stu-id="787cf-189">Running the application and verifying the database</span></span>

<span data-ttu-id="787cf-190">完成前面几节中的步骤后，应测试您的数据库。</span><span class="sxs-lookup"><span data-stu-id="787cf-190">Once you have completed the steps in the preceding sections, you should test your database.</span></span> <span data-ttu-id="787cf-191">为此，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="787cf-191">To do so, use the following steps:</span></span>

1. <span data-ttu-id="787cf-192">按**Ctrl + F5**生成并运行 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="787cf-192">Press **Ctrl + F5** to build and run the web application.</span></span>
2. <span data-ttu-id="787cf-193">单击**注册**页面顶部的选项卡：</span><span class="sxs-lookup"><span data-stu-id="787cf-193">Click the **Register** tab on the top of the page:</span></span>  
  
   <span data-ttu-id="787cf-194">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-194">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-195">]</span><span class="sxs-lookup"><span data-stu-id="787cf-195">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)
3. <span data-ttu-id="787cf-196">输入新用户名和密码，然后依次**注册**:</span><span class="sxs-lookup"><span data-stu-id="787cf-196">Enter a new user name and password, and then click **Register**:</span></span>  
  
   <span data-ttu-id="787cf-197">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-197">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-198">]</span><span class="sxs-lookup"><span data-stu-id="787cf-198">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)
4. <span data-ttu-id="787cf-199">此时在 MySQL 数据库中，创建了 ASP.NET 标识表和用户已注册并登录到应用程序：</span><span class="sxs-lookup"><span data-stu-id="787cf-199">At this point the ASP.NET Identity tables are created on the MySQL Database, and the user is registered and logged into the application:</span></span>  
  
   <span data-ttu-id="787cf-200">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-200">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-201">]</span><span class="sxs-lookup"><span data-stu-id="787cf-201">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a><span data-ttu-id="787cf-202">安装 MySQL Workbench 工具，以验证数据</span><span class="sxs-lookup"><span data-stu-id="787cf-202">Installing MySQL Workbench tool to verify the data</span></span>

1. <span data-ttu-id="787cf-203">安装**MySQL Workbench**工具从[MySQL 下载页](http://dev.mysql.com/downloads/windows/installer/)</span><span class="sxs-lookup"><span data-stu-id="787cf-203">Install the **MySQL Workbench** tool from the [MySQL downloads page](http://dev.mysql.com/downloads/windows/installer/)</span></span>
2. <span data-ttu-id="787cf-204">在安装向导中：**功能选择**选项卡上，选择**MySQL Workbench**下**应用程序**部分。</span><span class="sxs-lookup"><span data-stu-id="787cf-204">In the installation wizard: **Feature Selection** tab, select **MySQL Workbench** under **applications** section.</span></span>
3. <span data-ttu-id="787cf-205">启动应用并添加新的连接使用在本教程的急创建的 Azure MySQL 数据库的连接字符串数据。</span><span class="sxs-lookup"><span data-stu-id="787cf-205">Launch the app and add a new connection using the connection string data from the Azure MySQL database you created at the begging of this tutorial.</span></span>
4. <span data-ttu-id="787cf-206">建立连接后，检查**ASP.NET 标识**上创建的表**IdentityMySQLDatabase。**</span><span class="sxs-lookup"><span data-stu-id="787cf-206">After establishing the connection, inspect the **ASP.NET Identity** tables created on the **IdentityMySQLDatabase.**</span></span>
5. <span data-ttu-id="787cf-207">你将看到，所有 ASP.NET 标识所都需的表创建如下图中所示：</span><span class="sxs-lookup"><span data-stu-id="787cf-207">You will see that all ASP.NET Identity required tables are created as shown in the image below:</span></span>  
  
   <span data-ttu-id="787cf-208">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-208">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-209">]</span><span class="sxs-lookup"><span data-stu-id="787cf-209">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)
6. <span data-ttu-id="787cf-210">检查**aspnetusers**实例表若要检查的项，因为注册新用户。</span><span class="sxs-lookup"><span data-stu-id="787cf-210">Inspect the **aspnetusers** table for instance to check for the entries as you register new users.</span></span>  
  
   <span data-ttu-id="787cf-211">[单击以下图像以将其展开。</span><span class="sxs-lookup"><span data-stu-id="787cf-211">[Click the following image to expand it.</span></span> <span data-ttu-id="787cf-212">]</span><span class="sxs-lookup"><span data-stu-id="787cf-212">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)
