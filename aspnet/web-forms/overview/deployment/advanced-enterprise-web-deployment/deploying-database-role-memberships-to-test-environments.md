---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: 部署到测试环境的数据库角色成员身份 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何将用户帐户添加到数据库角色作为解决方案部署到测试环境的一部分。 当你部署一个解决方案，其中包含...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: 07442b7a016ce2a32b1c9e7f44010517e40d7189
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832057"
---
<a name="deploying-database-role-memberships-to-test-environments"></a><span data-ttu-id="013f6-104">部署到测试环境的数据库角色成员身份</span><span class="sxs-lookup"><span data-stu-id="013f6-104">Deploying Database Role Memberships to Test Environments</span></span>
====================
<span data-ttu-id="013f6-105">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="013f6-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="013f6-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="013f6-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="013f6-107">本主题介绍如何将用户帐户添加到数据库角色作为解决方案部署到测试环境的一部分。</span><span class="sxs-lookup"><span data-stu-id="013f6-107">This topic describes how to add user accounts to database roles as part of a solution deployment to a test environment.</span></span>
> 
> <span data-ttu-id="013f6-108">在部署包含到过渡或生产环境的数据库项目的解决方案时，您通常不希望开发人员自动添加到数据库角色的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="013f6-108">When you deploy a solution containing a database project to a staging or production environment, you typically don't want the developer to automate the addition of user accounts to database roles.</span></span> <span data-ttu-id="013f6-109">在大多数情况下，开发人员不会知道哪些用户帐户需要添加到的数据库角色，并在任何时候无法更改这些要求。</span><span class="sxs-lookup"><span data-stu-id="013f6-109">In most cases, the developer won't know which user accounts need to be added to which database roles, and these requirements could change at any time.</span></span> <span data-ttu-id="013f6-110">但是，如果你部署一个包含到开发数据库项目的解决方案或测试环境，这种情况通常是不同：</span><span class="sxs-lookup"><span data-stu-id="013f6-110">However, when you deploy a solution containing a database project to a development or test environment, the situation is usually rather different:</span></span>
> 
> - <span data-ttu-id="013f6-111">开发人员通常重新部署解决方案，定期进行，通常几次一天。</span><span class="sxs-lookup"><span data-stu-id="013f6-111">The developer typically re-deploys the solution on a regular basis, often several times a day.</span></span>
> - <span data-ttu-id="013f6-112">每次部署，这意味着必须创建并添加到角色中每个部署后的数据库用户通常重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="013f6-112">The database is typically re-created on every deployment, which means that database users must be created and added to roles after every deployment.</span></span>
> - <span data-ttu-id="013f6-113">开发人员通常具有完全控制目标开发或测试环境。</span><span class="sxs-lookup"><span data-stu-id="013f6-113">The developer typically has full control over the target development or test environment.</span></span>
> 
> <span data-ttu-id="013f6-114">在此方案中，通常很有利，可自动创建数据库用户并分配数据库角色成员身份作为部署过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="013f6-114">In this scenario, it's often beneficial to automatically create database users and assign database role memberships as part of the deployment process.</span></span>
> 
> <span data-ttu-id="013f6-115">关键因素是，此操作需要是有条件的目标环境。</span><span class="sxs-lookup"><span data-stu-id="013f6-115">The key factor is that this operation needs to be conditional based on the target environment.</span></span> <span data-ttu-id="013f6-116">如果要部署到过渡或生产环境中，你想要跳过该操作。</span><span class="sxs-lookup"><span data-stu-id="013f6-116">If you're deploying to a staging or a production environment, you want to skip the operation.</span></span> <span data-ttu-id="013f6-117">如果要部署到开发人员或测试环境，你想要部署而无需进一步干预的角色成员身份。</span><span class="sxs-lookup"><span data-stu-id="013f6-117">If you're deploying to a developer or test environment, you want to deploy role memberships without further intervention.</span></span> <span data-ttu-id="013f6-118">本主题介绍可用于解决这一难题的一种方法。</span><span class="sxs-lookup"><span data-stu-id="013f6-118">This topic describes one approach you can use to address this challenge.</span></span>


