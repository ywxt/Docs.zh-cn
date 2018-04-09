---
uid: web-pages/overview/data/5-working-with-data
title: 使用在 ASP.NET 网页中的数据库的简介页 (Razor) 站点 |Microsoft 文档
author: tfitzmac
description: 本章介绍如何从数据库访问数据并将其使用的 ASP.NET Web Pages 显示。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2014
ms.topic: article
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 563074cf3e60717c2e6c336a2c282b4203f73b8b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="a39a0-103">使用在 ASP.NET 网页中的数据库的简介页 (Razor) 站点</span><span class="sxs-lookup"><span data-stu-id="a39a0-103">Introduction to Working with a Database in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="a39a0-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a39a0-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a39a0-105">本文介绍如何使用 Microsoft WebMatrix 工具创建的数据库在一个 ASP.NET Web 页 (Razor) 的网站，以及如何创建网页，让你显示、 添加、 编辑和删除数据。</span><span class="sxs-lookup"><span data-stu-id="a39a0-105">This article describes how to use Microsoft WebMatrix tools to create a database in an ASP.NET Web Pages (Razor) website, and how to create pages that let you display, add, edit, and delete data.</span></span>
> 
> <span data-ttu-id="a39a0-106">**你将学习：**</span><span class="sxs-lookup"><span data-stu-id="a39a0-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="a39a0-107">如何创建数据库。</span><span class="sxs-lookup"><span data-stu-id="a39a0-107">How to create a database.</span></span>
> - <span data-ttu-id="a39a0-108">如何连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="a39a0-108">How to connect to a database.</span></span>
> - <span data-ttu-id="a39a0-109">如何在网页上显示数据。</span><span class="sxs-lookup"><span data-stu-id="a39a0-109">How to display data in a web page.</span></span>
> - <span data-ttu-id="a39a0-110">如何插入、 更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="a39a0-110">How to insert, update, and delete database records.</span></span>
> 
> <span data-ttu-id="a39a0-111">这些是文章中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="a39a0-111">These are the features introduced in the article:</span></span>
> 
> - <span data-ttu-id="a39a0-112">使用 Microsoft SQL Server Compact Edition 数据库。</span><span class="sxs-lookup"><span data-stu-id="a39a0-112">Working with a Microsoft SQL Server Compact Edition database.</span></span>
> - <span data-ttu-id="a39a0-113">使用 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="a39a0-113">Working with SQL queries.</span></span>
> - <span data-ttu-id="a39a0-114">`Database` 类。</span><span class="sxs-lookup"><span data-stu-id="a39a0-114">The `Database` class.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a39a0-115">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="a39a0-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a39a0-116">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="a39a0-116">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="a39a0-117">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="a39a0-117">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="a39a0-118">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="a39a0-118">This tutorial also works with WebMatrix 3.</span></span> <span data-ttu-id="a39a0-119">你可以使用 ASP.NET Web Pages 3 和 Visual Studio 2013 （或 Visual Studio Express 2013 for Web）;但是，用户界面将会不同。</span><span class="sxs-lookup"><span data-stu-id="a39a0-119">You can use ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web); however, the user interface will be different.</span></span>


## <a name="introduction-to-databases"></a><span data-ttu-id="a39a0-120">数据库简介</span><span class="sxs-lookup"><span data-stu-id="a39a0-120">Introduction to Databases</span></span>

<span data-ttu-id="a39a0-121">假设一个典型的通讯簿。</span><span class="sxs-lookup"><span data-stu-id="a39a0-121">Imagine a typical address book.</span></span> <span data-ttu-id="a39a0-122">每个条目的通讯簿中 (即，每人) 具有以下几条如名字、 姓氏、 地址、 电子邮件地址和电话号码的信息。</span><span class="sxs-lookup"><span data-stu-id="a39a0-122">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

<span data-ttu-id="a39a0-123">如下图数据的典型方法是为包含行和列的表。</span><span class="sxs-lookup"><span data-stu-id="a39a0-123">A typical way to picture data like this is as a table with rows and columns.</span></span> <span data-ttu-id="a39a0-124">在数据库术语中，每个行通常称为记录。</span><span class="sxs-lookup"><span data-stu-id="a39a0-124">In database terms, each row is often referred to as a record.</span></span> <span data-ttu-id="a39a0-125">每个列 （有时称为字段） 包含每种数据类型的值： 第一个名称，最后一个名称和等等。</span><span class="sxs-lookup"><span data-stu-id="a39a0-125">Each column (sometimes referred to as fields) contains a value for each type of data: first name, last name, and so on.</span></span>

| <span data-ttu-id="a39a0-126">**ID**</span><span class="sxs-lookup"><span data-stu-id="a39a0-126">**ID**</span></span> | <span data-ttu-id="a39a0-127">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="a39a0-127">**FirstName**</span></span> | <span data-ttu-id="a39a0-128">**LastName**</span><span class="sxs-lookup"><span data-stu-id="a39a0-128">**LastName**</span></span> | <span data-ttu-id="a39a0-129">**Address**</span><span class="sxs-lookup"><span data-stu-id="a39a0-129">**Address**</span></span> | <span data-ttu-id="a39a0-130">**Email**</span><span class="sxs-lookup"><span data-stu-id="a39a0-130">**Email**</span></span> | <span data-ttu-id="a39a0-131">**Phone**</span><span class="sxs-lookup"><span data-stu-id="a39a0-131">**Phone**</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="a39a0-132">1</span><span class="sxs-lookup"><span data-stu-id="a39a0-132">1</span></span> | <span data-ttu-id="a39a0-133">Jim</span><span class="sxs-lookup"><span data-stu-id="a39a0-133">Jim</span></span> | <span data-ttu-id="a39a0-134">Abrus</span><span class="sxs-lookup"><span data-stu-id="a39a0-134">Abrus</span></span> | <span data-ttu-id="a39a0-135">210 100th St SE Orcas WA 98031</span><span class="sxs-lookup"><span data-stu-id="a39a0-135">210 100th St SE Orcas WA 98031</span></span> | jim@contoso.com | <span data-ttu-id="a39a0-136">555 0100</span><span class="sxs-lookup"><span data-stu-id="a39a0-136">555 0100</span></span> |
| <span data-ttu-id="a39a0-137">2</span><span class="sxs-lookup"><span data-stu-id="a39a0-137">2</span></span> | <span data-ttu-id="a39a0-138">Terry</span><span class="sxs-lookup"><span data-stu-id="a39a0-138">Terry</span></span> | <span data-ttu-id="a39a0-139">Adams</span><span class="sxs-lookup"><span data-stu-id="a39a0-139">Adams</span></span> | <span data-ttu-id="a39a0-140">1234 Main St.西雅图市华盛顿州 99011</span><span class="sxs-lookup"><span data-stu-id="a39a0-140">1234 Main St. Seattle WA 99011</span></span> | terry@cohowinery.com | <span data-ttu-id="a39a0-141">555 0101</span><span class="sxs-lookup"><span data-stu-id="a39a0-141">555 0101</span></span> |

<span data-ttu-id="a39a0-142">对于大多数数据库表，该表必须有一列以包含的唯一标识符，如客户编号、 帐户号等。这称为表的*主键*，并使用它来标识表中的每个行。</span><span class="sxs-lookup"><span data-stu-id="a39a0-142">For most database tables, the table has to have a column that contains a unique identifier, like a customer number, account number, etc. This is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="a39a0-143">在示例中，ID 列是通讯簿的主键。</span><span class="sxs-lookup"><span data-stu-id="a39a0-143">In the example, the ID column is the primary key for the address book.</span></span>

<span data-ttu-id="a39a0-144">此数据库的基本的了解，你就可以了解如何创建一个简单的数据库并执行如添加、 修改和删除数据的操作。</span><span class="sxs-lookup"><span data-stu-id="a39a0-144">With this basic understanding of databases, you're ready to learn how to create a simple database and perform operations such as adding, modifying, and deleting data.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="a39a0-145">**关系数据库**</span><span class="sxs-lookup"><span data-stu-id="a39a0-145">**Relational Databases**</span></span>
> 
> <span data-ttu-id="a39a0-146">你可以将数据存储在大量方法，包括文本文件和电子表格。</span><span class="sxs-lookup"><span data-stu-id="a39a0-146">You can store data in lots of ways, including text files and spreadsheets.</span></span> <span data-ttu-id="a39a0-147">对于大多数的业务使用，不过，数据存储在关系数据库中。</span><span class="sxs-lookup"><span data-stu-id="a39a0-147">For most business uses, though, data is stored in a relational database.</span></span>
> 
> <span data-ttu-id="a39a0-148">本文不非常深进入数据库。</span><span class="sxs-lookup"><span data-stu-id="a39a0-148">This article doesn't go very deeply into databases.</span></span> <span data-ttu-id="a39a0-149">但是，你可能会发现它有助于了解一些有关它们的信息。</span><span class="sxs-lookup"><span data-stu-id="a39a0-149">However, you might find it useful to understand a little about them.</span></span> <span data-ttu-id="a39a0-150">在关系数据库中，信息在逻辑上划分为单独的表。</span><span class="sxs-lookup"><span data-stu-id="a39a0-150">In a relational database, information is logically divided into separate tables.</span></span> <span data-ttu-id="a39a0-151">例如，一所学校的数据库可能包含单独的表，学生版和类产品。</span><span class="sxs-lookup"><span data-stu-id="a39a0-151">For example, a database for a school might contain separate tables for students and for class offerings.</span></span> <span data-ttu-id="a39a0-152">数据库软件 （如 SQL Server) 支持强大命令，使您动态建立表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="a39a0-152">The database software (such as SQL Server) supports powerful commands that let you dynamically establish relationships between the tables.</span></span> <span data-ttu-id="a39a0-153">例如，关系数据库可用于逻辑之间建立关系学生和类以创建计划。</span><span class="sxs-lookup"><span data-stu-id="a39a0-153">For example, you can use the relational database to establish a logical relationship between students and classes in order to create a schedule.</span></span> <span data-ttu-id="a39a0-154">在单独的表中存储数据可减少表结构的复杂性，而无需将冗余数据保留在表。</span><span class="sxs-lookup"><span data-stu-id="a39a0-154">Storing data in separate tables reduces the complexity of the table structure and reduces the need to keep redundant data in tables.</span></span>


