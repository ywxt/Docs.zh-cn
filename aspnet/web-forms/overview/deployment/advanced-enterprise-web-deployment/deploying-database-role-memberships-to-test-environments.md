---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: "将数据库角色成员身份部署到测试环境 |Microsoft 文档"
author: jrjlee
description: "本主题介绍如何将用户帐户添加到解决方案部署到测试环境的一部分的数据库角色。 当你部署的解决方案包含..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: 226c28622f76e866fba1fc33cf9b9b7a01e5295b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="deploying-database-role-memberships-to-test-environments"></a><span data-ttu-id="b4ccd-104">将数据库角色成员身份部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="b4ccd-104">Deploying Database Role Memberships to Test Environments</span></span>
====================
<span data-ttu-id="b4ccd-105">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="b4ccd-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="b4ccd-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="b4ccd-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="b4ccd-107">本主题介绍如何将用户帐户添加到解决方案部署到测试环境的一部分的数据库角色。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-107">This topic describes how to add user accounts to database roles as part of a solution deployment to a test environment.</span></span>
> 
> <span data-ttu-id="b4ccd-108">在部署包含过渡或生产环境的数据库项目的解决方案时，你通常不想开发人员可以自动执行添加到数据库角色的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-108">When you deploy a solution containing a database project to a staging or production environment, you typically don't want the developer to automate the addition of user accounts to database roles.</span></span> <span data-ttu-id="b4ccd-109">在大多数情况下，开发人员不会知道哪些用户帐户需要添加到哪些数据库角色，并随时可以更改这些要求。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-109">In most cases, the developer won't know which user accounts need to be added to which database roles, and these requirements could change at any time.</span></span> <span data-ttu-id="b4ccd-110">但是，当你部署的解决方案包含一个数据库项目与一个开发或测试环境，这种情况通常是而不同：</span><span class="sxs-lookup"><span data-stu-id="b4ccd-110">However, when you deploy a solution containing a database project to a development or test environment, the situation is usually rather different:</span></span>
> 
> - <span data-ttu-id="b4ccd-111">开发人员通常重新部署解决方案定期，通常多次一天。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-111">The developer typically re-deploys the solution on a regular basis, often several times a day.</span></span>
> - <span data-ttu-id="b4ccd-112">通常在每个部署，这意味着数据库用户必须创建和添加到角色中每个部署后重新创建该数据库。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-112">The database is typically re-created on every deployment, which means that database users must be created and added to roles after every deployment.</span></span>
> - <span data-ttu-id="b4ccd-113">开发人员通常具有对目标开发或测试环境的完全控制。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-113">The developer typically has full control over the target development or test environment.</span></span>
> 
> <span data-ttu-id="b4ccd-114">在此方案中，通常很有利，可自动创建数据库用户并将数据库角色成员身份分配作为部署过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-114">In this scenario, it's often beneficial to automatically create database users and assign database role memberships as part of the deployment process.</span></span>
> 
> <span data-ttu-id="b4ccd-115">关键因素是，此操作需要条件基于目标环境。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-115">The key factor is that this operation needs to be conditional based on the target environment.</span></span> <span data-ttu-id="b4ccd-116">如果你要部署到过渡或生产环境，你想要跳过该操作。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-116">If you're deploying to a staging or a production environment, you want to skip the operation.</span></span> <span data-ttu-id="b4ccd-117">如果你正在将部署到开发人员或测试环境，你想要部署角色成员身份，而无需进一步的干预。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-117">If you're deploying to a developer or test environment, you want to deploy role memberships without further intervention.</span></span> <span data-ttu-id="b4ccd-118">本主题介绍一种方法可用来应对此挑战。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-118">This topic describes one approach you can use to address this challenge.</span></span>


<span data-ttu-id="b4ccd-119">本主题窗体的基于名为 Fabrikam，Inc.的虚构公司的企业部署要求的教程系列中的一部分本系列教程使用的示例解决方案 （&） #x 2014;[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; 来表示具有现实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 的 web 应用程序Communication Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="b4ccd-120">这些教程的核心的部署方法取决于中介绍的拆分项目文件方法[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在其中生成过程控制由两个项目文件 （&） #x 2014; 一个包含生成适用于每种目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="b4ccd-121">在生成期间，特定于环境的项目文件合并到环境无关的项目文件中以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="b4ccd-122">任务概述</span><span class="sxs-lookup"><span data-stu-id="b4ccd-122">Task Overview</span></span>

<span data-ttu-id="b4ccd-123">本主题假定：</span><span class="sxs-lookup"><span data-stu-id="b4ccd-123">This topic assumes that:</span></span>

