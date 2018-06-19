---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 创建数据库 |Microsoft 文档
author: microsoft
description: 步骤 2 显示的步骤来创建包含所有 dinner 数据库 RSVP 我们 NerdDinner 应用程序的数据。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: ba28d671bf13ec54b83b876462e2c23f90310037
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869135"
---
<a name="create-a-database"></a><span data-ttu-id="5805a-103">创建数据库</span><span class="sxs-lookup"><span data-stu-id="5805a-103">Create a Database</span></span>
====================
<span data-ttu-id="5805a-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5805a-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="5805a-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="5805a-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="5805a-106">这是一个免费的第 2 步["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，查找步程取如何生成一个较小，但完成，使用 ASP.NET MVC 1 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5805a-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="5805a-107">步骤 2 显示的步骤来创建包含所有 dinner 数据库 RSVP 我们 NerdDinner 应用程序的数据。</span><span class="sxs-lookup"><span data-stu-id="5805a-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="5805a-108">如果你使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="5805a-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="5805a-109">NerdDinner 步骤 2： 创建数据库</span><span class="sxs-lookup"><span data-stu-id="5805a-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="5805a-110">我们将使用数据库来存储所有的 Dinner 和回复数据我们 NerdDinner 为应用程序。</span><span class="sxs-lookup"><span data-stu-id="5805a-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="5805a-111">以下步骤说明了创建使用免费的 SQL Server Express 版的数据库 (你可以轻松地安装使用的 V2 [Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx))。</span><span class="sxs-lookup"><span data-stu-id="5805a-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="5805a-112">我们将编写的代码的所有适用于 SQL Server Express 和完整的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5805a-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="5805a-113">创建新的 SQL Server Express 数据库</span><span class="sxs-lookup"><span data-stu-id="5805a-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="5805a-114">我们将开始通过我们的 web 项目，右键单击，然后选择**添加-&gt;新项**菜单命令：</span><span class="sxs-lookup"><span data-stu-id="5805a-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="5805a-115">这将显示 Visual Studio 的"添加新项"对话框。</span><span class="sxs-lookup"><span data-stu-id="5805a-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="5805a-116">我们将按"数据"类别筛选，并选择"SQL Server 数据库"项模板：</span><span class="sxs-lookup"><span data-stu-id="5805a-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="5805a-117">我们将命名我们想要创建"NerdDinner.mdf"和确定命中的 SQL Server Express 的数据库。</span><span class="sxs-lookup"><span data-stu-id="5805a-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="5805a-118">Visual Studio 将然后问是否我们想要将此文件添加到我们 \App\_数据目录 （即一个目录已设置设置为这两个读取和写入安全 Acl）：</span><span class="sxs-lookup"><span data-stu-id="5805a-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="5805a-119">我们将单击"是"并将创建我们新数据库，并将其添加到我们的解决方案资源管理器：</span><span class="sxs-lookup"><span data-stu-id="5805a-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="5805a-120">创建我们数据库中的表</span><span class="sxs-lookup"><span data-stu-id="5805a-120">Creating Tables within our Database</span></span>

<span data-ttu-id="5805a-121">我们现在有新的空数据库。</span><span class="sxs-lookup"><span data-stu-id="5805a-121">We now have a new empty database.</span></span> <span data-ttu-id="5805a-122">让我们向其添加一些表。</span><span class="sxs-lookup"><span data-stu-id="5805a-122">Let's add some tables to it.</span></span>

