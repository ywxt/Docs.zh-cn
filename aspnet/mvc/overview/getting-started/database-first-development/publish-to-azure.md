---
uid: mvc/overview/getting-started/database-first-development/publish-to-azure
title: 将 MVC 数据库第一个站点发布到 Azure |Microsoft Docs
author: tfitzmac
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/22/2014
ms.topic: article
ms.assetid: 7131f1c1-cef3-4396-ab44-ed4519676546
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/database-first-development/publish-to-azure
msc.type: authoredcontent
ms.openlocfilehash: 5189d8ee92c6abac31d80ca4efdb06500e72126a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37387265"
---
<a name="publish-mvc-database-first-site-to-azure"></a><span data-ttu-id="7c7df-104">将 MVC 数据库第一个站点发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="7c7df-104">Publish MVC Database First site to Azure</span></span>
====================
<span data-ttu-id="7c7df-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7c7df-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7c7df-106">使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7c7df-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="7c7df-107">本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="7c7df-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="7c7df-108">生成的代码对应于数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="7c7df-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="7c7df-109">本系列的此部分重点介绍将 web 应用和数据库发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="7c7df-109">This part of the series focuses on publishing the web app and database to Azure.</span></span> <span data-ttu-id="7c7df-110">可以阅读本主题，了解如何发布 web 应用和数据库，但实际执行的步骤必须在本教程开始启动。</span><span class="sxs-lookup"><span data-stu-id="7c7df-110">You can read this topic to learn about publishing a web app and database, but to actually perform the steps you must start at the beginning of the tutorial.</span></span> <span data-ttu-id="7c7df-111">请参阅[入门](setting-up-database.md)。</span><span class="sxs-lookup"><span data-stu-id="7c7df-111">See [Getting Started](setting-up-database.md).</span></span>


## <a name="deploy-your-web-app-on-azure"></a><span data-ttu-id="7c7df-112">在 Azure 上的将 web 应用部署</span><span class="sxs-lookup"><span data-stu-id="7c7df-112">Deploy your web app on Azure</span></span>

<span data-ttu-id="7c7df-113">需要一个 Azure 帐户才能完成本教程中：</span><span class="sxs-lookup"><span data-stu-id="7c7df-113">You need an Azure account to complete this tutorial:</span></span>

- <span data-ttu-id="7c7df-114">你可以[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)-获取信用额度可用于试用付费版 Azure 服务，甚至在用之后最多可以保留帐户并使用免费的 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="7c7df-114">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="7c7df-115">你可以[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)-MSDN 订阅提供信用额度可以用于付费版 Azure 服务的每个月。</span><span class="sxs-lookup"><span data-stu-id="7c7df-115">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

<span data-ttu-id="7c7df-116">若要将 web 应用发布，右键单击该项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="7c7df-116">To publish your web app, right-click the project and select **Publish**.</span></span>

![发布站点](publish-to-azure/_static/image1.png)

<span data-ttu-id="7c7df-118">选择 Microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="7c7df-118">Select Microsoft Azure Websites.</span></span>

![选择 Azure](publish-to-azure/_static/image2.png)

<span data-ttu-id="7c7df-120">如果未登录到 Azure，提供你的 Azure 帐户凭据。</span><span class="sxs-lookup"><span data-stu-id="7c7df-120">If you are not signed in to Azure, provide your Azure account credentials.</span></span> <span data-ttu-id="7c7df-121">然后，选择新建以创建新的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="7c7df-121">Then, select New to create a new web app.</span></span>

![新的站点](publish-to-azure/_static/image3.png)

<span data-ttu-id="7c7df-123">创建 web 应用的唯一名称。</span><span class="sxs-lookup"><span data-stu-id="7c7df-123">Create a unique name for your web app.</span></span> <span data-ttu-id="7c7df-124">如果看到一个绿色的复选标记，右侧的名称字段，将知道名称是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7c7df-124">You will know the name is unique if you see a green check mark to the right of the name field.</span></span> <span data-ttu-id="7c7df-125">选择你的 web 应用的区域。</span><span class="sxs-lookup"><span data-stu-id="7c7df-125">Select a region for your web app.</span></span> <span data-ttu-id="7c7df-126">选择**创建新的服务器**数据库，并为此新的数据库服务器提供的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="7c7df-126">Select **Create new server** for the database, and provide a user name and password for this new database server.</span></span> <span data-ttu-id="7c7df-127">完成后，单击**创建**。</span><span class="sxs-lookup"><span data-stu-id="7c7df-127">When finished, click **Create**.</span></span>