- <span data-ttu-id="b4ccd-124">中所述使用解决方案部署的拆分项目文件方法[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-124">You use the split project file approach to solution deployment, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span>
- <span data-ttu-id="b4ccd-125">中所述从项目文件以部署数据库项目时，调用 VSDBCMD[了解该生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-125">You call VSDBCMD from the project file to deploy your database project, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

<span data-ttu-id="b4ccd-126">若要创建数据库用户并分配角色成员身份，数据库项目部署到测试环境时，你将需要：</span><span class="sxs-lookup"><span data-stu-id="b4ccd-126">To create database users and assign role memberships when you deploy a database project to a test environment, you'll need to:</span></span>

- <span data-ttu-id="b4ccd-127">创建一个将做出必要的数据库更改的 Transact 结构化查询语言 (Transact SQL) 脚本。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-127">Create a Transact Structured Query Language (Transact-SQL) script that makes the necessary database changes.</span></span>
- <span data-ttu-id="b4ccd-128">创建的 Microsoft Build Engine (MSBuild) 目标，使用 sqlcmd.exe 实用程序来运行 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-128">Create a Microsoft Build Engine (MSBuild) target that uses the sqlcmd.exe utility to run the SQL script.</span></span>
- <span data-ttu-id="b4ccd-129">配置你的项目文件时要调用目标正在将解决方案部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-129">Configure your project files to invoke the target when you're deploying your solution to a test environment.</span></span>

<span data-ttu-id="b4ccd-130">本主题将演示如何执行每个这些过程。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-130">This topic will show you how to perform each of these procedures.</span></span>

## <a name="scripting-the-database-role-memberships"></a><span data-ttu-id="b4ccd-131">脚本的数据库角色成员身份</span><span class="sxs-lookup"><span data-stu-id="b4ccd-131">Scripting the Database Role Memberships</span></span>

<span data-ttu-id="b4ccd-132">可以在许多不同的方式，创建 TRANSACT-SQL 脚本，然后在任何位置，你选择。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-132">You can create a Transact-SQL script in a lot of different ways, and in any location you choose.</span></span> <span data-ttu-id="b4ccd-133">最简单的方法是在 Visual Studio 2010 中创建你的解决方案内的脚本。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-133">The easiest approach is to create the script within your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="b4ccd-134">**若要创建 SQL 脚本**</span><span class="sxs-lookup"><span data-stu-id="b4ccd-134">**To create a SQL script**</span></span>

1. <span data-ttu-id="b4ccd-135">在**解决方案资源管理器**窗口中，展开你的数据库项目节点。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-135">In the **Solution Explorer** window, expand your database project node.</span></span>
2. <span data-ttu-id="b4ccd-136">右键单击**脚本**文件夹，指向**添加**，然后单击**新文件夹**。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-136">Right-click the **Scripts** folder, point to **Add**, and then click **New Folder**.</span></span>
3. <span data-ttu-id="b4ccd-137">类型**测试**作为文件夹名称，然后按 enter 键。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-137">Type **Test** as the folder name, and then press Enter.</span></span>
4. <span data-ttu-id="b4ccd-138">右键单击**测试**文件夹，指向**添加**，然后单击**脚本**。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-138">Right-click the **Test** folder, point to **Add**, and then click **Script**.</span></span>
5. <span data-ttu-id="b4ccd-139">在**添加新项**对话框框中，为你的脚本提供有意义的名称 (例如， **AddRoleMemberships.sql**)，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-139">In the **Add New Item** dialog box, give your script a meaningful name (for example, **AddRoleMemberships.sql**), and then click **Add**.</span></span>

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. <span data-ttu-id="b4ccd-140">在*AddRoleMemberships.sql*文件中，添加 TRANSACT-SQL 语句的：</span><span class="sxs-lookup"><span data-stu-id="b4ccd-140">In the *AddRoleMemberships.sql* file, add Transact-SQL statements that:</span></span>

    1. <span data-ttu-id="b4ccd-141">创建将访问你的数据库的 SQL Server 登录名的数据库用户。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-141">Create a database user for the SQL Server login that will access your database.</span></span>
    2. <span data-ttu-id="b4ccd-142">将数据库用户添加到任何所需的数据库角色。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-142">Add the database user to any required database roles.</span></span>
7. <span data-ttu-id="b4ccd-143">该文件应类似如下：</span><span class="sxs-lookup"><span data-stu-id="b4ccd-143">The file should resemble this:</span></span>

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. <span data-ttu-id="b4ccd-144">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-144">Save the file.</span></span>

## <a name="executing-the-script-on-the-target-database"></a><span data-ttu-id="b4ccd-145">在目标数据库上执行脚本</span><span class="sxs-lookup"><span data-stu-id="b4ccd-145">Executing the Script on the Target Database</span></span>

<span data-ttu-id="b4ccd-146">理想情况下，在部署您的数据库项目时将作为部署后脚本的一部分运行任何所需的 TRANSACT-SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-146">Ideally, you'd run any required Transact-SQL scripts as part of a post-deployment script when you deploy your database project.</span></span> <span data-ttu-id="b4ccd-147">但是，部署后脚本不允许您执行有条件地根据解决方案配置或生成属性的逻辑。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-147">However, post-deployment scripts don't allow you to execute logic conditionally based on solution configurations or build properties.</span></span> <span data-ttu-id="b4ccd-148">替代项是直接从 MSBuild 项目文件中，运行您的 SQL 脚本，通过创建**目标**执行 sqlcmd.exe 命令的元素。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-148">The alternative is to run your SQL scripts directly from the MSBuild project file, by creating a **Target** element that executes a sqlcmd.exe command.</span></span> <span data-ttu-id="b4ccd-149">此命令可用于在目标数据库上运行你的脚本：</span><span class="sxs-lookup"><span data-stu-id="b4ccd-149">You can use this command to run your script on the target database:</span></span>


[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]


> [!NOTE]
> <span data-ttu-id="b4ccd-150">Sqlcmd 命令行选项的详细信息，请参阅[sqlcmd 实用工具](https://msdn.microsoft.com/library/ms162773.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-150">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>


<span data-ttu-id="b4ccd-151">此命令嵌入的 MSBuild 目标之前，你需要考虑在什么条件下你想要运行的脚本：</span><span class="sxs-lookup"><span data-stu-id="b4ccd-151">Before you embed this command in an MSBuild target, you need to consider under what conditions you want the script to run:</span></span>

- <span data-ttu-id="b4ccd-152">在更改其角色成员身份之前，必须存在目标数据库。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-152">The target database must exist before you change its role memberships.</span></span> <span data-ttu-id="b4ccd-153">在这种情况下，你需要运行此脚本*后*的数据库部署。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-153">As such, you need to run this script *after* the database deployment.</span></span>
- <span data-ttu-id="b4ccd-154">你需要包括的条件，以便仅用于测试环境执行该脚本。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-154">You need to include a condition so that the script is only executed for test environments.</span></span>
- <span data-ttu-id="b4ccd-155">如果你正在运行的"假设"部署 （&） #x 2014; 换而言之，如果你正在生成部署脚本，但不是实际运行它们 （&） #x 2014; 你不应运行 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-155">If you're running a "what if" deployment&#x2014;in other words, if you're generating deployment scripts but not actually running them&#x2014;you shouldn't run the SQL script.</span></span>

<span data-ttu-id="b4ccd-156">如果你使用的拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，如的联系人管理器示例解决方案所示，你可以将构建说明拆分 SQL 脚本如下：</span><span class="sxs-lookup"><span data-stu-id="b4ccd-156">If you're using the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), as demonstrated by the Contact Manager sample solution, you can split the build instructions for your SQL script like this:</span></span>

- <span data-ttu-id="b4ccd-157">任何所需的特定于环境的属性，属性，用于确定是否将部署权限，以及应该在特定于环境的项目文件中 (例如， *Env Dev.proj*)。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-157">Any required environment-specific properties, together with the property that determines whether to deploy permissions, should go in the environment-specific project file (for example, *Env-Dev.proj*).</span></span>
- <span data-ttu-id="b4ccd-158">MSBuild 目标本身，以及将不会更改目标环境之间的任何属性应该在通用项目文件中 (例如， *Publish.proj*)。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-158">The MSBuild target itself, together with any properties that will not change between destination environments, should go in the universal project file (for example, *Publish.proj*).</span></span>

<span data-ttu-id="b4ccd-159">在特定于环境的项目文件中，你需要定义数据库服务器名称、 目标数据库名称和允许用户指定是否将部署角色成员身份的布尔值属性。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-159">In the environment-specific project file, you need to define the database server name, the target database name, and a Boolean property that lets the user specify whether to deploy role memberships.</span></span>


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]


<span data-ttu-id="b4ccd-160">在通用项目文件中，你需要提供 sqlcmd 可执行文件的位置以及你想要运行的 SQL 脚本的位置。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-160">In the universal project file, you need to provide the location of the sqlcmd executable and the location of the SQL script you want to run.</span></span> <span data-ttu-id="b4ccd-161">这些属性将保持不变，而目标环境无关。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-161">These properties will remain the same regardless of the destination environment.</span></span> <span data-ttu-id="b4ccd-162">你还需要创建用于执行 sqlcmd 命令 MSBuild 目标。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-162">You also need to create an MSBuild target to execute the sqlcmd command.</span></span>


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]


<span data-ttu-id="b4ccd-163">请注意将 sqlcmd 可执行文件的位置添加为静态属性，这可能十分有用到其他目标。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-163">Notice that you add the location of the sqlcmd executable as a static property, as this could be useful to other targets.</span></span> <span data-ttu-id="b4ccd-164">与此相反，你定义你的 SQL 脚本的位置和 sqlcmd 命令的语法为目标内的动态属性将不需要执行目标之前。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-164">In contrast, you define the location of your SQL script and the syntax of the sqlcmd command as dynamic properties within the target, as they will not be required before the target is executed.</span></span> <span data-ttu-id="b4ccd-165">在这种情况下， **DeployTestDBPermissions**如果满足这些条件，将仅执行目标：</span><span class="sxs-lookup"><span data-stu-id="b4ccd-165">In this case, the **DeployTestDBPermissions** target will only be executed if these conditions are met:</span></span>

- <span data-ttu-id="b4ccd-166">**DeployTestDBRoleMemberships**属性设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-166">The **DeployTestDBRoleMemberships** property is set to **true**.</span></span>
- <span data-ttu-id="b4ccd-167">用户未指定**WhatIf = true**标志。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-167">The user hasn't specified a **WhatIf=true** flag.</span></span>

<span data-ttu-id="b4ccd-168">最后，不要忘记调用目标。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-168">Finally, don't forget to invoke the target.</span></span> <span data-ttu-id="b4ccd-169">在*Publish.proj*文件，你可以执行此操作通过将目标添加到默认值的依赖项列表**FullPublish**目标。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-169">In the *Publish.proj* file, you can do this by adding the target to the dependency list for the default **FullPublish** target.</span></span> <span data-ttu-id="b4ccd-170">你需要确保**DeployTestDBPermissions**直到才执行目标**PublishDbPackages**目标已执行。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-170">You need to ensure that the **DeployTestDBPermissions** target is not executed until the **PublishDbPackages** target has been executed.</span></span>


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]