## <a name="creating-a-database"></a><span data-ttu-id="a39a0-155">创建数据库</span><span class="sxs-lookup"><span data-stu-id="a39a0-155">Creating a Database</span></span>

<span data-ttu-id="a39a0-156">此过程演示如何创建名 SmallBakery 为使用 SQL Server Compact 数据库设计工具在 WebMatrix 中包含的数据库。</span><span class="sxs-lookup"><span data-stu-id="a39a0-156">This procedure shows you how to create a database named SmallBakery by using the SQL Server Compact Database design tool that's included in WebMatrix.</span></span> <span data-ttu-id="a39a0-157">虽然你可以创建使用代码的数据库，它是更常见的做法创建数据库和数据库表使用 WebMatrix 之类的设计工具。</span><span class="sxs-lookup"><span data-stu-id="a39a0-157">Although you can create a database using code, it's more typical to create the database and database tables using a design tool like WebMatrix.</span></span>

1. <span data-ttu-id="a39a0-158">启动 WebMatrix，然后在快速启动页上，单击**站点从模板**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-158">Start WebMatrix, and on the Quick Start page, click **Site From Template**.</span></span>
2. <span data-ttu-id="a39a0-159">选择**空网站**，然后在**站点名称**框中输入"SmallBakery"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-159">Select **Empty Site**, and in the **Site Name** box enter "SmallBakery" and then click **OK**.</span></span> <span data-ttu-id="a39a0-160">创建站点并将其显示在 WebMatrix 中。</span><span class="sxs-lookup"><span data-stu-id="a39a0-160">The site is created and displayed in WebMatrix.</span></span>
3. <span data-ttu-id="a39a0-161">在左窗格中，单击**数据库**工作区。</span><span class="sxs-lookup"><span data-stu-id="a39a0-161">In the left pane, click the **Databases** workspace.</span></span>
4. <span data-ttu-id="a39a0-162">在功能区中，单击**新数据库**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-162">In the ribbon, click **New Database**.</span></span> <span data-ttu-id="a39a0-163">使用与你的站点相同的名称创建一个空数据库。</span><span class="sxs-lookup"><span data-stu-id="a39a0-163">An empty database is created with the same name as your site.</span></span>
5. <span data-ttu-id="a39a0-164">在左窗格中，展开**SmallBakery.sdf**节点，然后单击**表**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-164">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
6. <span data-ttu-id="a39a0-165">在功能区中，单击**新表**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-165">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="a39a0-166">WebMatrix 打开表设计器。</span><span class="sxs-lookup"><span data-stu-id="a39a0-166">WebMatrix opens the table designer.</span></span>

    ![[image]](5-working-with-data/_static/image1.jpg)
7. <span data-ttu-id="a39a0-168">在单击**名称**列和输入&quot;Id&quot;。</span><span class="sxs-lookup"><span data-stu-id="a39a0-168">Click in the **Name** column and enter &quot;Id&quot;.</span></span>
8. <span data-ttu-id="a39a0-169">在**数据类型**列中，选择**int**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-169">In the **Data Type** column, select **int**.</span></span>
9. <span data-ttu-id="a39a0-170">设置**是主键？**和**是识别？**选项到**是**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-170">Set the **Is Primary Key?** and **Is Identify?** options to **Yes**.</span></span>

    <span data-ttu-id="a39a0-171">顾名思义，**是 Primary Key**告诉数据库，这将是表的主键。</span><span class="sxs-lookup"><span data-stu-id="a39a0-171">As the name suggests, **Is Primary Key** tells the database that this will be the table's primary key.</span></span> <span data-ttu-id="a39a0-172">**是标识**告诉数据库自动创建新的每个记录的 ID 号并将其分配下一步的序列号 （从 1 开始）。</span><span class="sxs-lookup"><span data-stu-id="a39a0-172">**Is Identity** tells the database to automatically create an ID number for every new record and to assign it the next sequential number (starting at 1).</span></span>