![创建站点](publish-to-azure/_static/image4.png)

<span data-ttu-id="7c7df-129">连接值现在一切就绪。</span><span class="sxs-lookup"><span data-stu-id="7c7df-129">Your connection values are now all set.</span></span> <span data-ttu-id="7c7df-130">您可以将这些值保持不变。</span><span class="sxs-lookup"><span data-stu-id="7c7df-130">You can leave these values unchanged.</span></span>

![connection](publish-to-azure/_static/image5.png)

<span data-ttu-id="7c7df-132">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="7c7df-132">Click **Next**.</span></span>

<span data-ttu-id="7c7df-133">对于设置，请注意，两个数据库连接指定-ApplicationDBContext 和 ContosoUniversityDataEntities。</span><span class="sxs-lookup"><span data-stu-id="7c7df-133">For Settings, notice that two database connections are specified - ApplicationDBContext and ContosoUniversityDataEntities.</span></span> <span data-ttu-id="7c7df-134">ApplicationDBContext 是用户帐户表的连接。</span><span class="sxs-lookup"><span data-stu-id="7c7df-134">ApplicationDBContext is the connection for user account tables.</span></span> <span data-ttu-id="7c7df-135">这些值仅显示数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="7c7df-135">These values only show the connection strings for the databases.</span></span> <span data-ttu-id="7c7df-136">它并不意味着当你发布你的站点时，将发布这些数据库。</span><span class="sxs-lookup"><span data-stu-id="7c7df-136">It does not mean that these databases will be published when you publish your site.</span></span> <span data-ttu-id="7c7df-137">完成 web 应用发布后，您将发布您的数据库项目。</span><span class="sxs-lookup"><span data-stu-id="7c7df-137">You will publish your database project after you have finished publishing the web app.</span></span>

![](publish-to-azure/_static/image6.png)

<span data-ttu-id="7c7df-138">数据库连接旁边的省略号 （...） 显示连接字符串的详细信息。</span><span class="sxs-lookup"><span data-stu-id="7c7df-138">The ellipsis (...) next to the database connection shows you the details of the connection string.</span></span> <span data-ttu-id="7c7df-139">单击 ContosoUniversityDataEntities 旁边的省略号。</span><span class="sxs-lookup"><span data-stu-id="7c7df-139">Click the ellipsis next to ContosoUniversityDataEntities.</span></span>

![](publish-to-azure/_static/image7.png)

<span data-ttu-id="7c7df-140">记下数据库服务器和数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="7c7df-140">Note the name of the database server and the database.</span></span> <span data-ttu-id="7c7df-141">随机生成的服务器名称。</span><span class="sxs-lookup"><span data-stu-id="7c7df-141">The server name is randomly generated.</span></span> <span data-ttu-id="7c7df-142">数据库名称是简单的你的站点名称 **\_db**追加。</span><span class="sxs-lookup"><span data-stu-id="7c7df-142">The database name is simple the name of your site with **\_db** appended.</span></span> <span data-ttu-id="7c7df-143">当你发布你的数据库时，将更高版本需要两个名称。</span><span class="sxs-lookup"><span data-stu-id="7c7df-143">You will need both names later when you publish your database.</span></span>

<span data-ttu-id="7c7df-144">单击**确定**以关闭数据库连接字符串窗口。</span><span class="sxs-lookup"><span data-stu-id="7c7df-144">Click **OK** to close the database connection string window.</span></span>

<span data-ttu-id="7c7df-145">在发布 Web 窗口中，单击**下一步**以查看预览。</span><span class="sxs-lookup"><span data-stu-id="7c7df-145">In the Publish Web window, click **Next** to see the preview.</span></span>

![](publish-to-azure/_static/image8.png)

<span data-ttu-id="7c7df-146">您可以单击开始预览以查看要发布的文件的列表。</span><span class="sxs-lookup"><span data-stu-id="7c7df-146">You can click Start Preview to see a list of the files to publish.</span></span> <span data-ttu-id="7c7df-147">由于这是首次发布此站点，该列表将为项目中的每个相关文件。</span><span class="sxs-lookup"><span data-stu-id="7c7df-147">Since this is the first time you have published this site, the list is every relevant file in the project.</span></span>

<span data-ttu-id="7c7df-148">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="7c7df-148">Click **Publish**.</span></span>

<span data-ttu-id="7c7df-149">输出窗格将显示你发布的结果。</span><span class="sxs-lookup"><span data-stu-id="7c7df-149">The Output pane will display the result of your publication.</span></span>

