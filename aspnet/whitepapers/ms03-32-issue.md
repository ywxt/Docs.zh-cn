---
uid: whitepapers/ms03-32-issue
title: 应用 IE 安全更新后的服务器应用程序不可用错误修复 |Microsoft Docs
author: rick-anderson
description: 本白皮书介绍了影响 Wi 上运行的 ASP.NET 1.0 应用程序的 Internet explorer 与 MS03 32 安全更新解决了问题的修补程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: 1365eebb-bdf7-4a05-8d18-7f200531be55
ms.technology: ''
msc.legacyurl: /whitepapers/ms03-32-issue
msc.type: content
ms.openlocfilehash: 186ed7ea7ad9b317506fb3951a974682b44b27a1
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37402465"
---
<a name="fix-for-server-application-unavailable-error-after-applying-security-update-for-ie"></a><span data-ttu-id="a5d54-103">应用 IE 安全更新后的服务器应用程序不可用错误修复</span><span class="sxs-lookup"><span data-stu-id="a5d54-103">Fix for 'Server Application Unavailable' Error after Applying Security Update for IE</span></span>
====================
> <span data-ttu-id="a5d54-104">本白皮书介绍会影响 ASP.NET 1.0 应用程序在 Windows XP Professional 上运行的 Internet explorer 与 MS03 32 安全更新解决了问题的修补程序。</span><span class="sxs-lookup"><span data-stu-id="a5d54-104">This paper describes the patch that fixes an issue with the MS03-32 Security Update for Internet Explorer that affects ASP.NET 1.0 applications running on Windows XP Professional.</span></span>
> 
> <span data-ttu-id="a5d54-105">适用于 ASP.NET 1.0 和 Windows XP Professional。</span><span class="sxs-lookup"><span data-stu-id="a5d54-105">Applies to ASP.NET 1.0 and Windows XP Professional.</span></span>


<span data-ttu-id="a5d54-106">Microsoft 使用 Internet Explorer 的安全修补程序 MS03 32 安全更新和 Windows XP 上运行的 ASP.NET 1.0 标识问题。</span><span class="sxs-lookup"><span data-stu-id="a5d54-106">Microsoft identified an issue with the MS03-32 Security Update for Internet Explorer security patch and ASP.NET 1.0 running on Windows XP.</span></span> <span data-ttu-id="a5d54-107">手动或通过从 Windows 更新站点获取最新的关键更新，可以安装此修补程序。</span><span class="sxs-lookup"><span data-stu-id="a5d54-107">This patch can be installed manually or by obtaining recent critical updates from the Windows Update site.</span></span>

<span data-ttu-id="a5d54-108">此问题的症状是，在 Windows XP 计算机上安装此修补程序之后, 对本地 IIS 5.1 web 服务器上运行的 ASP.NET 应用程序的所有请求都导致错误消息，指出"服务器应用程序不可用"。</span><span class="sxs-lookup"><span data-stu-id="a5d54-108">The symptom of this issue is that after installing the patch on a Windows XP machine, all requests to ASP.NET applications running on the local IIS 5.1 web server result in an error message saying "Server Application Unavailable".</span></span> <span data-ttu-id="a5d54-109">对远程 web 服务器的请求不会受到影响。</span><span class="sxs-lookup"><span data-stu-id="a5d54-109">Requests to remote web servers are unaffected.</span></span>

<span data-ttu-id="a5d54-110">此问题只会影响在 Windows XP 上运行 ASP.NET 1.0 安装。</span><span class="sxs-lookup"><span data-stu-id="a5d54-110">This issue only impacts installations running ASP.NET 1.0 on Windows XP.</span></span> <span data-ttu-id="a5d54-111">它不会影响运行 Windows 2000 或 Windows Server 2003 的计算机。</span><span class="sxs-lookup"><span data-stu-id="a5d54-111">It does not impact machines running Windows 2000 or Windows Server 2003.</span></span> <span data-ttu-id="a5d54-112">它也不会影响 ASP.NET 1.1 安装运行 Windows XP 的计算机。</span><span class="sxs-lookup"><span data-stu-id="a5d54-112">It also does not impact machines running Windows XP with ASP.NET 1.1 installed.</span></span>

