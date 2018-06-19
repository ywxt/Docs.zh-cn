---
uid: whitepapers/ms03-32-issue
title: 应用安全更新，IE 后的修复不可用服务器应用程序错误 |Microsoft 文档
author: rick-anderson
description: 本白皮书介绍了为影响 Wi 上运行的 ASP.NET 1.0 应用程序的 Internet 资源管理器与 MS03 32 安全更新解决了问题的修补程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: 1365eebb-bdf7-4a05-8d18-7f200531be55
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/ms03-32-issue
msc.type: content
ms.openlocfilehash: dd1a564cd347364abc3ca5ac0a9ffda448bcede8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30898208"
---
<a name="fix-for-server-application-unavailable-error-after-applying-security-update-for-ie"></a><span data-ttu-id="6975f-103">应用安全更新的 IE 后为不可用服务器应用程序错误修复</span><span class="sxs-lookup"><span data-stu-id="6975f-103">Fix for 'Server Application Unavailable' Error after Applying Security Update for IE</span></span>
====================
> <span data-ttu-id="6975f-104">本白皮书介绍会影响 Windows XP 专业版上运行的 ASP.NET 1.0 应用程序的 Internet explorer 与 MS03 32 安全更新解决了问题的修补程序。</span><span class="sxs-lookup"><span data-stu-id="6975f-104">This paper describes the patch that fixes an issue with the MS03-32 Security Update for Internet Explorer that affects ASP.NET 1.0 applications running on Windows XP Professional.</span></span>
> 
> <span data-ttu-id="6975f-105">适用于 ASP.NET 1.0 和 Windows XP 专业版。</span><span class="sxs-lookup"><span data-stu-id="6975f-105">Applies to ASP.NET 1.0 and Windows XP Professional.</span></span>


<span data-ttu-id="6975f-106">Microsoft 与 Internet Explorer 的安全修补程序 MS03 32 安全更新和 Windows XP 上运行的 ASP.NET 1.0 标识的问题。</span><span class="sxs-lookup"><span data-stu-id="6975f-106">Microsoft identified an issue with the MS03-32 Security Update for Internet Explorer security patch and ASP.NET 1.0 running on Windows XP.</span></span> <span data-ttu-id="6975f-107">手动或通过从 Windows 更新站点中获取最新的关键更新，则可以安装此修补程序。</span><span class="sxs-lookup"><span data-stu-id="6975f-107">This patch can be installed manually or by obtaining recent critical updates from the Windows Update site.</span></span>

<span data-ttu-id="6975f-108">此问题的症状就是在一台 Windows XP 计算机上安装此修补程序后, 产生的本地 IIS 5.1 web 服务器上运行的 ASP.NET 应用程序的所有请求中一个表明"服务器应用程序不可用"错误消息。</span><span class="sxs-lookup"><span data-stu-id="6975f-108">The symptom of this issue is that after installing the patch on a Windows XP machine, all requests to ASP.NET applications running on the local IIS 5.1 web server result in an error message saying "Server Application Unavailable".</span></span> <span data-ttu-id="6975f-109">到远程 web 服务器的请求不会受到影响。</span><span class="sxs-lookup"><span data-stu-id="6975f-109">Requests to remote web servers are unaffected.</span></span>

<span data-ttu-id="6975f-110">此问题只会影响在 Windows XP 上运行 ASP.NET 1.0 安装。</span><span class="sxs-lookup"><span data-stu-id="6975f-110">This issue only impacts installations running ASP.NET 1.0 on Windows XP.</span></span> <span data-ttu-id="6975f-111">它不会影响运行 Windows 2000 或 Windows Server 2003 的计算机。</span><span class="sxs-lookup"><span data-stu-id="6975f-111">It does not impact machines running Windows 2000 or Windows Server 2003.</span></span> <span data-ttu-id="6975f-112">它也不会影响与 ASP.NET 1.1 安装运行 Windows XP 的计算机。</span><span class="sxs-lookup"><span data-stu-id="6975f-112">It also does not impact machines running Windows XP with ASP.NET 1.1 installed.</span></span>