<span data-ttu-id="5805a-123">若要这样做我们将导航到 Visual Studio 中，这使我们能够管理数据库和服务器内的"服务器资源管理器"选项卡窗口。</span><span class="sxs-lookup"><span data-stu-id="5805a-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="5805a-124">SQL Server Express 数据库存储在 \App\_的我们的应用程序数据文件夹将自动显示在服务器资源管理器。</span><span class="sxs-lookup"><span data-stu-id="5805a-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="5805a-125">我们可以选择使用"连接到数据库"图标"服务器资源管理器"窗口的顶部将其他 SQL Server 数据库 （本地和远程） 添加到列表以及：</span><span class="sxs-lookup"><span data-stu-id="5805a-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="5805a-126">我们将向我们的 NerdDinner 数据库 – 一个以用于存储我们晚餐，另一个跟踪对它们的回复接受添加两个表。</span><span class="sxs-lookup"><span data-stu-id="5805a-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="5805a-127">我们可以通过我们的数据库中的"表"文件夹中右键单击并选择"添加新表"菜单命令来创建新表：</span><span class="sxs-lookup"><span data-stu-id="5805a-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="5805a-128">这将会打开一个表设计器，使我们可以配置我们表的架构。</span><span class="sxs-lookup"><span data-stu-id="5805a-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="5805a-129">对于我们"晚餐"表中，我们将添加 10 列的数据：</span><span class="sxs-lookup"><span data-stu-id="5805a-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="5805a-130">我们想要将表的唯一主键的"DinnerID"列。</span><span class="sxs-lookup"><span data-stu-id="5805a-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="5805a-131">我们可以通过右键单击"DinnerID"列并选择"设置主键"菜单项对此进行配置：</span><span class="sxs-lookup"><span data-stu-id="5805a-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="5805a-132">除了进行 DinnerID 为主键，我们还希望将其配置为向表添加新的数据行时，其值将自动递增"标识"列 （这意味着第插入的 Dinner 一行将包含 1 DinnerID，第二个插入行将具有 DinnerID 为 2，等等)。</span><span class="sxs-lookup"><span data-stu-id="5805a-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="5805a-133">我们可以通过选择"DinnerID"列执行此操作，然后使用"列属性"编辑器以将"（是标识）"属性设置为"是"列。</span><span class="sxs-lookup"><span data-stu-id="5805a-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="5805a-134">我们将使用标准身份默认值 （从 1 开始和递增 1 上的每个新的 Dinner 行）：</span><span class="sxs-lookup"><span data-stu-id="5805a-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="5805a-135">我们将通过键入 CTRL-S 或使用保存我们表**文件-&gt;保存**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="5805a-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="5805a-136">这将提示我们命名表。</span><span class="sxs-lookup"><span data-stu-id="5805a-136">This will prompt us to name the table.</span></span> <span data-ttu-id="5805a-137">我们将其"晚餐"命名：</span><span class="sxs-lookup"><span data-stu-id="5805a-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="5805a-138">我们的新晚餐表将显示我们在服务器资源管理器中的数据库中。</span><span class="sxs-lookup"><span data-stu-id="5805a-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="5805a-139">我们然后重复上述步骤，创建"回复"表。</span><span class="sxs-lookup"><span data-stu-id="5805a-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="5805a-140">带有此表具有 3 列。</span><span class="sxs-lookup"><span data-stu-id="5805a-140">This table with have 3 columns.</span></span> <span data-ttu-id="5805a-141">我们将设置为主键，RsvpID 列，并还将为标识列：</span><span class="sxs-lookup"><span data-stu-id="5805a-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="5805a-142">我们将其保存，将其命名为"回复"。</span><span class="sxs-lookup"><span data-stu-id="5805a-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="5805a-143">设置表之间的外键关系</span><span class="sxs-lookup"><span data-stu-id="5805a-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="5805a-144">我们现在有两个表，我们的数据库中。</span><span class="sxs-lookup"><span data-stu-id="5805a-144">We now have two tables within our database.</span></span> <span data-ttu-id="5805a-145">我们最后一个架构设计步骤将设置这两个表 – 之间的"一到多"关系，以便我们可以将每个 Dinner 行与零个或多个应用于它的回复行相关联。</span><span class="sxs-lookup"><span data-stu-id="5805a-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="5805a-146">我们将配置的回复表的"DinnerID"列"晚餐"表中有"DinnerID"列的外键关系来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="5805a-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="5805a-147">若要执行此操作我们将通过在服务器资源管理器中双击它来打开表设计器中的回复表。</span><span class="sxs-lookup"><span data-stu-id="5805a-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="5805a-148">然后，我们将选择"DinnerID"列中，右键单击，然后选择"Relationshps..."</span><span class="sxs-lookup"><span data-stu-id="5805a-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationshps…"</span></span> <span data-ttu-id="5805a-149">上下文菜单命令：</span><span class="sxs-lookup"><span data-stu-id="5805a-149">context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="5805a-150">此时会弹出一个对话框，我们可以使用安装程序表之间的关系：</span><span class="sxs-lookup"><span data-stu-id="5805a-150">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="5805a-151">我们将单击"添加"按钮，以向对话框添加新的关系。</span><span class="sxs-lookup"><span data-stu-id="5805a-151">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="5805a-152">一旦添加关系，我们将右侧的对话框中，展开属性网格中的"表和列规范"树视图节点，然后单击右侧的"..."按钮：</span><span class="sxs-lookup"><span data-stu-id="5805a-152">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="5805a-153">单击"..."按钮将显示另一个对话框，从中我们需要指定哪些表和列所涉及的关系，以及使我们能够命名关系。</span><span class="sxs-lookup"><span data-stu-id="5805a-153">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="5805a-154">我们将更改为"晚餐"主键表并选择晚餐表中的"DinnerID"列为主键。</span><span class="sxs-lookup"><span data-stu-id="5805a-154">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="5805a-155">我们的回复表将外键表中，并回复。DinnerID 列将作为外键相关联：</span><span class="sxs-lookup"><span data-stu-id="5805a-155">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="5805a-156">现在的回复表中的每一行将 Dinner 表中的行与相关联。</span><span class="sxs-lookup"><span data-stu-id="5805a-156">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="5805a-157">SQL Server 将为我们 – 维护引用完整性，并使我们无法添加新的回复行，如果它不指向有效的 Dinner 行。</span><span class="sxs-lookup"><span data-stu-id="5805a-157">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="5805a-158">它还将删除 Dinner 行仍 RSVP 引用它的行是否阻止我们。</span><span class="sxs-lookup"><span data-stu-id="5805a-158">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="5805a-159">将数据添加到我们表</span><span class="sxs-lookup"><span data-stu-id="5805a-159">Adding Data to our Tables</span></span>

<span data-ttu-id="5805a-160">让我们通过将一些示例数据添加到我们晚餐表完成。</span><span class="sxs-lookup"><span data-stu-id="5805a-160">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="5805a-161">在服务器资源管理器在其上右键单击并选择"显示表数据"命令，我们可以向表中添加数据：</span><span class="sxs-lookup"><span data-stu-id="5805a-161">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="5805a-162">我们将添加几行 Dinner 我们可以在以后当我们开始实现应用程序使用的数据：</span><span class="sxs-lookup"><span data-stu-id="5805a-162">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="5805a-163">下一步</span><span class="sxs-lookup"><span data-stu-id="5805a-163">Next Step</span></span>

<span data-ttu-id="5805a-164">我们已经完成了创建我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="5805a-164">We've finished creating our database.</span></span> <span data-ttu-id="5805a-165">现在让我们创建我们可用于查询和更新它的模型类。</span><span class="sxs-lookup"><span data-stu-id="5805a-165">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5805a-166">[上一页](create-a-new-aspnet-mvc-project.md)
> [下一页](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="5805a-166">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