<span data-ttu-id="a5d54-113">请注意，此问题**不是**与 ASP.NET 是安全性错误。</span><span class="sxs-lookup"><span data-stu-id="a5d54-113">Please note that this issue **is not** a security bug with ASP.NET.</span></span> <span data-ttu-id="a5d54-114">它**却不**打开或允许 ASP.NET 应用程序或服务器遭受恶意攻击。</span><span class="sxs-lookup"><span data-stu-id="a5d54-114">It **does not** open up or allow any malicious attacks against an ASP.NET application or server.</span></span> <span data-ttu-id="a5d54-115">相反，它是纯粹的功能错误引起的修补程序本身。</span><span class="sxs-lookup"><span data-stu-id="a5d54-115">Instead, it is purely a functional bug caused by the patch itself.</span></span>

<span data-ttu-id="a5d54-116">我们正在努力针对此问题的永久解决方案。</span><span class="sxs-lookup"><span data-stu-id="a5d54-116">We are working hard on a permanent solution for this issue.</span></span> <span data-ttu-id="a5d54-117">在此期间，你可以执行以下批处理文件作为此问题的解决方法。</span><span class="sxs-lookup"><span data-stu-id="a5d54-117">In the meantime, you can execute the following batch file as a workaround for the issue.</span></span> <span data-ttu-id="a5d54-118">批处理文件执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="a5d54-118">The batch file does the following:</span></span>

1. <span data-ttu-id="a5d54-119">停止 IIS 和 ASP.NET 状态服务</span><span class="sxs-lookup"><span data-stu-id="a5d54-119">Stops the IIS and ASP.NET state services</span></span>
2. <span data-ttu-id="a5d54-120">删除并重新创建具有已知的临时密码的 ASPNET 帐户</span><span class="sxs-lookup"><span data-stu-id="a5d54-120">Deletes and recreates the ASPNET account with a known temporary password</span></span>
3. <span data-ttu-id="a5d54-121">使用 Windows`runas`命令以启动创建 ASPNET 用户配置文件的可执行文件</span><span class="sxs-lookup"><span data-stu-id="a5d54-121">Uses the Windows `runas` command to launch an executable that creates an ASPNET user profile</span></span>
4. <span data-ttu-id="a5d54-122">重新注册 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="a5d54-122">Re-registers ASP.NET.</span></span> <span data-ttu-id="a5d54-123">这将创建新的随机密码的帐户并应用它的默认 ASP.NET 访问控制设置</span><span class="sxs-lookup"><span data-stu-id="a5d54-123">This creates a new random password for the account and applies default ASP.NET access control settings for it</span></span>
5. <span data-ttu-id="a5d54-124">重新启动 IIS 服务</span><span class="sxs-lookup"><span data-stu-id="a5d54-124">Restarts the IIS service</span></span>

<span data-ttu-id="a5d54-125">批处理文件包含硬编码的临时密码"<strong>1pass@word</strong>"您将提示你输入的 runas 命令运行此批处理文件。</span><span class="sxs-lookup"><span data-stu-id="a5d54-125">The batch file contains a hardcoded temporary password of "<strong>1pass@word</strong>" which you will be prompted to enter for the runas command when the batch file is run.</span></span> <span data-ttu-id="a5d54-126">Runas 命令完成后，ASPNET 帐户密码的强随机值重新创建。</span><span class="sxs-lookup"><span data-stu-id="a5d54-126">After the runas command completes, the ASPNET account password is recreated with a strong random value.</span></span> <span data-ttu-id="a5d54-127">请注意，如果硬编码密码不符合您的环境中的密码复杂性要求，可能会失败的批处理文件。</span><span class="sxs-lookup"><span data-stu-id="a5d54-127">Note that the batch file may fail if the hardcoded password does not meet the password complexity requirements in your environment.</span></span> <span data-ttu-id="a5d54-128">如果是这种情况，可以将其更改为另一个适用于你的环境的值。</span><span class="sxs-lookup"><span data-stu-id="a5d54-128">If that's the case, you can change it to another value that is appropriate for your environment.</span></span>

<span data-ttu-id="a5d54-129">*> [!IMPORTANT]* 如果已添加自定义访问控制设置或数据库帐户为 ASPNET 帐户的权限，他们将需要此批处理文件完成后重新创建。</span><span class="sxs-lookup"><span data-stu-id="a5d54-129">*> [!IMPORTANT]* If you have added custom access control settings or database account permissions for the ASPNET account, they will need to be recreated after this batch file completes.</span></span> <span data-ttu-id="a5d54-130">这是因为时重新创建该帐户，它将获取新的安全标识符 (SID)。</span><span class="sxs-lookup"><span data-stu-id="a5d54-130">This is because when the account is recreated, it will get a new security identifier (SID).</span></span>