<span data-ttu-id="6975f-113">请注意，此问题**不**使用 ASP.NET 安全 bug。</span><span class="sxs-lookup"><span data-stu-id="6975f-113">Please note that this issue **is not** a security bug with ASP.NET.</span></span> <span data-ttu-id="6975f-114">它**不**打开或允许对某个 ASP.NET 应用程序或服务器的任何恶意攻击。</span><span class="sxs-lookup"><span data-stu-id="6975f-114">It **does not** open up or allow any malicious attacks against an ASP.NET application or server.</span></span> <span data-ttu-id="6975f-115">相反，它是纯函数 bug 引起的修补程序本身。</span><span class="sxs-lookup"><span data-stu-id="6975f-115">Instead, it is purely a functional bug caused by the patch itself.</span></span>

<span data-ttu-id="6975f-116">我们正在努力针对此问题的永久解决方案。</span><span class="sxs-lookup"><span data-stu-id="6975f-116">We are working hard on a permanent solution for this issue.</span></span> <span data-ttu-id="6975f-117">在此期间，你可以执行以下的批处理文件作为一个问题的解决方法。</span><span class="sxs-lookup"><span data-stu-id="6975f-117">In the meantime, you can execute the following batch file as a workaround for the issue.</span></span> <span data-ttu-id="6975f-118">批处理文件执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="6975f-118">The batch file does the following:</span></span>

1. <span data-ttu-id="6975f-119">停止 IIS 和 ASP.NET 状态服务</span><span class="sxs-lookup"><span data-stu-id="6975f-119">Stops the IIS and ASP.NET state services</span></span>
2. <span data-ttu-id="6975f-120">删除并重新创建具有已知的临时密码的 ASPNET 帐户</span><span class="sxs-lookup"><span data-stu-id="6975f-120">Deletes and recreates the ASPNET account with a known temporary password</span></span>
3. <span data-ttu-id="6975f-121">使用 Windows`runas`命令以启动创建 ASPNET 用户配置文件的可执行文件</span><span class="sxs-lookup"><span data-stu-id="6975f-121">Uses the Windows `runas` command to launch an executable that creates an ASPNET user profile</span></span>
4. <span data-ttu-id="6975f-122">重新注册 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="6975f-122">Re-registers ASP.NET.</span></span> <span data-ttu-id="6975f-123">这将创建新的随机密码的帐户并将应用为其默认 ASP.NET 访问控制设置</span><span class="sxs-lookup"><span data-stu-id="6975f-123">This creates a new random password for the account and applies default ASP.NET access control settings for it</span></span>
5. <span data-ttu-id="6975f-124">重新启动 IIS 服务</span><span class="sxs-lookup"><span data-stu-id="6975f-124">Restarts the IIS service</span></span>

<span data-ttu-id="6975f-125">批处理文件包含硬编码的临时密码"<strong>1pass@word</strong>"你将提示您输入的 runas 命令运行批处理文件时。</span><span class="sxs-lookup"><span data-stu-id="6975f-125">The batch file contains a hardcoded temporary password of "<strong>1pass@word</strong>" which you will be prompted to enter for the runas command when the batch file is run.</span></span> <span data-ttu-id="6975f-126">Runas 命令完成后，ASPNET 帐户密码的强随机值使用重新创建。</span><span class="sxs-lookup"><span data-stu-id="6975f-126">After the runas command completes, the ASPNET account password is recreated with a strong random value.</span></span> <span data-ttu-id="6975f-127">请注意，如果硬编码密码不符合你的环境中的密码复杂性要求，可能会失败的批处理文件。</span><span class="sxs-lookup"><span data-stu-id="6975f-127">Note that the batch file may fail if the hardcoded password does not meet the password complexity requirements in your environment.</span></span> <span data-ttu-id="6975f-128">如果是这种情况，你可以将其更改为适合于你的环境的另一个值。</span><span class="sxs-lookup"><span data-stu-id="6975f-128">If that's the case, you can change it to another value that is appropriate for your environment.</span></span>

<span data-ttu-id="6975f-129">*> [!IMPORTANT]* 如果你已添加自定义访问控制设置或数据库帐户为 ASPNET 帐户的权限，它们将需要此批处理文件完成后重新创建。</span><span class="sxs-lookup"><span data-stu-id="6975f-129">*> [!IMPORTANT]* If you have added custom access control settings or database account permissions for the ASPNET account, they will need to be recreated after this batch file completes.</span></span> <span data-ttu-id="6975f-130">这是因为当该帐户将重新创建，它将获取新的安全标识符 (SID)。</span><span class="sxs-lookup"><span data-stu-id="6975f-130">This is because when the account is recreated, it will get a new security identifier (SID).</span></span>

