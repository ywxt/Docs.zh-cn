---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: 自动执行所有内容 （构建使用 Azure 真实世界云应用） |Microsoft 文档
author: MikeWasson
description: 构建真实世界云应用程序与 Azure 的电子书基于由 Scott Guthrie 的演示。 它还说明了 13 模式和实践，他可以...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: 2e30ab7831a10f215a08f74e61adf2d147e76543
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="automate-everything-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="c9275-104">自动执行所有内容 （构建真实世界云应用与 Azure）</span><span class="sxs-lookup"><span data-stu-id="c9275-104">Automate Everything (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="c9275-105">通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c9275-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="c9275-106">[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="c9275-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="c9275-107">**构建真实世界云应用程序与 Azure**电子书基于由 Scott Guthrie 的演示。</span><span class="sxs-lookup"><span data-stu-id="c9275-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="c9275-108">它还说明了 13 模式和实践，从而帮助你为成功开发适用于云中的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="c9275-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="c9275-109">电子书的简介，请参阅[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="c9275-109">For an introduction to the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="c9275-110">我们将考察的前三个模式实际适用于任何软件开发项目一样，但特别是用于云项目。</span><span class="sxs-lookup"><span data-stu-id="c9275-110">The first three patterns we'll look at actually apply to any software development project, but especially to cloud projects.</span></span> <span data-ttu-id="c9275-111">此模式为有关自动执行开发任务。</span><span class="sxs-lookup"><span data-stu-id="c9275-111">This pattern is about automating development tasks.</span></span> <span data-ttu-id="c9275-112">它是一个重要的主题，因为手动流程速度慢而且容易出错;尽可能多的它们作为设置快速、 可靠且 agile 工作流的可能有助于实现自动化。</span><span class="sxs-lookup"><span data-stu-id="c9275-112">It's an important topic because manual processes are slow and error-prone; automating as many of them as possible helps set up a fast, reliable, and agile workflow.</span></span> <span data-ttu-id="c9275-113">它是云开发的唯一重要，因为你可以轻松地自动处理许多很难或无法在本地环境中自动运行的任务。</span><span class="sxs-lookup"><span data-stu-id="c9275-113">It's uniquely important for cloud development because you can easily automate many tasks that are difficult or impossible to automate in an on-premises environment.</span></span> <span data-ttu-id="c9275-114">例如，可以设置整个测试环境包括新的 web 服务器和后端 Vm，数据库，blob 存储 （文件存储）、 队列等。</span><span class="sxs-lookup"><span data-stu-id="c9275-114">For example, you can set up whole test environments including new web server and back-end VMs, databases, blob storage (file storage), queues, etc.</span></span>

## <a name="devops-workflow"></a><span data-ttu-id="c9275-115">DevOps 工作流</span><span class="sxs-lookup"><span data-stu-id="c9275-115">DevOps Workflow</span></span>

<span data-ttu-id="c9275-116">越来越多地听到术语"DevOps。"</span><span class="sxs-lookup"><span data-stu-id="c9275-116">Increasingly you hear the term "DevOps."</span></span> <span data-ttu-id="c9275-117">术语开发外，您需要将集成开发和操作任务，以便高效地开发软件识别。</span><span class="sxs-lookup"><span data-stu-id="c9275-117">The term developed out of a recognition that you have to integrate development and operations tasks in order to develop software efficiently.</span></span> <span data-ttu-id="c9275-118">你想要启用的工作流的类型是指在其中你可以开发应用程序、 将其部署、 了解从它的生产使用情况、 将其更改以响应您已了解，并快速且可靠地重复这一循环。</span><span class="sxs-lookup"><span data-stu-id="c9275-118">The kind of workflow you want to enable is one in which you can develop an app, deploy it, learn from production usage of it, change it in response to what you've learned, and repeat the cycle quickly and reliably.</span></span>

<span data-ttu-id="c9275-119">一些成功的云开发团队将部署每天到实时环境多次。</span><span class="sxs-lookup"><span data-stu-id="c9275-119">Some successful cloud development teams deploy multiple times a day to a live environment.</span></span> <span data-ttu-id="c9275-120">用于部署一个较大 Azure 团队更新每 2-3 个月，但现在它版本较少更新的每个 2-3 天和主要释放每 2-3 周。</span><span class="sxs-lookup"><span data-stu-id="c9275-120">The Azure team used to deploy a major update every 2-3 months, but now it releases minor updates every 2-3 days and major releases every 2-3 weeks.</span></span> <span data-ttu-id="c9275-121">进入该频率确实可以帮助您立即响应客户反馈。</span><span class="sxs-lookup"><span data-stu-id="c9275-121">Getting into that cadence really helps you be responsive to customer feedback.</span></span>

<span data-ttu-id="c9275-122">为此，你必须启用开发和部署周期可重复、 可靠且可预测，并具有低的周期时间。</span><span class="sxs-lookup"><span data-stu-id="c9275-122">In order to do that, you have to enable a development and deployment cycle that is repeatable, reliable, predictable, and has low cycle time.</span></span>

![DevOps 工作流](automate-everything/_static/image1.png)

<span data-ttu-id="c9275-124">换而言之，如果你具有了解功能和当客户使用它，且提供反馈之间的时间段必须尽可能短。</span><span class="sxs-lookup"><span data-stu-id="c9275-124">In other words, the period of time between when you have an idea for a feature and when the customers are using it and providing feedback must be as short as possible.</span></span> <span data-ttu-id="c9275-125">前三个模式 – 使一切，源代码管理自动化和持续集成和传递-就是指最佳做法，我们建议要使该类型的过程。</span><span class="sxs-lookup"><span data-stu-id="c9275-125">The first three patterns – automate everything, source control, and continuous integration and delivery -- are all about best practices that we recommend in order to enable that kind of process.</span></span>

## <a name="azure-management-scripts"></a><span data-ttu-id="c9275-126">Azure 管理脚本</span><span class="sxs-lookup"><span data-stu-id="c9275-126">Azure management scripts</span></span>

<span data-ttu-id="c9275-127">在[简介此电子书](introduction.md)，你看到的基于 web 的控制台中，Azure 管理门户。</span><span class="sxs-lookup"><span data-stu-id="c9275-127">In the [introduction to this e-book](introduction.md), you saw the web-based console, the Azure Management Portal.</span></span> <span data-ttu-id="c9275-128">管理门户，你可以监视和管理所有已部署在 Azure 的资源。</span><span class="sxs-lookup"><span data-stu-id="c9275-128">The management portal enables you to monitor and manage all of the resources that you have deployed on Azure.</span></span> <span data-ttu-id="c9275-129">它是创建和删除服务，如 web apps 和 Vm、 配置这些服务、 监视服务操作和等等的简单办法。</span><span class="sxs-lookup"><span data-stu-id="c9275-129">It's an easy way to create and delete services such as web apps and VMs, configure those services, monitor service operation, and so forth.</span></span> <span data-ttu-id="c9275-130">它是一个强大的工具，但使用它是一个手动过程。</span><span class="sxs-lookup"><span data-stu-id="c9275-130">It's a great tool, but using it is a manual process.</span></span> <span data-ttu-id="c9275-131">如果你要开发生产应用程序的任何大小，尤其是在团队环境中，我们建议你通过门户 UI 以便了解和探索 Azure，然后自动将重复执行你的进程。</span><span class="sxs-lookup"><span data-stu-id="c9275-131">If you're going to develop a production application of any size, and especially in a team environment, we recommend that you go through the portal UI in order to learn and explore Azure, and then automate the processes that you'll be doing repetitively.</span></span>

<span data-ttu-id="c9275-132">也可以通过调用 REST 管理 API 几乎所有可以在管理门户或从 Visual Studio 手动操作。</span><span class="sxs-lookup"><span data-stu-id="c9275-132">Nearly everything that you can do manually in the management portal or from Visual Studio can also be done by calling the REST management API.</span></span> <span data-ttu-id="c9275-133">你可以编写脚本，使用[Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)，或者可以使用一种开放源代码框架，如[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)。</span><span class="sxs-lookup"><span data-stu-id="c9275-133">You can write scripts using [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx), or you can use an open source framework such as [Chef](http://www.opscode.com/chef/) or [Puppet](http://puppetlabs.com/puppet/what-is-puppet).</span></span> <span data-ttu-id="c9275-134">你还可以在 Mac 或 Linux 的环境中使用 Bash 命令行工具。</span><span class="sxs-lookup"><span data-stu-id="c9275-134">You can also use the Bash command-line tool in a Mac or Linux environment.</span></span> <span data-ttu-id="c9275-135">Azure 具有对所有这些不同的环境，脚本编写 Api，它具有[.NET 管理 API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)以防你想要编写代码而不是脚本。</span><span class="sxs-lookup"><span data-stu-id="c9275-135">Azure has scripting APIs for all those different environments, and it has a [.NET management API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) in case you want to write code instead of script.</span></span>

<span data-ttu-id="c9275-136">为 Fix It 应用我们已创建了自动执行过程的创建测试环境并将项目部署到该环境中，一些 Windows PowerShell 脚本和我们将回顾一下这些脚本的内容。</span><span class="sxs-lookup"><span data-stu-id="c9275-136">For the Fix It app we've created some Windows PowerShell scripts that automate the processes of creating a test environment and deploying the project to that environment, and we'll review some of the contents of those scripts.</span></span>

## <a name="environment-creation-script"></a><span data-ttu-id="c9275-137">环境创建脚本</span><span class="sxs-lookup"><span data-stu-id="c9275-137">Environment creation script</span></span>

<span data-ttu-id="c9275-138">我们将查看的第一个脚本名为*新建 AzureWebsiteEnv.ps1*。</span><span class="sxs-lookup"><span data-stu-id="c9275-138">The first script we'll look at is named *New-AzureWebsiteEnv.ps1*.</span></span> <span data-ttu-id="c9275-139">它将创建 Azure 环境，你可以解决它将应用部署到用于测试。</span><span class="sxs-lookup"><span data-stu-id="c9275-139">It creates an Azure environment that you can deploy the Fix It app to for testing.</span></span> <span data-ttu-id="c9275-140">此脚本将执行的主要任务如下所示：</span><span class="sxs-lookup"><span data-stu-id="c9275-140">The main tasks that this script performs are the following:</span></span>

- <span data-ttu-id="c9275-141">创建 web 应用。</span><span class="sxs-lookup"><span data-stu-id="c9275-141">Create a web app.</span></span>
- <span data-ttu-id="c9275-142">创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="c9275-142">Create a storage account.</span></span> <span data-ttu-id="c9275-143">（要求为 blob 和队列，正如在后面的章节看到）。</span><span class="sxs-lookup"><span data-stu-id="c9275-143">(Required for blobs and queues, as you'll see in later chapters.)</span></span>
- <span data-ttu-id="c9275-144">创建 SQL 数据库服务器和两个数据库： 应用程序数据库和成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="c9275-144">Create a SQL Database server and two databases: an application database, and a membership database.</span></span>
- <span data-ttu-id="c9275-145">设置存储在 Azure 应用程序将用于访问存储帐户和数据库。</span><span class="sxs-lookup"><span data-stu-id="c9275-145">Store settings in Azure that the app will use to access the storage account and databases.</span></span>
- <span data-ttu-id="c9275-146">创建将用于自动部署的设置文件。</span><span class="sxs-lookup"><span data-stu-id="c9275-146">Create settings files that will be used to automate deployment.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="c9275-147">运行脚本</span><span class="sxs-lookup"><span data-stu-id="c9275-147">Run the script</span></span>


> [!NOTE]
> <span data-ttu-id="c9275-148">本章本部分将显示脚本和你输入才能运行这些命令的示例。</span><span class="sxs-lookup"><span data-stu-id="c9275-148">This part of the chapter shows examples of scripts and the commands that you enter in order to run them.</span></span> <span data-ttu-id="c9275-149">此演示，并不提供你需要知道才能运行的脚本的所有内容。</span><span class="sxs-lookup"><span data-stu-id="c9275-149">This a demo and doesn't provide everything you need to know in order to run the scripts.</span></span> <span data-ttu-id="c9275-150">操作方法-到-执行-it 的分步说明，请参阅[附录： 修复它示例应用程序](the-fix-it-sample-application.md#deploybase)。</span><span class="sxs-lookup"><span data-stu-id="c9275-150">For step-by-step how-to-do-it instructions, see [Appendix: The Fix It Sample Application](the-fix-it-sample-application.md#deploybase).</span></span>


<span data-ttu-id="c9275-151">若要运行 PowerShell 脚本，用于管理 Azure 服务，必须安装 Azure PowerShell 控制台，配置它以使用你的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="c9275-151">To run a PowerShell script that manages Azure services you have to install the Azure PowerShell console and configure it to work with your Azure subscription.</span></span> <span data-ttu-id="c9275-152">你在设置后，你可以使用类似此命令的命令运行修复它环境创建脚本：</span><span class="sxs-lookup"><span data-stu-id="c9275-152">Once you're set up, you can run the Fix It environment creation script with a command like this one:</span></span>

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

<span data-ttu-id="c9275-153">`Name`参数指定要创建数据库和存储帐户时使用的名称和`SqlDatabasePassword`参数指定将为 SQL 数据库创建的管理员帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="c9275-153">The `Name` parameter specifies the name to be used when creating the database and storage accounts, and the `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="c9275-154">有您可以使用，我们将考察更高版本的其他参数。</span><span class="sxs-lookup"><span data-stu-id="c9275-154">There are other parameters you can use that we'll look at later.</span></span>

![PowerShell 窗口](automate-everything/_static/image2.png)

<span data-ttu-id="c9275-156">该脚本完成后你可以在管理门户中看到已创建的内容。</span><span class="sxs-lookup"><span data-stu-id="c9275-156">After the script finishes you can see in the management portal what was created.</span></span> <span data-ttu-id="c9275-157">你将找到两个数据库：</span><span class="sxs-lookup"><span data-stu-id="c9275-157">You'll find two databases:</span></span>

![数据库](automate-everything/_static/image3.png)

<span data-ttu-id="c9275-159">存储帐户：</span><span class="sxs-lookup"><span data-stu-id="c9275-159">A storage account:</span></span>

![存储帐户](automate-everything/_static/image4.png)

<span data-ttu-id="c9275-161">和 web 应用：</span><span class="sxs-lookup"><span data-stu-id="c9275-161">And a web app:</span></span>

![网站](automate-everything/_static/image5.png)

<span data-ttu-id="c9275-163">上**配置**选项卡对于 web 应用中，你可以看到，它具有存储帐户设置和 SQL 数据库连接字符串设置为修复它应用。</span><span class="sxs-lookup"><span data-stu-id="c9275-163">On the **Configure** tab for the web app, you can see that it has the storage account settings and SQL database connection strings set up for the Fix It app.</span></span>

![appSettings 和 connectionStrings](automate-everything/_static/image6.png)

<span data-ttu-id="c9275-165">*自动化*文件夹现在还包含 *&lt;websitename&gt;.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="c9275-165">The *Automation* folder now also contains a *&lt;websitename&gt;.pubxml* file.</span></span> <span data-ttu-id="c9275-166">此文件存储 MSBuild 将用于将应用部署到刚创建的 Azure 环境的设置。</span><span class="sxs-lookup"><span data-stu-id="c9275-166">This file stores settings that MSBuild will use to deploy the application to the Azure environment that was just created.</span></span> <span data-ttu-id="c9275-167">例如：</span><span class="sxs-lookup"><span data-stu-id="c9275-167">For example:</span></span>

[!code-xml[Main](automate-everything/samples/sample1.xml)]

<span data-ttu-id="c9275-168">如你所见，脚本已创建完整的测试环境中，并在大约 90 秒钟内完成整个过程。</span><span class="sxs-lookup"><span data-stu-id="c9275-168">As you can see, the script has created a complete test environment, and the whole process is done in about 90 seconds.</span></span>

<span data-ttu-id="c9275-169">如果你的团队的其他人想要创建的测试环境，它们只需运行该脚本。</span><span class="sxs-lookup"><span data-stu-id="c9275-169">If someone else on your team wants to create a test environment, they can just run the script.</span></span> <span data-ttu-id="c9275-170">不仅是快，而且还它们可以确信它们使用与你正在使用相同的环境。</span><span class="sxs-lookup"><span data-stu-id="c9275-170">Not only is it fast, but also they can be confident that they are using an environment identical to the one you're using.</span></span> <span data-ttu-id="c9275-171">无法完全确信，如果每个人都已进行设置手动使用管理门户 UI 进行。</span><span class="sxs-lookup"><span data-stu-id="c9275-171">You couldn't be quite as confident of that if everyone was setting things up manually by using the management portal UI.</span></span>

### <a name="a-look-at-the-scripts"></a><span data-ttu-id="c9275-172">查看脚本</span><span class="sxs-lookup"><span data-stu-id="c9275-172">A look at the scripts</span></span>

<span data-ttu-id="c9275-173">有实际执行此操作的三个脚本。</span><span class="sxs-lookup"><span data-stu-id="c9275-173">There are actually three scripts that do this work.</span></span> <span data-ttu-id="c9275-174">调用一个从命令行，并自动使用与其他两个执行的一些任务：</span><span class="sxs-lookup"><span data-stu-id="c9275-174">You call one from the command line and it automatically uses the other two to do some of the tasks:</span></span>

- <span data-ttu-id="c9275-175">*新 AzureWebSiteEnv.ps1*是主要的脚本。</span><span class="sxs-lookup"><span data-stu-id="c9275-175">*New-AzureWebSiteEnv.ps1* is the main script.</span></span>

    - <span data-ttu-id="c9275-176">*新 AzureStorage.ps1*创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="c9275-176">*New-AzureStorage.ps1* creates the storage account.</span></span>
    - <span data-ttu-id="c9275-177">*新 AzureSql.ps1*创建数据库。</span><span class="sxs-lookup"><span data-stu-id="c9275-177">*New-AzureSql.ps1* creates the databases.</span></span>

### <a name="parameters-in-the-main-script"></a><span data-ttu-id="c9275-178">主脚本中的参数</span><span class="sxs-lookup"><span data-stu-id="c9275-178">Parameters in the main script</span></span>

<span data-ttu-id="c9275-179">主脚本中，*新建 AzureWebSiteEnv.ps1*，定义多个参数：</span><span class="sxs-lookup"><span data-stu-id="c9275-179">The main script, *New-AzureWebSiteEnv.ps1*, defines several parameters:</span></span>

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

<span data-ttu-id="c9275-180">两个参数是必需的：</span><span class="sxs-lookup"><span data-stu-id="c9275-180">Two parameters are required:</span></span>

- <span data-ttu-id="c9275-181">该脚本创建的 web 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="c9275-181">The name of the web app that the script creates.</span></span> <span data-ttu-id="c9275-182">(这也适用于 URL: `<name>.azurewebsites.net`。)</span><span class="sxs-lookup"><span data-stu-id="c9275-182">(This is also used for the URL: `<name>.azurewebsites.net`.)</span></span>
- <span data-ttu-id="c9275-183">数据库服务器脚本创建新管理用户的密码。</span><span class="sxs-lookup"><span data-stu-id="c9275-183">The password for the new administrative user of the database server that the script creates.</span></span>

<span data-ttu-id="c9275-184">可选参数，你可以指定的数据中心位置 （默认为"美国西部"）、 数据库服务器管理员名称 （默认为"dbuser"） 和数据库服务器的防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="c9275-184">Optional parameters enable you to specify the data center location (defaults to "West US"), database server administrator name (defaults to "dbuser"), and a firewall rule for the database server.</span></span>

### <a name="create-the-web-app"></a><span data-ttu-id="c9275-185">创建 web 应用</span><span class="sxs-lookup"><span data-stu-id="c9275-185">Create the web app</span></span>

<span data-ttu-id="c9275-186">脚本执行的第一件事是通过调用创建 web 应用`New-AzureWebsite`cmdlet，在向其 web 应用名称和位置将参数值传递：</span><span class="sxs-lookup"><span data-stu-id="c9275-186">The first thing the script does is create the web app by calling the `New-AzureWebsite` cmdlet, passing in to it the web app name and location parameter values:</span></span>

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a><span data-ttu-id="c9275-187">创建存储帐户</span><span class="sxs-lookup"><span data-stu-id="c9275-187">Create the storage account</span></span>

<span data-ttu-id="c9275-188">然后运行主脚本<em>新建 AzureStorage.ps1</em>编写脚本，请指定"<em>&lt;websitename&gt;</em>存储"的存储帐户名称，和的相同数据中心位置为web 应用。</span><span class="sxs-lookup"><span data-stu-id="c9275-188">Then the main script runs the <em>New-AzureStorage.ps1</em> script, specifying "<em>&lt;websitename&gt;</em>storage" for the storage account name, and the same data center location as the web app.</span></span>

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

<span data-ttu-id="c9275-189">*新 AzureStorage.ps1*调用`New-AzureStorageAccount`cmdlet 来创建存储帐户中，和它返回的帐户名称和访问密钥值。</span><span class="sxs-lookup"><span data-stu-id="c9275-189">*New-AzureStorage.ps1* calls the `New-AzureStorageAccount` cmdlet to create the storage account, and it returns the account name and access key values.</span></span> <span data-ttu-id="c9275-190">若要访问的 blob 和队列的存储帐户中，应用程序将需要这些值。</span><span class="sxs-lookup"><span data-stu-id="c9275-190">The application will need these values in order to access the blobs and queues in the storage account.</span></span>

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

<span data-ttu-id="c9275-191">你可能并不始终希望创建新的存储帐户;你无法通过添加参数，根据需要将它以使用现有存储帐户定向增强脚本。</span><span class="sxs-lookup"><span data-stu-id="c9275-191">You might not always want to create a new storage account; you could enhance the script by adding a parameter that optionally directs it to use an existing storage account.</span></span>

### <a name="create-the-databases"></a><span data-ttu-id="c9275-192">创建数据库</span><span class="sxs-lookup"><span data-stu-id="c9275-192">Create the databases</span></span>

<span data-ttu-id="c9275-193">然后运行主脚本的数据库创建脚本，*新建 AzureSql.ps1*、 后设置默认数据库和防火墙规则名称：</span><span class="sxs-lookup"><span data-stu-id="c9275-193">The main script then runs the database creation script, *New-AzureSql.ps1*, after setting up default database and firewall rule names:</span></span>

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

<span data-ttu-id="c9275-194">数据库创建脚本检索的开发计算机的 IP 地址，设置防火墙规则，以便开发计算机可以连接到和管理服务器。</span><span class="sxs-lookup"><span data-stu-id="c9275-194">The database creation script retrieves the dev machine's IP address and sets a firewall rule so the dev machine can connect to and manage the server.</span></span> <span data-ttu-id="c9275-195">数据库创建脚本然后将经历几个步骤来设置数据库：</span><span class="sxs-lookup"><span data-stu-id="c9275-195">The database creation script then goes through several steps to set up the databases:</span></span>

- <span data-ttu-id="c9275-196">创建服务器时使用`New-AzureSqlDatabaseServer`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c9275-196">Creates the server by using the `New-AzureSqlDatabaseServer` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- <span data-ttu-id="c9275-197">创建防火墙规则以启用开发计算机来管理服务器并使 web 应用程序连接到它。</span><span class="sxs-lookup"><span data-stu-id="c9275-197">Creates firewall rules to enable the dev machine to manage the server and to enable the web app to connect to it.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- <span data-ttu-id="c9275-198">创建包含服务器名称和凭据，通过使用的数据库上下文`New-AzureSqlDatabaseServerContext`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c9275-198">Creates a database context that includes the server name and credentials, by using the `New-AzureSqlDatabaseServerContext` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    <span data-ttu-id="c9275-199">`New-PSCredentialFromPlainText` 是一个函数调用的脚本中`ConvertTo-SecureString`cmdlet 可加密的密码和返回`PSCredential`对象，相同的类型， `Get-Credential` cmdlet 将返回。</span><span class="sxs-lookup"><span data-stu-id="c9275-199">`New-PSCredentialFromPlainText` is a function in the script that calls the `ConvertTo-SecureString` cmdlet to encrypt the password and returns a `PSCredential` object, the same type that the `Get-Credential` cmdlet returns.</span></span>
- <span data-ttu-id="c9275-200">通过使用创建应用程序数据库和成员资格数据库`New-AzureSqlDatabase`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c9275-200">Creates the application database and the membership database by using the `New-AzureSqlDatabase` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- <span data-ttu-id="c9275-201">调用为每个数据库的本地定义的函数 tocreates 连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c9275-201">Calls a locally defined function tocreates a connection string for each database.</span></span> <span data-ttu-id="c9275-202">应用程序将使用这些连接字符串访问数据库。</span><span class="sxs-lookup"><span data-stu-id="c9275-202">The application will use these connection strings to access the databases.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    <span data-ttu-id="c9275-203">Get SQLAzureDatabaseConnectionString 是用于从提供给它的参数值中创建的连接字符串的脚本中定义的函数。</span><span class="sxs-lookup"><span data-stu-id="c9275-203">Get-SQLAzureDatabaseConnectionString is a function defined in the script that creates the connection string from the parameter values supplied to it.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- <span data-ttu-id="c9275-204">返回具有数据库服务器名称和连接字符串的哈希表。</span><span class="sxs-lookup"><span data-stu-id="c9275-204">Returns a hash table with the database server name and the connection strings.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

<span data-ttu-id="c9275-205">修复它应用使用单独的成员身份和应用程序数据库。</span><span class="sxs-lookup"><span data-stu-id="c9275-205">The Fix It app uses separate membership and application databases.</span></span> <span data-ttu-id="c9275-206">还有可能将单个数据库中的成员资格和应用程序数据。</span><span class="sxs-lookup"><span data-stu-id="c9275-206">It's also possible to put both membership and application data in a single database.</span></span>

### <a name="store-app-settings-and-connection-strings"></a><span data-ttu-id="c9275-207">应用商店应用程序设置和连接字符串</span><span class="sxs-lookup"><span data-stu-id="c9275-207">Store app settings and connection strings</span></span>

<span data-ttu-id="c9275-208">Azure 具有一种功能，使你能够存储设置和自动重写时它会尝试来读取返回到应用程序的连接字符串`appSettings`或`connectionStrings`Web.config 文件中的集合。</span><span class="sxs-lookup"><span data-stu-id="c9275-208">Azure has a feature that enables you to store settings and connection strings that automatically override what is returned to the application when it tries to read the `appSettings` or `connectionStrings` collections in the Web.config file.</span></span> <span data-ttu-id="c9275-209">这是与应用的替代[Web.config 转换](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)部署时。</span><span class="sxs-lookup"><span data-stu-id="c9275-209">This is an alternative to applying [Web.config transformations](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) when you deploy.</span></span> <span data-ttu-id="c9275-210">有关详细信息，请参阅[在 Azure 中存储敏感数据](source-control.md#appsettings)此电子书中更高版本。</span><span class="sxs-lookup"><span data-stu-id="c9275-210">For more information, see [Store sensitive data in Azure](source-control.md#appsettings) later in this e-book.</span></span>

<span data-ttu-id="c9275-211">环境创建脚本将存储在 Azure 所有`appSettings`和`connectionStrings`应用程序需要访问的存储帐户和数据库，它在 Azure 中运行时的值。</span><span class="sxs-lookup"><span data-stu-id="c9275-211">The environment creation script stores in Azure all of the `appSettings` and `connectionStrings` values that the application needs to access the storage account and databases when it runs in Azure.</span></span>

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

<span data-ttu-id="c9275-212">[New Relic](http://newrelic.com/)是我们在中演示的遥测框架[监视和遥测](monitoring-and-telemetry.md)章。</span><span class="sxs-lookup"><span data-stu-id="c9275-212">[New Relic](http://newrelic.com/) is a telemetry framework that we demonstrate in the [Monitoring and Telemetry](monitoring-and-telemetry.md) chapter.</span></span> <span data-ttu-id="c9275-213">环境创建脚本还会重新启动 web 应用程序，以确保它拾取 New Relic 设置。</span><span class="sxs-lookup"><span data-stu-id="c9275-213">The environment creation script also restarts the web app to make sure that it picks up the New Relic settings.</span></span>

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a><span data-ttu-id="c9275-214">为部署准备</span><span class="sxs-lookup"><span data-stu-id="c9275-214">Preparing for deployment</span></span>

<span data-ttu-id="c9275-215">在过程结束时，环境创建脚本调用两个函数来创建部署脚本将使用的文件。</span><span class="sxs-lookup"><span data-stu-id="c9275-215">At the end of the process, the environment creation script calls two functions to create files that will be used by the deployment script.</span></span>

<span data-ttu-id="c9275-216">这些函数之一可创建的发布配置文件*(&lt;websitename&gt;.pubxml*文件)。</span><span class="sxs-lookup"><span data-stu-id="c9275-216">One of these functions creates a publish profile *(&lt;websitename&gt;.pubxml* file).</span></span> <span data-ttu-id="c9275-217">该代码调用 Azure REST API，以获取发布设置，并将保存中的信息*.publishsettings*文件。</span><span class="sxs-lookup"><span data-stu-id="c9275-217">The code calls the Azure REST API to get the publish settings, and it saves the information in a *.publishsettings* file.</span></span> <span data-ttu-id="c9275-218">然后，它使用的模板文件以及该文件中的信息 (*pubxml.template*) 创建*.pubxml*包含发布配置文件的文件。</span><span class="sxs-lookup"><span data-stu-id="c9275-218">Then it uses the information from that file along with a template file (*pubxml.template*) to create the *.pubxml* file that contains the publish profile.</span></span> <span data-ttu-id="c9275-219">此两步过程模拟你在 Visual Studio 中所执行的操作： 下载*.publishsettings*文件并导入，若要创建的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="c9275-219">This two-step process simulates what you do in Visual Studio: download a *.publishsettings* file and import that to create a publish profile.</span></span>

<span data-ttu-id="c9275-220">其他函数使用另一个模板文件 (网站 environment.template) 来创建*网站 environment.xml*包含部署脚本将一起使用的设置文件*.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="c9275-220">The other function uses another template file (website-environment.template) to create a *website-environment.xml* file that contains settings the deployment script will use along with the *.pubxml* file.</span></span>

### <a name="troubleshooting-and-error-handling"></a><span data-ttu-id="c9275-221">疑难解答和错误处理</span><span class="sxs-lookup"><span data-stu-id="c9275-221">Troubleshooting and error handling</span></span>

<span data-ttu-id="c9275-222">脚本就像程序： 它们可能会失败，并且当他们执行你想要了解有关失败和引起可以非常相似的。</span><span class="sxs-lookup"><span data-stu-id="c9275-222">Scripts are like programs: they can fail, and when they do you want to know as much as you can about the failure and what caused it.</span></span> <span data-ttu-id="c9275-223">值更改为此，环境创建脚本`VerbosePreference`变量从`SilentlyContinue`到`Continue`，以便显示所有详细消息。</span><span class="sxs-lookup"><span data-stu-id="c9275-223">For this reason, the environment creation script changes the value of the `VerbosePreference` variable from `SilentlyContinue` to `Continue` so that all verbose messages are displayed.</span></span> <span data-ttu-id="c9275-224">它也会更改的值`ErrorActionPreference`变量从`Continue`到`Stop`，以便脚本将停止甚至时遇到非终止错误：</span><span class="sxs-lookup"><span data-stu-id="c9275-224">It also changes the value of the `ErrorActionPreference` variable from `Continue` to `Stop`, so that the script stops even when it encounters non-terminating errors:</span></span>

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

<span data-ttu-id="c9275-225">它执行任何工作之前，该脚本将存储的开始时间，以便它可以完成后计算经过的时间：</span><span class="sxs-lookup"><span data-stu-id="c9275-225">Before it does any work, the script stores the start time so that it can calculate the elapsed time when it's done:</span></span>

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

<span data-ttu-id="c9275-226">它完成其工作后，该脚本将显示的运行时间：</span><span class="sxs-lookup"><span data-stu-id="c9275-226">After it completes its work, the script displays the elapsed time:</span></span>

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

<span data-ttu-id="c9275-227">和执行每个密钥操作脚本写入详细消息，例如：</span><span class="sxs-lookup"><span data-stu-id="c9275-227">And for every key operation the script writes verbose messages, for example:</span></span>

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a><span data-ttu-id="c9275-228">部署脚本</span><span class="sxs-lookup"><span data-stu-id="c9275-228">Deployment script</span></span>

<span data-ttu-id="c9275-229">什么*新建 AzureWebsiteEnv.ps1*脚本执行的环境的创建，*发布 AzureWebsite.ps1*脚本执行的应用程序部署。</span><span class="sxs-lookup"><span data-stu-id="c9275-229">What the *New-AzureWebsiteEnv.ps1* script does for environment creation, the *Publish-AzureWebsite.ps1* script does for application deployment.</span></span>

<span data-ttu-id="c9275-230">部署脚本获取 web 应用程序的名称*网站 environment.xml*创建环境创建脚本文件。</span><span class="sxs-lookup"><span data-stu-id="c9275-230">The deployment script gets the name of the web app from the *website-environment.xml* file created by the environment creation script.</span></span>

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

<span data-ttu-id="c9275-231">它获取部署用户密码从*.publishsettings*文件：</span><span class="sxs-lookup"><span data-stu-id="c9275-231">It gets the deployment user password from the *.publishsettings* file:</span></span>

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

<span data-ttu-id="c9275-232">它会执行[MSBuild](http://msbuildbook.com/)用于构建和部署项目的命令：</span><span class="sxs-lookup"><span data-stu-id="c9275-232">It executes the [MSBuild](http://msbuildbook.com/) command that builds and deploys the project:</span></span>

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

<span data-ttu-id="c9275-233">如果你指定`Launch`命令行上的参数，它调用`Show-AzureWebsite`cmdlet 打开默认浏览器到网站的 URL。</span><span class="sxs-lookup"><span data-stu-id="c9275-233">And if you've specified the `Launch` parameter on the command line, it calls the `Show-AzureWebsite` cmdlet to open your default browser to the website URL.</span></span>

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

<span data-ttu-id="c9275-234">可以使用类似此命令的命令来运行部署脚本：</span><span class="sxs-lookup"><span data-stu-id="c9275-234">You can run the deployment script with a command like this one:</span></span>

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

<span data-ttu-id="c9275-235">完成后，浏览器将打开与在云中运行的站点和`<websitename>.azurewebsites.net`URL。</span><span class="sxs-lookup"><span data-stu-id="c9275-235">And when it's done, the browser opens with the site running in the cloud at the `<websitename>.azurewebsites.net` URL.</span></span>

![修复此错误应用程序部署到 Windows Azure](automate-everything/_static/image7.png)

## <a name="summary"></a><span data-ttu-id="c9275-237">总结</span><span class="sxs-lookup"><span data-stu-id="c9275-237">Summary</span></span>

<span data-ttu-id="c9275-238">使用这些脚本可以确信与使用相同的选项相同的顺序将始终执行相同的步骤。</span><span class="sxs-lookup"><span data-stu-id="c9275-238">With these scripts you can be confident that the same steps will always be executed in the same order using the same options.</span></span> <span data-ttu-id="c9275-239">这有助于确保团队每个开发人员不缺少某些内容或内容扰乱或部署自定义自己不会实际工作方式类似，在另一个团队成员的环境中或在生产环境中的计算机上的内容。</span><span class="sxs-lookup"><span data-stu-id="c9275-239">This helps ensure that each developer on the team doesn't miss something or mess something up or deploy something custom on his own machine that won't actually work the same way in another team member's environment or in production.</span></span>

<span data-ttu-id="c9275-240">以类似的方式，你可以自动执行大多数 Azure 的管理功能，你可以在管理门户中，执行通过 REST API、 Windows PowerShell 脚本、.NET 语言 API 或一个 Bash 实用程序，你可以运行在 Linux 或 mac。</span><span class="sxs-lookup"><span data-stu-id="c9275-240">In a similar way, you can automate most Azure management functions that you can do in the management portal, by using the REST API, Windows PowerShell scripts, a .NET language API, or a Bash utility that you can run on Linux or Mac.</span></span>

<span data-ttu-id="c9275-241">在[下一章](source-control.md)我们将查看源代码，并解释了为什么很重要，在你源代码存储库中包括你的脚本。</span><span class="sxs-lookup"><span data-stu-id="c9275-241">In the [next chapter](source-control.md) we'll look at source code and explain why it's important to include your scripts in your source code repository.</span></span>

## <a name="resources"></a><span data-ttu-id="c9275-242">资源</span><span class="sxs-lookup"><span data-stu-id="c9275-242">Resources</span></span>

- <span data-ttu-id="c9275-243">[安装和配置 Windows PowerShell 以 Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。</span><span class="sxs-lookup"><span data-stu-id="c9275-243">[Install and Configure Windows PowerShell for Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span> <span data-ttu-id="c9275-244">说明如何安装 Azure PowerShell cmdlet 和如何安装，你需要在你的计算机以便管理你的 Azure 帐户的证书。</span><span class="sxs-lookup"><span data-stu-id="c9275-244">Explains how to install the Azure PowerShell cmdlets and how to install the certificate that you need on your computer in order to manage your Azure account.</span></span> <span data-ttu-id="c9275-245">这是很好的位置，若要开始，因为它还具有用于学习 PowerShell 本身的资源链接。</span><span class="sxs-lookup"><span data-stu-id="c9275-245">This is a great place to get started because it also has links to resources for learning PowerShell itself.</span></span>
- <span data-ttu-id="c9275-246">[Azure 脚本中心](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)。</span><span class="sxs-lookup"><span data-stu-id="c9275-246">[Azure Script Center](https://docs.microsoft.com/azure/automation/automation-runbook-gallery).</span></span> <span data-ttu-id="c9275-247">WindowsAzure.com 门户开发管理 Azure 服务，其中包含指向入门教程、 cmdlet 参考文档和源代码和示例脚本的脚本资源</span><span class="sxs-lookup"><span data-stu-id="c9275-247">WindowsAzure.com portal to resources for developing scripts that manage Azure services, with links to getting started tutorials, cmdlet reference documentation and source code, and sample scripts</span></span>
- <span data-ttu-id="c9275-248">[周末脚本编写器： 开始使用 Azure 和 PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c9275-248">[Weekend Scripter: Getting Started with Azure and PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx).</span></span> <span data-ttu-id="c9275-249">在专用于 Windows PowerShell 博客中，此文章提供了使用 PowerShell for Azure 的管理功能的出色介绍。</span><span class="sxs-lookup"><span data-stu-id="c9275-249">In a blog dedicated to Windows PowerShell, this post provides a great introduction to using PowerShell for Azure management functions.</span></span>
- <span data-ttu-id="c9275-250">[安装和配置 Azure 跨平台命令行界面](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)。</span><span class="sxs-lookup"><span data-stu-id="c9275-250">[Install and Configure the Azure Cross-Platform Command-Line Interface](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span> <span data-ttu-id="c9275-251">关于适用于 Mac 和 Linux 以及 Windows 系统的 Azure 脚本框架入门教程。</span><span class="sxs-lookup"><span data-stu-id="c9275-251">Getting-started tutorial for an Azure scripting framework that works on Mac and Linux as well as Windows systems.</span></span>
- <span data-ttu-id="c9275-252">[下载 Azure Sdk 和工具主题的命令行工具部分](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="c9275-252">[Command-line tools section of the Download Azure SDKs and Tools topic](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="c9275-253">有关文档和下载 azure 命令行工具与相关门户页面。</span><span class="sxs-lookup"><span data-stu-id="c9275-253">Portal page for documentation and downloads related to command-line tools for Azure.</span></span>
- <span data-ttu-id="c9275-254">[使用 Azure 管理库和.NET 使一切自动化](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c9275-254">[Automating everything with the Azure Management Libraries and .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx).</span></span> <span data-ttu-id="c9275-255">Scott Hanselman 介绍 Azure.NET 管理 API。</span><span class="sxs-lookup"><span data-stu-id="c9275-255">Scott Hanselman introduces the .NET management API for Azure.</span></span>
- <span data-ttu-id="c9275-256">[使用 Windows PowerShell 脚本发布到开发和测试环境](https://msdn.microsoft.com/library/azure/dn642480.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c9275-256">[Using Windows PowerShell Scripts to Publish to Dev and Test Environments](https://msdn.microsoft.com/library/azure/dn642480.aspx).</span></span> <span data-ttu-id="c9275-257">说明如何使用的 MSDN 文档发布 Visual Studio 自动生成用于 web 项目的脚本。</span><span class="sxs-lookup"><span data-stu-id="c9275-257">MSDN documentation that explains how to use publish scripts that Visual Studio automatically generates for web projects.</span></span>
- <span data-ttu-id="c9275-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)。</span><span class="sxs-lookup"><span data-stu-id="c9275-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597).</span></span> <span data-ttu-id="c9275-259">在 Visual Studio 中添加 Windows PowerShell 语言支持的 visual Studio 扩展。</span><span class="sxs-lookup"><span data-stu-id="c9275-259">Visual Studio extension that adds language support for Windows PowerShell in Visual Studio.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c9275-260">[上一页](introduction.md)
> [下一页](source-control.md)</span><span class="sxs-lookup"><span data-stu-id="c9275-260">[Previous](introduction.md)
[Next](source-control.md)</span></span>