<span data-ttu-id="a5d54-131">*> [!IMPORTANT]* 如果运行的 ASP.NET 工作进程的非 ASPNET 帐户的自定义帐户，则应不运行此批处理文件。</span><span class="sxs-lookup"><span data-stu-id="a5d54-131">*> [!IMPORTANT]* If you are running the ASP.NET worker process with a custom account other than the ASPNET account, then you should not run this batch file.</span></span> <span data-ttu-id="a5d54-132">相反，应以交互方式登录，或与该帐户将创建该帐户的用户配置文件中使用 runas 命令。</span><span class="sxs-lookup"><span data-stu-id="a5d54-132">Instead, you should log in interactively or use the runas command with that account which will create a user profile for that account.</span></span>

<span data-ttu-id="a5d54-133">下面的自解压缩存档中包含的批处理文件。</span><span class="sxs-lookup"><span data-stu-id="a5d54-133">The batch file is included in the self-extracting archive below.</span></span> <span data-ttu-id="a5d54-134">若要使用它：</span><span class="sxs-lookup"><span data-stu-id="a5d54-134">To use it:</span></span>

1. <span data-ttu-id="a5d54-135">您必须为帐户运行，使用管理员权限</span><span class="sxs-lookup"><span data-stu-id="a5d54-135">You must be running as an account with Administrator privileges</span></span>
2. [<span data-ttu-id="a5d54-136">下载并打开自解压可执行文件</span><span class="sxs-lookup"><span data-stu-id="a5d54-136">Download and open the self-extracting executable file</span></span>](ms03-32-issue/_static/fixup1.exe)
3. <span data-ttu-id="a5d54-137">将内容提取到 c:\\</span><span class="sxs-lookup"><span data-stu-id="a5d54-137">Extract the contents to c:\\</span></span>
4. <span data-ttu-id="a5d54-138">从开始菜单中，选择运行...并输入 `cmd.exe`</span><span class="sxs-lookup"><span data-stu-id="a5d54-138">Select Run... from the start menu, and enter `cmd.exe`</span></span>
5. <span data-ttu-id="a5d54-139">在打开命令窗口中，键入`c:\fixup.cmd`。</span><span class="sxs-lookup"><span data-stu-id="a5d54-139">In the open command windows, type `c:\fixup.cmd`.</span></span>
6. <span data-ttu-id="a5d54-140">出现提示时，输入<strong>1pass@word</strong>作为密码。</span><span class="sxs-lookup"><span data-stu-id="a5d54-140">When prompted, enter <strong>1pass@word</strong> as the password.</span></span>
7. <span data-ttu-id="a5d54-141">如果你有以前自定义访问控制设置或数据库帐户为 ASPNET 帐户的权限，你需要立即重新应用这些设置。</span><span class="sxs-lookup"><span data-stu-id="a5d54-141">If you have previously custom access control settings or database account permissions for the ASPNET account, you'll need to re-apply these settings now.</span></span>

<span data-ttu-id="a5d54-142">这导致不便的许多道歉。</span><span class="sxs-lookup"><span data-stu-id="a5d54-142">Many apologies for the inconvenience that this has caused.</span></span> <span data-ttu-id="a5d54-143">当提供时，我们将发布的其他信息。</span><span class="sxs-lookup"><span data-stu-id="a5d54-143">We'll post additional information as it becomes available.</span></span>

<span data-ttu-id="a5d54-144">下表详细介绍了平台和版本受此问题。</span><span class="sxs-lookup"><span data-stu-id="a5d54-144">The matrix below details platforms and versions impacted by this issue.</span></span>