<span data-ttu-id="6975f-131">*> [!IMPORTANT]* 如果运行的 ASP.NET 工作进程具有自定义在 ASPNET 帐户以外的帐户，则你不应运行此批处理文件。</span><span class="sxs-lookup"><span data-stu-id="6975f-131">*> [!IMPORTANT]* If you are running the ASP.NET worker process with a custom account other than the ASPNET account, then you should not run this batch file.</span></span> <span data-ttu-id="6975f-132">相反，你应该以交互方式登录或与该帐户将创建该帐户的用户配置文件中使用 runas 命令。</span><span class="sxs-lookup"><span data-stu-id="6975f-132">Instead, you should log in interactively or use the runas command with that account which will create a user profile for that account.</span></span>

<span data-ttu-id="6975f-133">批处理文件包含以下自解压缩的存档中。</span><span class="sxs-lookup"><span data-stu-id="6975f-133">The batch file is included in the self-extracting archive below.</span></span> <span data-ttu-id="6975f-134">若要使用它：</span><span class="sxs-lookup"><span data-stu-id="6975f-134">To use it:</span></span>

1. <span data-ttu-id="6975f-135">你必须为帐户运行，使用管理员权限</span><span class="sxs-lookup"><span data-stu-id="6975f-135">You must be running as an account with Administrator privileges</span></span>
2. [<span data-ttu-id="6975f-136">下载并打开自解压可执行文件</span><span class="sxs-lookup"><span data-stu-id="6975f-136">Download and open the self-extracting executable file</span></span>](ms03-32-issue/_static/fixup1.exe)
3. <span data-ttu-id="6975f-137">将内容提取到 c:\\</span><span class="sxs-lookup"><span data-stu-id="6975f-137">Extract the contents to c:\\</span></span>
4. <span data-ttu-id="6975f-138">从开始菜单中，选择运行...和输入 `cmd.exe`</span><span class="sxs-lookup"><span data-stu-id="6975f-138">Select Run... from the start menu, and enter `cmd.exe`</span></span>
5. <span data-ttu-id="6975f-139">在打开命令窗口中，键入`c:\fixup.cmd`。</span><span class="sxs-lookup"><span data-stu-id="6975f-139">In the open command windows, type `c:\fixup.cmd`.</span></span>
6. <span data-ttu-id="6975f-140">出现提示时，输入<strong>1pass@word</strong>作为密码。</span><span class="sxs-lookup"><span data-stu-id="6975f-140">When prompted, enter <strong>1pass@word</strong> as the password.</span></span>
7. <span data-ttu-id="6975f-141">如果你有以前自定义访问控制设置或数据库帐户为 ASPNET 帐户的权限，你将需要重新立即应用这些设置。</span><span class="sxs-lookup"><span data-stu-id="6975f-141">If you have previously custom access control settings or database account permissions for the ASPNET account, you'll need to re-apply these settings now.</span></span>

<span data-ttu-id="6975f-142">许多歉意，这导致歉意。</span><span class="sxs-lookup"><span data-stu-id="6975f-142">Many apologies for the inconvenience that this has caused.</span></span> <span data-ttu-id="6975f-143">随着可用，我们将发布的其他信息。</span><span class="sxs-lookup"><span data-stu-id="6975f-143">We'll post additional information as it becomes available.</span></span>

<span data-ttu-id="6975f-144">以下表详细说明了平台和版本受到此问题。</span><span class="sxs-lookup"><span data-stu-id="6975f-144">The matrix below details platforms and versions impacted by this issue.</span></span>