## <a name="conclusion"></a><span data-ttu-id="b4ccd-171">结束语</span><span class="sxs-lookup"><span data-stu-id="b4ccd-171">Conclusion</span></span>

<span data-ttu-id="b4ccd-172">本主题介绍一种方法可以在其中你添加数据库用户和角色成员身份作为后期部署操作部署数据库项目时。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-172">This topic described one way in which you can add database users and role memberships as a post-deployment action when you deploy a database project.</span></span> <span data-ttu-id="b4ccd-173">当你定期重新创建在测试环境中，一个数据库，但它通常如果应避免在将数据库部署到过渡环境或生产环境时，这是通常有用。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-173">This is typically useful when you regularly re-create a database in a test environment, but it should usually be avoided when you deploy databases to staging or production environments.</span></span> <span data-ttu-id="b4ccd-174">在这种情况下，应确保你使用的所需的条件逻辑，以便相应若要这样做时仅创建数据库用户和角色成员身份。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-174">As such, you should ensure that you use the necessary conditional logic so that database users and role memberships are only created when it's appropriate to do so.</span></span>

## <a name="further-reading"></a><span data-ttu-id="b4ccd-175">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="b4ccd-175">Further Reading</span></span>

<span data-ttu-id="b4ccd-176">使用 VSDBCMD 部署数据库项目的详细信息，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-176">For more information on using VSDBCMD to deploy database projects, see [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="b4ccd-177">有关自定义不同的目标环境的数据库部署的指南，请参阅[为多个环境自定义数据库部署](customizing-database-deployments-for-multiple-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-177">For guidance on customizing database deployments for different target environments, see [Customizing Database Deployments for Multiple Environments](customizing-database-deployments-for-multiple-environments.md).</span></span> <span data-ttu-id="b4ccd-178">使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解该生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-178">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="b4ccd-179">Sqlcmd 命令行选项的详细信息，请参阅[sqlcmd 实用工具](https://msdn.microsoft.com/library/ms162773.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b4ccd-179">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="b4ccd-180">[上一页](customizing-database-deployments-for-multiple-environments.md)
[下一页](deploying-membership-databases-to-enterprise-environments.md)</span><span class="sxs-lookup"><span data-stu-id="b4ccd-180">[Previous](customizing-database-deployments-for-multiple-environments.md)
[Next](deploying-membership-databases-to-enterprise-environments.md)</span></span>
