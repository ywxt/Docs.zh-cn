---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: 引入的 ASP.NET Web Pages-显示数据 |Microsoft 文档
author: tfitzmac
description: 本教程演示了如何在 WebMatrix 中创建数据库以及如何使用 ASP.NET Web 页 (Razor) 时，在页中显示数据库数据。 它假定 y...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: 6c66e5fb0a1a49da411286e19c7954f83055c3fd
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="introducing-aspnet-web-pages---displaying-data"></a><span data-ttu-id="b38c2-104">引入了 ASP.NET Web 页的显示数据</span><span class="sxs-lookup"><span data-stu-id="b38c2-104">Introducing ASP.NET Web Pages - Displaying Data</span></span>
====================
<span data-ttu-id="b38c2-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b38c2-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b38c2-106">本教程演示了如何在 WebMatrix 中创建数据库以及如何使用 ASP.NET Web 页 (Razor) 时，在页中显示数据库数据。</span><span class="sxs-lookup"><span data-stu-id="b38c2-106">This tutorial shows you how to create a database in WebMatrix and how to display database data in a page when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="b38c2-107">它假定你已完成通过系列[为 ASP.NET 网页编程的介绍](../introducing-razor-syntax-c.md)。</span><span class="sxs-lookup"><span data-stu-id="b38c2-107">It assumes you have completed the series through [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md).</span></span>
> 
> <span data-ttu-id="b38c2-108">你将学习：</span><span class="sxs-lookup"><span data-stu-id="b38c2-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="b38c2-109">如何使用 WebMatrix 工具来创建数据库和数据库表。</span><span class="sxs-lookup"><span data-stu-id="b38c2-109">How to use WebMatrix tools to create a database and database tables.</span></span>
> - <span data-ttu-id="b38c2-110">如何使用 WebMatrix 工具将数据添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="b38c2-110">How to use WebMatrix tools to add data to a database.</span></span>
> - <span data-ttu-id="b38c2-111">如何在页上显示来自数据库的数据。</span><span class="sxs-lookup"><span data-stu-id="b38c2-111">How to display data from the database on a page.</span></span>
> - <span data-ttu-id="b38c2-112">如何运行 ASP.NET 网页中的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="b38c2-112">How to run SQL commands in ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="b38c2-113">如何自定义`WebGrid`帮助器以更改显示的数据并将添加分页和排序。</span><span class="sxs-lookup"><span data-stu-id="b38c2-113">How to customize the `WebGrid` helper to change the data display and to add paging and sorting.</span></span>
>   
> 
> <span data-ttu-id="b38c2-114">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="b38c2-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="b38c2-115">WebMatrix 数据库工具。</span><span class="sxs-lookup"><span data-stu-id="b38c2-115">WebMatrix database tools.</span></span>
> - <span data-ttu-id="b38c2-116">`WebGrid` 帮助器。</span><span class="sxs-lookup"><span data-stu-id="b38c2-116">`WebGrid` helper.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="b38c2-117">你将生成</span><span class="sxs-lookup"><span data-stu-id="b38c2-117">What You'll Build</span></span>

<span data-ttu-id="b38c2-118">在前面的教程，你已引入到 ASP.NET Web Pages (*.cshtml*文件)、 Razor 语法的基础知识和帮助器。</span><span class="sxs-lookup"><span data-stu-id="b38c2-118">In the previous tutorial, you were introduced to ASP.NET Web Pages (*.cshtml* files), to the basics of Razor syntax, and to helpers.</span></span> <span data-ttu-id="b38c2-119">在本教程中，你将开始创建的实际 web 应用程序将使用序列的其余部分。</span><span class="sxs-lookup"><span data-stu-id="b38c2-119">In this tutorial, you'll begin creating the actual web application that you'll use for the rest of the series.</span></span> <span data-ttu-id="b38c2-120">应用程序是一个简单的影片应用程序，你可以查看、 添加、 更改和删除电影有关的信息。</span><span class="sxs-lookup"><span data-stu-id="b38c2-120">The app is a simple movie application that lets you view, add, change, and delete information about movies.</span></span>

<span data-ttu-id="b38c2-121">完成本教程后，你将能够查看类似于此页的影片列表：</span><span class="sxs-lookup"><span data-stu-id="b38c2-121">When you're done with this tutorial, you'll be able to view a movie listing that looks like this page:</span></span>

![包含参数的 WebGrid 显示设置为 CSS 类名称](displaying-data/_static/image1.png)

<span data-ttu-id="b38c2-123">但是，若要开始，你必须创建数据库。</span><span class="sxs-lookup"><span data-stu-id="b38c2-123">But to begin, you have to create a database.</span></span>

## <a name="a-very-brief-introduction-to-databases"></a><span data-ttu-id="b38c2-124">对数据库的非常简短介绍</span><span class="sxs-lookup"><span data-stu-id="b38c2-124">A Very Brief Introduction to Databases</span></span>

<span data-ttu-id="b38c2-125">本教程将提供到数据库仅 briefest 的简介。</span><span class="sxs-lookup"><span data-stu-id="b38c2-125">This tutorial will provide only the briefest introduction to databases.</span></span> <span data-ttu-id="b38c2-126">如果你有数据库经验，则可以跳过此较短的节。</span><span class="sxs-lookup"><span data-stu-id="b38c2-126">If you have database experience, you can skip this short section.</span></span>

<span data-ttu-id="b38c2-127">数据库包含一个或多个表包含的信息&mdash;例如，表为客户、 订单和供应商或学生、 教师、 类和年级。</span><span class="sxs-lookup"><span data-stu-id="b38c2-127">A database contains one or more tables that contain information &mdash; for example, tables for customers, orders, and vendors, or for students, teachers, classes, and grades.</span></span> <span data-ttu-id="b38c2-128">在结构上，数据库表就像电子表格。</span><span class="sxs-lookup"><span data-stu-id="b38c2-128">Structurally, a database table is like a spreadsheet.</span></span> <span data-ttu-id="b38c2-129">假设一个典型的通讯簿。</span><span class="sxs-lookup"><span data-stu-id="b38c2-129">Imagine a typical address book.</span></span> <span data-ttu-id="b38c2-130">每个条目的通讯簿中 (即，每人) 具有以下几条如名字、 姓氏、 地址、 电子邮件地址和电话号码的信息。</span><span class="sxs-lookup"><span data-stu-id="b38c2-130">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

![为简单网格示例数据库表](displaying-data/_static/image2.png)

<span data-ttu-id="b38c2-132">(行有时称为*记录*，和列有时称为*字段*。)</span><span class="sxs-lookup"><span data-stu-id="b38c2-132">(Rows are sometimes referred to as *records*, and columns are sometimes referred to as *fields*.)</span></span>

<span data-ttu-id="b38c2-133">对于大多数数据库表，表必须有一列以包含一个唯一值，如客户编号、 帐户号，依次类推。</span><span class="sxs-lookup"><span data-stu-id="b38c2-133">For most database tables, the table has to have a column that contains a unique value, like a customer number, account number, and so on.</span></span> <span data-ttu-id="b38c2-134">此值称为表的*主键*，并使用它来标识表中的每个行。</span><span class="sxs-lookup"><span data-stu-id="b38c2-134">This value is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="b38c2-135">在示例中，ID 列是在前面的示例所示的通讯簿的主键。</span><span class="sxs-lookup"><span data-stu-id="b38c2-135">In the example, the ID column is the primary key for the address book shown in the previous example.</span></span>