10. <span data-ttu-id="a39a0-173">单击下一步的行中。</span><span class="sxs-lookup"><span data-stu-id="a39a0-173">Click in the next row.</span></span> <span data-ttu-id="a39a0-174">此时将启动一个新的列定义编辑器。</span><span class="sxs-lookup"><span data-stu-id="a39a0-174">The editor starts a new column definition.</span></span>
11. <span data-ttu-id="a39a0-175">对于名称值中，输入&quot;名称&quot;。</span><span class="sxs-lookup"><span data-stu-id="a39a0-175">For the Name value, enter &quot;Name&quot;.</span></span>
12. <span data-ttu-id="a39a0-176">有关**数据类型**，选择&quot;nvarchar&quot;和长度设置为 50。</span><span class="sxs-lookup"><span data-stu-id="a39a0-176">For **Data Type**, choose &quot;nvarchar&quot; and set the length to 50.</span></span> <span data-ttu-id="a39a0-177">*Var*属于`nvarchar`告诉数据库此列的数据将为其大小可能有所不同记录之间的字符串。</span><span class="sxs-lookup"><span data-stu-id="a39a0-177">The *var* part of `nvarchar` tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="a39a0-178">( *N*前缀表示*国家/地区*、，该值指示字段可以保存表示任何字母的字符数据或写入系统&#8212;，即，该字段将持有 Unicode 数据。)</span><span class="sxs-lookup"><span data-stu-id="a39a0-178">(The *n* prefix represents *national*, indicating that the field can hold character data that represents any alphabet or writing system &#8212; that is, that the field holds Unicode data.)</span></span>
13. <span data-ttu-id="a39a0-179">设置**允许 null 值**选项设为**否**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-179">Set the **Allow Nulls** option to **No**.</span></span> <span data-ttu-id="a39a0-180">这会强制此要求*名称*列不会保留空白。</span><span class="sxs-lookup"><span data-stu-id="a39a0-180">This will enforce that the *Name* column is not left blank.</span></span>
14. <span data-ttu-id="a39a0-181">使用此相同的过程中，创建一个名为列*说明*。</span><span class="sxs-lookup"><span data-stu-id="a39a0-181">Using this same process, create a column named *Description*.</span></span> <span data-ttu-id="a39a0-182">设置**数据类型**"nvarchar"和长度，并设置 50**允许 null 值**为 false。</span><span class="sxs-lookup"><span data-stu-id="a39a0-182">Set **Data Type** to "nvarchar" and 50 for the length, and set **Allow Nulls** to false.</span></span>
15. <span data-ttu-id="a39a0-183">创建一个名为列*价格*。</span><span class="sxs-lookup"><span data-stu-id="a39a0-183">Create a column named *Price*.</span></span> <span data-ttu-id="a39a0-184">设置**数据类型设置为"货币"**并设置**允许 null 值**为 false。</span><span class="sxs-lookup"><span data-stu-id="a39a0-184">Set **Data Type to "money"** and set **Allow Nulls** to false.</span></span>
16. <span data-ttu-id="a39a0-185">在顶部的框中，命名表&quot;产品&quot;。</span><span class="sxs-lookup"><span data-stu-id="a39a0-185">In the box at the top, name the table &quot;Product&quot;.</span></span>

    <span data-ttu-id="a39a0-186">完成后，定义将如下所示：</span><span class="sxs-lookup"><span data-stu-id="a39a0-186">When you're done, the definition will look like this:</span></span>

    ![[image]](5-working-with-data/_static/image2.jpg)
17. <span data-ttu-id="a39a0-188">按 Ctrl + S 以保存表。</span><span class="sxs-lookup"><span data-stu-id="a39a0-188">Press Ctrl+S to save the table.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="a39a0-189">向数据库添加数据</span><span class="sxs-lookup"><span data-stu-id="a39a0-189">Adding Data to the Database</span></span>

<span data-ttu-id="a39a0-190">现在你可以添加到你的数据库，你将在本文的后面使用的一些示例数据。</span><span class="sxs-lookup"><span data-stu-id="a39a0-190">Now you can add some sample data to your database that you'll work with later in the article.</span></span>

1. <span data-ttu-id="a39a0-191">在左窗格中，展开**SmallBakery.sdf**节点，然后单击**表**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-191">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
2. <span data-ttu-id="a39a0-192">右键单击产品表，然后单击**数据**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-192">Right-click the Product table and then click **Data**.</span></span>
3. <span data-ttu-id="a39a0-193">在编辑窗格中，输入以下记录：</span><span class="sxs-lookup"><span data-stu-id="a39a0-193">In the edit pane, enter the following records:</span></span>

    | <span data-ttu-id="a39a0-194">**名称**</span><span class="sxs-lookup"><span data-stu-id="a39a0-194">**Name**</span></span> | <span data-ttu-id="a39a0-195">**说明**</span><span class="sxs-lookup"><span data-stu-id="a39a0-195">**Description**</span></span> | <span data-ttu-id="a39a0-196">**价格**</span><span class="sxs-lookup"><span data-stu-id="a39a0-196">**Price**</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="a39a0-197">痕迹</span><span class="sxs-lookup"><span data-stu-id="a39a0-197">Bread</span></span> | <span data-ttu-id="a39a0-198">由新颖度每日。</span><span class="sxs-lookup"><span data-stu-id="a39a0-198">Baked fresh every day.</span></span> | <span data-ttu-id="a39a0-199">2.99</span><span class="sxs-lookup"><span data-stu-id="a39a0-199">2.99</span></span> |
    | <span data-ttu-id="a39a0-200">草莓 Shortcake</span><span class="sxs-lookup"><span data-stu-id="a39a0-200">Strawberry Shortcake</span></span> | <span data-ttu-id="a39a0-201">从我们园使用环保 strawberries 进行。</span><span class="sxs-lookup"><span data-stu-id="a39a0-201">Made with organic strawberries from our garden.</span></span> | <span data-ttu-id="a39a0-202">9.99</span><span class="sxs-lookup"><span data-stu-id="a39a0-202">9.99</span></span> |
    | <span data-ttu-id="a39a0-203">Apple 饼图</span><span class="sxs-lookup"><span data-stu-id="a39a0-203">Apple Pie</span></span> | <span data-ttu-id="a39a0-204">仅为你的妈妈饼图的第二个。</span><span class="sxs-lookup"><span data-stu-id="a39a0-204">Second only to your mom's pie.</span></span> | <span data-ttu-id="a39a0-205">12.99</span><span class="sxs-lookup"><span data-stu-id="a39a0-205">12.99</span></span> |
    | <span data-ttu-id="a39a0-206">Pecan 饼图</span><span class="sxs-lookup"><span data-stu-id="a39a0-206">Pecan Pie</span></span> | <span data-ttu-id="a39a0-207">如果你喜欢 pecans，这是为你。</span><span class="sxs-lookup"><span data-stu-id="a39a0-207">If you like pecans, this is for you.</span></span> | <span data-ttu-id="a39a0-208">10.99</span><span class="sxs-lookup"><span data-stu-id="a39a0-208">10.99</span></span> |
    | <span data-ttu-id="a39a0-209">柠檬饼图</span><span class="sxs-lookup"><span data-stu-id="a39a0-209">Lemon Pie</span></span> | <span data-ttu-id="a39a0-210">使用世界上的最佳柠檬进行。</span><span class="sxs-lookup"><span data-stu-id="a39a0-210">Made with the best lemons in the world.</span></span> | <span data-ttu-id="a39a0-211">11.99</span><span class="sxs-lookup"><span data-stu-id="a39a0-211">11.99</span></span> |
    | <span data-ttu-id="a39a0-212">蛋糕</span><span class="sxs-lookup"><span data-stu-id="a39a0-212">Cupcakes</span></span> | <span data-ttu-id="a39a0-213">你的孩子和在你的孩子将喜欢这些。</span><span class="sxs-lookup"><span data-stu-id="a39a0-213">Your kids and the kid in you will love these.</span></span> | <span data-ttu-id="a39a0-214">7.99</span><span class="sxs-lookup"><span data-stu-id="a39a0-214">7.99</span></span> |

    <span data-ttu-id="a39a0-215">请记住，你不必输入任何内容的*Id*列。</span><span class="sxs-lookup"><span data-stu-id="a39a0-215">Remember that you don't have to enter anything for the *Id* column.</span></span> <span data-ttu-id="a39a0-216">你在创建时*Id*列中，设置其**是标识**属性为 true，这会导致它自动填充的。</span><span class="sxs-lookup"><span data-stu-id="a39a0-216">When you created the *Id* column, you set its **Is Identity** property to true, which causes it to automatically be filled in.</span></span>

    <span data-ttu-id="a39a0-217">当完成输入数据时，表设计器将如下所示：</span><span class="sxs-lookup"><span data-stu-id="a39a0-217">When you're finished entering the data, the table designer will look like this:</span></span>

    ![[image]](5-working-with-data/_static/image3.jpg)
4. <span data-ttu-id="a39a0-219">关闭包含的数据库数据的选项卡。</span><span class="sxs-lookup"><span data-stu-id="a39a0-219">Close the tab that contains the database data.</span></span>

## <a name="displaying-data-from-a-database"></a><span data-ttu-id="a39a0-220">显示数据库中的数据</span><span class="sxs-lookup"><span data-stu-id="a39a0-220">Displaying Data from a Database</span></span>

<span data-ttu-id="a39a0-221">一旦在其中配置了具有数据的数据库，你可以在 ASP.NET 网页中显示数据。</span><span class="sxs-lookup"><span data-stu-id="a39a0-221">Once you've got a database with data in it, you can display the data in an ASP.NET web page.</span></span> <span data-ttu-id="a39a0-222">若要选择要显示的表行，你可以使用 SQL 语句，这是一个可将传递到数据库的命令。</span><span class="sxs-lookup"><span data-stu-id="a39a0-222">To select the table rows to display, you use a SQL statement, which is a command that you pass to the database.</span></span>

1. <span data-ttu-id="a39a0-223">在左窗格中，单击**文件**工作区。</span><span class="sxs-lookup"><span data-stu-id="a39a0-223">In the left pane, click the **Files** workspace.</span></span>
2. <span data-ttu-id="a39a0-224">在网站的根目录，创建一个名为的新 CSHTML 页*ListProducts.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a39a0-224">In the root of the website, create a new CSHTML page named *ListProducts.cshtml*.</span></span>
3. <span data-ttu-id="a39a0-225">现有的标记替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="a39a0-225">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    <span data-ttu-id="a39a0-226">你可以在第一个代码块中，打开*SmallBakery.sdf*前面创建的文件 （数据库）。</span><span class="sxs-lookup"><span data-stu-id="a39a0-226">In the first code block, you open the *SmallBakery.sdf* file (database) that you created earlier.</span></span> <span data-ttu-id="a39a0-227">`Database.Open`方法假设*.sdf*文件位于你的网站*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="a39a0-227">The `Database.Open` method assumes that the *.sdf* file is in your website's *App\_Data* folder.</span></span> <span data-ttu-id="a39a0-228">(请注意，不需要指定*.sdf*扩展&#8212;事实上，如果这样做，`Open`方法将不起作用。)</span><span class="sxs-lookup"><span data-stu-id="a39a0-228">(Notice that you don't need to specify the *.sdf* extension &#8212; in fact, if you do, the `Open` method won't work.)</span></span>

    > [!NOTE]
    > <span data-ttu-id="a39a0-229">*应用\_数据*文件夹是用于存储数据文件的 ASP.NET 中的特殊文件夹。</span><span class="sxs-lookup"><span data-stu-id="a39a0-229">The *App\_Data* folder is a special folder in ASP.NET that's used to store data files.</span></span> <span data-ttu-id="a39a0-230">有关详细信息，请参阅[连接到数据库](#SB_ConnectingToADatabase)本文后续部分中。</span><span class="sxs-lookup"><span data-stu-id="a39a0-230">For more information, see [Connecting to a Database](#SB_ConnectingToADatabase) later in this article.</span></span>

    <span data-ttu-id="a39a0-231">然后发出请求以查询数据库中使用以下 SQL`Select`语句：</span><span class="sxs-lookup"><span data-stu-id="a39a0-231">You then make a request to query the database using the following SQL `Select` statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    <span data-ttu-id="a39a0-232">在语句中，`Product`标识要查询表。</span><span class="sxs-lookup"><span data-stu-id="a39a0-232">In the statement, `Product` identifies the table to query.</span></span> <span data-ttu-id="a39a0-233">`*`字符指定查询应返回表中的所有列。</span><span class="sxs-lookup"><span data-stu-id="a39a0-233">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="a39a0-234">（你可能还列出列单独，由逗号分隔，如果你想要看到仅某些列。）`Order By`子句指示数据的排序方式&#8212;在这种情况下，通过*名称*列。</span><span class="sxs-lookup"><span data-stu-id="a39a0-234">(You could also list columns individually, separated by commas, if you wanted to see only some of the columns.) The `Order By` clause indicates how the data should be sorted &#8212; in this case, by the *Name* column.</span></span> <span data-ttu-id="a39a0-235">这意味着对数据进行排序的值按字母顺序基于*名称*每一行的列。</span><span class="sxs-lookup"><span data-stu-id="a39a0-235">This means that the data is sorted alphabetically based on the value of the *Name* column for each row.</span></span>

    <span data-ttu-id="a39a0-236">在页的正文中，标记将创建一个 HTML 表以将用于显示数据。</span><span class="sxs-lookup"><span data-stu-id="a39a0-236">In the body of the page, the markup creates an HTML table that will be used to display the data.</span></span> <span data-ttu-id="a39a0-237">内部`<tbody>`元素，你使用`foreach`循环单独获取由查询返回的每个数据行。</span><span class="sxs-lookup"><span data-stu-id="a39a0-237">Inside the `<tbody>` element, you use a `foreach` loop to individually get each data row that's returned by the query.</span></span> <span data-ttu-id="a39a0-238">对于每个数据行，创建一个 HTML 表行 (`<tr>`元素)。</span><span class="sxs-lookup"><span data-stu-id="a39a0-238">For each data row, you create an HTML table row (`<tr>` element).</span></span> <span data-ttu-id="a39a0-239">然后创建 HTML 表格单元格 (`<td>`元素) 为每个列。</span><span class="sxs-lookup"><span data-stu-id="a39a0-239">Then you create HTML table cells (`<td>` elements) for each column.</span></span> <span data-ttu-id="a39a0-240">每次执行循环时，请转到下一步的可用行从数据库已处于`row`变量 (你对此进行设置`foreach`语句)。</span><span class="sxs-lookup"><span data-stu-id="a39a0-240">Each time you go through the loop, the next available row from the database is in the `row` variable (you set this up in the `foreach` statement).</span></span> <span data-ttu-id="a39a0-241">若要获取行中的单个列，可以使用`row.Name`或`row.Description`或者的列的任何名称是你想。</span><span class="sxs-lookup"><span data-stu-id="a39a0-241">To get an individual column from the row, you can use `row.Name` or `row.Description` or whatever the name is of the column you want.</span></span>
4. <span data-ttu-id="a39a0-242">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="a39a0-242">Run the page in a browser.</span></span> <span data-ttu-id="a39a0-243">(请确保页中选择**文件**工作区之前运行它。)该页显示如下所示的列表：</span><span class="sxs-lookup"><span data-stu-id="a39a0-243">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays a list like the following:</span></span>

    ![[image]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="a39a0-245">**结构化的查询语言 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="a39a0-245">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="a39a0-246">SQL 是一种语言，可在大多数关系数据库中用于管理数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="a39a0-246">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="a39a0-247">它包括能够让你检索数据和更新它，并能够让你创建、 修改和管理数据库表的命令。</span><span class="sxs-lookup"><span data-stu-id="a39a0-247">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage database tables.</span></span> <span data-ttu-id="a39a0-248">SQL 是不同于编程语言 （如你在 WebMatrix 中使用的一个） 因为使用 SQL 的想法是告诉数据库所需的并且在各数据库的作业，以了解如何获取数据或执行任务。</span><span class="sxs-lookup"><span data-stu-id="a39a0-248">SQL is different than a programming language (like the one you're using in WebMatrix) because with SQL, the idea is that you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="a39a0-249">下面是一些 SQL 命令的示例和它们执行的操作：</span><span class="sxs-lookup"><span data-stu-id="a39a0-249">Here are examples of some SQL commands and what they do:</span></span>
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="a39a0-250">这提取*Id*，*名称*，和*价格*中记录的列*产品*表如果的值*价格*大于 10，并将结果返回的值为基础的按字母顺序*名称*列。</span><span class="sxs-lookup"><span data-stu-id="a39a0-250">This fetches the *Id*, *Name*, and *Price* columns from records in the *Product* table if the value of *Price* is more than 10, and returns the results in alphabetical order based on the values of the *Name* column.</span></span> <span data-ttu-id="a39a0-251">此命令将返回包含满足条件或为空集，如果没有与匹配记录的记录的结果集。</span><span class="sxs-lookup"><span data-stu-id="a39a0-251">This command will return a result set that contains the records that meet the criteria, or an empty set if no records match.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> <span data-ttu-id="a39a0-252">这会插入新记录到*产品*表，设置*名称*列&quot;Croissant&quot;、*说明*列&quot;发生异常喜欢广为&quot;，到 1.99 与价格。</span><span class="sxs-lookup"><span data-stu-id="a39a0-252">This inserts a new record into the *Product* table, setting the *Name* column to &quot;Croissant&quot;, the *Description* column to &quot;A flaky delight&quot;, and the price to 1.99.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> <span data-ttu-id="a39a0-253">此命令删除中的记录*产品*其到期日期列是早于 2008 年 1 月 1 日的表。</span><span class="sxs-lookup"><span data-stu-id="a39a0-253">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="a39a0-254">(此操作假定*产品*表具有这样的列，这是当然的。)采用 MM/DD/YYYY 格式，在此处输入日期，但它应该用于你的区域设置的格式输入。</span><span class="sxs-lookup"><span data-stu-id="a39a0-254">(This assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="a39a0-255">`Insert Into`和`Delete`命令不返回结果集。</span><span class="sxs-lookup"><span data-stu-id="a39a0-255">The `Insert Into` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="a39a0-256">相反，它们返回一个数字，告诉你该命令影响了多少条记录。</span><span class="sxs-lookup"><span data-stu-id="a39a0-256">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="a39a0-257">对于某些这些操作 （例如插入和删除记录），请求操作的过程必须在数据库中具有适当的权限。</span><span class="sxs-lookup"><span data-stu-id="a39a0-257">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="a39a0-258">这是通常必须提供用户名和密码连接到数据库时的生产数据库的原因。</span><span class="sxs-lookup"><span data-stu-id="a39a0-258">This is why for production databases you often have to supply a username and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="a39a0-259">有多个 SQL 命令，但它们都遵循如下模式。</span><span class="sxs-lookup"><span data-stu-id="a39a0-259">There are dozens of SQL commands, but they all follow a pattern like this.</span></span> <span data-ttu-id="a39a0-260">SQL 命令可用于创建数据库表、 计算的表中的记录数、 计算价格，和执行许多的更多操作。</span><span class="sxs-lookup"><span data-stu-id="a39a0-260">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>


## <a name="inserting-data-in-a-database"></a><span data-ttu-id="a39a0-261">在数据库中插入数据</span><span class="sxs-lookup"><span data-stu-id="a39a0-261">Inserting Data in a Database</span></span>

<span data-ttu-id="a39a0-262">本部分演示如何创建一个允许用户添加到新的产品页面*产品*数据库表。</span><span class="sxs-lookup"><span data-stu-id="a39a0-262">This section shows how to create a page that lets users add a new product to the *Product* database table.</span></span> <span data-ttu-id="a39a0-263">插入新的产品记录后，页面将显示更新后的表使用*ListProducts.cshtml*你在上一节中创建的页。</span><span class="sxs-lookup"><span data-stu-id="a39a0-263">After a new product record is inserted, the page displays the updated table using the *ListProducts.cshtml* page that you created in the previous section.</span></span>

<span data-ttu-id="a39a0-264">该页面包括验证以确保用户输入的数据有效的数据库。</span><span class="sxs-lookup"><span data-stu-id="a39a0-264">The page includes validation to make sure that the data that the user enters is valid for the database.</span></span> <span data-ttu-id="a39a0-265">例如，在页中的代码可确保已为所有所需的列输入值。</span><span class="sxs-lookup"><span data-stu-id="a39a0-265">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>

1. <span data-ttu-id="a39a0-266">在网站中，创建一个名为的新 CSHTML 文件*InsertProducts.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a39a0-266">In the website, create a new CSHTML file named *InsertProducts.cshtml*.</span></span>
2. <span data-ttu-id="a39a0-267">现有的标记替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="a39a0-267">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    <span data-ttu-id="a39a0-268">页的正文包含使用户可以输入名称、 描述和价格的三个文本框一个 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="a39a0-268">The body of the page contains an HTML form with three text boxes that let users enter a name, description, and price.</span></span> <span data-ttu-id="a39a0-269">当用户单击**插入**按钮，在页面顶部的代码打开的连接*SmallBakery.sdf*数据库。</span><span class="sxs-lookup"><span data-stu-id="a39a0-269">When users click the **Insert** button, the code at the top of the page opens a connection to the *SmallBakery.sdf* database.</span></span> <span data-ttu-id="a39a0-270">您会收到用户通过使用已提交的值`Request`对象并将这些值分配给本地变量。</span><span class="sxs-lookup"><span data-stu-id="a39a0-270">You then get the values that the user has submitted by using the `Request` object and assign those values to local variables.</span></span>

    <span data-ttu-id="a39a0-271">若要验证用户为每个所需的列输入一个值，你注册每个`<input>`你想要验证的元素：</span><span class="sxs-lookup"><span data-stu-id="a39a0-271">To validate that the user entered a value for each required column, you register each `<input>` element that you want to validate:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    <span data-ttu-id="a39a0-272">`Validation`帮助器检查每个已注册的字段中是否有一个值。</span><span class="sxs-lookup"><span data-stu-id="a39a0-272">The `Validation` helper checks that there is a value in each of the fields that you've registered.</span></span> <span data-ttu-id="a39a0-273">你可以测试是否所有字段通过检查已都通过验证`Validation.IsValid()`，后者通常执行之前处理从用户获取的信息：</span><span class="sxs-lookup"><span data-stu-id="a39a0-273">You can test whether all the fields passed validation by checking `Validation.IsValid()`, which you typically do before you process the information you get from the user:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    <span data-ttu-id="a39a0-274">(`&&`运算符表示 AND-此测试*如果这是提交窗体和所有字段已都通过验证*。)</span><span class="sxs-lookup"><span data-stu-id="a39a0-274">(The `&&` operator means AND — this test is *If this is a form submission AND all the fields have passed validation*.)</span></span>

    <span data-ttu-id="a39a0-275">如果验证了所有列 （无为空），请继续并创建一个 SQL 语句来将数据插入，然后执行它，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a39a0-275">If all the columns validated (none were empty), you go ahead and create a SQL statement to insert the data and then execute it as shown next:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    <span data-ttu-id="a39a0-276">要插入的值，包括参数占位符 (`@0`， `@1`， `@2`)。</span><span class="sxs-lookup"><span data-stu-id="a39a0-276">For the values to insert, you include parameter placeholders (`@0`, `@1`, `@2`).</span></span>

    > [!NOTE]
    > <span data-ttu-id="a39a0-277">作为安全措施，始终将值传递给 SQL 语句使用参数，如上所示在前面的示例。</span><span class="sxs-lookup"><span data-stu-id="a39a0-277">As a security precaution, always pass values to a SQL statement using parameters, as you see in the preceding example.</span></span> <span data-ttu-id="a39a0-278">这使你可以首先验证用户的数据，以及它有助于保护计算机免受恶意命令发送到数据库 （有时称为 SQL 注入式攻击） 的尝试。</span><span class="sxs-lookup"><span data-stu-id="a39a0-278">This gives you a chance to validate the user's data, plus it helps protect against attempts to send malicious commands to your database (sometimes referred to as SQL injection attacks).</span></span>

    <span data-ttu-id="a39a0-279">若要执行查询时，你使用此语句中，将传递到它包含要替换的占位符的值的变量：</span><span class="sxs-lookup"><span data-stu-id="a39a0-279">To execute the query, you use this statement, passing to it the variables that contain the values to substitute for the placeholders:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    <span data-ttu-id="a39a0-280">后`Insert Into`已执行语句，将用户发送给页，其中列出的产品使用以下行：</span><span class="sxs-lookup"><span data-stu-id="a39a0-280">After the `Insert Into` statement has executed, you send the user to the page that lists the products using this line:</span></span>

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    <span data-ttu-id="a39a0-281">如果验证未成功，则跳过插入。</span><span class="sxs-lookup"><span data-stu-id="a39a0-281">If validation didn't succeed, you skip the insert.</span></span> <span data-ttu-id="a39a0-282">相反，你可以显示累积的错误消息 （如果有） 的页中具有帮助器：</span><span class="sxs-lookup"><span data-stu-id="a39a0-282">Instead, you have a helper in the page that can display the accumulated error messages (if any):</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    <span data-ttu-id="a39a0-283">请注意，在标记中的样式块包括 CSS 类定义名为`.validation-summary-errors`。</span><span class="sxs-lookup"><span data-stu-id="a39a0-283">Notice that the style block in the markup includes a CSS class definition named `.validation-summary-errors`.</span></span> <span data-ttu-id="a39a0-284">这是默认情况下，为使用 CSS 类的名称`<div>`包含任何验证错误的元素。</span><span class="sxs-lookup"><span data-stu-id="a39a0-284">This is the name of the CSS class that's used by default for the `<div>` element that contains any validation errors.</span></span> <span data-ttu-id="a39a0-285">在这种情况下，CSS 类指定验证摘要错误显示为红色和显示为粗体，但你可以定义`.validation-summary-errors`类来显示任何您喜欢的格式设置。</span><span class="sxs-lookup"><span data-stu-id="a39a0-285">In this case, the CSS class specifies that validation summary errors are displayed in red and in bold, but you can define the `.validation-summary-errors` class to display any formatting you like.</span></span>

### <a name="testing-the-insert-page"></a><span data-ttu-id="a39a0-286">测试插入页</span><span class="sxs-lookup"><span data-stu-id="a39a0-286">Testing the Insert Page</span></span>

1. <span data-ttu-id="a39a0-287">在浏览器中查看的页面。</span><span class="sxs-lookup"><span data-stu-id="a39a0-287">View the page in a browser.</span></span> <span data-ttu-id="a39a0-288">该页面显示类似于下图中所示的一个窗体。</span><span class="sxs-lookup"><span data-stu-id="a39a0-288">The page displays a form that's similar to the one that's shown in the following illustration.</span></span>

    ![[image]](5-working-with-data/_static/image5.jpg)
2. <span data-ttu-id="a39a0-290">对于所有列，输入值，但请确保你保留*价格*列保留为空。</span><span class="sxs-lookup"><span data-stu-id="a39a0-290">Enter values for all the columns, but make sure that you leave the *Price* column blank.</span></span>
3. <span data-ttu-id="a39a0-291">单击“插入” 。</span><span class="sxs-lookup"><span data-stu-id="a39a0-291">Click **Insert**.</span></span> <span data-ttu-id="a39a0-292">页面显示错误消息，如下面的插图中所示。</span><span class="sxs-lookup"><span data-stu-id="a39a0-292">The page displays an error message, as shown in the following illustration.</span></span> <span data-ttu-id="a39a0-293">（不创建任何新的记录。）</span><span class="sxs-lookup"><span data-stu-id="a39a0-293">(No new record is created.)</span></span>

    ![[image]](5-working-with-data/_static/image6.jpg)
4. <span data-ttu-id="a39a0-295">完全，填写表单，然后单击**插入**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-295">Fill the form out completely, and then click **Insert**.</span></span> <span data-ttu-id="a39a0-296">此时， *ListProducts.cshtml*页会显示，并显示新的记录。</span><span class="sxs-lookup"><span data-stu-id="a39a0-296">This time, the *ListProducts.cshtml* page is displayed and shows the new record.</span></span>

## <a name="updating-data-in-a-database"></a><span data-ttu-id="a39a0-297">更新数据库中的数据</span><span class="sxs-lookup"><span data-stu-id="a39a0-297">Updating Data in a Database</span></span>

<span data-ttu-id="a39a0-298">数据输入到表后，你可能需要更新它。</span><span class="sxs-lookup"><span data-stu-id="a39a0-298">After data has been entered into a table, you might need to update it.</span></span> <span data-ttu-id="a39a0-299">此过程演示如何创建类似于前面的数据插入操作创建的两个页面。</span><span class="sxs-lookup"><span data-stu-id="a39a0-299">This procedure shows you how to create two pages that are similar to the ones you created for data insertion earlier.</span></span> <span data-ttu-id="a39a0-300">第一页显示产品，并使用户可以选择一个计数器以更改。</span><span class="sxs-lookup"><span data-stu-id="a39a0-300">The first page displays products and lets users select one to change.</span></span> <span data-ttu-id="a39a0-301">可以在第二个页的实际进行的编辑和保存它们的用户。</span><span class="sxs-lookup"><span data-stu-id="a39a0-301">The second page lets the users actually make the edits and save them.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a39a0-302">**重要**在生产网站中，你通常限制允许哪些人具有对数据进行更改。</span><span class="sxs-lookup"><span data-stu-id="a39a0-302">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="a39a0-303">有关如何将成员资格设置以及如何授权用户的站点上执行任务的信息，请参阅[添加安全和 ASP.NET Web Pages 站点的成员资格](https://go.microsoft.com/fwlink/?LinkId=202904)。</span><span class="sxs-lookup"><span data-stu-id="a39a0-303">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>


1. <span data-ttu-id="a39a0-304">在网站中，创建一个名为的新 CSHTML 文件*EditProducts.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a39a0-304">In the website, create a new CSHTML file named *EditProducts.cshtml*.</span></span>
2. <span data-ttu-id="a39a0-305">文件中的现有标记替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="a39a0-305">Replace the existing markup in the file with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    <span data-ttu-id="a39a0-306">此页之间唯一的区别和*ListProducts.cshtml*页从更早版本是在此页中的 HTML 表包含的额外的列显示**编辑**链接。</span><span class="sxs-lookup"><span data-stu-id="a39a0-306">The only difference between this page and the *ListProducts.cshtml* page from earlier is that the HTML table in this page includes an extra column that displays an **Edit** link.</span></span> <span data-ttu-id="a39a0-307">单击此链接时，它将带你访问*UpdateProducts.cshtml*页面 （其中你将创建下一步） 可以在其中编辑选定的记录。</span><span class="sxs-lookup"><span data-stu-id="a39a0-307">When you click this link, it takes you to the *UpdateProducts.cshtml* page (which you'll create next) where you can edit the selected record.</span></span>

    <span data-ttu-id="a39a0-308">查看创建的代码**编辑**链接：</span><span class="sxs-lookup"><span data-stu-id="a39a0-308">Look at the code that creates the **Edit** link:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    <span data-ttu-id="a39a0-309">这将创建 HTML`<a>`元素其`href`动态设置属性。</span><span class="sxs-lookup"><span data-stu-id="a39a0-309">This creates an HTML `<a>` element whose `href` attribute is set dynamically.</span></span> <span data-ttu-id="a39a0-310">`href`属性指定当用户单击该链接时要显示的页。</span><span class="sxs-lookup"><span data-stu-id="a39a0-310">The `href` attribute specifies the page to display when the user clicks the link.</span></span> <span data-ttu-id="a39a0-311">它还将传递`Id`链接到当前行的值。</span><span class="sxs-lookup"><span data-stu-id="a39a0-311">It also passes the `Id` value of the current row to the link.</span></span> <span data-ttu-id="a39a0-312">当运行页面时，页面源文件可能包含类似这样的链接：</span><span class="sxs-lookup"><span data-stu-id="a39a0-312">When the page runs, the page source might contain links like these:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    <span data-ttu-id="a39a0-313">请注意，`href`属性设置为`UpdateProducts/n`，其中*n*是产品编号。</span><span class="sxs-lookup"><span data-stu-id="a39a0-313">Notice that the `href` attribute is set to `UpdateProducts/n`, where *n* is a product number.</span></span> <span data-ttu-id="a39a0-314">当用户单击这些链接之一时，生成的 URL 将如下所示：</span><span class="sxs-lookup"><span data-stu-id="a39a0-314">When a user clicks one of these links, the resulting URL will look something like this:</span></span>

    `http://localhost:18816/UpdateProducts/6`

    <span data-ttu-id="a39a0-315">换而言之，将在 URL 中传递的产品编号，以对其进行编辑。</span><span class="sxs-lookup"><span data-stu-id="a39a0-315">In other words, the product number to be edited will be passed in the URL.</span></span>
3. <span data-ttu-id="a39a0-316">在浏览器中查看的页面。</span><span class="sxs-lookup"><span data-stu-id="a39a0-316">View the page in a browser.</span></span> <span data-ttu-id="a39a0-317">该页显示数据的格式如下：</span><span class="sxs-lookup"><span data-stu-id="a39a0-317">The page displays the data in a format like this:</span></span>

    ![[image]](5-working-with-data/_static/image7.jpg)

    <span data-ttu-id="a39a0-319">接下来，你将创建页面，从而让用户实际更新的数据。</span><span class="sxs-lookup"><span data-stu-id="a39a0-319">Next, you'll create the page that lets users actually update the data.</span></span> <span data-ttu-id="a39a0-320">更新页面包括验证来验证用户输入的数据。</span><span class="sxs-lookup"><span data-stu-id="a39a0-320">The update page includes validation to validate the data that the user enters.</span></span> <span data-ttu-id="a39a0-321">例如，在页中的代码可确保已为所有所需的列输入值。</span><span class="sxs-lookup"><span data-stu-id="a39a0-321">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>
4. <span data-ttu-id="a39a0-322">在网站中，创建一个名为的新 CSHTML 文件*UpdateProducts.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a39a0-322">In the website, create a new CSHTML file named *UpdateProducts.cshtml*.</span></span>
5. <span data-ttu-id="a39a0-323">将替换为以下文件中的现有标记。</span><span class="sxs-lookup"><span data-stu-id="a39a0-323">Replace the existing markup in the file with the following.</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    <span data-ttu-id="a39a0-324">页面的正文包含 HTML 窗体，其中显示产品和用户可以在其中编辑。</span><span class="sxs-lookup"><span data-stu-id="a39a0-324">The body of the page contains an HTML form where a product is displayed and where users can edit it.</span></span> <span data-ttu-id="a39a0-325">若要获取要显示的产品，你可以使用此 SQL 语句：</span><span class="sxs-lookup"><span data-stu-id="a39a0-325">To get the product to display, you use this SQL statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    <span data-ttu-id="a39a0-326">这将选择其 ID 与传入的值匹配的产品`@0`参数。</span><span class="sxs-lookup"><span data-stu-id="a39a0-326">This will select the product whose ID matches the value that's passed in the `@0` parameter.</span></span> <span data-ttu-id="a39a0-327">(因为*Id*是主键，因此必须是唯一的只有一个产品记录可以不断选择这种方式。)若要获取的 ID 值传递给这`Select`语句中，你可以读取的值传递到页的 url 的一部分使用以下语法：</span><span class="sxs-lookup"><span data-stu-id="a39a0-327">(Because *Id* is the primary key and therefore must be unique, only one product record can ever be selected this way.) To get the ID value to pass to this `Select` statement, you can read the value that's passed to the page as part of the URL, using the following syntax:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    <span data-ttu-id="a39a0-328">若要实际提取的产品记录，请使用`QuerySingle`方法，它将返回一个记录：</span><span class="sxs-lookup"><span data-stu-id="a39a0-328">To actually fetch the product record, you use the `QuerySingle` method, which will return just one record:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    <span data-ttu-id="a39a0-329">中的单个行返回到`row`变量。</span><span class="sxs-lookup"><span data-stu-id="a39a0-329">The single row is returned into the `row` variable.</span></span> <span data-ttu-id="a39a0-330">你可以获取超出每个列的数据，并将其分配给本地变量如下：</span><span class="sxs-lookup"><span data-stu-id="a39a0-330">You can get data out of each column and assign it to local variables like this:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    <span data-ttu-id="a39a0-331">在窗体标记中，这些值则会自动显示在单个文本框中通过使用嵌入的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="a39a0-331">In the markup for the form, these values are displayed automatically in individual text boxes by using embedded code like the following:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    <span data-ttu-id="a39a0-332">该代码的一部分显示要更新的产品记录。</span><span class="sxs-lookup"><span data-stu-id="a39a0-332">That part of the code displays the product record to be updated.</span></span> <span data-ttu-id="a39a0-333">一旦已显示该记录，用户可以编辑单个列。</span><span class="sxs-lookup"><span data-stu-id="a39a0-333">Once the record has been displayed, the user can edit individual columns.</span></span>

    <span data-ttu-id="a39a0-334">当用户通过单击提交窗体**更新**按钮中的代码`if(IsPost)`块将运行。</span><span class="sxs-lookup"><span data-stu-id="a39a0-334">When the user submits the form by clicking the **Update** button, the code in the `if(IsPost)` block runs.</span></span> <span data-ttu-id="a39a0-335">这将获取用户的值从`Request`对象，将值存储在变量，并验证每个列已填写。</span><span class="sxs-lookup"><span data-stu-id="a39a0-335">This gets the user's values from the `Request` object, stores the values in variables, and validates that each column has been filled in.</span></span> <span data-ttu-id="a39a0-336">如果通过验证，该代码将创建以下 SQL Update 语句：</span><span class="sxs-lookup"><span data-stu-id="a39a0-336">If validation passes, the code creates the following SQL Update statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    <span data-ttu-id="a39a0-337">在 SQL`Update`语句，您可以指定更新和的值将它设置为每个列。</span><span class="sxs-lookup"><span data-stu-id="a39a0-337">In a SQL `Update` statement, you specify each column to update and the value to set it to.</span></span> <span data-ttu-id="a39a0-338">在此代码中，使用参数占位符指定的值`@0`， `@1`， `@2`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="a39a0-338">In this code, the values are specified using the parameter placeholders `@0`, `@1`, `@2`, and so on.</span></span> <span data-ttu-id="a39a0-339">（如前文所述，为安全起见，你应始终将值传递给 SQL 语句中使用的参数。）</span><span class="sxs-lookup"><span data-stu-id="a39a0-339">(As noted earlier, for security, you should always pass values to a SQL statement by using parameters.)</span></span>

    <span data-ttu-id="a39a0-340">当调用`db.Execute`方法，将变量传递包含对应于 SQL 语句中的参数的顺序中的值：</span><span class="sxs-lookup"><span data-stu-id="a39a0-340">When you call the `db.Execute` method, you pass the variables that contain the values in the order that corresponds to the parameters in the SQL statement:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    <span data-ttu-id="a39a0-341">后`Update`执行语句，以便将用户重定向回编辑页调用以下方法：</span><span class="sxs-lookup"><span data-stu-id="a39a0-341">After the `Update` statement has been executed, you call the following method in order to redirect the user back to the edit page:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    <span data-ttu-id="a39a0-342">其效果是用户将数据库中的数据的更新的列表，并且可以编辑另一种产品。</span><span class="sxs-lookup"><span data-stu-id="a39a0-342">The effect is that the user sees an updated listing of the data in the database and can edit another product.</span></span>
6. <span data-ttu-id="a39a0-343">保存页。</span><span class="sxs-lookup"><span data-stu-id="a39a0-343">Save the page.</span></span>
7. <span data-ttu-id="a39a0-344">运行*EditProducts.cshtml*页 （不是在更新页面），然后单击**编辑**以选择要编辑的产品。</span><span class="sxs-lookup"><span data-stu-id="a39a0-344">Run the *EditProducts.cshtml* page (not the update page) and then click **Edit** to select a product to edit.</span></span> <span data-ttu-id="a39a0-345">*UpdateProducts.cshtml*页面显示时，显示你选择的记录。</span><span class="sxs-lookup"><span data-stu-id="a39a0-345">The *UpdateProducts.cshtml* page is displayed, showing the record you selected.</span></span>

    ![[image]](5-working-with-data/_static/image8.jpg)
8. <span data-ttu-id="a39a0-347">进行更改，然后单击**更新**。</span><span class="sxs-lookup"><span data-stu-id="a39a0-347">Make a change and click **Update**.</span></span> <span data-ttu-id="a39a0-348">使用更新的数据，则需再次显示产品列表文件。</span><span class="sxs-lookup"><span data-stu-id="a39a0-348">The products list is shown again with your updated data.</span></span>

## <a name="deleting-data-in-a-database"></a><span data-ttu-id="a39a0-349">删除数据库中的数据</span><span class="sxs-lookup"><span data-stu-id="a39a0-349">Deleting Data in a Database</span></span>

<span data-ttu-id="a39a0-350">本部分演示如何使用户可以删除从产品*产品*数据库表。</span><span class="sxs-lookup"><span data-stu-id="a39a0-350">This section shows how to let users delete a product from the *Product* database table.</span></span> <span data-ttu-id="a39a0-351">此示例由两个页组成。</span><span class="sxs-lookup"><span data-stu-id="a39a0-351">The example consists of two pages.</span></span> <span data-ttu-id="a39a0-352">在第一页中，用户选择要删除的记录。</span><span class="sxs-lookup"><span data-stu-id="a39a0-352">In the first page, users select a record to delete.</span></span> <span data-ttu-id="a39a0-353">要删除的记录随后显示在第二页，以便确认他们想要删除的记录。</span><span class="sxs-lookup"><span data-stu-id="a39a0-353">The record to be deleted is then displayed in a second page that lets them confirm that they want to delete the record.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a39a0-354">**重要**在生产网站中，你通常限制允许哪些人具有对数据进行更改。</span><span class="sxs-lookup"><span data-stu-id="a39a0-354">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="a39a0-355">有关如何将成员资格设置以及方式来授予用户在站点上执行任务的信息，请参阅[添加安全和 ASP.NET Web Pages 站点的成员资格](https://go.microsoft.com/fwlink/?LinkId=202904)。</span><span class="sxs-lookup"><span data-stu-id="a39a0-355">For information about how to set up membership and about ways to authorize user to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>


1. <span data-ttu-id="a39a0-356">在网站中，创建一个名为的新 CSHTML 文件*ListProductsForDelete.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a39a0-356">In the website, create a new CSHTML file named *ListProductsForDelete.cshtml*.</span></span>
2. <span data-ttu-id="a39a0-357">现有的标记替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="a39a0-357">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    <span data-ttu-id="a39a0-358">此页是类似于*EditProducts.cshtml*从前面的页。</span><span class="sxs-lookup"><span data-stu-id="a39a0-358">This page is similar to the *EditProducts.cshtml* page from earlier.</span></span> <span data-ttu-id="a39a0-359">但是，而不是显示**编辑**链接为每个产品，它显示**删除**链接。</span><span class="sxs-lookup"><span data-stu-id="a39a0-359">However, instead of displaying an **Edit** link for each product, it displays a **Delete** link.</span></span> <span data-ttu-id="a39a0-360">**删除**标记中使用下面的嵌入的代码创建链接：</span><span class="sxs-lookup"><span data-stu-id="a39a0-360">The **Delete** link is created using the following embedded code in the markup:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    <span data-ttu-id="a39a0-361">这将创建如下所示，当用户单击此链接的 URL:</span><span class="sxs-lookup"><span data-stu-id="a39a0-361">This creates a URL that looks like this when users click the link:</span></span>

    `http://<server>/DeleteProduct/4`

    <span data-ttu-id="a39a0-362">URL 调用一个名为页*DeleteProduct.cshtml* （这将在下一步创建） 并将其传递要删除的产品 ID （此处，4）。</span><span class="sxs-lookup"><span data-stu-id="a39a0-362">The URL calls a page named *DeleteProduct.cshtml* (which you'll create next) and passes it the ID of the product to delete (here, 4).</span></span>
3. <span data-ttu-id="a39a0-363">保存该文件，但使它保持打开状态。</span><span class="sxs-lookup"><span data-stu-id="a39a0-363">Save the file, but leave it open.</span></span>
4. <span data-ttu-id="a39a0-364">创建名为的另一个 CHTML 文件*DeleteProduct.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a39a0-364">Create another CHTML file named *DeleteProduct.cshtml*.</span></span> <span data-ttu-id="a39a0-365">将现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="a39a0-365">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    <span data-ttu-id="a39a0-366">此页由*ListProductsForDelete.cshtml*并允许用户确认他们想要删除产品。</span><span class="sxs-lookup"><span data-stu-id="a39a0-366">This page is called by *ListProductsForDelete.cshtml* and lets users confirm that they want to delete a product.</span></span> <span data-ttu-id="a39a0-367">若要列出要删除的产品，可以从 URL 中删除该产品的 ID 使用下面的代码：</span><span class="sxs-lookup"><span data-stu-id="a39a0-367">To list the product to be deleted, you get the ID of the product to delete from the URL using the following code:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    <span data-ttu-id="a39a0-368">然后，页会询问用户单击一个按钮以实际删除的记录。</span><span class="sxs-lookup"><span data-stu-id="a39a0-368">The page then asks the user to click a button to actually delete the record.</span></span> <span data-ttu-id="a39a0-369">这是一项重要的安全措施： 当在更新或删除数据等网站执行敏感的操作，应始终执行这些操作使用 POST 操作，而不是 GET 操作。</span><span class="sxs-lookup"><span data-stu-id="a39a0-369">This is an important security measure: when you perform sensitive operations in your website like updating or deleting data, these operations should always be done using a POST operation, not a GET operation.</span></span> <span data-ttu-id="a39a0-370">如果你的站点设置，以便可以使用 GET 操作执行删除操作，任何人都可以传递的 URL，如`http://<server>/DeleteProduct/4`和从数据库中删除任何操作。</span><span class="sxs-lookup"><span data-stu-id="a39a0-370">If your site is set up so that a delete operation can be performed using a GET operation, anyone can pass a URL like `http://<server>/DeleteProduct/4` and delete anything they want from your database.</span></span> <span data-ttu-id="a39a0-371">通过添加确认和编码页，以便可以只能通过使用 POST 执行删除，向网站添加安全的措施。</span><span class="sxs-lookup"><span data-stu-id="a39a0-371">By adding the confirmation and coding the page so that the deletion can be performed only by using a POST, you add a measure of security to your site.</span></span>

    <span data-ttu-id="a39a0-372">使用以下代码，以首先确认这是 post 操作 ID 不为空来执行实际的删除操作：</span><span class="sxs-lookup"><span data-stu-id="a39a0-372">The actual delete operation is performed using the following code, which first confirms that this is a post operation and that the ID isn't empty:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    <span data-ttu-id="a39a0-373">代码将运行 SQL 语句中删除指定的记录，然后将用户重定向回列表页。</span><span class="sxs-lookup"><span data-stu-id="a39a0-373">The code runs a SQL statement that deletes the specified record and then redirects the user back to the listing page.</span></span>
5. <span data-ttu-id="a39a0-374">运行*ListProductsForDelete.cshtml*在浏览器。</span><span class="sxs-lookup"><span data-stu-id="a39a0-374">Run *ListProductsForDelete.cshtml* in a browser.</span></span>

    ![[image]](5-working-with-data/_static/image9.jpg)
6. <span data-ttu-id="a39a0-376">单击**删除**链接，获取的产品之一。</span><span class="sxs-lookup"><span data-stu-id="a39a0-376">Click the **Delete** link for one of the products.</span></span> <span data-ttu-id="a39a0-377">*DeleteProduct.cshtml*显示页以确认你想要删除该记录。</span><span class="sxs-lookup"><span data-stu-id="a39a0-377">The *DeleteProduct.cshtml* page is displayed to confirm that you want to delete that record.</span></span>
7. <span data-ttu-id="a39a0-378">单击**删除**按钮。</span><span class="sxs-lookup"><span data-stu-id="a39a0-378">Click the **Delete** button.</span></span> <span data-ttu-id="a39a0-379">删除该产品记录，并使用更新的产品列表刷新页面。</span><span class="sxs-lookup"><span data-stu-id="a39a0-379">The product record is deleted and the page is refreshed with an updated product listing.</span></span>

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a><span data-ttu-id="a39a0-380">连接到数据库</span><span class="sxs-lookup"><span data-stu-id="a39a0-380">Connecting to a Database</span></span>
> 
> <span data-ttu-id="a39a0-381">你可以连接到两种方法中的数据库。</span><span class="sxs-lookup"><span data-stu-id="a39a0-381">You can connect to a database in two ways.</span></span> <span data-ttu-id="a39a0-382">第一种是使用`Database.Open`方法并指定数据库文件的名称 (较少*.sdf*扩展):</span><span class="sxs-lookup"><span data-stu-id="a39a0-382">The first is to use the `Database.Open` method and to specify the name of the database file (less the *.sdf* extension):</span></span>
> 
> `var db = Database.Open("SmallBakery");`
> 
> <span data-ttu-id="a39a0-383">`Open`方法假设。*sdf*文件是在网站的*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="a39a0-383">The `Open` method assumes that the .*sdf* file is in the website's *App\_Data* folder.</span></span> <span data-ttu-id="a39a0-384">此文件夹被专为保存数据。</span><span class="sxs-lookup"><span data-stu-id="a39a0-384">This folder is designed specifically for holding data.</span></span> <span data-ttu-id="a39a0-385">例如，它具有适当的权限以允许网站以读取和写入数据，以及作为一种安全措施，WebMatrix 不允许访问到文件从该文件夹。</span><span class="sxs-lookup"><span data-stu-id="a39a0-385">For example, it has appropriate permissions to allow the website to read and write data, and as a security measure, WebMatrix does not allow access to files from this folder.</span></span>
> 
> <span data-ttu-id="a39a0-386">第二种方法是使用连接字符串。</span><span class="sxs-lookup"><span data-stu-id="a39a0-386">The second way is to use a connection string.</span></span> <span data-ttu-id="a39a0-387">连接字符串包含有关如何连接到数据库的信息。</span><span class="sxs-lookup"><span data-stu-id="a39a0-387">A connection string contains information about how to connect to a database.</span></span> <span data-ttu-id="a39a0-388">这可以包括文件路径，也可以包括本地或远程服务器，以及用户名和密码以连接到该服务器上的 SQL Server 数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="a39a0-388">This can include a file path, or it can include the name of a SQL Server database on a local or remote server, along with a user name and password to connect to that server.</span></span> <span data-ttu-id="a39a0-389">（如果你在集中管理版本的 SQL Server 中保留数据，例如在托管提供商的网站上，则始终使用连接字符串来指定数据库连接信息。）</span><span class="sxs-lookup"><span data-stu-id="a39a0-389">(If you keep data in a centrally managed version of SQL Server, such as on a hosting provider's site, you always use a connection string to specify the database connection information.)</span></span>
> 
> <span data-ttu-id="a39a0-390">在 WebMatrix 中，连接字符串通常存储在名为 XML 文件*Web.config*。顾名思义，你可以使用*Web.config*你的网站以存储站点的配置信息，包括你的站点可能需要的任意连接字符串的根目录中的文件。</span><span class="sxs-lookup"><span data-stu-id="a39a0-390">In WebMatrix, connection strings are usually stored in an XML file named *Web.config*. As the name implies, you can use a *Web.config* file in the root of your website to store the site's configuration information, including any connection strings that your site might require.</span></span> <span data-ttu-id="a39a0-391">中的连接字符串的示例*Web.config*文件可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="a39a0-391">An example of a connection string in a *Web.config* file might look like the following:</span></span>
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> <span data-ttu-id="a39a0-392">在示例中，连接字符串指向的某处的服务器运行的 SQL Server 实例中的数据库 (而不是本地*.sdf*文件)。</span><span class="sxs-lookup"><span data-stu-id="a39a0-392">In the example, the connection string points to a database in an instance of SQL Server that's running on a server somewhere (as opposed to a local *.sdf* file).</span></span> <span data-ttu-id="a39a0-393">你将需要进行替换为相应的名称`myServer`和`myDatabase`，并指定 SQL Server 登录名值`username`和`password`。</span><span class="sxs-lookup"><span data-stu-id="a39a0-393">You would need to substitute the appropriate names for `myServer` and `myDatabase`, and specify SQL Server login values for `username` and `password`.</span></span> <span data-ttu-id="a39a0-394">（用户名和密码值不一定是相同作为您的 Windows 凭据或你托管提供商已授予你用于登录到其服务器的值。</span><span class="sxs-lookup"><span data-stu-id="a39a0-394">(The username and password values are not necessarily the same as your Windows credentials or as the values that your hosting provider has given you for logging in to their servers.</span></span> <span data-ttu-id="a39a0-395">与管理员一起检查所需的确切值。）</span><span class="sxs-lookup"><span data-stu-id="a39a0-395">Check with the administrator for the exact values you need.)</span></span>
> 
> <span data-ttu-id="a39a0-396">`Database.Open`方法非常灵活，因为它允许您将数据库名称传递*.sdf*文件或存储在连接字符串的名称*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="a39a0-396">The `Database.Open` method is flexible, because it lets you pass either the name of a database *.sdf* file or the name of a connection string that's stored in the *Web.config* file.</span></span> <span data-ttu-id="a39a0-397">下面的示例演示如何使用连接到数据库的连接字符串，在前面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="a39a0-397">The following example shows how to connect to the database using the connection string illustrated in the previous example:</span></span>
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> <span data-ttu-id="a39a0-398">如前所述，`Database.Open`方法使你可以将数据库名称或连接字符串，传递和它将找出使用哪一个。</span><span class="sxs-lookup"><span data-stu-id="a39a0-398">As noted, the `Database.Open` method lets you pass either a database name or a connection string, and it'll figure out which to use.</span></span> <span data-ttu-id="a39a0-399">在部署时，这是非常有用 （发布） 网站。</span><span class="sxs-lookup"><span data-stu-id="a39a0-399">This is very useful when you deploy (publish) your website.</span></span> <span data-ttu-id="a39a0-400">你可以使用*.sdf*文件中*应用\_数据*文件夹时你开发和测试你的站点。</span><span class="sxs-lookup"><span data-stu-id="a39a0-400">You can use an *.sdf* file in the *App\_Data* folder when you're developing and testing your site.</span></span> <span data-ttu-id="a39a0-401">然后，将你的站点移到生产服务器时，可以使用中的连接字符串*Web.config*具有同名的文件您*.sdf*文件，但该点添加到托管提供商的数据库&#8212;所有而无需更改代码。</span><span class="sxs-lookup"><span data-stu-id="a39a0-401">Then when you move your site to a production server, you can use a connection string in the *Web.config* file that has the same name as your *.sdf* file but that points to the hosting provider's database &#8212; all without having to change your code.</span></span>
> 
> <span data-ttu-id="a39a0-402">最后，如果你想要直接使用连接字符串，则可以调用`Database.OpenConnectionString`方法并传入该实际的连接字符串而不只在中的名称，它*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="a39a0-402">Finally, if you want to work directly with a connection string, you can call the `Database.OpenConnectionString` method and pass it the actual connection string instead of just the name of one in the *Web.config* file.</span></span> <span data-ttu-id="a39a0-403">这可能会在其中出于某种原因不具备访问权限的连接字符串的情况下很有用 (或值，例如*.sdf*文件名称) 之前运行页面。</span><span class="sxs-lookup"><span data-stu-id="a39a0-403">This might be useful in situations where for some reason you don't have access to the connection string (or values in it, such as the *.sdf* file name) until the page is running.</span></span> <span data-ttu-id="a39a0-404">但是，对于大多数情况下，你可以使用`Database.Open`这篇文章中所述。</span><span class="sxs-lookup"><span data-stu-id="a39a0-404">However, for most scenarios, you can use `Database.Open` as described in this article.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a39a0-405">其他资源</span><span class="sxs-lookup"><span data-stu-id="a39a0-405">Additional Resources</span></span>

- [<span data-ttu-id="a39a0-406">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="a39a0-406">SQL Server Compact</span></span>](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [<span data-ttu-id="a39a0-407">连接到 SQL Server 或 MySQL 数据库在 WebMatrix 中</span><span class="sxs-lookup"><span data-stu-id="a39a0-407">Connecting to a SQL Server or MySQL Database in WebMatrix</span></span>](https://go.microsoft.com/fwlink/?LinkId=208661)
- [<span data-ttu-id="a39a0-408">在 ASP.NET 网站中验证用户输入</span><span class="sxs-lookup"><span data-stu-id="a39a0-408">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
