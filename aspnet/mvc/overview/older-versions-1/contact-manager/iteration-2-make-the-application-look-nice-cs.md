---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
title: 迭代 2 – 使应用程序外表美观的 (C#) |Microsoft Docs
author: microsoft
description: 在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1173feb-11ee-4017-8f3f-86599ea6ae13
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
msc.type: authoredcontent
ms.openlocfilehash: c8bbd20cb64fb27a0a6de2cdc14743f6961f4bf0
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834962"
---
<a name="iteration-2--make-the-application-look-nice-c"></a><span data-ttu-id="1ec2a-103">迭代 2 – 使应用程序外表美观的 (C#)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-103">Iteration #2 – Make the application look nice (C#)</span></span>
====================
<span data-ttu-id="1ec2a-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="1ec2a-105">下载代码</span><span class="sxs-lookup"><span data-stu-id="1ec2a-105">Download Code</span></span>](iteration-2-make-the-application-look-nice-cs/_static/contactmanager_2_cs1.zip)

> <span data-ttu-id="1ec2a-106">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-106">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="1ec2a-107">生成联系人管理 ASP.NET MVC 应用程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-107">Building a Contact Management ASP.NET MVC Application (C#)</span></span>
  

<span data-ttu-id="1ec2a-108">在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-108">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="1ec2a-109">联系人管理器应用程序，可存储联系人信息的名称，电话号码和电子邮件地址的人的列表。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-109">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="1ec2a-110">我们通过多个迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-110">We build the application over multiple iterations.</span></span> <span data-ttu-id="1ec2a-111">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-111">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="1ec2a-112">此多个迭代方法的目标是帮助你了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-112">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="1ec2a-113">迭代 1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-113">Iteration #1 - Create the application.</span></span> <span data-ttu-id="1ec2a-114">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-114">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="1ec2a-115">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-115">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="1ec2a-116">迭代 2 – 使应用程序看上去更美观。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-116">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="1ec2a-117">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-117">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="1ec2a-118">迭代 3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-118">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="1ec2a-119">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-119">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="1ec2a-120">我们阻止用户提交窗体而无法完成所需的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-120">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="1ec2a-121">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-121">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="1ec2a-122">迭代 4-使应用程序松散耦合。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-122">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="1ec2a-123">在此第四个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-123">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="1ec2a-124">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-124">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="1ec2a-125">迭代 5 — 创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-125">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="1ec2a-126">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-126">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="1ec2a-127">我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-127">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="1ec2a-128">迭代 6-使用测试驱动的开发。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-128">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="1ec2a-129">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-129">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="1ec2a-130">在此迭代中，我们将添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-130">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="1ec2a-131">迭代 7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-131">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="1ec2a-132">在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-132">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="1ec2a-133">此迭代</span><span class="sxs-lookup"><span data-stu-id="1ec2a-133">This Iteration</span></span>

<span data-ttu-id="1ec2a-134">此迭代的目标是提高联系人管理器应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-134">The goal of this iteration is to improve the appearance of the Contact Manager application.</span></span> <span data-ttu-id="1ec2a-135">目前，联系人管理器使用默认 ASP.NET MVC 视图母版页和级联样式表 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-135">Currently, the Contact Manager uses the default ASP.NET MVC view master page and cascading style sheet (see Figure 1).</span></span> <span data-ttu-id="1ec2a-136">这些不要看上去有错误，但我不想要看起来正像 ASP.NET MVC 的其他每个网站的联系人管理器。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-136">These don t look bad, but I don t want the Contact Manager to look just like every other ASP.NET MVC website.</span></span> <span data-ttu-id="1ec2a-137">我想要自定义文件中替换这些文件。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-137">I want to replace these files with custom files.</span></span>


<span data-ttu-id="1ec2a-138">[![新建项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-138">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)</span></span>

<span data-ttu-id="1ec2a-139">**图 01**： 将 ASP.NET MVC 应用程序的默认外观 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="1ec2a-139">**Figure 01**: The default appearance of an ASP.NET MVC Application ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image2.png))</span></span>


<span data-ttu-id="1ec2a-140">在此迭代中，我将介绍两种方法可以改进我们的应用程序的可视设计。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-140">In this iteration, I discuss two approaches to improving the visual design of our application.</span></span> <span data-ttu-id="1ec2a-141">首先，我介绍您如何充分利用 ASP.NET MVC 设计库下载免费的 ASP.NET MVC 设计模板。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-141">First, I show you how to take advantage of the ASP.NET MVC Design gallery to download a free ASP.NET MVC design template.</span></span> <span data-ttu-id="1ec2a-142">ASP.NET MVC 设计库，可创建专业的 web 应用程序不执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-142">The ASP.NET MVC Design gallery enables you to create a professional web application without doing any work.</span></span>

<span data-ttu-id="1ec2a-143">我决定不使用 ASP.NET MVC 设计库中的联系人管理器应用程序模板。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-143">I decided to not use a template from the ASP.NET MVC Design gallery for the Contact Manager application.</span></span> <span data-ttu-id="1ec2a-144">相反，我创建的专业设计公司的自定义设计。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-144">Instead, I had a custom design created by a professional design firm.</span></span> <span data-ttu-id="1ec2a-145">在本教程的第二部分，我将说明我的专业设计公司创建最终的 ASP.NET MVC 设计的工作方式。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-145">In the second part of this tutorial, I explain how I worked with a professional design company to create the final ASP.NET MVC design.</span></span>

## <a name="the-aspnet-mvc-design-gallery"></a><span data-ttu-id="1ec2a-146">ASP.NET MVC 设计库</span><span class="sxs-lookup"><span data-stu-id="1ec2a-146">The ASP.NET MVC Design Gallery</span></span>

<span data-ttu-id="1ec2a-147">ASP.NET MVC 设计库是由 Microsoft 提供的免费资源。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-147">The ASP.NET MVC Design Gallery is a free resource provided by Microsoft.</span></span> <span data-ttu-id="1ec2a-148">ASP.NET MVC 库位于以下地址：</span><span class="sxs-lookup"><span data-stu-id="1ec2a-148">The ASP.NET MVC Gallery is located at the following address:</span></span>

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

<span data-ttu-id="1ec2a-149">ASP.NET MVC 设计库托管的免费网站设计专门为使用 ASP.NET MVC 项目中创建的集合。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-149">The ASP.NET MVC Design Gallery hosts a collection of free website designs that were created specifically for using in an ASP.NET MVC project.</span></span> <span data-ttu-id="1ec2a-150">设计会上传由社区的成员。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-150">Designs are uploaded by members of the community.</span></span> <span data-ttu-id="1ec2a-151">库的访问者可以对他们最喜爱的设计进行投票 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-151">Visitors to the Gallery can vote for their favorite designs (see Figure 2).</span></span>


<span data-ttu-id="1ec2a-152">[![新建项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-152">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)</span></span>

<span data-ttu-id="1ec2a-153">**图 02**: ASP.NET MVC 设计库 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="1ec2a-153">**Figure 02**: The ASP.NET MVC Design Gallery ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image4.png))</span></span>


<span data-ttu-id="1ec2a-154">在我撰写本教程中，在库中最受欢迎的设计是由 David Hauser 命名年 10 月的设计。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-154">As I write this tutorial, the most popular design in the gallery is a design named October by David Hauser.</span></span> <span data-ttu-id="1ec2a-155">可以通过完成以下步骤来为 ASP.NET MVC 项目中使用这种设计：</span><span class="sxs-lookup"><span data-stu-id="1ec2a-155">You can use this design for an ASP.NET MVC project by completing the following steps:</span></span>

1. <span data-ttu-id="1ec2a-156">单击**下载**按钮 October.zip 文件下载到您的计算机。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-156">Click the **Download** button to download the October.zip file to your computer.</span></span>
2. <span data-ttu-id="1ec2a-157">右键单击下载的 October.zip 文件，然后单击**解除阻止**按钮 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-157">Right-click the downloaded October.zip file and click the **Unblock** button (see Figure 3).</span></span>
3. <span data-ttu-id="1ec2a-158">将文件提取到名为年 10 月的文件夹。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-158">Unzip the file to a folder named October.</span></span>
4. <span data-ttu-id="1ec2a-159">从年 10 月文件夹中包含 DesignTemplate 文件夹中选择的所有文件，右键单击文件，然后选择菜单选项**复制**。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-159">Select all of the files from the DesignTemplate folder contained in the October folder, right-click the files, and select the menu option **Copy**.</span></span>
5. <span data-ttu-id="1ec2a-160">右键单击 Visual Studio 解决方案资源管理器窗口中的 ContactManager 项目节点，然后选择菜单选项**粘贴**（请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-160">Right-click the ContactManager project node in the Visual Studio Solution Explorer window and select the menu option **Paste** (see Figure 4).</span></span>
6. <span data-ttu-id="1ec2a-161">选择 Visual Studio 的菜单选项**编辑、 查找和替换，快速替换**和替换 *[MyProjectName]* 与*ContactManager* （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-161">Select the Visual Studio menu option **Edit, Find and Replace, Quick Replace** and replace *[MyProjectName]* with *ContactManager* (see Figure 5).</span></span>


<span data-ttu-id="1ec2a-162">[![新建项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-162">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)</span></span>

<span data-ttu-id="1ec2a-163">**图 03**： 取消阻止文件从 web 下载 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="1ec2a-163">**Figure 03**: Unblocking a file downloaded from the web ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image6.png))</span></span>


<span data-ttu-id="1ec2a-164">[![新建项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-164">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)</span></span>

<span data-ttu-id="1ec2a-165">**图 04**： 重写在解决方案资源管理器中的文件 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="1ec2a-165">**Figure 04**: Overwriting files in the Solution Explorer ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image8.png))</span></span>


<span data-ttu-id="1ec2a-166">[![新建项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-166">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)</span></span>

<span data-ttu-id="1ec2a-167">**图 05**: [ProjectName] 替换为 ContactManager ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="1ec2a-167">**Figure 05**: Replacing [ProjectName] with ContactManager ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image10.png))</span></span>


<span data-ttu-id="1ec2a-168">完成这些步骤后，web 应用程序将使用新的设计。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-168">After you complete these steps, your web application will use the new design.</span></span> <span data-ttu-id="1ec2a-169">图 6 中的页说明了与年 10 月设计 Contact Manager 应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-169">The page in Figure 6 illustrates the appearance of the Contact Manager application with the October design.</span></span>


<span data-ttu-id="1ec2a-170">[![新建项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-170">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)</span></span>

<span data-ttu-id="1ec2a-171">**图 06**： 使用年 10 月模板 ContactManager ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="1ec2a-171">**Figure 06**: ContactManager with the October template ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image12.png))</span></span>


## <a name="creating-a-custom-aspnet-mvc-design"></a><span data-ttu-id="1ec2a-172">创建自定义 ASP.NET MVC 设计</span><span class="sxs-lookup"><span data-stu-id="1ec2a-172">Creating a Custom ASP.NET MVC Design</span></span>

<span data-ttu-id="1ec2a-173">ASP.NET MVC 设计库具有不同的设计样式的不错的选择。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-173">The ASP.NET MVC Design Gallery has a good selection of different design styles.</span></span> <span data-ttu-id="1ec2a-174">库提供了一种轻松的方法，以自定义 ASP.NET MVC 应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-174">The Gallery provides you with a painless way to customize the appearance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="1ec2a-175">而且，当然，库已大优点是完全免费。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-175">And, of course, the Gallery has the big advantage of being completely free.</span></span>

<span data-ttu-id="1ec2a-176">但是，您可能需要创建你的网站的完全唯一设计。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-176">However, you might need to create a completely unique design for your website.</span></span> <span data-ttu-id="1ec2a-177">在这种情况下，最好使用网站设计公司。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-177">In that case, it makes sense to work with a website design company.</span></span> <span data-ttu-id="1ec2a-178">我决定采用此方法的联系人管理器应用程序的设计。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-178">I decided to take this approach for the design for the Contact Manager application.</span></span>

<span data-ttu-id="1ec2a-179">我压缩了联系人管理器从迭代 #1 并发送到设计公司的项目。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-179">I zipped up the Contact Manager from Iteration #1 and sent the project to the design company.</span></span> <span data-ttu-id="1ec2a-180">它们不归 Visual Studio （感到难为情它们 ！），但该无效 t 出现问题。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-180">They did not own Visual Studio (shame on them!), but that didn t present a problem.</span></span> <span data-ttu-id="1ec2a-181">他们就能够从免费下载 Microsoft Visual Web Developer [ https://www.asp.net ](https://www.asp.net)网站，然后打开 Visual Web Developer 中的联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-181">They were able to download Microsoft Visual Web Developer for free from the [https://www.asp.net](https://www.asp.net) website and open the Contact Manager application in Visual Web Developer.</span></span> <span data-ttu-id="1ec2a-182">在几天，它们必须生成图 7 中的设计。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-182">In a couple of days, they had produced the design in Figure 7.</span></span>


<span data-ttu-id="1ec2a-183">[![新建项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-183">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)</span></span>

<span data-ttu-id="1ec2a-184">**图 07**: ASP.NET MVC 联系人管理器中设计 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="1ec2a-184">**Figure 07**: The ASP.NET MVC Contact Manager Design ([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image14.png))</span></span>


<span data-ttu-id="1ec2a-185">新的设计包括两个主要文件： 新的级联样式表文件和新视图母版页文件。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-185">The new design consisted of two main files: a new cascading style sheet file and a new view master page file.</span></span> <span data-ttu-id="1ec2a-186">视图母版页包含布局和共享的内容的 ASP.NET MVC 应用程序中的视图。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-186">A view master page contains the layout and shared content for views in an ASP.NET MVC application.</span></span> <span data-ttu-id="1ec2a-187">例如，视图母版页包括标头、 导航选项卡和页脚显示在图 7。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-187">For example, the view master page includes the header, navigation tabs, and footer that appear in Figure 7.</span></span> <span data-ttu-id="1ec2a-188">我使用从设计公司中，新的 Site.Master 文件覆盖现有 Site.Master 视图母版页中的 Views\Shared 文件夹</span><span class="sxs-lookup"><span data-stu-id="1ec2a-188">I overwrote the existing Site.Master view master page in the Views\Shared folder with the new Site.Master file from the design company,</span></span>

<span data-ttu-id="1ec2a-189">设计公司还创建了新的级联样式表和的图像集。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-189">The design company also created a new cascading style sheet and set of images.</span></span> <span data-ttu-id="1ec2a-190">我的内容文件夹中放置了这些新文件，并覆盖现有 Site.css 文件。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-190">I placed these new files in the Content folder and overwrote the existing Site.css file.</span></span> <span data-ttu-id="1ec2a-191">应将所有静态内容放在内容文件夹中。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-191">You should place all static content in the Content folder.</span></span>

<span data-ttu-id="1ec2a-192">请注意，新设计的联系人管理器中包含图像编辑和删除联系人。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-192">Notice that the new design for the Contact Manager includes images for editing and deleting contacts.</span></span> <span data-ttu-id="1ec2a-193">联系人的 HTML 表中每个联系人旁边出现的编辑和删除映像。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-193">An Edit and Delete image appear next to each contact in the HTML table of contacts.</span></span>

<span data-ttu-id="1ec2a-194">最初，这些链接在呈现的 HTML。此类 ActionLink() 帮助程序：</span><span class="sxs-lookup"><span data-stu-id="1ec2a-194">Originally, these links that were rendered with the HTML.ActionLink() helper like this:</span></span>

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample1.aspx)]

<span data-ttu-id="1ec2a-195">Html.ActionLink() 方法不支持 （方法 HTML 编码的链接文本出于安全原因） 的映像。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-195">The Html.ActionLink() method does not support images (the method HTML encodes the link text for security reasons).</span></span> <span data-ttu-id="1ec2a-196">因此，我可以对 Html.ActionLink() 调用替换到 Url.Action() 如下调用：</span><span class="sxs-lookup"><span data-stu-id="1ec2a-196">Therefore, I replaced the calls to Html.ActionLink() with calls to Url.Action() like this:</span></span>

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample2.aspx)]

<span data-ttu-id="1ec2a-197">Html.ActionLink() 方法将呈现整个 HTML 超链接。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-197">The Html.ActionLink() method renders an entire HTML hyperlink.</span></span> <span data-ttu-id="1ec2a-198">Url.Action() 方法，但是，呈现只是不带 URL &lt;&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-198">The Url.Action() method, on the other hand, renders just the URL without the &lt;a&gt; tag.</span></span>

<span data-ttu-id="1ec2a-199">此外，请注意，新的设计包括选定和未选定的选项卡。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-199">Notice, furthermore, that the new design includes both selected and unselected tabs.</span></span> <span data-ttu-id="1ec2a-200">例如，在图 8**创建新的联系人**选择选项卡和**我的联系人**不选择选项卡。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-200">For example, in Figure 8, the **Create New Contact** tab is selected and the **My Contacts** tab is not selected.</span></span>


<span data-ttu-id="1ec2a-201">[![新建项目对话框](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-201">[![The New Project dialog box](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)</span></span>

<span data-ttu-id="1ec2a-202">**图 08**： 选中和取消选中选项卡 ([单击以查看实际尺寸的图像](iteration-2-make-the-application-look-nice-cs/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="1ec2a-202">**Figure 08**: Selected and unselected tabs([Click to view full-size image](iteration-2-make-the-application-look-nice-cs/_static/image16.png))</span></span>


<span data-ttu-id="1ec2a-203">若要支持呈现选定和未选定的选项卡，我创建了名为 MenuItemHelper 的自定义 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-203">To support rendering both selected and unselected tabs, I created a custom HTML helper named the MenuItemHelper.</span></span> <span data-ttu-id="1ec2a-204">此帮助器方法将呈现任一&lt;li&gt;标记或&lt;l i 类 ="所选"&gt;具体取决于当前的控制器和操作是否对应于传递给帮助者的控制器和操作名称的标记。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-204">This helper method renders either a &lt;li&gt; tag or a &lt;li class="selected"&gt; tag depending on whether the current controller and action corresponds to the controller and action name passed to the helper.</span></span> <span data-ttu-id="1ec2a-205">MenuItemHelper 的代码包含在列表 1 中。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-205">The code for the MenuItemHelper is contained in Listing 1.</span></span>

<span data-ttu-id="1ec2a-206">**代码清单 1-Helpers\MenuItemHelper.cs**</span><span class="sxs-lookup"><span data-stu-id="1ec2a-206">**Listing 1 - Helpers\MenuItemHelper.cs**</span></span>

[!code-csharp[Main](iteration-2-make-the-application-look-nice-cs/samples/sample3.cs)]

<span data-ttu-id="1ec2a-207">MenuItemHelper TagBuilder 类在内部用于生成&lt;li&gt; HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-207">The MenuItemHelper uses the TagBuilder class internally to build the &lt;li&gt; HTML tag.</span></span> <span data-ttu-id="1ec2a-208">TagBuilder 类是无论何时需要新的 HTML 标记生成可以使用一个非常有用的实用工具类。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-208">The TagBuilder class is a very useful utility class that you can use whenever you need to build up a new HTML tag.</span></span> <span data-ttu-id="1ec2a-209">它包括用于添加属性、 添加 CSS 类、 生成 Id，和修改标记的方法内部 HTML。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-209">It includes methods for adding attributes, adding CSS classes, generating Ids, and modifying the tag s inner HTML.</span></span>

## <a name="summary"></a><span data-ttu-id="1ec2a-210">总结</span><span class="sxs-lookup"><span data-stu-id="1ec2a-210">Summary</span></span>

<span data-ttu-id="1ec2a-211">在此迭代中，我们改进了 ASP.NET MVC 应用程序的可视设计。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-211">In this iteration, we improved the visual design of our ASP.NET MVC application.</span></span> <span data-ttu-id="1ec2a-212">首先，已引入到 ASP.NET MVC 设计库。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-212">First, you were introduced to the ASP.NET MVC Design Gallery.</span></span> <span data-ttu-id="1ec2a-213">您学习了如何从 ASP.NET MVC 设计库，可以使用 ASP.NET MVC 应用程序中下载免费的设计模板。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-213">You learned how to download free design templates from the ASP.NET MVC Design Gallery that you can use in your ASP.NET MVC applications.</span></span>

<span data-ttu-id="1ec2a-214">接下来，我们讨论了如何通过修改默认级联样式表文件和母版视图页文件创建自定义设计。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-214">Next, we discussed how you can create a custom design by modifying the default cascading style sheet file and master view page file.</span></span> <span data-ttu-id="1ec2a-215">为了支持新的设计，我们需要对我们的联系人管理器应用程序进行少量更改。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-215">In order to support the new design, we had to make some minor changes to our Contact Manager application.</span></span> <span data-ttu-id="1ec2a-216">例如，我们添加了名为显示选定和未选定的选项卡 MenuItemHelper 的新 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-216">For example, we added a new HTML helper named the MenuItemHelper that displays selected and unselected tabs.</span></span>

<span data-ttu-id="1ec2a-217">在下一个迭代中，我们将探讨的验证非常重要的主题。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-217">In the next iteration, we tackle the very important subject of validation.</span></span> <span data-ttu-id="1ec2a-218">以便用户不能创建新的联系人，无需首先提供所需的值，例如一个人 s 名和姓，我们将验证代码添加到我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1ec2a-218">We add validation code to our application so that a user cannot create a new contact without supplying required values such as a person s first and last name.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ec2a-219">[上一页](iteration-1-create-the-application-cs.md)
> [下一页](iteration-3-add-form-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1ec2a-219">[Previous](iteration-1-create-the-application-cs.md)
[Next](iteration-3-add-form-validation-cs.md)</span></span>