<span data-ttu-id="b38c2-136">Web 应用程序中所做的工作大部分组成读取出数据库的信息以及在页面上显示它。</span><span class="sxs-lookup"><span data-stu-id="b38c2-136">Much of the work you do in web applications consists of reading information out of the database and displaying it on a page.</span></span> <span data-ttu-id="b38c2-137">你通常还将从用户收集信息并将其添加到数据库，或将修改已存在于数据库中的记录。</span><span class="sxs-lookup"><span data-stu-id="b38c2-137">You'll also often gather information from users and add it to a database, or you'll modify records that are already in the database.</span></span> <span data-ttu-id="b38c2-138">（我们将介绍所有这些操作在此教程的集的过程中。）</span><span class="sxs-lookup"><span data-stu-id="b38c2-138">(We'll cover all of these operations in the course of this tutorial set.)</span></span>

<span data-ttu-id="b38c2-139">数据库工作可以大大地复杂，可能需要专用的知识。</span><span class="sxs-lookup"><span data-stu-id="b38c2-139">Database work can be enormously complex and can require specialized knowledge.</span></span> <span data-ttu-id="b38c2-140">此教程的集，不过，您需要了解仅基本概念，这些概念将所有能解释根据自己的意愿。</span><span class="sxs-lookup"><span data-stu-id="b38c2-140">For this tutorial set, though, you have to understand only basic concepts, which will all be explained as you go.</span></span>

## <a name="creating-a-database"></a><span data-ttu-id="b38c2-141">创建数据库</span><span class="sxs-lookup"><span data-stu-id="b38c2-141">Creating a Database</span></span>

<span data-ttu-id="b38c2-142">WebMatrix 包含工具，可以轻松创建数据库，并在数据库中创建表。</span><span class="sxs-lookup"><span data-stu-id="b38c2-142">WebMatrix includes tools that make it easy to create a database and to create tables in the database.</span></span> <span data-ttu-id="b38c2-143">(数据库的结构称为数据库的*架构*。)此教程的集，你将创建在其中具有只有一个表的数据库&mdash;电影。</span><span class="sxs-lookup"><span data-stu-id="b38c2-143">(The structure of a database is referred to as the database's *schema*.) For this tutorial set, you'll create a database that has only one table in it &mdash; Movies.</span></span>

<span data-ttu-id="b38c2-144">打开 WebMatrix，如果尚未这样做并打开你在前面的教程中创建的 WebPagesMovies 站点。</span><span class="sxs-lookup"><span data-stu-id="b38c2-144">Open WebMatrix if you haven't already done so, and open the WebPagesMovies site that you created in the previous tutorial.</span></span>

<span data-ttu-id="b38c2-145">在左窗格中，单击**数据库**工作区。</span><span class="sxs-lookup"><span data-stu-id="b38c2-145">In the left pane, click the **Database** workspace.</span></span>

![WebMatrix 数据库工作区选项卡](displaying-data/_static/image3.png)

<span data-ttu-id="b38c2-147">功能区更改为显示与数据库相关的任务。</span><span class="sxs-lookup"><span data-stu-id="b38c2-147">The ribbon changes to show database-related tasks.</span></span> <span data-ttu-id="b38c2-148">在功能区中，单击**新数据库**。</span><span class="sxs-lookup"><span data-stu-id="b38c2-148">In the ribbon, click **New Database**.</span></span>

![在 WebMatrix 功能区的新数据库按钮](displaying-data/_static/image4.png)

<span data-ttu-id="b38c2-150">WebMatrix 创建 SQL Server CE 数据库 ( *.sdf*文件) 作为你的站点具有相同名称&mdash; *WebPagesMovies.sdf*。</span><span class="sxs-lookup"><span data-stu-id="b38c2-150">WebMatrix creates a SQL Server CE database (an *.sdf* file) that has the same name as your site &mdash; *WebPagesMovies.sdf*.</span></span> <span data-ttu-id="b38c2-151">(不会执行此操作在这里，但你可以将重命名该文件为您喜欢的任何，只要它具有*.sdf*扩展。)</span><span class="sxs-lookup"><span data-stu-id="b38c2-151">(You won't do this here, but you can rename the file to anything you like, as long as it has an *.sdf* extension.)</span></span>

## <a name="creating-a-table"></a><span data-ttu-id="b38c2-152">创建表</span><span class="sxs-lookup"><span data-stu-id="b38c2-152">Creating a Table</span></span>

<span data-ttu-id="b38c2-153">在功能区中，单击**新表**。</span><span class="sxs-lookup"><span data-stu-id="b38c2-153">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="b38c2-154">WebMatrix 将在新选项卡中打开表设计器。（如果新的表选项不可用，请确保在左侧树视图中选择新的数据库。）</span><span class="sxs-lookup"><span data-stu-id="b38c2-154">WebMatrix opens the table designer in a new tab. (If the New Table option isn't available, make sure that the new database is selected in the tree view on the left.)</span></span>

![在 WebMatrix 功能区的新表按钮](displaying-data/_static/image5.png)

<span data-ttu-id="b38c2-156">在顶部 （其中水印显示"输入表名称"） 的文本框，输入"电影"。</span><span class="sxs-lookup"><span data-stu-id="b38c2-156">In the text box at the top (where the watermark says "Enter table name"), enter "Movies".</span></span>

![在 WebMatrix 数据库设计器中输入一个表名](displaying-data/_static/image6.png)

<span data-ttu-id="b38c2-158">表名称下方窗格是你在其中定义单独的列。</span><span class="sxs-lookup"><span data-stu-id="b38c2-158">The pane underneath the table name is where you define individual columns.</span></span> <span data-ttu-id="b38c2-159">有关*电影*表在本教程中，你将创建仅少量的列： *ID*，*标题*，*流派*，和*年*.</span><span class="sxs-lookup"><span data-stu-id="b38c2-159">For the *Movies* table in this tutorial, you'll create only a few columns: *ID*, *Title*, *Genre*, and *Year*.</span></span>

<span data-ttu-id="b38c2-160">在**名称**框中，输入"ID"。</span><span class="sxs-lookup"><span data-stu-id="b38c2-160">In the **Name** box, enter "ID".</span></span> <span data-ttu-id="b38c2-161">输入一个值，则会激活的新列的所有控件。</span><span class="sxs-lookup"><span data-stu-id="b38c2-161">Entering a value here activates all the controls for the new column.</span></span>

<span data-ttu-id="b38c2-162">Tab 键移动到**数据类型**列表并选择**int**。此值指定 ID 列将包含整数 （数字） 数据。</span><span class="sxs-lookup"><span data-stu-id="b38c2-162">Tab to the **Data Type** list and choose **int**. This value specifies that the ID column will contain integer (number) data.</span></span>

> [!NOTE]
> <span data-ttu-id="b38c2-163">我们不会调出任何此处详细 （得多），但你可以使用标准的 Windows 键盘手势在此网格中进行导航。</span><span class="sxs-lookup"><span data-stu-id="b38c2-163">We won't call it out any more here (much), but you can use standard Windows keyboard gestures to navigate in this grid.</span></span> <span data-ttu-id="b38c2-164">例如，你可以使用 tab 键字段之间，就可以开始键入以便在列表中，选择一个项，依次类推。</span><span class="sxs-lookup"><span data-stu-id="b38c2-164">For example, you can tab between fields, you can just start typing in order to select an item in a list, and so on.</span></span>


<span data-ttu-id="b38c2-165">过去的选项卡上**默认值**框 （即，将其留空）。</span><span class="sxs-lookup"><span data-stu-id="b38c2-165">Tab past the **Default Value** box (that is, leave it blank).</span></span> <span data-ttu-id="b38c2-166">Tab 键移动到**是 Primary Key**复选框，然后选择它。</span><span class="sxs-lookup"><span data-stu-id="b38c2-166">Tab to the **Is Primary Key** check box and select it.</span></span> <span data-ttu-id="b38c2-167">此选项指示数据库*ID*列将包含标识单个行的数据。</span><span class="sxs-lookup"><span data-stu-id="b38c2-167">This option tells the database that the *ID* column will contain the data that identifies individual rows.</span></span> <span data-ttu-id="b38c2-168">（这就是，每一行将具有一个唯一的值可用来查找该行 ID 列中。）</span><span class="sxs-lookup"><span data-stu-id="b38c2-168">(That is, each row will have a unique value in the ID column that you can use to find that row.)</span></span>

<span data-ttu-id="b38c2-169">选择**是标识**选项。</span><span class="sxs-lookup"><span data-stu-id="b38c2-169">Choose the **Is Identity** option.</span></span> <span data-ttu-id="b38c2-170">此选项指示数据库，它应自动生成每个新行的下一个顺序编号。</span><span class="sxs-lookup"><span data-stu-id="b38c2-170">This option tells the database that it should automatically generate the next sequential number for each new row.</span></span> <span data-ttu-id="b38c2-171">(**是标识**选项仅当你已选择**是 Primary Key**选项。)</span><span class="sxs-lookup"><span data-stu-id="b38c2-171">(The **Is Identity** option works only if you've also selected the **Is Primary Key** option.)</span></span>

<span data-ttu-id="b38c2-172">在下一步的网格行中，单击或按 tab 键两次以完成当前行。</span><span class="sxs-lookup"><span data-stu-id="b38c2-172">Click in the next grid row, or press Tab twice to finish the current row.</span></span> <span data-ttu-id="b38c2-173">任一笔势保存当前行，并启动下一个。</span><span class="sxs-lookup"><span data-stu-id="b38c2-173">Either gesture saves the current row and starts the next one.</span></span> <span data-ttu-id="b38c2-174">请注意，**默认值**列现在显示**Null**。</span><span class="sxs-lookup"><span data-stu-id="b38c2-174">Notice that the **Default Value** column now says **Null**.</span></span> <span data-ttu-id="b38c2-175">（null 是默认值为默认值，这样说。）</span><span class="sxs-lookup"><span data-stu-id="b38c2-175">(Null is the default value for the default value, so to speak.)</span></span>

<span data-ttu-id="b38c2-176">当你已定义新**ID**列中，设计器将类似于此图中：</span><span class="sxs-lookup"><span data-stu-id="b38c2-176">When you've finished defining the new **ID** column, the designer will look like this illustration:</span></span>

![WebMatrix 定义电影表的 ID 列后的数据库设计器](displaying-data/_static/image7.png)

<span data-ttu-id="b38c2-178">若要创建下一列，请单击框中**名称**列。</span><span class="sxs-lookup"><span data-stu-id="b38c2-178">To create the next column, click in the box in the **Name** column.</span></span> <span data-ttu-id="b38c2-179">为列中输入"Title"，然后选择**nvarchar**为**数据类型**值。</span><span class="sxs-lookup"><span data-stu-id="b38c2-179">Enter "Title" for the column and then select **nvarchar** for the **Data Type** value.</span></span> <span data-ttu-id="b38c2-180">"Var"属于**nvarchar**告诉数据库此列的数据将为其大小可能有所不同记录之间的字符串。</span><span class="sxs-lookup"><span data-stu-id="b38c2-180">The "var" part of **nvarchar** tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="b38c2-181">("N"前缀表示"国家/地区，"指示字段可以包含任何字母或书写体系的字符数据-即，该字段将持有 Unicode 数据。)</span><span class="sxs-lookup"><span data-stu-id="b38c2-181">(The "n" prefix represents "national," which indicates that the field can hold character data for any alphabet or writing system — that is, the field holds Unicode data.)</span></span>

<span data-ttu-id="b38c2-182">当你选择**nvarchar**，另一个框中将出现，为该字段输入的最大长度。</span><span class="sxs-lookup"><span data-stu-id="b38c2-182">When you choose **nvarchar**, another box appears where you can enter the maximum length for the field.</span></span> <span data-ttu-id="b38c2-183">输入 50，假定您将在本教程中使用无影片标题将会超过 50 个字符。</span><span class="sxs-lookup"><span data-stu-id="b38c2-183">Enter 50, on the assumption that no movie title that you'll work with in this tutorial will be longer than 50 characters.</span></span>

<span data-ttu-id="b38c2-184">跳过**默认值**和清除**允许 null 值**选项。</span><span class="sxs-lookup"><span data-stu-id="b38c2-184">Skip **Default Value** and clear the **Allow Nulls** option.</span></span> <span data-ttu-id="b38c2-185">你不想要允许任何以输入到数据库过的电影没有标题的数据库。</span><span class="sxs-lookup"><span data-stu-id="b38c2-185">You don't want the database to allow any movies to be entered into the database that don't have a title.</span></span>

<span data-ttu-id="b38c2-186">当你完成此操作后，并移动到下一行时，设计器将类似于此图中：</span><span class="sxs-lookup"><span data-stu-id="b38c2-186">When you're done and move to the next row, the designer looks like this illustration:</span></span>

![WebMatrix 定义电影表的标题列后的数据库设计器](displaying-data/_static/image8.png)

<span data-ttu-id="b38c2-188">重复以下步骤创建一个名为除外长度的"Genre"列将其设置为只是 30。</span><span class="sxs-lookup"><span data-stu-id="b38c2-188">Repeat these steps to create a column named "Genre", except for the length, set it to just 30.</span></span>

<span data-ttu-id="b38c2-189">创建名为"Year。"的另一个列</span><span class="sxs-lookup"><span data-stu-id="b38c2-189">Create another column named "Year."</span></span> <span data-ttu-id="b38c2-190">对于数据类型中，选择**nchar** (不**nvarchar**) 并将长度设置为 4。</span><span class="sxs-lookup"><span data-stu-id="b38c2-190">For the data type, choose **nchar** (not **nvarchar**) and set the length to 4.</span></span> <span data-ttu-id="b38c2-191">年，你要使用 4 位数字，如"1995"或"2010"，因此不需要的大小可变的列。</span><span class="sxs-lookup"><span data-stu-id="b38c2-191">For the year, you're going to use a 4-digit number like "1995" or "2010", so you don't require a variable-sized column.</span></span>

<span data-ttu-id="b38c2-192">下面是已完成的设计如下所示：</span><span class="sxs-lookup"><span data-stu-id="b38c2-192">Here's what the finished design looks like:</span></span>

![WebMatrix 数据库设计器后为电影表定义的所有字段](displaying-data/_static/image9.png)

<span data-ttu-id="b38c2-194">按 Ctrl + S 或单击**保存**中快速访问工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="b38c2-194">Press Ctrl+S or click the **Save** button in the Quick Access toolbar.</span></span> <span data-ttu-id="b38c2-195">通过关闭选项卡来关闭数据库设计器。</span><span class="sxs-lookup"><span data-stu-id="b38c2-195">Close the database designer by closing the tab.</span></span>

## <a name="adding-some-example-data"></a><span data-ttu-id="b38c2-196">添加了一些示例数据</span><span class="sxs-lookup"><span data-stu-id="b38c2-196">Adding Some Example Data</span></span>

<span data-ttu-id="b38c2-197">稍后在本教程系列中，你将创建可以在窗体中输入新影片的页。</span><span class="sxs-lookup"><span data-stu-id="b38c2-197">Later in this tutorial series you'll create a page where you can enter new movies in a form.</span></span> <span data-ttu-id="b38c2-198">但是，现在，可以添加一些示例数据，然后可以显示在页面上。</span><span class="sxs-lookup"><span data-stu-id="b38c2-198">For now, however, you can add some example data that you can then display on a page.</span></span>

<span data-ttu-id="b38c2-199">在**数据库**在 WebMatrix 中，请注意，没有一个树，它显示你的工作区*.sdf*前面创建的文件。</span><span class="sxs-lookup"><span data-stu-id="b38c2-199">In the **Database** workspace in WebMatrix, notice that there's a tree that shows you the *.sdf* file you created earlier.</span></span> <span data-ttu-id="b38c2-200">打开新的节点*.sdf*文件中，并随后打开**表**节点。</span><span class="sxs-lookup"><span data-stu-id="b38c2-200">Open the node for your new *.sdf* file, and then open the **Tables** node.</span></span>

![目录树到电影表打开 WebMatrix 数据库工作区](displaying-data/_static/image10.png)

<span data-ttu-id="b38c2-202">右键单击**电影**节点，然后选择**数据**。</span><span class="sxs-lookup"><span data-stu-id="b38c2-202">Right-click the **Movies** node and then choose **Data**.</span></span> <span data-ttu-id="b38c2-203">WebMatrix 将打开一个网格，你可以在其中输入数据*电影*表：</span><span class="sxs-lookup"><span data-stu-id="b38c2-203">WebMatrix opens a grid where you can enter data for the *Movies* table:</span></span>

![在 WebMatrix 中 （空） 的数据库条目网格](displaying-data/_static/image11.png)

<span data-ttu-id="b38c2-205">单击**标题**列并输入"时 Harry 满足 Sally"。</span><span class="sxs-lookup"><span data-stu-id="b38c2-205">Click the **Title** column and enter "When Harry Met Sally".</span></span> <span data-ttu-id="b38c2-206">将移动到**流派**（你可以使用 Tab 键） 的列，然后输入"浪漫喜剧"。</span><span class="sxs-lookup"><span data-stu-id="b38c2-206">Move to the **Genre** column (you can use the Tab key) and enter "Romantic Comedy".</span></span> <span data-ttu-id="b38c2-207">将移动到**年**列并输入"1989":</span><span class="sxs-lookup"><span data-stu-id="b38c2-207">Move to the **Year** column and enter "1989":</span></span>

![在 WebMatrix 中使用一条记录的数据库条目网格](displaying-data/_static/image12.png)

<span data-ttu-id="b38c2-209">按 Enter 和 WebMatrix 将保存新的影片。</span><span class="sxs-lookup"><span data-stu-id="b38c2-209">Press Enter, and WebMatrix saves the new movie.</span></span> <span data-ttu-id="b38c2-210">请注意， **ID**填写列。</span><span class="sxs-lookup"><span data-stu-id="b38c2-210">Notice that the **ID** column has been filled in.</span></span>

![在 WebMatrix 中使用一条记录和自动生成的 ID 的数据库条目网格](displaying-data/_static/image13.png)

<span data-ttu-id="b38c2-212">输入另一电影 （例如，"进入与风暴"、"戏曲"，"1939"）。</span><span class="sxs-lookup"><span data-stu-id="b38c2-212">Enter another movie (for example, "Gone with the Wind", "Drama", "1939").</span></span> <span data-ttu-id="b38c2-213">再次填写 ID 列：</span><span class="sxs-lookup"><span data-stu-id="b38c2-213">The ID column is filled in again:</span></span>

![在 WebMatrix 中使用两条记录和自动生成 Id 的数据库条目网格](displaying-data/_static/image14.png)

<span data-ttu-id="b38c2-215">输入第三个影片 （例如，"Ghostbusters"、"喜剧"）。</span><span class="sxs-lookup"><span data-stu-id="b38c2-215">Enter a third movie (for example, "Ghostbusters", "Comedy").</span></span> <span data-ttu-id="b38c2-216">作为试验，使**年**列留空，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="b38c2-216">As an experiment, leave the **Year** column blank and then press Enter.</span></span> <span data-ttu-id="b38c2-217">因为你未选定的**允许 null 值**选项，数据库将显示错误：</span><span class="sxs-lookup"><span data-stu-id="b38c2-217">Because you unselected the **Allow Nulls** option, the database shows an error:</span></span>

![如果所需的列的值为空，将显示无效的数据错误](displaying-data/_static/image15.png)

<span data-ttu-id="b38c2-219">单击**确定**以返回并修复 （"Ghostbusters"的年份是 1984年） 的条目，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="b38c2-219">Click **OK** to go back and fix the entry (the year for "Ghostbusters" is 1984), and then press Enter.</span></span>

<span data-ttu-id="b38c2-220">填写几个电影，直到有 8 或以便。</span><span class="sxs-lookup"><span data-stu-id="b38c2-220">Fill in several movies until you have 8 or so.</span></span> <span data-ttu-id="b38c2-221">（输入 8 便于更轻松地使用分页更高版本。</span><span class="sxs-lookup"><span data-stu-id="b38c2-221">(Entering 8 makes it easier to work with paging later.</span></span> <span data-ttu-id="b38c2-222">但如果是太多，输入只是几个现在。）实际数据并不重要。</span><span class="sxs-lookup"><span data-stu-id="b38c2-222">But if that's too many, enter just a few for now.) The actual data doesn't matter.</span></span>

![在 WebMatrix 中包含的任一记录的数据库条目网格](displaying-data/_static/image16.png)

<span data-ttu-id="b38c2-224">如果输入未出现任何错误的所有影片，ID 值是连续的。</span><span class="sxs-lookup"><span data-stu-id="b38c2-224">If you entered all the movies without any errors, the ID values are sequential.</span></span> <span data-ttu-id="b38c2-225">如果尝试保存一个不完整的电影记录，可能不是连续的 ID 号。</span><span class="sxs-lookup"><span data-stu-id="b38c2-225">If you tried to save an incomplete movie record, the ID numbers might not be sequential.</span></span> <span data-ttu-id="b38c2-226">如果是这样，没关系。</span><span class="sxs-lookup"><span data-stu-id="b38c2-226">If so, that's okay.</span></span> <span data-ttu-id="b38c2-227">数字没有任何固有的含义，又是重要的唯一操作是它们在中唯一*电影*表。</span><span class="sxs-lookup"><span data-stu-id="b38c2-227">The numbers don't have any inherent meaning, and the only thing that's important is that they're unique in the *Movies* table.</span></span>

<span data-ttu-id="b38c2-228">关闭包含数据库设计器的选项卡。</span><span class="sxs-lookup"><span data-stu-id="b38c2-228">Close the tab that contains the database designer.</span></span>

<span data-ttu-id="b38c2-229">现在你可以启用在网页上显示此数据。</span><span class="sxs-lookup"><span data-stu-id="b38c2-229">Now you can turn to displaying this data on a web page.</span></span>

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a><span data-ttu-id="b38c2-230">通过使用 WebGrid 帮助器在页上显示数据</span><span class="sxs-lookup"><span data-stu-id="b38c2-230">Displaying Data in a Page by Using the WebGrid Helper</span></span>

<span data-ttu-id="b38c2-231">若要在页中显示数据，你将使用`WebGrid`帮助器。</span><span class="sxs-lookup"><span data-stu-id="b38c2-231">To display data in a page, you're going to use the `WebGrid` helper.</span></span> <span data-ttu-id="b38c2-232">此帮助器生成的网格或表 （行和列） 中显示。</span><span class="sxs-lookup"><span data-stu-id="b38c2-232">This helper produces a display in a grid or table (rows and columns).</span></span> <span data-ttu-id="b38c2-233">如你所见，你将能够调整网格与格式设置和其他功能。</span><span class="sxs-lookup"><span data-stu-id="b38c2-233">As you'll see, you'll be able refine the grid with formatting and other features.</span></span>

<span data-ttu-id="b38c2-234">若要运行网格，你将需要编写几行代码。</span><span class="sxs-lookup"><span data-stu-id="b38c2-234">To run the grid, you'll have to write a few lines of code.</span></span> <span data-ttu-id="b38c2-235">以下几行将充当一种类型的几乎所有在本教程中执行的数据访问模式。</span><span class="sxs-lookup"><span data-stu-id="b38c2-235">These few lines will serve as a kind of pattern for almost all of the data access that you do in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="b38c2-236">实际上有许多选项在页上显示数据`WebGrid`帮助器只是其中一个。</span><span class="sxs-lookup"><span data-stu-id="b38c2-236">You actually have many options for displaying data on a page; the `WebGrid` helper is just one.</span></span> <span data-ttu-id="b38c2-237">我们选择它本教程中，因为它显示数据的最简单方法并且因为它是相当灵活。</span><span class="sxs-lookup"><span data-stu-id="b38c2-237">We chose it for this tutorial because it's the easiest way to display data and because it's reasonably flexible.</span></span> <span data-ttu-id="b38c2-238">在下一步教程组中，你将了解如何使用详细的"手动"方式处理在页中，这为你提供更直接控制如何显示数据的数据。</span><span class="sxs-lookup"><span data-stu-id="b38c2-238">In the next tutorial set, you'll see how to use a more "manual" way to work with data in the page, which gives you more direct control over how to display the data.</span></span>


<span data-ttu-id="b38c2-239">在 WebMatrix 中左窗格中，单击**文件**工作区。</span><span class="sxs-lookup"><span data-stu-id="b38c2-239">In the left pane in WebMatrix, click the **Files** workspace.</span></span>

<span data-ttu-id="b38c2-240">你创建的新数据库处于*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="b38c2-240">The new database you created is in the *App\_Data* folder.</span></span> <span data-ttu-id="b38c2-241">如果文件夹尚不存在，WebMatrix 将创建它为新的数据库。</span><span class="sxs-lookup"><span data-stu-id="b38c2-241">If the folder didn't already exist, WebMatrix created it for your new database.</span></span> <span data-ttu-id="b38c2-242">（文件夹可能已存在如果以前已安装了帮助器。）</span><span class="sxs-lookup"><span data-stu-id="b38c2-242">(The folder might have existed if you'd previously installed helpers.)</span></span>

<span data-ttu-id="b38c2-243">在树视图中，选择在网站的根目录。</span><span class="sxs-lookup"><span data-stu-id="b38c2-243">In the tree view, select the root of the website.</span></span> <span data-ttu-id="b38c2-244">您必须选择网站; 的根目录否则，可能会向应用添加新文件\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="b38c2-244">You must select the root of the website; otherwise, the new file might be added to the App\_Data folder.</span></span>

<span data-ttu-id="b38c2-245">在功能区中，单击**新建**。</span><span class="sxs-lookup"><span data-stu-id="b38c2-245">In the ribbon, click **New**.</span></span> <span data-ttu-id="b38c2-246">在**选择文件类型**框中，选择**CSHTML**。</span><span class="sxs-lookup"><span data-stu-id="b38c2-246">In the **Choose a File Type** box, choose **CSHTML**.</span></span>

<span data-ttu-id="b38c2-247">在**名称**框中，将新该页"Movies.cshtml":</span><span class="sxs-lookup"><span data-stu-id="b38c2-247">In the **Name** box, name the new page "Movies.cshtml":</span></span>

![选择文件类型对话框中显示电影页](displaying-data/_static/image17.png)

<span data-ttu-id="b38c2-249">单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="b38c2-249">Click the **OK** button.</span></span> <span data-ttu-id="b38c2-250">WebMatrix 打开具有在其中一些主干元素的新文件。</span><span class="sxs-lookup"><span data-stu-id="b38c2-250">WebMatrix opens a new file with some skeleton elements in it.</span></span> <span data-ttu-id="b38c2-251">首先，你将编写一些代码，可从数据库中获取数据。</span><span class="sxs-lookup"><span data-stu-id="b38c2-251">First you'll write some code to go get the data from the database.</span></span> <span data-ttu-id="b38c2-252">然后你将添加到页后，可以实际显示数据的标记。</span><span class="sxs-lookup"><span data-stu-id="b38c2-252">Then you'll add markup to the page to actually display the data.</span></span>

### <a name="writing-the-data-query-code"></a><span data-ttu-id="b38c2-253">编写数据查询代码</span><span class="sxs-lookup"><span data-stu-id="b38c2-253">Writing the Data Query Code</span></span>

<span data-ttu-id="b38c2-254">在页上，顶部之间`@{`和`}`字符，输入下面的代码。</span><span class="sxs-lookup"><span data-stu-id="b38c2-254">At the top of the page, between the `@{` and `}` characters, enter the following code.</span></span> <span data-ttu-id="b38c2-255">（请确保你输入此代码，开始标记和右大括号之间。）</span><span class="sxs-lookup"><span data-stu-id="b38c2-255">(Make sure that you enter this code between the opening and closing braces.)</span></span>

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

<span data-ttu-id="b38c2-256">第一行将打开更早版本，创建的数据库，这是始终第一个步骤之前执行某项与数据库。</span><span class="sxs-lookup"><span data-stu-id="b38c2-256">The first line opens the database that you created earlier, which is always the first step before doing something with the database.</span></span> <span data-ttu-id="b38c2-257">你判断`Database.Open`要打开的数据库的方法名称。</span><span class="sxs-lookup"><span data-stu-id="b38c2-257">You tell the `Database.Open` method name of the database to open.</span></span> <span data-ttu-id="b38c2-258">请注意，不包含*.sdf*名称中。</span><span class="sxs-lookup"><span data-stu-id="b38c2-258">Notice that you don't include *.sdf* in the name.</span></span> <span data-ttu-id="b38c2-259">`Open`方法假设它正在寻找*.sdf*文件 (即， *WebPagesMovies.sdf*) 并且*.sdf*文件位于*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="b38c2-259">The `Open` method assumes that it's looking for an *.sdf* file (that is, *WebPagesMovies.sdf*) and that the *.sdf* file is in the *App\_Data* folder.</span></span> <span data-ttu-id="b38c2-260">(前面我们注意到，*应用\_数据*保留文件夹; 这种情况下是 ASP.NET 其中假定该名称的位置之一。)</span><span class="sxs-lookup"><span data-stu-id="b38c2-260">(Earlier we noted that the *App\_Data* folder is reserved; this scenario is one of the places where ASP.NET makes assumptions about that name.)</span></span>

<span data-ttu-id="b38c2-261">当打开该数据库时，对它的引用被放置到命名的变量`db`。</span><span class="sxs-lookup"><span data-stu-id="b38c2-261">When the database is opened, a reference to it is put into the variable named `db`.</span></span> <span data-ttu-id="b38c2-262">（这可以命名为任何内容。）`db`变量是如何将显示与数据库交互。</span><span class="sxs-lookup"><span data-stu-id="b38c2-262">(Which could be named anything.) The `db` variable is how you'll end up interacting with the database.</span></span>

<span data-ttu-id="b38c2-263">第二行实际上会获取数据库数据，通过使用`Query`方法。</span><span class="sxs-lookup"><span data-stu-id="b38c2-263">The second line actually fetches the database data by using the `Query` method.</span></span> <span data-ttu-id="b38c2-264">请注意此代码的工作原理：`db`变量具有对打开的数据库的引用和调用`Query`方法通过使用使用`db`变量 (`db.Query`)。</span><span class="sxs-lookup"><span data-stu-id="b38c2-264">Notice how this code works: the `db` variable has a reference to the opened database, and you invoke the `Query` method by using the `db` variable (`db.Query`).</span></span>

<span data-ttu-id="b38c2-265">查询本身是一个 SQL`Select`语句。</span><span class="sxs-lookup"><span data-stu-id="b38c2-265">The query itself is a SQL `Select` statement.</span></span> <span data-ttu-id="b38c2-266">（有关少量 SQL 有关背景信息，请参阅说明更高版本）。在语句中，`Movies`标识要查询表。</span><span class="sxs-lookup"><span data-stu-id="b38c2-266">(For a little background about SQL, see the explanation later.) In the statement, `Movies` identifies the table to query.</span></span> <span data-ttu-id="b38c2-267">`*`字符指定查询应返回表中的所有列。</span><span class="sxs-lookup"><span data-stu-id="b38c2-267">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="b38c2-268">（你可能还列出列单独，并用逗号隔开。）</span><span class="sxs-lookup"><span data-stu-id="b38c2-268">(You could also list columns individually, separated by commas.)</span></span>

<span data-ttu-id="b38c2-269">结果的查询，如果有的话，将返回，并且中可`selectedData`变量。</span><span class="sxs-lookup"><span data-stu-id="b38c2-269">The results of the query, if any, are returned and made available in the `selectedData` variable.</span></span> <span data-ttu-id="b38c2-270">同样，该变量可以命名为任何内容。</span><span class="sxs-lookup"><span data-stu-id="b38c2-270">Again, the variable could be named anything.</span></span>

<span data-ttu-id="b38c2-271">最后，第三行是告诉 ASP.NET，你想要使用的实例`WebGrid`帮助器。</span><span class="sxs-lookup"><span data-stu-id="b38c2-271">Finally, the third line tells ASP.NET that you want to use an instance of the `WebGrid` helper.</span></span> <span data-ttu-id="b38c2-272">创建 (*实例化*) 使用的帮助程序对象`new`关键字并将其传递通过查询结果`selectedData`变量。</span><span class="sxs-lookup"><span data-stu-id="b38c2-272">You create (*instantiate*) the helper object by using the `new` keyword and pass it the query results via the `selectedData` variable.</span></span> <span data-ttu-id="b38c2-273">新`WebGrid`对象，以及数据库查询的结果可在`grid`变量。</span><span class="sxs-lookup"><span data-stu-id="b38c2-273">The new `WebGrid` object, along with the results of the database query, are made available in the `grid` variable.</span></span> <span data-ttu-id="b38c2-274">在一段时间来实际在页中显示数据，你将需要该结果。</span><span class="sxs-lookup"><span data-stu-id="b38c2-274">You'll need that result in a moment to actually display the data in the page.</span></span>

<span data-ttu-id="b38c2-275">在此阶段中，打开该数据库，你已收到数据，并已准备好`WebGrid`与该数据的帮助器。</span><span class="sxs-lookup"><span data-stu-id="b38c2-275">At this stage, the database has been opened, you've gotten the data you want, and you've prepared the `WebGrid` helper with that data.</span></span> <span data-ttu-id="b38c2-276">下一步是在页中创建的标记。</span><span class="sxs-lookup"><span data-stu-id="b38c2-276">Next is to create the markup in the page.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="b38c2-277">**结构化的查询语言 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="b38c2-277">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="b38c2-278">SQL 是一种语言，可在大多数关系数据库中用于管理数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="b38c2-278">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="b38c2-279">它包括能够让你检索数据和更新它，并能够让你创建、 修改和管理数据库表中的数据的命令。</span><span class="sxs-lookup"><span data-stu-id="b38c2-279">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage data in database tables.</span></span> <span data-ttu-id="b38c2-280">SQL 是不同于编程语言 （如 C# 中)。</span><span class="sxs-lookup"><span data-stu-id="b38c2-280">SQL is different than a programming language (like C#).</span></span> <span data-ttu-id="b38c2-281">使用 SQL 告诉数据库所需的并且数据库的作业，以了解如何获取数据或执行任务。</span><span class="sxs-lookup"><span data-stu-id="b38c2-281">With SQL, you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="b38c2-282">下面是一些 SQL 命令的示例和它们执行的操作：</span><span class="sxs-lookup"><span data-stu-id="b38c2-282">Here are examples of some SQL commands and what they do:</span></span>
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="b38c2-283">第一个`Select`语句获取所有列 (由指定`*`) 从*电影*表。</span><span class="sxs-lookup"><span data-stu-id="b38c2-283">The first `Select` statement gets all the columns (specified by `*`) from the *Movies* table.</span></span>
> 
> <span data-ttu-id="b38c2-284">第二个`Select`语句从记录中提取的 ID、 名称和价格列*产品*其价格列的值是 10 个以上的表。</span><span class="sxs-lookup"><span data-stu-id="b38c2-284">The second `Select` statement fetches the ID, Name, and Price columns from records in the *Product* table whose Price column value is more than 10.</span></span> <span data-ttu-id="b38c2-285">此命令根据名称列的值的按字母顺序返回结果。</span><span class="sxs-lookup"><span data-stu-id="b38c2-285">The command returns the results in alphabetical order based on the values of the Name column.</span></span> <span data-ttu-id="b38c2-286">如果没有记录匹配价格条件，该命令将返回空集。</span><span class="sxs-lookup"><span data-stu-id="b38c2-286">If no records match the price criteria, the command returns an empty set.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> <span data-ttu-id="b38c2-287">此命令将插入新记录到*产品*表，将"Croissant"、"A 发生喜欢广为"，说明列和价格的名称列设置为 1.99。</span><span class="sxs-lookup"><span data-stu-id="b38c2-287">This command inserts a new record into the *Product* table, setting the Name column to "Croissant", the Description column to "A flaky delight", and the price to 1.99.</span></span>
> 
> <span data-ttu-id="b38c2-288">请注意，当你要指定一个非数字值，该值将用单引号引起来 （不双引号，如下所示 C#）。</span><span class="sxs-lookup"><span data-stu-id="b38c2-288">Notice that when you're specifying a non-numeric value, the value is enclosed in single quotation marks (not double quotation marks, as in C#).</span></span> <span data-ttu-id="b38c2-289">你使用围绕文本或日期值，但不是解决数字这些引号引起来。</span><span class="sxs-lookup"><span data-stu-id="b38c2-289">You use these quotation marks around text or date values, but not around numbers.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> <span data-ttu-id="b38c2-290">此命令删除中的记录*产品*其到期日期列是早于 2008 年 1 月 1 日的表。</span><span class="sxs-lookup"><span data-stu-id="b38c2-290">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="b38c2-291">(该命令假定*产品*表具有这样的列，这是当然的。)采用 MM/DD/YYYY 格式，在此处输入日期，但它应该用于你的区域设置的格式输入。</span><span class="sxs-lookup"><span data-stu-id="b38c2-291">(The command assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="b38c2-292">`Insert`和`Delete`命令不返回结果集。</span><span class="sxs-lookup"><span data-stu-id="b38c2-292">The `Insert` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="b38c2-293">相反，它们返回一个数字，告诉你该命令影响了多少条记录。</span><span class="sxs-lookup"><span data-stu-id="b38c2-293">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="b38c2-294">对于某些这些操作 （例如插入和删除记录），请求操作的过程必须在数据库中具有适当的权限。</span><span class="sxs-lookup"><span data-stu-id="b38c2-294">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="b38c2-295">这就是为什么对于生产数据库通常具有以便在连接到数据库时提供用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="b38c2-295">That's why for production databases you often have to supply a user name and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="b38c2-296">有多个 SQL 命令，但它们都遵循与你在此处看到命令一样模式。</span><span class="sxs-lookup"><span data-stu-id="b38c2-296">There are dozens of SQL commands, but they all follow a pattern like the commands you see here.</span></span> <span data-ttu-id="b38c2-297">SQL 命令可用于创建数据库表、 计算的表中的记录数、 计算价格，和执行许多的更多操作。</span><span class="sxs-lookup"><span data-stu-id="b38c2-297">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>


### <a name="adding-markup-to-display-the-data"></a><span data-ttu-id="b38c2-298">添加标记以显示数据</span><span class="sxs-lookup"><span data-stu-id="b38c2-298">Adding Markup to Display the Data</span></span>

<span data-ttu-id="b38c2-299">内部`<head>`元素，集内容`<title>`"电影"的元素：</span><span class="sxs-lookup"><span data-stu-id="b38c2-299">Inside the `<head>` element, set contents of the `<title>` element to "Movies":</span></span>

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

<span data-ttu-id="b38c2-300">内部`<body>`元素的页上，添加以下：</span><span class="sxs-lookup"><span data-stu-id="b38c2-300">Inside the `<body>` element of the page, add the following:</span></span>

[!code-html[Main](displaying-data/samples/sample3.html)]

<span data-ttu-id="b38c2-301">介绍完毕。</span><span class="sxs-lookup"><span data-stu-id="b38c2-301">That's it.</span></span> <span data-ttu-id="b38c2-302">`grid`变量是在创建时创建的值`WebGrid`前面代码中的对象。</span><span class="sxs-lookup"><span data-stu-id="b38c2-302">The `grid` variable is the value you created when you created the `WebGrid` object in code earlier.</span></span>

<span data-ttu-id="b38c2-303">在 WebMatrix 树视图中，右击该页并选择**在浏览器中启动**。</span><span class="sxs-lookup"><span data-stu-id="b38c2-303">In the WebMatrix tree view, right-click the page and select **Launch in browser**.</span></span> <span data-ttu-id="b38c2-304">你将看到类似于此页：</span><span class="sxs-lookup"><span data-stu-id="b38c2-304">You'll see something like this page:</span></span>

![电影表中的默认 WebGrid 帮助器输出](displaying-data/_static/image18.png)

<span data-ttu-id="b38c2-306">单击列标题链接以按该列排序。</span><span class="sxs-lookup"><span data-stu-id="b38c2-306">Click a column heading link to sort by that column.</span></span> <span data-ttu-id="b38c2-307">能够作为排序依据单击标题是一项功能内置于**WebGrid**帮助器。</span><span class="sxs-lookup"><span data-stu-id="b38c2-307">Being able to sort by clicking a heading is a feature that's built into the **WebGrid** helper.</span></span>

<span data-ttu-id="b38c2-308">`GetHtml`方法，顾名思义，生成显示的数据的标记。</span><span class="sxs-lookup"><span data-stu-id="b38c2-308">The `GetHtml` method, as its name suggests, generates markup that displays the data.</span></span> <span data-ttu-id="b38c2-309">默认情况下，`GetHtml`方法将生成一个 HTML`<table>`元素。</span><span class="sxs-lookup"><span data-stu-id="b38c2-309">By default, the `GetHtml` method generates an HTML `<table>` element.</span></span> <span data-ttu-id="b38c2-310">（如果你想，你可以验证呈现通过查看浏览器中的页面的源。）</span><span class="sxs-lookup"><span data-stu-id="b38c2-310">(If you want, you can verify the rendering by looking at the source of the page in the browser.)</span></span>

## <a name="modifying-the-look-of-the-grid"></a><span data-ttu-id="b38c2-311">修改网格的外观</span><span class="sxs-lookup"><span data-stu-id="b38c2-311">Modifying the Look of the Grid</span></span>

<span data-ttu-id="b38c2-312">使用`WebGrid`帮助程序只需像是变得简单，但生成的显示为 plain。</span><span class="sxs-lookup"><span data-stu-id="b38c2-312">Using the `WebGrid` helper like you just did is easy, but the resulting display is plain.</span></span> <span data-ttu-id="b38c2-313">`WebGrid`帮助程序具有各种类型的选项，可让你控制如何显示数据。</span><span class="sxs-lookup"><span data-stu-id="b38c2-313">The `WebGrid` helper has all sorts of options that let you control how the data is displayed.</span></span> <span data-ttu-id="b38c2-314">有太多，以浏览本教程中，但是此部分可让你了解一些这些选项。</span><span class="sxs-lookup"><span data-stu-id="b38c2-314">There are far too many to explore in this tutorial, but this section will give you an idea of some of those options.</span></span> <span data-ttu-id="b38c2-315">将在后面的这一系列教程中介绍几个其他选项。</span><span class="sxs-lookup"><span data-stu-id="b38c2-315">A few additional options will be covered in later tutorials in this series.</span></span>

### <a name="specifying-individual-columns-to-display"></a><span data-ttu-id="b38c2-316">指定显示的单个列</span><span class="sxs-lookup"><span data-stu-id="b38c2-316">Specifying Individual Columns to Display</span></span>

<span data-ttu-id="b38c2-317">若要开始，可以指定你想要只显示某些列。</span><span class="sxs-lookup"><span data-stu-id="b38c2-317">To start, you can specify that you want to display only certain columns.</span></span> <span data-ttu-id="b38c2-318">默认情况下，如你所见，该网格显示中的列的所有四个*电影*表。</span><span class="sxs-lookup"><span data-stu-id="b38c2-318">By default, as you've seen, the grid shows all four of the columns from the *Movies* table.</span></span>

<span data-ttu-id="b38c2-319">在*Movies.cshtml*文件中，将`@grid.GetHtml()`刚添加替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="b38c2-319">In the *Movies.cshtml* file, replace the `@grid.GetHtml()` markup that you just added with the following:</span></span>

[!code-css[Main](displaying-data/samples/sample4.css)]

<span data-ttu-id="b38c2-320">若要指示帮助器要显示的列，则包含`columns`参数`GetHtml`方法并传入集合中的列。</span><span class="sxs-lookup"><span data-stu-id="b38c2-320">To tell the helper which columns to display, you include a `columns` parameter for the `GetHtml` method and pass in a collection of columns.</span></span> <span data-ttu-id="b38c2-321">在集合中，你可以指定要包括每个列。</span><span class="sxs-lookup"><span data-stu-id="b38c2-321">In the collection, you specify each column to include.</span></span> <span data-ttu-id="b38c2-322">指定各个列以显示通过包括`grid.Column`对象，并传入所需的数据列的名称。</span><span class="sxs-lookup"><span data-stu-id="b38c2-322">You specify an individual column to display by including a `grid.Column` object, and pass in the name of the data column you want.</span></span> <span data-ttu-id="b38c2-323">(这些列必须包含在 SQL 查询结果-`WebGrid`帮助器无法显示未由查询返回的列。)</span><span class="sxs-lookup"><span data-stu-id="b38c2-323">(These columns must be included in the SQL query results — the `WebGrid` helper cannot display columns that were not returned by the query.)</span></span>

<span data-ttu-id="b38c2-324">启动*Movies.cshtml*浏览器中的同样，和获取以下所示显示此时间 （请注意，显示没有 ID 列）：</span><span class="sxs-lookup"><span data-stu-id="b38c2-324">Launch the *Movies.cshtml* page in the browser again, and this time you get a display like the following one (notice that no ID column is displayed):</span></span>

![显示仅所选的列的 WebGrid 显示](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a><span data-ttu-id="b38c2-326">更改查找范围的网格</span><span class="sxs-lookup"><span data-stu-id="b38c2-326">Changing the Look of the Grid</span></span>

<span data-ttu-id="b38c2-327">有相当多的更多用于显示的列，将此集中的更高版本教程中介绍其中一些选项。</span><span class="sxs-lookup"><span data-stu-id="b38c2-327">There are quite a few more options for displaying columns, some of which will be explored in later tutorials in this set.</span></span> <span data-ttu-id="b38c2-328">现在，本节将向你介绍你可以在其中设置样式为整个网格的方式。</span><span class="sxs-lookup"><span data-stu-id="b38c2-328">For now, this section will introduce you to ways in which you can style the grid as a whole.</span></span>

<span data-ttu-id="b38c2-329">内部`<head>`的页上，只需在关闭之前的部分`</head>`标记中，添加以下`<style>`元素：</span><span class="sxs-lookup"><span data-stu-id="b38c2-329">Inside the `<head>` section of the page, just before the closing `</head>` tag, add the following `<style>` element:</span></span>

[!code-css[Main](displaying-data/samples/sample5.css)]

<span data-ttu-id="b38c2-330">此 CSS 标记定义名为的类`grid`， `head`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="b38c2-330">This CSS markup defines classes named `grid`, `head`, and so on.</span></span> <span data-ttu-id="b38c2-331">您还可以通过以下方式将这些样式定义在单独*.css*文件并将该链接到页。</span><span class="sxs-lookup"><span data-stu-id="b38c2-331">You could also put these style definitions in a separate *.css* file and link that to the page.</span></span> <span data-ttu-id="b38c2-332">（事实上，您将执行的更高版本中此教程的集。）但是，为了方便起见出于本教程，它们很内显示的数据的同一页面。</span><span class="sxs-lookup"><span data-stu-id="b38c2-332">(In fact, you'll do that later in this tutorial set.) But to make things easy for this tutorial, they're inside the same page that displays the data.</span></span>

<span data-ttu-id="b38c2-333">现在你可以获取`WebGrid`帮助器以使用这些样式类。</span><span class="sxs-lookup"><span data-stu-id="b38c2-333">Now you can get the `WebGrid` helper to use these style classes.</span></span> <span data-ttu-id="b38c2-334">帮助器具有多个属性 (例如， `tableStyle`) 只需这样 — 为它们，分配的 CSS 样式类名称并作为一部分的帮助程序呈现的标记呈现该类的名称。</span><span class="sxs-lookup"><span data-stu-id="b38c2-334">The helper has a number of properties (for example, `tableStyle`) for just this purpose — you assign a CSS style class name to them, and that class name is rendered as part of the markup that's rendered by the helper.</span></span>

<span data-ttu-id="b38c2-335">更改`grid.GetHtml`标记以便它现在看起来像此代码：</span><span class="sxs-lookup"><span data-stu-id="b38c2-335">Change the `grid.GetHtml` markup so that it now looks like this code:</span></span>

[!code-css[Main](displaying-data/samples/sample6.css)]

<span data-ttu-id="b38c2-336">什么是新此处为你添加的`tableStyle`， `headerStyle`，和`alternatingRowStyle`参数`GetHtml`方法。</span><span class="sxs-lookup"><span data-stu-id="b38c2-336">What's new here is that you've added `tableStyle`, `headerStyle`, and `alternatingRowStyle` parameters to the `GetHtml` method.</span></span> <span data-ttu-id="b38c2-337">这些参数已设置为添加前一段时间的 CSS 样式的名称。</span><span class="sxs-lookup"><span data-stu-id="b38c2-337">These parameters have been set to the names of the CSS styles that you added a moment ago.</span></span>

<span data-ttu-id="b38c2-338">运行此页面，和此时会显示一个网格，看起来比大大降低纯之前：</span><span class="sxs-lookup"><span data-stu-id="b38c2-338">Run the page, and this time you see a grid that looks much less plain than before:</span></span>

![包含参数的 WebGrid 显示设置为 CSS 类名称](displaying-data/_static/image20.png)

<span data-ttu-id="b38c2-340">若要了解`GetHtml`生成的方法，你可以查看在浏览器中的页面的源。</span><span class="sxs-lookup"><span data-stu-id="b38c2-340">To see what the `GetHtml` method generated, you can look at the source of the page in the browser.</span></span> <span data-ttu-id="b38c2-341">我们将不会进行详细信息在这里，但重要的一点是，通过指定类似于的参数`tableStyle`，导致网格以生成 HTML 标记，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b38c2-341">We won't go into detail here, but the important point is that by specifying parameters like `tableStyle`, you caused the grid to generate HTML tags like the following:</span></span>

`<table class="grid">`

<span data-ttu-id="b38c2-342">`<table>`标记已`class`引用了一个以前添加的 CSS 规则的属性添加到它。</span><span class="sxs-lookup"><span data-stu-id="b38c2-342">The `<table>` tag has had a `class` attribute added to it that references one of the CSS rules that you added earlier.</span></span> <span data-ttu-id="b38c2-343">此代码演示了基本模式&mdash;不同参数`GetHtml`方法让你引用 CSS 类方法然后生成以及标记。</span><span class="sxs-lookup"><span data-stu-id="b38c2-343">This code shows you the basic pattern &mdash; different parameters for the `GetHtml` method let you reference CSS classes that the method then generates along with the markup.</span></span> <span data-ttu-id="b38c2-344">你使用 CSS 类所执行的操作是由您决定。</span><span class="sxs-lookup"><span data-stu-id="b38c2-344">What you do with the CSS classes is up to you.</span></span>

## <a name="adding-paging"></a><span data-ttu-id="b38c2-345">添加分页</span><span class="sxs-lookup"><span data-stu-id="b38c2-345">Adding Paging</span></span>

<span data-ttu-id="b38c2-346">作为本教程的最后一个任务，你将在网格中添加分页。</span><span class="sxs-lookup"><span data-stu-id="b38c2-346">As the last task for this tutorial, you'll add paging to the grid.</span></span> <span data-ttu-id="b38c2-347">现在，它是要每次显示所有电影没问题。</span><span class="sxs-lookup"><span data-stu-id="b38c2-347">Right now it's no problem to display all your movies at once.</span></span> <span data-ttu-id="b38c2-348">但如果你添加数百个电影，页面显示将获得长。</span><span class="sxs-lookup"><span data-stu-id="b38c2-348">But if you added hundreds of movies, the page display would get long.</span></span>

<span data-ttu-id="b38c2-349">在网页代码中，更改创建的行`WebGrid`于下面的代码的对象：</span><span class="sxs-lookup"><span data-stu-id="b38c2-349">In the page code, change the line that creates the `WebGrid` object to the following code:</span></span>

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

<span data-ttu-id="b38c2-350">与之前的唯一差异是你已添加`rowsPerPage`设置为 3 的参数。</span><span class="sxs-lookup"><span data-stu-id="b38c2-350">The only difference from before is that you've added a `rowsPerPage` parameter that's set to 3.</span></span>

<span data-ttu-id="b38c2-351">运行页面。</span><span class="sxs-lookup"><span data-stu-id="b38c2-351">Run the page.</span></span> <span data-ttu-id="b38c2-352">在网格中显示在时间，以及让电影的你的数据库中翻页的导航链接 3 行：</span><span class="sxs-lookup"><span data-stu-id="b38c2-352">The grid displays 3 rows at a time, plus navigation links that let you page through the movies in your database:</span></span>

![使用分页 WebGrid 显示](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a><span data-ttu-id="b38c2-354">接下来</span><span class="sxs-lookup"><span data-stu-id="b38c2-354">Coming Up Next</span></span>

<span data-ttu-id="b38c2-355">在下一步的教程中，你将了解如何使用 Razor 和 C# 代码来获取用户输入的窗体。</span><span class="sxs-lookup"><span data-stu-id="b38c2-355">In the next tutorial, you'll learn how to use Razor and C# code to get user input in a form.</span></span> <span data-ttu-id="b38c2-356">以便您可以找到按标题或风格的影片，你将添加到电影页搜索框。</span><span class="sxs-lookup"><span data-stu-id="b38c2-356">You'll add a search box to the Movies page so that you can find movies by title or genre.</span></span>

## <a name="complete-listing-for-movies-page"></a><span data-ttu-id="b38c2-357">电影页的完整列表</span><span class="sxs-lookup"><span data-stu-id="b38c2-357">Complete Listing for Movies Page</span></span>

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="b38c2-358">其他资源</span><span class="sxs-lookup"><span data-stu-id="b38c2-358">Additional Resources</span></span>

- [<span data-ttu-id="b38c2-359">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="b38c2-359">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)

> [!div class="step-by-step"]
> <span data-ttu-id="b38c2-360">[上一页](intro-to-web-pages-programming.md)
> [下一页](form-basics.md)</span><span class="sxs-lookup"><span data-stu-id="b38c2-360">[Previous](intro-to-web-pages-programming.md)
[Next](form-basics.md)</span></span>