![](publish-to-azure/_static/image9.png)

<span data-ttu-id="7c7df-150">在发布后的站点是 immedialely web 浏览器中启动。</span><span class="sxs-lookup"><span data-stu-id="7c7df-150">After publication, the site is immedialely launched in a web browser.</span></span> <span data-ttu-id="7c7df-151">已部署你的站点，并且可以注册到站点; 一个新用户但是，在 ContosoUniversityData 项目中的表具有尚未发布。</span><span class="sxs-lookup"><span data-stu-id="7c7df-151">Your site has been deployed and you can register a new user to the site; however, your tables in the ContosoUniversityData project have not yet been published.</span></span> <span data-ttu-id="7c7df-152">如果学生链接的列表中单击你将收到错误。</span><span class="sxs-lookup"><span data-stu-id="7c7df-152">If you click on the List of students link you will receive an error.</span></span>

## <a name="publish-database-to-sql-azure"></a><span data-ttu-id="7c7df-153">将数据库发布到 SQL Azure</span><span class="sxs-lookup"><span data-stu-id="7c7df-153">Publish database to SQL Azure</span></span>

<span data-ttu-id="7c7df-154">在发布之前您的数据库，您必须确保在本地计算机可以连接到数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="7c7df-154">Before publishing your database, you must make sure your local computer can connect to the database server.</span></span> <span data-ttu-id="7c7df-155">数据库服务器的防火墙将限制哪些计算机可以连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="7c7df-155">The firewall for your database server restricts which machines can connect to the database.</span></span> <span data-ttu-id="7c7df-156">您需要将您的计算机的 IP 地址添加到防火墙允许的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="7c7df-156">You need to add the IP address of your computer to the allowed IP addresses for the firewall.</span></span>

<span data-ttu-id="7c7df-157">登录到 Azure 帐户通过 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="7c7df-157">Login to your Azure account through the Azure portal.</span></span>

<span data-ttu-id="7c7df-158">选择新数据库，并选择**管理**。</span><span class="sxs-lookup"><span data-stu-id="7c7df-158">Select your new database and select **Manage**.</span></span>

![管理](publish-to-azure/_static/image10.png)

<span data-ttu-id="7c7df-160">必须配置你的数据库服务器以允许从您的计算机的连接。</span><span class="sxs-lookup"><span data-stu-id="7c7df-160">You must configure your database server to allow connections from your computer.</span></span> <span data-ttu-id="7c7df-161">选择管理，系统会要求将当前的 IP 地址添加到数据库服务器允许的方式。</span><span class="sxs-lookup"><span data-stu-id="7c7df-161">When you select Manage, you are asked to add the current IP address as permitted to the database server.</span></span> <span data-ttu-id="7c7df-162">选择是。</span><span class="sxs-lookup"><span data-stu-id="7c7df-162">Select Yes.</span></span>

![添加 ip 地址](publish-to-azure/_static/image11.png)

<span data-ttu-id="7c7df-164">没有机会在上一步中添加的 IP 地址不是您需要为连接配置的唯一 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="7c7df-164">There is a chance that the IP address you added in the previous step is not the only IP address you need to configure for connections.</span></span> <span data-ttu-id="7c7df-165">您可以尝试登录到数据库以查看是否连接已正确设置。</span><span class="sxs-lookup"><span data-stu-id="7c7df-165">You can attempt to login to the database to see if the connections have been properly set up.</span></span> <span data-ttu-id="7c7df-166">提供的用户和前面创建的密码。</span><span class="sxs-lookup"><span data-stu-id="7c7df-166">Provide the user and password you created earlier.</span></span>

![登录](publish-to-azure/_static/image12.png)

<span data-ttu-id="7c7df-168">如果你收到一条错误消息，您需要添加另一个 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="7c7df-168">If you receive an error message, you need to add another IP address.</span></span> <span data-ttu-id="7c7df-169">单击以查看有关错误的更多详细信息的错误消息。</span><span class="sxs-lookup"><span data-stu-id="7c7df-169">Click the error message to see more details about error.</span></span> <span data-ttu-id="7c7df-170">在详细信息，您将看到您需要添加的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="7c7df-170">In the details you will see the IP address that you need to add.</span></span> <span data-ttu-id="7c7df-171">记下此 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="7c7df-171">Note this IP address.</span></span>

![不允许](publish-to-azure/_static/image13.png)

<span data-ttu-id="7c7df-173">关闭此登录窗口中，并返回到 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="7c7df-173">Close this login window, and return to the Azure portal.</span></span>