| <span data-ttu-id="a5d54-145">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a5d54-145">.NET Framework</span></span> | <span data-ttu-id="a5d54-146">平台</span><span class="sxs-lookup"><span data-stu-id="a5d54-146">Platform</span></span> | <span data-ttu-id="a5d54-147">受影响</span><span class="sxs-lookup"><span data-stu-id="a5d54-147">Affected</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a5d54-148">版本 1.0</span><span class="sxs-lookup"><span data-stu-id="a5d54-148">Version 1.0</span></span> | <span data-ttu-id="a5d54-149">Windows 2000 Professional</span><span class="sxs-lookup"><span data-stu-id="a5d54-149">Windows 2000 Professional</span></span> | <span data-ttu-id="a5d54-150">否</span><span class="sxs-lookup"><span data-stu-id="a5d54-150">No</span></span> |
| <span data-ttu-id="a5d54-151">版本 1.0</span><span class="sxs-lookup"><span data-stu-id="a5d54-151">Version 1.0</span></span> | <span data-ttu-id="a5d54-152">Windows 2000 Server</span><span class="sxs-lookup"><span data-stu-id="a5d54-152">Windows 2000 Server</span></span> | <span data-ttu-id="a5d54-153">否</span><span class="sxs-lookup"><span data-stu-id="a5d54-153">No</span></span> |
| <span data-ttu-id="a5d54-154">版本 1.0</span><span class="sxs-lookup"><span data-stu-id="a5d54-154">Version 1.0</span></span> | <span data-ttu-id="a5d54-155">Windows XP Professional</span><span class="sxs-lookup"><span data-stu-id="a5d54-155">Windows XP Professional</span></span> | <span data-ttu-id="a5d54-156">是</span><span class="sxs-lookup"><span data-stu-id="a5d54-156">Yes</span></span> |
| <span data-ttu-id="a5d54-157">版本 1.0</span><span class="sxs-lookup"><span data-stu-id="a5d54-157">Version 1.0</span></span> | <span data-ttu-id="a5d54-158">Windows Server 2003</span><span class="sxs-lookup"><span data-stu-id="a5d54-158">Windows Server 2003</span></span> | <span data-ttu-id="a5d54-159">否</span><span class="sxs-lookup"><span data-stu-id="a5d54-159">No</span></span> |
| <span data-ttu-id="a5d54-160">版本 1.0</span><span class="sxs-lookup"><span data-stu-id="a5d54-160">Version 1.0</span></span> | <span data-ttu-id="a5d54-161">使用 Cassini 的 Windows XP Home</span><span class="sxs-lookup"><span data-stu-id="a5d54-161">Windows XP Home with Cassini</span></span> | <span data-ttu-id="a5d54-162">否</span><span class="sxs-lookup"><span data-stu-id="a5d54-162">No</span></span> |
| <span data-ttu-id="a5d54-163">版本 1.1</span><span class="sxs-lookup"><span data-stu-id="a5d54-163">Version 1.1</span></span> | <span data-ttu-id="a5d54-164">Windows 2000 Professional</span><span class="sxs-lookup"><span data-stu-id="a5d54-164">Windows 2000 Professional</span></span> | <span data-ttu-id="a5d54-165">否</span><span class="sxs-lookup"><span data-stu-id="a5d54-165">No</span></span> |
| <span data-ttu-id="a5d54-166">版本 1.1</span><span class="sxs-lookup"><span data-stu-id="a5d54-166">Version 1.1</span></span> | <span data-ttu-id="a5d54-167">Windows 2000 Server</span><span class="sxs-lookup"><span data-stu-id="a5d54-167">Windows 2000 Server</span></span> | <span data-ttu-id="a5d54-168">否</span><span class="sxs-lookup"><span data-stu-id="a5d54-168">No</span></span> |
| <span data-ttu-id="a5d54-169">版本 1.1</span><span class="sxs-lookup"><span data-stu-id="a5d54-169">Version 1.1</span></span> | <span data-ttu-id="a5d54-170">Windows XP Professional</span><span class="sxs-lookup"><span data-stu-id="a5d54-170">Windows XP Professional</span></span> | <span data-ttu-id="a5d54-171">否</span><span class="sxs-lookup"><span data-stu-id="a5d54-171">No</span></span> |
| <span data-ttu-id="a5d54-172">版本 1.1</span><span class="sxs-lookup"><span data-stu-id="a5d54-172">Version 1.1</span></span> | <span data-ttu-id="a5d54-173">Windows Server 2003</span><span class="sxs-lookup"><span data-stu-id="a5d54-173">Windows Server 2003</span></span> | <span data-ttu-id="a5d54-174">否</span><span class="sxs-lookup"><span data-stu-id="a5d54-174">No</span></span> |
| <span data-ttu-id="a5d54-175">版本 1.1</span><span class="sxs-lookup"><span data-stu-id="a5d54-175">Version 1.1</span></span> | <span data-ttu-id="a5d54-176">使用 Cassini 的 Windows XP Home</span><span class="sxs-lookup"><span data-stu-id="a5d54-176">Windows XP Home with Cassini</span></span> | <span data-ttu-id="a5d54-177">否</span><span class="sxs-lookup"><span data-stu-id="a5d54-177">No</span></span> |

<span data-ttu-id="a5d54-178">谢谢你，</span><span class="sxs-lookup"><span data-stu-id="a5d54-178">Thanks,</span></span>   
 <span data-ttu-id="a5d54-179">ASP.NET 团队</span><span class="sxs-lookup"><span data-stu-id="a5d54-179">The ASP.NET Team</span></span>