<span data-ttu-id="013f6-119">本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="013f6-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="013f6-120">这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="013f6-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="013f6-121">在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="013f6-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="013f6-122">任务概述</span><span class="sxs-lookup"><span data-stu-id="013f6-122">Task Overview</span></span>

<span data-ttu-id="013f6-123">本主题假定：</span><span class="sxs-lookup"><span data-stu-id="013f6-123">This topic assumes that:</span></span>

- <span data-ttu-id="013f6-124">如中所述使用解决方案部署到的项目文件方法拆分[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。</span><span class="sxs-lookup"><span data-stu-id="013f6-124">You use the split project file approach to solution deployment, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span>
- <span data-ttu-id="013f6-125">如中所述从项目文件以部署数据库项目时，调用 VSDBCMD[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="013f6-125">You call VSDBCMD from the project file to deploy your database project, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

<span data-ttu-id="013f6-126">若要创建的数据库用户并分配角色成员身份数据库项目部署到测试环境时，将需要：</span><span class="sxs-lookup"><span data-stu-id="013f6-126">To create database users and assign role memberships when you deploy a database project to a test environment, you'll need to:</span></span>

- <span data-ttu-id="013f6-127">创建进行必要的数据库更改的 Transact 结构化查询语言 (Transact SQL) 脚本。</span><span class="sxs-lookup"><span data-stu-id="013f6-127">Create a Transact Structured Query Language (Transact-SQL) script that makes the necessary database changes.</span></span>
- <span data-ttu-id="013f6-128">创建使用 sqlcmd.exe 实用工具来运行 SQL 脚本的 Microsoft Build Engine (MSBuild) 目标。</span><span class="sxs-lookup"><span data-stu-id="013f6-128">Create a Microsoft Build Engine (MSBuild) target that uses the sqlcmd.exe utility to run the SQL script.</span></span>
- <span data-ttu-id="013f6-129">配置您的项目文件时要调用的目标将解决方案部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="013f6-129">Configure your project files to invoke the target when you're deploying your solution to a test environment.</span></span>

<span data-ttu-id="013f6-130">本主题将演示如何执行每个这些过程。</span><span class="sxs-lookup"><span data-stu-id="013f6-130">This topic will show you how to perform each of these procedures.</span></span>

## <a name="scripting-the-database-role-memberships"></a><span data-ttu-id="013f6-131">脚本的数据库角色成员身份</span><span class="sxs-lookup"><span data-stu-id="013f6-131">Scripting the Database Role Memberships</span></span>

<span data-ttu-id="013f6-132">可以在很多不同的方式，创建 TRANSACT-SQL 脚本，并选择在任何位置。</span><span class="sxs-lookup"><span data-stu-id="013f6-132">You can create a Transact-SQL script in a lot of different ways, and in any location you choose.</span></span> <span data-ttu-id="013f6-133">最简单的方法是在 Visual Studio 2010 中创建你的解决方案内的脚本。</span><span class="sxs-lookup"><span data-stu-id="013f6-133">The easiest approach is to create the script within your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="013f6-134">**若要创建 SQL 脚本**</span><span class="sxs-lookup"><span data-stu-id="013f6-134">**To create a SQL script**</span></span>

1. <span data-ttu-id="013f6-135">在中**解决方案资源管理器**窗口中，展开你的数据库项目节点。</span><span class="sxs-lookup"><span data-stu-id="013f6-135">In the **Solution Explorer** window, expand your database project node.</span></span>
2. <span data-ttu-id="013f6-136">右键单击**脚本**文件夹，指向**添加**，然后单击**新文件夹**。</span><span class="sxs-lookup"><span data-stu-id="013f6-136">Right-click the **Scripts** folder, point to **Add**, and then click **New Folder**.</span></span>
3. <span data-ttu-id="013f6-137">类型**测试**作为文件夹名称，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="013f6-137">Type **Test** as the folder name, and then press Enter.</span></span>
4. <span data-ttu-id="013f6-138">右键单击**测试**文件夹，指向**添加**，然后单击**脚本**。</span><span class="sxs-lookup"><span data-stu-id="013f6-138">Right-click the **Test** folder, point to **Add**, and then click **Script**.</span></span>
5. <span data-ttu-id="013f6-139">在中**添加新项**对话框框中，为您的脚本提供一个有意义的名称 (例如， **AddRoleMemberships.sql**)，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="013f6-139">In the **Add New Item** dialog box, give your script a meaningful name (for example, **AddRoleMemberships.sql**), and then click **Add**.</span></span>

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. <span data-ttu-id="013f6-140">在中*AddRoleMemberships.sql*文件中，添加 TRANSACT-SQL 语句的：</span><span class="sxs-lookup"><span data-stu-id="013f6-140">In the *AddRoleMemberships.sql* file, add Transact-SQL statements that:</span></span>

    1. <span data-ttu-id="013f6-141">创建将访问你的数据库的 SQL Server 登录名的数据库用户。</span><span class="sxs-lookup"><span data-stu-id="013f6-141">Create a database user for the SQL Server login that will access your database.</span></span>
    2. <span data-ttu-id="013f6-142">将数据库用户添加到任何所需的数据库角色。</span><span class="sxs-lookup"><span data-stu-id="013f6-142">Add the database user to any required database roles.</span></span>
7. <span data-ttu-id="013f6-143">该文件应类似如下：</span><span class="sxs-lookup"><span data-stu-id="013f6-143">The file should resemble this:</span></span>

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. <span data-ttu-id="013f6-144">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="013f6-144">Save the file.</span></span>

## <a name="executing-the-script-on-the-target-database"></a><span data-ttu-id="013f6-145">在目标数据库上执行脚本</span><span class="sxs-lookup"><span data-stu-id="013f6-145">Executing the Script on the Target Database</span></span>

<span data-ttu-id="013f6-146">理想情况下，在部署数据库项目时将作为后期部署脚本的一部分运行任何所需的 TRANSACT-SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="013f6-146">Ideally, you'd run any required Transact-SQL scripts as part of a post-deployment script when you deploy your database project.</span></span> <span data-ttu-id="013f6-147">但是，部署后脚本不允许你执行有条件地根据解决方案配置或生成属性的逻辑。</span><span class="sxs-lookup"><span data-stu-id="013f6-147">However, post-deployment scripts don't allow you to execute logic conditionally based on solution configurations or build properties.</span></span> <span data-ttu-id="013f6-148">替代方法是通过创建直接从 MSBuild 项目文件中，运行您的 SQL 脚本**目标**执行 sqlcmd.exe 命令的元素。</span><span class="sxs-lookup"><span data-stu-id="013f6-148">The alternative is to run your SQL scripts directly from the MSBuild project file, by creating a **Target** element that executes a sqlcmd.exe command.</span></span> <span data-ttu-id="013f6-149">此命令可用于目标数据库上运行脚本：</span><span class="sxs-lookup"><span data-stu-id="013f6-149">You can use this command to run your script on the target database:</span></span>


[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]


> [!NOTE]
> <span data-ttu-id="013f6-150">Sqlcmd 命令行选项的详细信息，请参阅[sqlcmd 实用工具](https://msdn.microsoft.com/library/ms162773.aspx)。</span><span class="sxs-lookup"><span data-stu-id="013f6-150">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>


<span data-ttu-id="013f6-151">在 MSBuild 目标中嵌入此命令之前，需要考虑在什么条件下你想要运行的脚本：</span><span class="sxs-lookup"><span data-stu-id="013f6-151">Before you embed this command in an MSBuild target, you need to consider under what conditions you want the script to run:</span></span>

- <span data-ttu-id="013f6-152">目标数据库必须存在才能更改其角色成员身份。</span><span class="sxs-lookup"><span data-stu-id="013f6-152">The target database must exist before you change its role memberships.</span></span> <span data-ttu-id="013f6-153">在这种情况下，您需要运行此脚本*后*数据库部署。</span><span class="sxs-lookup"><span data-stu-id="013f6-153">As such, you need to run this script *after* the database deployment.</span></span>
- <span data-ttu-id="013f6-154">您需要包含一个条件，以便仅用于测试环境执行的脚本。</span><span class="sxs-lookup"><span data-stu-id="013f6-154">You need to include a condition so that the script is only executed for test environments.</span></span>
- <span data-ttu-id="013f6-155">如果你正在运行"假设"部署&#x2014;换而言之，如果你正在生成部署脚本，但实际上未运行它们&#x2014;不应运行 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="013f6-155">If you're running a "what if" deployment&#x2014;in other words, if you're generating deployment scripts but not actually running them&#x2014;you shouldn't run the SQL script.</span></span>

<span data-ttu-id="013f6-156">如果您正使用拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，如下所示的联系人管理器示例解决方案，可以拆分的生成说明 SQL 脚本如下：</span><span class="sxs-lookup"><span data-stu-id="013f6-156">If you're using the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), as demonstrated by the Contact Manager sample solution, you can split the build instructions for your SQL script like this:</span></span>

- <span data-ttu-id="013f6-157">任何所需的特定于环境的属性，属性，用于确定是否要部署的权限，以及应该在特定于环境的项目文件中 (例如， *Env Dev.proj*)。</span><span class="sxs-lookup"><span data-stu-id="013f6-157">Any required environment-specific properties, together with the property that determines whether to deploy permissions, should go in the environment-specific project file (for example, *Env-Dev.proj*).</span></span>
- <span data-ttu-id="013f6-158">MSBuild 目标本身，以及将不会更改目标环境之间的任何属性应该在通用项目文件中 (例如， *Publish.proj*)。</span><span class="sxs-lookup"><span data-stu-id="013f6-158">The MSBuild target itself, together with any properties that will not change between destination environments, should go in the universal project file (for example, *Publish.proj*).</span></span>

<span data-ttu-id="013f6-159">在特定于环境的项目文件中，您需要定义数据库服务器名称、 目标数据库名称和一个布尔属性，使用户可以指定是否部署角色成员身份。</span><span class="sxs-lookup"><span data-stu-id="013f6-159">In the environment-specific project file, you need to define the database server name, the target database name, and a Boolean property that lets the user specify whether to deploy role memberships.</span></span>


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]


<span data-ttu-id="013f6-160">在通用项目文件中，你需要提供 sqlcmd 可执行文件的位置以及你想要运行的 SQL 脚本的位置。</span><span class="sxs-lookup"><span data-stu-id="013f6-160">In the universal project file, you need to provide the location of the sqlcmd executable and the location of the SQL script you want to run.</span></span> <span data-ttu-id="013f6-161">这些属性将保持不变而不考虑目标环境。</span><span class="sxs-lookup"><span data-stu-id="013f6-161">These properties will remain the same regardless of the destination environment.</span></span> <span data-ttu-id="013f6-162">此外需要创建一个 MSBuild 目标执行 sqlcmd 命令。</span><span class="sxs-lookup"><span data-stu-id="013f6-162">You also need to create an MSBuild target to execute the sqlcmd command.</span></span>


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]


<span data-ttu-id="013f6-163">请注意将 sqlcmd 可执行文件的位置添加作为静态属性，因为这可能是到其他目标很有用。</span><span class="sxs-lookup"><span data-stu-id="013f6-163">Notice that you add the location of the sqlcmd executable as a static property, as this could be useful to other targets.</span></span> <span data-ttu-id="013f6-164">与此相反，您定义 SQL 脚本的位置和 sqlcmd 命令的语法在目标内的动态属性作为它们将不会需要之前执行该目标。</span><span class="sxs-lookup"><span data-stu-id="013f6-164">In contrast, you define the location of your SQL script and the syntax of the sqlcmd command as dynamic properties within the target, as they will not be required before the target is executed.</span></span> <span data-ttu-id="013f6-165">在这种情况下， **DeployTestDBPermissions**满足这些条件时，才会执行目标：</span><span class="sxs-lookup"><span data-stu-id="013f6-165">In this case, the **DeployTestDBPermissions** target will only be executed if these conditions are met:</span></span>

- <span data-ttu-id="013f6-166">**DeployTestDBRoleMemberships**属性设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="013f6-166">The **DeployTestDBRoleMemberships** property is set to **true**.</span></span>
- <span data-ttu-id="013f6-167">用户未指定**WhatIf = true**标志。</span><span class="sxs-lookup"><span data-stu-id="013f6-167">The user hasn't specified a **WhatIf=true** flag.</span></span>

<span data-ttu-id="013f6-168">最后，别忘了调用目标。</span><span class="sxs-lookup"><span data-stu-id="013f6-168">Finally, don't forget to invoke the target.</span></span> <span data-ttu-id="013f6-169">在中*Publish.proj*文件中，您可以执行此操作通过将目标添加到默认值的依赖项列表**FullPublish**目标。</span><span class="sxs-lookup"><span data-stu-id="013f6-169">In the *Publish.proj* file, you can do this by adding the target to the dependency list for the default **FullPublish** target.</span></span> <span data-ttu-id="013f6-170">您需要确保**DeployTestDBPermissions**之前未执行目标**PublishDbPackages**执行目标。</span><span class="sxs-lookup"><span data-stu-id="013f6-170">You need to ensure that the **DeployTestDBPermissions** target is not executed until the **PublishDbPackages** target has been executed.</span></span>


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]