| <span data-ttu-id="6975f-145">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="6975f-145">.NET Framework</span></span> | <span data-ttu-id="6975f-146">平台</span><span class="sxs-lookup"><span data-stu-id="6975f-146">Platform</span></span> | <span data-ttu-id="6975f-147">受影响</span><span class="sxs-lookup"><span data-stu-id="6975f-147">Affected</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6975f-148">版本 1.0</span><span class="sxs-lookup"><span data-stu-id="6975f-148">Version 1.0</span></span> | <span data-ttu-id="6975f-149">Windows 2000 Professional</span><span class="sxs-lookup"><span data-stu-id="6975f-149">Windows 2000 Professional</span></span> | <span data-ttu-id="6975f-150">否</span><span class="sxs-lookup"><span data-stu-id="6975f-150">No</span></span> |
| <span data-ttu-id="6975f-151">版本 1.0</span><span class="sxs-lookup"><span data-stu-id="6975f-151">Version 1.0</span></span> | <span data-ttu-id="6975f-152">Windows 2000 Server</span><span class="sxs-lookup"><span data-stu-id="6975f-152">Windows 2000 Server</span></span> | <span data-ttu-id="6975f-153">否</span><span class="sxs-lookup"><span data-stu-id="6975f-153">No</span></span> |
| <span data-ttu-id="6975f-154">版本 1.0</span><span class="sxs-lookup"><span data-stu-id="6975f-154">Version 1.0</span></span> | <span data-ttu-id="6975f-155">Windows XP Professional</span><span class="sxs-lookup"><span data-stu-id="6975f-155">Windows XP Professional</span></span> | <span data-ttu-id="6975f-156">是</span><span class="sxs-lookup"><span data-stu-id="6975f-156">Yes</span></span> |
| <span data-ttu-id="6975f-157">版本 1.0</span><span class="sxs-lookup"><span data-stu-id="6975f-157">Version 1.0</span></span> | <span data-ttu-id="6975f-158">Windows Server 2003</span><span class="sxs-lookup"><span data-stu-id="6975f-158">Windows Server 2003</span></span> | <span data-ttu-id="6975f-159">否</span><span class="sxs-lookup"><span data-stu-id="6975f-159">No</span></span> |
| <span data-ttu-id="6975f-160">版本 1.0</span><span class="sxs-lookup"><span data-stu-id="6975f-160">Version 1.0</span></span> | <span data-ttu-id="6975f-161">使用 Cassini 的 Windows XP 家庭版</span><span class="sxs-lookup"><span data-stu-id="6975f-161">Windows XP Home with Cassini</span></span> | <span data-ttu-id="6975f-162">否</span><span class="sxs-lookup"><span data-stu-id="6975f-162">No</span></span> |
| <span data-ttu-id="6975f-163">版本 1.1</span><span class="sxs-lookup"><span data-stu-id="6975f-163">Version 1.1</span></span> | <span data-ttu-id="6975f-164">Windows 2000 Professional</span><span class="sxs-lookup"><span data-stu-id="6975f-164">Windows 2000 Professional</span></span> | <span data-ttu-id="6975f-165">否</span><span class="sxs-lookup"><span data-stu-id="6975f-165">No</span></span> |
| <span data-ttu-id="6975f-166">版本 1.1</span><span class="sxs-lookup"><span data-stu-id="6975f-166">Version 1.1</span></span> | <span data-ttu-id="6975f-167">Windows 2000 Server</span><span class="sxs-lookup"><span data-stu-id="6975f-167">Windows 2000 Server</span></span> | <span data-ttu-id="6975f-168">否</span><span class="sxs-lookup"><span data-stu-id="6975f-168">No</span></span> |
| <span data-ttu-id="6975f-169">版本 1.1</span><span class="sxs-lookup"><span data-stu-id="6975f-169">Version 1.1</span></span> | <span data-ttu-id="6975f-170">Windows XP Professional</span><span class="sxs-lookup"><span data-stu-id="6975f-170">Windows XP Professional</span></span> | <span data-ttu-id="6975f-171">否</span><span class="sxs-lookup"><span data-stu-id="6975f-171">No</span></span> |
| <span data-ttu-id="6975f-172">版本 1.1</span><span class="sxs-lookup"><span data-stu-id="6975f-172">Version 1.1</span></span> | <span data-ttu-id="6975f-173">Windows Server 2003</span><span class="sxs-lookup"><span data-stu-id="6975f-173">Windows Server 2003</span></span> | <span data-ttu-id="6975f-174">否</span><span class="sxs-lookup"><span data-stu-id="6975f-174">No</span></span> |
| <span data-ttu-id="6975f-175">版本 1.1</span><span class="sxs-lookup"><span data-stu-id="6975f-175">Version 1.1</span></span> | <span data-ttu-id="6975f-176">使用 Cassini 的 Windows XP 家庭版</span><span class="sxs-lookup"><span data-stu-id="6975f-176">Windows XP Home with Cassini</span></span> | <span data-ttu-id="6975f-177">否</span><span class="sxs-lookup"><span data-stu-id="6975f-177">No</span></span> |

<span data-ttu-id="6975f-178">谢谢，</span><span class="sxs-lookup"><span data-stu-id="6975f-178">Thanks,</span></span>   
 <span data-ttu-id="6975f-179">ASP.NET 团队</span><span class="sxs-lookup"><span data-stu-id="6975f-179">The ASP.NET Team</span></span>