<span data-ttu-id="7c7df-174">导航到你的数据库的仪表板。</span><span class="sxs-lookup"><span data-stu-id="7c7df-174">Navigate to the Dashboard for your database.</span></span> <span data-ttu-id="7c7df-175">单击**允许的 IP 地址管理**。</span><span class="sxs-lookup"><span data-stu-id="7c7df-175">Click **Manage allowed IP addresses**.</span></span>

![管理 ip 地址](publish-to-azure/_static/image14.png)

<span data-ttu-id="7c7df-177">现在必须从错误消息添加 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="7c7df-177">You must now add the IP address from the error message.</span></span> <span data-ttu-id="7c7df-178">更改允许的 IP 地址以包括错误消息中的一个范围，或者将该 IP 地址添加为一个单独的条目。</span><span class="sxs-lookup"><span data-stu-id="7c7df-178">Either change the range of allowed IP addresses to include the one from the error message, or add that IP address as a separate entry.</span></span>

![添加新地址](publish-to-azure/_static/image15.png)

<span data-ttu-id="7c7df-180">将更改保存到允许的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="7c7df-180">Save the change to allowed IP addresses.</span></span>

<span data-ttu-id="7c7df-181">单击管理，并尝试再次登录到数据库。</span><span class="sxs-lookup"><span data-stu-id="7c7df-181">Click Manage, and try logging in again to the database.</span></span> <span data-ttu-id="7c7df-182">您可能需要等待几分钟才能正确地为防火墙配置允许的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="7c7df-182">You may need to wait a few minutes before the allowed IP addresses are correctly configured for the firewall.</span></span> <span data-ttu-id="7c7df-183">如果可以成功登录数据库中，你已完成与数据库的连接设置。</span><span class="sxs-lookup"><span data-stu-id="7c7df-183">When you can successfully log in the database, you have finished setting up your connection to the database.</span></span>

<span data-ttu-id="7c7df-184">因为您稍后将检查数据库部署的结果，可以将此管理窗口打开。</span><span class="sxs-lookup"><span data-stu-id="7c7df-184">You can leave this management window open because you will check the result of your database deployment shortly.</span></span>

<span data-ttu-id="7c7df-185">返回到您的数据库项目。</span><span class="sxs-lookup"><span data-stu-id="7c7df-185">Return to your database project.</span></span> <span data-ttu-id="7c7df-186">右键单击项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="7c7df-186">Right-click the project and select **Publish**.</span></span>

![发布数据库](publish-to-azure/_static/image16.png)

<span data-ttu-id="7c7df-188">在发布数据库窗口中，选择**编辑**。</span><span class="sxs-lookup"><span data-stu-id="7c7df-188">In the Publish Database window, select **Edit**.</span></span>

![编辑](publish-to-azure/_static/image17.png)

<span data-ttu-id="7c7df-190">为服务器提供数据库服务器和身份验证凭据的名称。</span><span class="sxs-lookup"><span data-stu-id="7c7df-190">Provide the name of the database server and your authentication credentials for the server.</span></span> <span data-ttu-id="7c7df-191">提供凭据后，选择从可用数据库列表创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="7c7df-191">After providing the credentials, select the database you created from the list of available databases.</span></span> <span data-ttu-id="7c7df-192">默认情况下，Visual Studio 将数据库字段的名称设置为你的项目可能不是你创建的数据库相同的名称。</span><span class="sxs-lookup"><span data-stu-id="7c7df-192">By default, Visual Studio sets the name of the database field to the name of your project which might not be the same as the database you created.</span></span>

![](publish-to-azure/_static/image18.png)

<span data-ttu-id="7c7df-193">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="7c7df-193">Click OK.</span></span>

<span data-ttu-id="7c7df-194">您可能会想要保存此配置文件，以便可以发布在将来的更新而无需重新输入的所有连接信息。</span><span class="sxs-lookup"><span data-stu-id="7c7df-194">You will probably want to save this profile so you can publish updates in the future without re-entering all of the connection information.</span></span> <span data-ttu-id="7c7df-195">选择“创建配置文件”。</span><span class="sxs-lookup"><span data-stu-id="7c7df-195">Select **Create Profile**.</span></span>

![保存配置文件](publish-to-azure/_static/image19.png)