## <a name="conclusion"></a><span data-ttu-id="013f6-171">结束语</span><span class="sxs-lookup"><span data-stu-id="013f6-171">Conclusion</span></span>

<span data-ttu-id="013f6-172">本主题描述了在其中您可以添加数据库用户和角色成员身份作为后期部署操作部署数据库项目时的一种方法。</span><span class="sxs-lookup"><span data-stu-id="013f6-172">This topic described one way in which you can add database users and role memberships as a post-deployment action when you deploy a database project.</span></span> <span data-ttu-id="013f6-173">定期重新创建数据库在测试环境中，但通常当将数据库部署到过渡或生产环境时要避免这样做时，这是通常很有用。</span><span class="sxs-lookup"><span data-stu-id="013f6-173">This is typically useful when you regularly re-create a database in a test environment, but it should usually be avoided when you deploy databases to staging or production environments.</span></span> <span data-ttu-id="013f6-174">在这种情况下，应确保使用所需的条件逻辑，以便适合要执行此操作时仅创建数据库用户和角色成员身份。</span><span class="sxs-lookup"><span data-stu-id="013f6-174">As such, you should ensure that you use the necessary conditional logic so that database users and role memberships are only created when it's appropriate to do so.</span></span>

## <a name="further-reading"></a><span data-ttu-id="013f6-175">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="013f6-175">Further Reading</span></span>

<span data-ttu-id="013f6-176">有关使用 VSDBCMD 部署数据库项目的详细信息，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="013f6-176">For more information on using VSDBCMD to deploy database projects, see [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="013f6-177">有关自定义不同的目标环境的数据库部署的指导，请参阅[多个环境自定义数据库部署](customizing-database-deployments-for-multiple-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="013f6-177">For guidance on customizing database deployments for different target environments, see [Customizing Database Deployments for Multiple Environments](customizing-database-deployments-for-multiple-environments.md).</span></span> <span data-ttu-id="013f6-178">使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)并[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="013f6-178">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="013f6-179">Sqlcmd 命令行选项的详细信息，请参阅[sqlcmd 实用工具](https://msdn.microsoft.com/library/ms162773.aspx)。</span><span class="sxs-lookup"><span data-stu-id="013f6-179">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="013f6-180">[上一页](customizing-database-deployments-for-multiple-environments.md)
> [下一页](deploying-membership-databases-to-enterprise-environments.md)</span><span class="sxs-lookup"><span data-stu-id="013f6-180">[Previous](customizing-database-deployments-for-multiple-environments.md)
[Next](deploying-membership-databases-to-enterprise-environments.md)</span></span>
