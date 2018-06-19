---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: 源代码管理 （使用 Azure 构建真实世界云应用） |Microsoft 文档
author: MikeWasson
description: 构建真实世界云应用程序与 Azure 的电子书基于由 Scott Guthrie 的演示。 它还说明了 13 模式和实践，他可以...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/23/2015
ms.topic: article
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: 0022458fa89a3be7ee8303750ad0e072df3b1bab
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875690"
---
<a name="source-control-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="f5ae8-104">源代码管理 （使用 Azure 构建真实世界云应用）</span><span class="sxs-lookup"><span data-stu-id="f5ae8-104">Source Control (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="f5ae8-105">通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f5ae8-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="f5ae8-106">[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="f5ae8-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="f5ae8-107">**构建真实世界云应用程序与 Azure**电子书基于由 Scott Guthrie 的演示。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="f5ae8-108">它还说明了 13 模式和实践，从而帮助你为成功开发适用于云中的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="f5ae8-109">有关电子书的信息，请参阅[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="f5ae8-110">源代码管理的所有云开发项目，而不仅仅是团队环境至关重要。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-110">Source control is essential for all cloud development projects, not just team environments.</span></span> <span data-ttu-id="f5ae8-111">你不会认为的编辑源代码或甚至 Word 文档，无需撤消的功能和自动备份和源控件提供这些函数在项目级别它们可以在其中保存时出现问题的更多时间。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-111">You wouldn't think of editing source code or even a Word document without an undo function and automatic backups, and source control gives you those functions at a project level where they can save even more time when something goes wrong.</span></span> <span data-ttu-id="f5ae8-112">与云源控件服务，你不再需要担心复杂的设置，并可以使用 Visual Studio Online 为最多 5 个用户可用的源代码管理。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-112">With cloud source control services, you no longer have to worry about complicated set-up, and you can use Visual Studio Online source control free for up to 5 users.</span></span>

<span data-ttu-id="f5ae8-113">本章的第一部分介绍了三个关键的最佳做法要记住：</span><span class="sxs-lookup"><span data-stu-id="f5ae8-113">The first part of this chapter explains three key best practices to keep in mind:</span></span>

- <span data-ttu-id="f5ae8-114">[自动化脚本视为源代码](#scripts)和版本以及应用程序代码对其。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-114">[Treat automation scripts as source code](#scripts) and version them together with your application code.</span></span>
- <span data-ttu-id="f5ae8-115">[中的机密永远不会检查](#secrets)（例如凭据的敏感数据） 到源代码存储库。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-115">[Never check in secrets](#secrets) (sensitive data such as credentials) into a source code repository.</span></span>
- <span data-ttu-id="f5ae8-116">[设置源分支](#devops)启用 DevOps 工作流。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-116">[Set up source branches](#devops) to enable the DevOps workflow.</span></span>

<span data-ttu-id="f5ae8-117">本章的其余部分提供了这些模式在 Visual Studio、 Azure 和 Visual Studio Online 中的某些示例实现：</span><span class="sxs-lookup"><span data-stu-id="f5ae8-117">The remainder of the chapter gives some sample implementations of these patterns in Visual Studio, Azure, and Visual Studio Online:</span></span>

- [<span data-ttu-id="f5ae8-118">将脚本添加到 Visual Studio 中的源控件</span><span class="sxs-lookup"><span data-stu-id="f5ae8-118">Add scripts to source control in Visual Studio</span></span>](#vsscripts)
- [<span data-ttu-id="f5ae8-119">在 Azure 中存储敏感数据</span><span class="sxs-lookup"><span data-stu-id="f5ae8-119">Store sensitive data in Azure</span></span>](#appsettings)
- [<span data-ttu-id="f5ae8-120">在 Visual Studio 和 Visual Studio Online 中使用 Git</span><span class="sxs-lookup"><span data-stu-id="f5ae8-120">Use Git in Visual Studio and Visual Studio Online</span></span>](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a><span data-ttu-id="f5ae8-121">自动化脚本视为源代码</span><span class="sxs-lookup"><span data-stu-id="f5ae8-121">Treat automation scripts as source code</span></span>

<span data-ttu-id="f5ae8-122">在你使用在云项目时您要频繁更改操作，并且你想要能够快速响应由你的客户报告的问题。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-122">When you're working on a cloud project you're changing things frequently and you want to be able to react quickly to issues reported by your customers.</span></span> <span data-ttu-id="f5ae8-123">快速响应涉及使用自动化脚本中所述[使一切自动化](automate-everything.md)章。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-123">Responding quickly involves using automation scripts, as explained in the [Automate Everything](automate-everything.md) chapter.</span></span> <span data-ttu-id="f5ae8-124">所有用于创建你的环境，脚本将部署到它，它等，需要与你的应用程序的源代码同步的小数位数。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-124">All of the scripts that you use to create your environment, deploy to it, scale it, etc., need to be in sync with your application source code.</span></span>

<span data-ttu-id="f5ae8-125">若要使脚本与代码同步，请将其存储在源代码管理系统中。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-125">To keep scripts in sync with code, store them in your source control system.</span></span> <span data-ttu-id="f5ae8-126">然后如果某个时候需要回滚更改或对不同于开发代码的生产代码中进行快速解决问题，你不必浪费时间想要跟踪哪些设置已更改或哪些团队成员具有所需的版本的副本。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-126">Then if you ever need to roll back changes or make a quick fix to production code which is different from development code, you don't have to waste time trying to track down which settings have changed or which team members have copies of the version you need.</span></span> <span data-ttu-id="f5ae8-127">您就可以保证，你需要的脚本是与基本代码，你的需要您就可以保证所有团队成员都使用相同的脚本同步。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-127">You're assured that the scripts you need are in sync with the code base that you need them for, and you're assured that all team members are working with the same scripts.</span></span> <span data-ttu-id="f5ae8-128">然后你是否需要自动测试和部署热修复的生产或开发新的功能，你将有正确的脚本需要更新的代码。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-128">Then whether you need to automate testing and deployment of a hot fix to production or new feature development, you'll have the right script for the code that needs to be updated.</span></span>

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a><span data-ttu-id="f5ae8-129">未签入机密</span><span class="sxs-lookup"><span data-stu-id="f5ae8-129">Don't check in secrets</span></span>

<span data-ttu-id="f5ae8-130">通常可太多的人，它是一个密码等敏感数据的适当安全位置到源代码存储库进行访问。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-130">A source code repository is typically accessible to too many people for it to be an appropriately secure place for sensitive data such as passwords.</span></span> <span data-ttu-id="f5ae8-131">如果脚本依赖于机密例如密码，参数化这些设置，以便它们不保存在源代码中，并将存储您的机密信息的其他位置。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-131">If scripts rely on secrets such as passwords, parameterize those settings so that they don't get saved in source code, and store your secrets somewhere else.</span></span>

<span data-ttu-id="f5ae8-132">例如，Azure 可让你下载包含的文件以自动发布配置文件创建发布设置。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-132">For example, Azure lets you download files that contain publish settings in order to automate the creation of publish profiles.</span></span> <span data-ttu-id="f5ae8-133">这些文件包括用户名和密码用于列出被授权管理你的 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-133">These files include user names and passwords that are authorized to manage your Azure services.</span></span> <span data-ttu-id="f5ae8-134">如果你使用此方法来创建发布配置文件，并签入到源代码管理这些文件时，如果有权访问你的存储库的任何人都可以看到这些用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-134">If you use this method to create publish profiles, and if you check in these files to source control, anyone with access to your repository can see those user names and passwords.</span></span> <span data-ttu-id="f5ae8-135">你可以安全地将密码存储在发布配置文件本身由于对其进行加密，并且它是 *。 pubxml.user*默认情况下不包括在源代码管理中的文件。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-135">You can safely store the password in the publish profile itself because it's encrypted and it's in a *.pubxml.user* file that by default is not included in source control.</span></span>

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a><span data-ttu-id="f5ae8-136">结构源分支来促进 DevOps 工作流</span><span class="sxs-lookup"><span data-stu-id="f5ae8-136">Structure source branches to facilitate DevOps workflow</span></span>

<span data-ttu-id="f5ae8-137">在你的存储库中实现分支如何影响你能够同时开发新功能和在生产中修复问题。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-137">How you implement branches in your repository affects your ability to both develop new features and fix issues in production.</span></span> <span data-ttu-id="f5ae8-138">此处是中等的大量大小团队使用的模式：</span><span class="sxs-lookup"><span data-stu-id="f5ae8-138">Here is a pattern that a lot of medium sized teams use:</span></span>

![源分支结构](source-control/_static/image1.png)

<span data-ttu-id="f5ae8-140">主分支始终匹配是在生产环境中的代码。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-140">The master branch always matches code that is in production.</span></span> <span data-ttu-id="f5ae8-141">在开发生命周期中，主分支对应于不同阶段。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-141">Branches underneath master correspond to different stages in the development life cycle.</span></span> <span data-ttu-id="f5ae8-142">Development 分支是实现新功能的位置。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-142">The development branch is where you implement new features.</span></span> <span data-ttu-id="f5ae8-143">对于小团队可能只是必须 master 和开发，但我们通常建议人具有过渡分支开发和主机之间。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-143">For a small team you might just have master and development, but we often recommend that people have a staging branch between development and master.</span></span> <span data-ttu-id="f5ae8-144">用于最终集成测试更新移动到生产环境之前，可以使用过渡。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-144">You can use staging for final integration testing before an update is moved to production.</span></span>

<span data-ttu-id="f5ae8-145">对于较大的团队可能针对每个新的功能; 单独的分支对于小团队中，你可能必须签入到 development 分支的每个人。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-145">For big teams there may be separate branches for each new feature; for a smaller team you might have everyone checking in to the development branch.</span></span>

<span data-ttu-id="f5ae8-146">如果你有每项功能，分支功能 A 时准备你合并其源代码更改向上到开发分支和其他功能分支到向下。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-146">If you have a branch for each feature, when Feature A is ready you merge its source code changes up into the development branch and down into the other feature branches.</span></span> <span data-ttu-id="f5ae8-147">此合并进程的源代码可以非常耗时，并且若要避免该工作的同时仍保持功能分离，一些团队实现一种替代方法，调用*[功能切换](http://en.wikipedia.org/wiki/Feature_toggle)* （也称为*功能标志*)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-147">This source code merging process can be time-consuming, and to avoid that work while still keeping features separate, some teams implement an alternative called *[feature toggles](http://en.wikipedia.org/wiki/Feature_toggle)* (also known as *feature flags*).</span></span> <span data-ttu-id="f5ae8-148">这意味着所有的所有功能的代码都在同一个分支，但您启用或禁用通过使用代码中的交换机的每个功能。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-148">This means all of the code for all of the features is in the same branch, but you enable or disable each feature by using switches in the code.</span></span> <span data-ttu-id="f5ae8-149">例如，假设功能 A 是修复它应用任务，新的字段，并功能 B 添加缓存功能。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-149">For example, suppose Feature A is a new field for Fix It app tasks, and Feature B adds caching functionality.</span></span> <span data-ttu-id="f5ae8-150">这两项功能的代码可以出现在 development 分支，但应用程序将仅显示新字段时变量设置为 true，并且将仅使用缓存设置不同的变量时为 true。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-150">The code for both features can be in the development branch, but the app will only display the new field when a variable is set to true, and it will only use caching when a different variable is set to true.</span></span> <span data-ttu-id="f5ae8-151">如果功能 A 未准备好进行升级，但功能 B 可以，你可以升级所有到生产环境的代码与功能 A 开关设置为 off 并且功能 B 切换。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-151">If Feature A isn't ready to be promoted but the Feature B is ready, you can promote all of the code to Production with the Feature A switch off and the Feature B switch on.</span></span> <span data-ttu-id="f5ae8-152">你可以然后完成功能 A 并将其升级更高版本，所有与任何源代码合并。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-152">You can then finish Feature A and promote it later, all with no source code merging.</span></span>

<span data-ttu-id="f5ae8-153">无论使用分支或切换功能，如下的分支结构可以灵活和可重复的方式流动开发到生产环境中的代码。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-153">Whether or not you use branches or toggles for features, a branching structure like this enables you to flow your code from development into production in an agile and repeatable way.</span></span>

<span data-ttu-id="f5ae8-154">此结构还可以以快速响应客户反馈。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-154">This structure also enables you to react quickly to customer feedback.</span></span> <span data-ttu-id="f5ae8-155">如果你需要对生产进行快速解决问题，你可以还，有效地执行操作中以灵活的方式。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-155">If you need to make a quick fix to production, you can also do that efficiently in an agile way.</span></span> <span data-ttu-id="f5ae8-156">你可以创建从移出 master 或暂存，分支和何时准备好主数据时将其合并向上和向下到开发和功能的分支。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-156">You can create a branch off of master or staging, and when it's ready merge it up into master and down into development and feature branches.</span></span>

![修补程序分支](source-control/_static/image2.png)

<span data-ttu-id="f5ae8-158">没有具有其单独的生产和开发分支的分支结构如下，生产问题可能使您处于无需提升新功能的代码，以及生产修复的位置。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-158">Without a branching structure like this with its separation of production and development branches, a production problem could put you in the position of having to promote new feature code along with your production fix.</span></span> <span data-ttu-id="f5ae8-159">新功能代码中可能不是经过充分测试和准备好进行生产，而且可能需要执行大量工作正在放弃未准备好的更改。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-159">The new feature code might not be fully tested and ready for production and you might have to do a lot of work backing out changes that aren't ready.</span></span> <span data-ttu-id="f5ae8-160">或者，你可能必须延迟以便测试更改，并使其准备好部署修复。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-160">Or you might have to delay your fix in order to test changes and get them ready to deploy.</span></span>

<span data-ttu-id="f5ae8-161">接下来你将看到如何在 Visual Studio、 Azure 和 Visual Studio Online 中实现这些三种模式的示例。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-161">Next you'll see examples of how to implement these three patterns in Visual Studio, Azure, and Visual Studio Online.</span></span> <span data-ttu-id="f5ae8-162">这些是示例而不是详细的分步操作方法-到-执行-it 说明;提供所有必需的上下文的详细说明，请参阅[资源](#resources)章结尾部分。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-162">These are examples rather than detailed step-by-step how-to-do-it instructions; for detailed instructions that provide all of the context necessary, see the [Resources](#resources) section at the end of the chapter.</span></span>

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a><span data-ttu-id="f5ae8-163">将脚本添加到 Visual Studio 中的源控件</span><span class="sxs-lookup"><span data-stu-id="f5ae8-163">Add scripts to source control in Visual Studio</span></span>

<span data-ttu-id="f5ae8-164">它们包含在 Visual Studio 解决方案文件夹中 （假定你的项目在源代码管理中），可以将脚本添加到 Visual Studio 中的源控件。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-164">You can add scripts to source control in Visual Studio by including them in a Visual Studio solution folder (assuming your project is in source control).</span></span> <span data-ttu-id="f5ae8-165">此处是一种方法来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-165">Here's one way to do it.</span></span>

<span data-ttu-id="f5ae8-166">在解决方案文件夹中创建的脚本的文件夹 (为相同文件夹中你 *.sln*文件)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-166">Create a folder for the scripts in your solution folder (the same folder that has your *.sln* file).</span></span>

![自动化文件夹](source-control/_static/image3.png)

<span data-ttu-id="f5ae8-168">将脚本文件复制到的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-168">Copy the script files into the folder.</span></span>

![自动化文件夹内容](source-control/_static/image4.png)

<span data-ttu-id="f5ae8-170">在 Visual Studio 中，将添加到项目的解决方案文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-170">In Visual Studio, add a solution folder to the project.</span></span>

![新的解决方案文件夹菜单选择](source-control/_static/image5.png)

<span data-ttu-id="f5ae8-172">然后，将脚本文件添加到的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-172">And add the script files to the solution folder.</span></span>

![添加现有项菜单选择](source-control/_static/image6.png)

![“添加现有项”对话框](source-control/_static/image7.png)

<span data-ttu-id="f5ae8-175">你的项目中现在包含脚本文件和源控件在跟踪以及相应的源代码更改其版本更改。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-175">The script files are now included in your project and source control is tracking their version changes along with corresponding source code changes.</span></span>

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a><span data-ttu-id="f5ae8-176">在 Azure 中存储敏感数据</span><span class="sxs-lookup"><span data-stu-id="f5ae8-176">Store sensitive data in Azure</span></span>

<span data-ttu-id="f5ae8-177">如果在 Azure 网站中运行你的应用程序时，避免将凭据存储在源代码管理中的一种方法是将它们存储在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-177">If you run your application in an Azure Web Site, one way to avoid storing credentials in source control is to store them in Azure instead.</span></span>

<span data-ttu-id="f5ae8-178">例如，修复它应用程序将存储在其 Web.config 文件两个连接字符串，将要生产和访问你的 Azure 存储帐户的密钥中的密码。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-178">For example, the Fix It application stores in its Web.config file two connection strings that will have passwords in production and a key that gives access to your Azure storage account.</span></span>

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

<span data-ttu-id="f5ae8-179">如果将实际生产中的这些设置的值你*Web.config*文件，或如果将它们放在*Web.Release.config*文件来配置用于将其插入在部署期间，Web.config 转换它们将存储在源代码存储库中。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-179">If you put actual production values for these settings in your *Web.config* file, or if you put them in the *Web.Release.config* file to configure a Web.config transform to insert them during deployment, they'll be stored in the source repository.</span></span> <span data-ttu-id="f5ae8-180">如果在生产中输入数据库连接字符串时发布配置文件，密码将在你 *.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-180">If you enter the database connection strings into the production publish profile, the password will be in your *.pubxml* file.</span></span> <span data-ttu-id="f5ae8-181">(你无法排除 *.pubxml*从源代码管理文件，但共享所有其他部署设置的优势的丧失然后。)</span><span class="sxs-lookup"><span data-stu-id="f5ae8-181">(You could exclude the *.pubxml* file from source control, but then you lose the benefit of sharing all the other deployment settings.)</span></span>

<span data-ttu-id="f5ae8-182">Azure 允许你提供的备用**appSettings**和连接字符串的部分*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-182">Azure gives you an alternative for the **appSettings** and connection strings sections of the *Web.config* file.</span></span> <span data-ttu-id="f5ae8-183">以下是相关的部分**配置**Azure 管理门户中的 web 站点的选项卡：</span><span class="sxs-lookup"><span data-stu-id="f5ae8-183">Here is the relevant part of the **Configuration** tab for a web site in the Azure management portal:</span></span>

![appSettings 和在门户中的 connectionstrings 节](source-control/_static/image8.png)

<span data-ttu-id="f5ae8-185">在项目部署到此网站和应用程序运行时，具有在 Azure 中存储任何值重写任何值位于 Web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-185">When you deploy a project to this web site and the application runs, whatever values you have stored in Azure override whatever values are in the Web.config file.</span></span>

<span data-ttu-id="f5ae8-186">通过使用管理门户或脚本，可以在 Azure 中设置这些值。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-186">You can set these values in Azure by using either the management portal or scripts.</span></span> <span data-ttu-id="f5ae8-187">在中看到环境创建自动化脚本[使一切自动化](automate-everything.md)章创建 Azure SQL 数据库、 获取的存储和 SQL 数据库连接字符串，并将这些机密存储在您的网站的设置。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-187">The environment creation automation script you saw in the [Automate Everything](automate-everything.md) chapter creates an Azure SQL Database, gets the storage and SQL Database connection strings, and stores these secrets in the settings for your web site.</span></span>

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

<span data-ttu-id="f5ae8-188">请注意，以便实际值不保存到源存储库的脚本进行参数化。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-188">Notice that the scripts are parameterized so that actual values don't get persisted to the source repository.</span></span>

<span data-ttu-id="f5ae8-189">当你在开发环境中本地运行时，应用程序读取本地 Web.config 文件和您的连接字符串中的 LocalDB SQL Server 数据库指向*应用\_数据*您的 web 项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-189">When you run locally in your development environment, the app reads your local Web.config file and your connection string points to a LocalDB SQL Server database in the *App\_Data* folder of your web project.</span></span> <span data-ttu-id="f5ae8-190">在 Azure 中运行应用程序和应用程序尝试从 Web.config 文件中读取这些值，它重新获取并使用时对于网站，不是什么实际在 Web.config 文件中存储的值。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-190">When you run the app in Azure and the app tries to read these values from the Web.config file, what it gets back and uses are the values stored for the Web Site, not what's actually in Web.config file.</span></span>

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-visual-studio-online"></a><span data-ttu-id="f5ae8-191">在 Visual Studio 和 Visual Studio Online 中使用 Git</span><span class="sxs-lookup"><span data-stu-id="f5ae8-191">Use Git in Visual Studio and Visual Studio Online</span></span>

<span data-ttu-id="f5ae8-192">你可以使用任何源控件环境实现前面提供的 DevOps 分支结构。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-192">You can use any source control environment to implement the DevOps branching structure presented earlier.</span></span> <span data-ttu-id="f5ae8-193">分布式团队[分布式版本控制系统](http://en.wikipedia.org/wiki/Distributed_revision_control)(DVCS) 可以达到最佳效果; 对于其他团队[集中式系统](http://en.wikipedia.org/wiki/Revision_control)可能更好地工作。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-193">For distributed teams a [distributed version control system](http://en.wikipedia.org/wiki/Distributed_revision_control) (DVCS) might work best; for other teams a [centralized system](http://en.wikipedia.org/wiki/Revision_control) might work better.</span></span>

<span data-ttu-id="f5ae8-194">[Git](http://git-scm.com/)是 DVCS 变得非常流行。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-194">[Git](http://git-scm.com/) is a DVCS that is has become very popular.</span></span> <span data-ttu-id="f5ae8-195">当你使用 Git 进行源代码管理时，你将拥有其历史记录的所有存储库的完整副本，在本地计算机。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-195">When you use Git for source control, you have a complete copy of the repository with all of its history on your local computer.</span></span> <span data-ttu-id="f5ae8-196">很多人喜欢，因为可以很方便可以继续工作时未连接到网络-你可以继续执行提交并回滚，创建和切换分支，和等等。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-196">Many people prefer that because it's easier to continue working when you're not connected to the network -- you can continue to do commits and rollbacks, create and switch branches, and so forth.</span></span> <span data-ttu-id="f5ae8-197">即使你要连接到网络，它是更方便和快捷以创建分支并切换分支的所有内容时本地。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-197">Even when you're connected to the network, it's easier and quicker to create branches and switch branches when everything is local.</span></span> <span data-ttu-id="f5ae8-198">此外可以执行本地提交和回滚不会影响在其他开发人员。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-198">You can also do local commits and rollbacks without having an impact on other developers.</span></span> <span data-ttu-id="f5ae8-199">并且，你可以通过批处理提交之前将它们发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-199">And you can batch commits before sending them to the server.</span></span>

<span data-ttu-id="f5ae8-200">[Microsoft Visual Studio Online](https://www.visualstudio.com/)(VSO) 以前称为 Team Foundation Service 提供这两个 Git 和[Team Foundation 版本控制](https://msdn.microsoft.com/library/ms181237(v=vs.120).aspx)(TFVC; 集中式源代码管理)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-200">[Microsoft Visual Studio Online](https://www.visualstudio.com/)(VSO), formerly known as Team Foundation Service, offers both Git and [Team Foundation Version Control](https://msdn.microsoft.com/library/ms181237(v=vs.120).aspx) (TFVC; centralized source control).</span></span> <span data-ttu-id="f5ae8-201">此处在 Microsoft Azure 的组中某些团队使用集中式的源代码管理，某些使用分布式，而某些连接使用混合 （对于某些项目集中式和分布式对其他项目）。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-201">Here at Microsoft in the Azure group some teams use centralized source control, some use distributed, and some use a mix (centralized for some projects and distributed for other projects).</span></span> <span data-ttu-id="f5ae8-202">VSO 服务是免费的最多 5 个用户。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-202">The VSO service is free for up to 5 users.</span></span> <span data-ttu-id="f5ae8-203">你可以注册免费计划[此处](https://go.microsoft.com/fwlink/?LinkId=307137)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-203">You can sign up for a free plan [here](https://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="f5ae8-204">Visual Studio 2013 包含的内置第一类[Git 支持](https://msdn.microsoft.com/library/hh850437.aspx); 下面是快速的工作原理的演示。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-204">Visual Studio 2013 includes built-in first-class [Git support](https://msdn.microsoft.com/library/hh850437.aspx); here's a quick demo of how that works.</span></span>

<span data-ttu-id="f5ae8-205">在 Visual Studio 2013 中打开项目，右键单击该解决方案中的**解决方案资源管理器**，然后选择**将解决方案添加到源代码管理**。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-205">With a project open in Visual Studio 2013, right-click the solution in **Solution Explorer**, and choose **Add Solution to Source Control**.</span></span>

![将解决方案添加到源代码管理](source-control/_static/image9.png)

<span data-ttu-id="f5ae8-207">Visual Studio 会要求你想要使用 TFVC （集中式的版本控制） 或 Git。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-207">Visual Studio asks if you want to use TFVC (centralized version control) or Git.</span></span>

![选择源代码管理](source-control/_static/image10.png)

<span data-ttu-id="f5ae8-209">当您选择 Git 并单击**确定**，Visual Studio 在你的解决方案文件夹中创建新的本地 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-209">When you select Git and click **OK**, Visual Studio creates a new local Git repository in your solution folder.</span></span> <span data-ttu-id="f5ae8-210">新的存储库有任何文件尚未;你必须通过执行 Git commit 将它们添加到存储库。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-210">The new repository has no files yet; you have to add them to the repository by doing a Git commit.</span></span> <span data-ttu-id="f5ae8-211">右键单击该解决方案中的**解决方案资源管理器**，然后单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-211">Right-click the solution in **Solution Explorer**, and then click **Commit**.</span></span>

![提交](source-control/_static/image11.png)

<span data-ttu-id="f5ae8-213">Visual Studio 自动转移所有提交的项目文件，并将它们在列出**团队资源管理器**中**包含的更改**窗格。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-213">Visual Studio automatically stages all of the project files for the commit and lists them in **Team Explorer** in the **Included Changes** pane.</span></span> <span data-ttu-id="f5ae8-214">(如果存在一些你不想要包含在提交中，你可以选择它们，右键单击，然后单击**排除**。)</span><span class="sxs-lookup"><span data-stu-id="f5ae8-214">(If there were some you didn't want to include in the commit, you could select them, right-click, and click **Exclude**.)</span></span>

![Team Explorer](source-control/_static/image12.png)

<span data-ttu-id="f5ae8-216">输入提交注释，然后单击**提交**，Visual Studio 将执行提交并显示提交 id。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-216">Enter a commit comment and click **Commit**, and Visual Studio executes the commit and displays the commit ID.</span></span>

![团队资源管理器更改](source-control/_static/image13.png)

<span data-ttu-id="f5ae8-218">现在如果你更改某些代码，以便它与什么是存储库中都不同，你可以轻松地查看差异。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-218">Now if you change some code so that it's different from what's in the repository, you can easily view the differences.</span></span> <span data-ttu-id="f5ae8-219">右键单击您已更改，请选择一个文件**与 Unmodified 比较**，并获取比较显示它显示在你未提交的更改。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-219">Right-click a file that you've changed, select **Compare with Unmodified**, and you get a comparison display that shows your uncommitted change.</span></span>

![与未修改进行比较](source-control/_static/image14.png)

![显示更改的差异](source-control/_static/image15.png)

<span data-ttu-id="f5ae8-222">你可轻松看到哪些更改正在进行和签入。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-222">You can easily see what changes you're making and check them in.</span></span>

<span data-ttu-id="f5ae8-223">假设你需要进行分支 – 你可以执行该操作在 Visual Studio 中太。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-223">Suppose you need to make a branch – you can do that in Visual Studio too.</span></span> <span data-ttu-id="f5ae8-224">在**团队资源管理器**，单击**新分支**。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-224">In **Team Explorer**, click **New Branch**.</span></span>

![团队资源管理器中新的分支](source-control/_static/image16.png)

<span data-ttu-id="f5ae8-226">输入分支名称，单击**创建分支**，并且选中**签出分支**，Visual Studio 自动签出新分支。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-226">Enter a branch name, click **Create Branch**, and if you selected **Checkout branch**, Visual Studio automatically checks out the new branch.</span></span>

![团队资源管理器中新的分支](source-control/_static/image17.png)

<span data-ttu-id="f5ae8-228">你现在可以对文件进行更改并签入到此分支。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-228">You can now make changes to files and check them in to this branch.</span></span> <span data-ttu-id="f5ae8-229">并且可以轻松地切换分支和 Visual Studio 之间自动同步到者为准分支你的文件已签出。在此示例中的网页标题中 *\_Layout.cshtml*已更改为"热修复补丁程序 1"中 HotFix1 分支。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-229">And you can easily switch between branches and Visual Studio automatically syncs the files to whichever branch you have checked out. In this example the web page title in *\_Layout.cshtml* has been changed to "Hot Fix 1" in HotFix1 branch.</span></span>

![Hotfix1 分支](source-control/_static/image18.png)

<span data-ttu-id="f5ae8-231">如果你切换回主分支中的内容 *\_Layout.cshtml*文件自动还原到这些主分支中的凭据。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-231">If you switch back to the master branch, the contents of the *\_Layout.cshtml* file automatically revert to what they are in the master branch.</span></span>

![主分支](source-control/_static/image19.png)

<span data-ttu-id="f5ae8-233">此方式可以快速创建分支和分支之间来回翻转的一个简单的示例。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-233">This a simple example of how you can quickly create a branch and flip back and forth between branches.</span></span> <span data-ttu-id="f5ae8-234">此功能允许使用的分支结构高度 agile 工作流和自动化脚本中显示[使一切自动化](automate-everything.md)章。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-234">This feature enables a highly agile workflow using the branch structure and automation scripts presented in the [Automate Everything](automate-everything.md) chapter.</span></span> <span data-ttu-id="f5ae8-235">例如，你可以在 Development 分支中工作，创建从 master 中移出热修复补丁程序分支，切换到新分支，使所做的更改那里和提交更改，然后切换回开发分支并继续正在执行的操作。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-235">For example, you can be working in the Development branch, create a hot fix branch off of master, switch to the new branch, make your changes there and commit them, and then switch back to the Development branch and continue what you were doing.</span></span>

<span data-ttu-id="f5ae8-236">你已了解了您的工作方式与 Visual Studio 中的本地 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-236">What you've seen here is how you work with a local Git repository in Visual Studio.</span></span> <span data-ttu-id="f5ae8-237">在团队环境中你通常还将更改推送到的公共储存库。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-237">In a team environment you typically also push changes up to a common repository.</span></span> <span data-ttu-id="f5ae8-238">Visual Studio 工具还使你以指向远程 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-238">The Visual Studio tools also enable you to point to a remote Git repository.</span></span> <span data-ttu-id="f5ae8-239">你可以使用 GitHub.com 出于这个目的，或者可以使用[Visual Studio Online 中的 Git](https://msdn.microsoft.com/library/hh850437.aspx)与所有其他 Visual Studio Online 功能，例如工作项和 bug 跟踪集成在一起。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-239">You can use GitHub.com for that purpose, or you can use [Git in Visual Studio Online](https://msdn.microsoft.com/library/hh850437.aspx) integrated with all the other Visual Studio Online capabilities such as work item and bug tracking.</span></span>

<span data-ttu-id="f5ae8-240">这不是你可以实现敏捷的分支策略，这是当然的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-240">This isn't the only way you can implement an agile branching strategy, of course.</span></span> <span data-ttu-id="f5ae8-241">你可以启用使用集中式的源代码控制存储库的相同 agile 工作流。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-241">You can enable the same agile workflow using a centralized source control repository.</span></span>

## <a name="summary"></a><span data-ttu-id="f5ae8-242">总结</span><span class="sxs-lookup"><span data-stu-id="f5ae8-242">Summary</span></span>

<span data-ttu-id="f5ae8-243">衡量成功的源代码管理系统基于多快的速度，你可以进行更改，并获取它实时安全且可预测的方式。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-243">Measure the success of your source control system based on how quickly you can make a change and get it live in a safe and predictable way.</span></span> <span data-ttu-id="f5ae8-244">如果你发现自己害怕进行更改，因为你所要做一天或两个在其上的手动测试，您可能会问自己你需要执行 process-wise 或 test-wise，以便您可以使所做的更改，以分钟为单位或在最差不再比一小时。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-244">If you find yourself scared to make a change because you have to do a day or two of manual testing on it, you might ask yourself what you have to do process-wise or test-wise so that you can make that change in minutes or at worst no longer than an hour.</span></span> <span data-ttu-id="f5ae8-245">执行该操作的一个策略是以实现持续集成和持续交付，我们将介绍在[下一章](continuous-integration-and-continuous-delivery.md)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-245">One strategy for doing that is to implement continuous integration and continuous delivery, which we'll cover in the [next chapter](continuous-integration-and-continuous-delivery.md).</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="f5ae8-246">资源</span><span class="sxs-lookup"><span data-stu-id="f5ae8-246">Resources</span></span>

<span data-ttu-id="f5ae8-247">[Visual Studio Online](https://www.visualstudio.com/)门户提供文档和支持服务，并且你可以注册一个帐户。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-247">The [Visual Studio Online](https://www.visualstudio.com/) portal provides documentation and support services, and you can sign up for an account.</span></span> <span data-ttu-id="f5ae8-248">如果你有 Visual Studio 2012，并且想要使用 Git，请参阅[Visual Studio Tools for Git](https://visualstudiogallery.msdn.microsoft.com/abafc7d6-dcaa-40f4-8a5e-d6724bdb980c)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-248">If you have Visual Studio 2012 and would like to use Git, see [Visual Studio Tools for Git](https://visualstudiogallery.msdn.microsoft.com/abafc7d6-dcaa-40f4-8a5e-d6724bdb980c).</span></span>

<span data-ttu-id="f5ae8-249">有关 （集中式的版本控制） TFVC 和 Git （分布式的版本控制） 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="f5ae8-249">For more information about TFVC (centralized version control) and Git (distributed version control), see the following resources:</span></span>

- [<span data-ttu-id="f5ae8-250">应使用哪个版本控制系统： TFVC 或 Git？</span><span class="sxs-lookup"><span data-stu-id="f5ae8-250">Which version control system should I use: TFVC or Git?</span></span>](https://msdn.microsoft.com/library/vstudio/ms181368.aspx#tfvc_or_git_summary) <span data-ttu-id="f5ae8-251">MSDN 文档，包括汇总 TFVC 和 Git 之间的差异的表。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-251">MSDN documentation, includes a table summarizing the differences between TFVC and Git.</span></span>
- [<span data-ttu-id="f5ae8-252">嗯，我喜欢 Team Foundation Server 和我喜欢 Git，但这是更好？</span><span class="sxs-lookup"><span data-stu-id="f5ae8-252">Well, I like Team Foundation Server and I like Git, but which is better?</span></span>](https://blogs.msdn.com/b/visualstudiouk/archive/2013/08/05/well-i-like-team-foundation-server-and-i-like-git-but-which-is-better.aspx) <span data-ttu-id="f5ae8-253">Git 和 TFVC 的比较。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-253">Comparison of Git and TFVC.</span></span>

<span data-ttu-id="f5ae8-254">有关分支策略的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="f5ae8-254">For more information about branching strategies, see the following resources:</span></span>

- <span data-ttu-id="f5ae8-255">[生成使用 Team Foundation Server 2012 的发行管道](https://msdn.microsoft.com/library/dn449957.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-255">[Building a Release Pipeline with Team Foundation Server 2012](https://msdn.microsoft.com/library/dn449957.aspx).</span></span> <span data-ttu-id="f5ae8-256">Microsoft 模式和实践文档。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-256">Microsoft Patterns and Practices documentation.</span></span> <span data-ttu-id="f5ae8-257">请参阅有关的分支策略讨论的第 6 章。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-257">See chapter 6 for a discussion of branching strategies.</span></span> <span data-ttu-id="f5ae8-258">自身功能通过功能分支切换和如果使用的功能的分支，律师有帮助保持它们短生存期 （小时数或最多天）。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-258">Advocates feature toggles over feature branches, and if branches for features are used, advocates keeping them short-lived (hours or days at most).</span></span>
- <span data-ttu-id="f5ae8-259">[版本控制指南](https://aka.ms/vsarsolutions)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-259">[Version Control Guide](https://aka.ms/vsarsolutions).</span></span> <span data-ttu-id="f5ae8-260">由 ALM Rangers 指南分支策略。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-260">Guide to branching strategies by the ALM Rangers.</span></span> <span data-ttu-id="f5ae8-261">在下载选项卡上，请参阅分支 Strategies.pdf。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-261">See Branching Strategies.pdf on the Downloads tab.</span></span>
- <span data-ttu-id="f5ae8-262">[使用功能切换软件开发](https://msdn.microsoft.com/magazine/dn683796.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-262">[Software Development with Feature Toggles](https://msdn.microsoft.com/magazine/dn683796.aspx).</span></span> <span data-ttu-id="f5ae8-263">MSDN 杂志文章。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-263">MSDN Magazine article.</span></span>
- <span data-ttu-id="f5ae8-264">[功能切换](http://martinfowler.com/bliki/FeatureToggle.html)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-264">[Feature Toggle](http://martinfowler.com/bliki/FeatureToggle.html).</span></span> <span data-ttu-id="f5ae8-265">功能简介切换/功能 Martin Fowler 博客上的标志。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-265">Introduction to feature toggles / feature flags on Martin Fowler's blog.</span></span>
- <span data-ttu-id="f5ae8-266">[功能在切换 vs 功能分支](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-266">[Feature Toggles vs Feature Branches](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx).</span></span> <span data-ttu-id="f5ae8-267">有关功能开关，通过 Dylan Smith 的另一个博客文章。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-267">Another blog post about feature toggles, by Dylan Smith.</span></span>

<span data-ttu-id="f5ae8-268">有关如何处理不应保存在源控件存储库中的敏感信息的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="f5ae8-268">For more information about how to handle sensitive information that should not be kept in source control repositories, see the following resources:</span></span>

- <span data-ttu-id="f5ae8-269">[用于将密码和其他敏感数据部署到 ASP.NET 和 Azure App Service 的最佳做法](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-269">[Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
- <span data-ttu-id="f5ae8-270">[Azure 网站： 如何应用程序字符串和连接字符串的工作](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-270">[Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="f5ae8-271">介绍了重写的 Azure 功能`appSettings`和`connectionStrings`中的数据*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-271">Explains the Azure feature that overrides `appSettings` and `connectionStrings` data in the *Web.config* file.</span></span>
- <span data-ttu-id="f5ae8-272">[自定义配置和应用程序设置在 Azure 网站-使用 Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-272">[Custom configuration and application settings in Azure Web Sites - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/).</span></span>

<span data-ttu-id="f5ae8-273">若要保持出源控件的敏感信息的其他方法有关的信息，请参阅[ASP.NET MVC： 外出时的源代码管理中保留私有设置](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f5ae8-273">For information about other methods for keeping sensitive information out of source control, see [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f5ae8-274">[上一页](automate-everything.md)
> [下一页](continuous-integration-and-continuous-delivery.md)</span><span class="sxs-lookup"><span data-stu-id="f5ae8-274">[Previous](automate-everything.md)
[Next](continuous-integration-and-continuous-delivery.md)</span></span>