<span data-ttu-id="7c7df-197">它将创建一个文件中名为的项目**ContosoUniversityData.publish.xml**。</span><span class="sxs-lookup"><span data-stu-id="7c7df-197">It will create a file in your project named **ContosoUniversityData.publish.xml**.</span></span> <span data-ttu-id="7c7df-198">下次你想要将数据库发布到 Azure，只需加载该配置文件。</span><span class="sxs-lookup"><span data-stu-id="7c7df-198">The next time you want to publish the database to Azure, simply load that profile.</span></span>

<span data-ttu-id="7c7df-199">现在，单击**发布**在 Azure 上创建数据库。</span><span class="sxs-lookup"><span data-stu-id="7c7df-199">Now, click **Publish** to create the database on Azure.</span></span>

![publish](publish-to-azure/_static/image20.png)

<span data-ttu-id="7c7df-201">后运行一段时间，显示发布结果。</span><span class="sxs-lookup"><span data-stu-id="7c7df-201">After running for a while, the publishing results are displayed.</span></span>

![results](publish-to-azure/_static/image21.png)

<span data-ttu-id="7c7df-203">现在，你可以返回到管理门户为你的数据库。</span><span class="sxs-lookup"><span data-stu-id="7c7df-203">Now, you can go back to the management portal for your database.</span></span> <span data-ttu-id="7c7df-204">刷新设计视图中，并请注意，已部署包含预填充的数据的 3 个表。</span><span class="sxs-lookup"><span data-stu-id="7c7df-204">Refresh the design view, and notice the 3 tables with pre-filled data have been deployed.</span></span>

![新表](publish-to-azure/_static/image22.png)

<span data-ttu-id="7c7df-206">现在已准备好部署到 Azure web 应用进行测试。</span><span class="sxs-lookup"><span data-stu-id="7c7df-206">Now you are ready to test the web app that is deployed to Azure.</span></span> <span data-ttu-id="7c7df-207">导航到在 Azure 上的 web 应用 (如http://contosositeexample.azurewebsites.net/)。</span><span class="sxs-lookup"><span data-stu-id="7c7df-207">Navigate to the web app on Azure (such as http://contosositeexample.azurewebsites.net/).</span></span> <span data-ttu-id="7c7df-208">单击链接获取学生列表，您应看到面向学生的索引视图。</span><span class="sxs-lookup"><span data-stu-id="7c7df-208">Click the link for List of students and you should see the index view for students.</span></span>

![查看](publish-to-azure/_static/image23.png)

<span data-ttu-id="7c7df-210">有时候，数据库和连接需要一些时间来正确配置。</span><span class="sxs-lookup"><span data-stu-id="7c7df-210">Occasionally, the database and connection need a little time to be properly configured.</span></span> <span data-ttu-id="7c7df-211">如果收到错误，等待几分钟并再试一次。</span><span class="sxs-lookup"><span data-stu-id="7c7df-211">If you receive an error, wait a few minutes and then try again.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7c7df-212">结束语</span><span class="sxs-lookup"><span data-stu-id="7c7df-212">Conclusion</span></span>

<span data-ttu-id="7c7df-213">本系列提供一个简单的示例说明如何从现有数据库，使用户能够编辑、 更新、 创建和删除数据生成代码。</span><span class="sxs-lookup"><span data-stu-id="7c7df-213">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="7c7df-214">它使用 ASP.NET MVC 5，实体框架和 ASP.NET 基架创建项目。</span><span class="sxs-lookup"><span data-stu-id="7c7df-214">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span>

<span data-ttu-id="7c7df-215">Code First 开发的介绍性示例，请参阅[Getting Started with ASP.NET MVC 5](../introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="7c7df-215">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span>

<span data-ttu-id="7c7df-216">有关更高级的示例，请参阅[为 ASP.NET MVC 4 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="7c7df-216">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="7c7df-217">请注意，使用第一个数据库中的数据使用 DbContext API 是用于在第一个代码中使用数据的 API 相同。</span><span class="sxs-lookup"><span data-stu-id="7c7df-217">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="7c7df-218">即使你想要使用第一个数据库，您可以了解如何处理更复杂的方案，如读取和更新相关的数据，处理并发冲突，请从代码第一个教程，等等。</span><span class="sxs-lookup"><span data-stu-id="7c7df-218">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="7c7df-219">如何创建数据库、 上下文类和实体类中是唯一的区别。</span><span class="sxs-lookup"><span data-stu-id="7c7df-219">The only difference is in how the database, context class, and entity classes are created.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7c7df-220">上一篇</span><span class="sxs-lookup"><span data-stu-id="7c7df-220">Previous</span></span>](enhancing-data-validation.md)
