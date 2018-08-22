---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: 创建数据库 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 596a491b4152da341a7779236dab17967a6de670
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830855"
---
<a name="creating-a-database"></a><span data-ttu-id="07070-104">创建数据库</span><span class="sxs-lookup"><span data-stu-id="07070-104">Creating a Database</span></span>
====================
<span data-ttu-id="07070-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="07070-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="07070-106">这是介绍 ASP.NET MVC 的基础知识初学者教程。</span><span class="sxs-lookup"><span data-stu-id="07070-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="07070-107">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="07070-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="07070-108">请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="07070-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="07070-109">在本部分中我们要创建新 SQL Express 数据库，我们将使用它来存储和检索电影数据。</span><span class="sxs-lookup"><span data-stu-id="07070-109">In this section we are going to create a new SQL Express database that we'll use to store and retrieve our movie data.</span></span> <span data-ttu-id="07070-110">从 Visual Web 开发人员 IDE 中，选择视图 |服务器资源管理器。</span><span class="sxs-lookup"><span data-stu-id="07070-110">From within the Visual Web Developer IDE, select View | Server Explorer.</span></span> <span data-ttu-id="07070-111">右键单击数据连接，然后单击添加连接...</span><span class="sxs-lookup"><span data-stu-id="07070-111">Right click on Data Connections and click Add Connection...</span></span>

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

<span data-ttu-id="07070-113">在选择数据源对话框中，选择 Microsoft SQL Server 并选择继续。</span><span class="sxs-lookup"><span data-stu-id="07070-113">In the Choose Data Source dialog, select Microsoft SQL Server and select Continue.</span></span>

![](getting-started-with-mvc-part4/_static/image2.png)

<span data-ttu-id="07070-114">在添加连接对话框中，输入"。 \SQLEXPRESS"服务器名称，并输入"电影"作为新数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="07070-114">In the Add Connection dialog, enter ".\SQLEXPRESS" for your Server Name, and enter "Movies" as the name for your new database.</span></span>

<span data-ttu-id="07070-115">[![添加连接对话框](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="07070-115">[![Add Connection dialog](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span></span>

<span data-ttu-id="07070-116">单击确定，并将你想要创建该数据库要求你。</span><span class="sxs-lookup"><span data-stu-id="07070-116">Click OK and you'll be asked if you want to create that database.</span></span> <span data-ttu-id="07070-117">选择是。</span><span class="sxs-lookup"><span data-stu-id="07070-117">Select yes.</span></span>

<span data-ttu-id="07070-118">[![创建电影？](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="07070-118">[![Create Movies?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span></span>

<span data-ttu-id="07070-119">现在你已在服务器资源管理器中生成一个空数据库。</span><span class="sxs-lookup"><span data-stu-id="07070-119">Now you've got an empty database in Server Explorer.</span></span>

![添加新表](getting-started-with-mvc-part4/_static/image7.png)

<span data-ttu-id="07070-121">右键单击表，然后单击添加表。</span><span class="sxs-lookup"><span data-stu-id="07070-121">Right click on Tables and click Add Table.</span></span> <span data-ttu-id="07070-122">表设计器将显示。</span><span class="sxs-lookup"><span data-stu-id="07070-122">The Table Designer will appear.</span></span> <span data-ttu-id="07070-123">添加 Id、 标题、 ReleaseDate、 Genre 和价格列。</span><span class="sxs-lookup"><span data-stu-id="07070-123">Add columns for Id, Title, ReleaseDate, Genre, and Price.</span></span> <span data-ttu-id="07070-124">右键单击 ID 列，然后单击设置 Primary Key。</span><span class="sxs-lookup"><span data-stu-id="07070-124">Right click on the ID column and click set Primary Key.</span></span> <span data-ttu-id="07070-125">下面是哪些我设计方面的问题如下所示。</span><span class="sxs-lookup"><span data-stu-id="07070-125">Here's what my design areas looks like.</span></span>

<span data-ttu-id="07070-126">[![数据库表编辑器](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="07070-126">[![Database Table Editor](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span></span>

<span data-ttu-id="07070-127">此外，选择 Id 列，并在下面的列属性下更改"标识规范"为"是"。</span><span class="sxs-lookup"><span data-stu-id="07070-127">Also, select the Id column and under Column Properties below change "Identity Specification" to "Yes."</span></span>

<span data-ttu-id="07070-128">[![IsIdentity-列属性](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="07070-128">[![IsIdentity - Column Properties](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span></span>

<span data-ttu-id="07070-129">获得其完成后，单击工具栏中的保存图标，或选择文件 |从菜单中，保存并命名为您的表"**电影**"（单数）。</span><span class="sxs-lookup"><span data-stu-id="07070-129">When you've got it done, click the Save icon in the toolbar or select File | Save from the menu, and name your table "**Movie**" (singular).</span></span> <span data-ttu-id="07070-130">我们有一个数据库和表 ！</span><span class="sxs-lookup"><span data-stu-id="07070-130">We've got a database and a table!</span></span>

<span data-ttu-id="07070-131">[![选择名称](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="07070-131">[![Choose Name](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span></span>

<span data-ttu-id="07070-132">返回到服务器资源管理器和右键单击的 Movie 表，然后选择"显示表数据"。</span><span class="sxs-lookup"><span data-stu-id="07070-132">Go back to Server Explorer and right click the Movie table, then select "Show Table Data."</span></span> <span data-ttu-id="07070-133">输入几个电影，以便我们的数据库有一些数据。</span><span class="sxs-lookup"><span data-stu-id="07070-133">Enter a few movies so our database has some data.</span></span>

<span data-ttu-id="07070-134">[![数据库表格编辑](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="07070-134">[![Database Table Editing](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span></span>

## <a name="creating-a-model"></a><span data-ttu-id="07070-135">创建模型</span><span class="sxs-lookup"><span data-stu-id="07070-135">Creating a Model</span></span>

<span data-ttu-id="07070-136">现在，切换回 IDE 右侧的解决方案资源管理器和右键单击模型文件夹并选择添加 |新项。</span><span class="sxs-lookup"><span data-stu-id="07070-136">Now, switch back to the Solution Explorer on the right hand side of the IDE and right-click on the Models folder and select Add | New Item.</span></span>

<span data-ttu-id="07070-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="07070-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span></span>

<span data-ttu-id="07070-138">我们将我们新的数据库中创建实体模型。</span><span class="sxs-lookup"><span data-stu-id="07070-138">We're going to create an Entity Model from our new database.</span></span> <span data-ttu-id="07070-139">这会将一组类添加到我们的项目，以便轻松我们来查询和操作数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="07070-139">This will add a set of classes to our project that makes it easy for us to query and manipulate the data within our database.</span></span> <span data-ttu-id="07070-140">选择对话框中，左侧的数据节点，然后选择 ADO.NET 实体数据模型项模板。</span><span class="sxs-lookup"><span data-stu-id="07070-140">Select the Data node on the left-hand side of the dialog, and then select the ADO.NET Entity Data Model item template.</span></span> <span data-ttu-id="07070-141">将其命名 Movies.edmx。</span><span class="sxs-lookup"><span data-stu-id="07070-141">Name it Movies.edmx.</span></span>

<span data-ttu-id="07070-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="07070-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span></span>

<span data-ttu-id="07070-143">单击"添加"按钮。</span><span class="sxs-lookup"><span data-stu-id="07070-143">Click the "Add" button.</span></span> <span data-ttu-id="07070-144">然后，这将启动"实体数据模型向导"。</span><span class="sxs-lookup"><span data-stu-id="07070-144">This will then launch the "Entity Data Model Wizard".</span></span>

<span data-ttu-id="07070-145">在新弹出的对话框，从数据库中选择生成。</span><span class="sxs-lookup"><span data-stu-id="07070-145">In the new dialog that pops up, select Generate from Database.</span></span> <span data-ttu-id="07070-146">由于我们进行了数据库，我们只需要告诉我们新的数据库和其表的实体框架。</span><span class="sxs-lookup"><span data-stu-id="07070-146">Since we've just made a database, we'll only need to tell the Entity Framework about our new database and its table.</span></span> <span data-ttu-id="07070-147">单击保存在我们的 web 应用程序的配置数据库连接下一步。</span><span class="sxs-lookup"><span data-stu-id="07070-147">Click Next to save our database connection in our web application's configuration.</span></span> <span data-ttu-id="07070-148">现在，检查表和电影复选框，并单击完成。</span><span class="sxs-lookup"><span data-stu-id="07070-148">Now, check the Tables and Movie checkbox and click Finish.</span></span>

<span data-ttu-id="07070-149">[![实体数据模型向导](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="07070-149">[![Entity Data Model Wizard](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span></span>

<span data-ttu-id="07070-150">现在，我们可以看到我们新的 Movie 表中实体框架设计器，并从代码访问它。</span><span class="sxs-lookup"><span data-stu-id="07070-150">Now we can see our new Movie table in the Entity Framework Designer and access it from code.</span></span>

<span data-ttu-id="07070-151">[![电影-Microsoft Visual Web Developer 2010 速成版](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="07070-151">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span></span>

<span data-ttu-id="07070-152">在设计图面上可以看到"Movie"类。</span><span class="sxs-lookup"><span data-stu-id="07070-152">On the design surface you can see a "Movie" class.</span></span> <span data-ttu-id="07070-153">此类映射到在数据库中，"电影"表并在其中每个属性将映射到具有表的列。</span><span class="sxs-lookup"><span data-stu-id="07070-153">This class maps to the "Movie" table in our database, and each property within it maps to a column with the table.</span></span> <span data-ttu-id="07070-154">"电影"类的每个实例将对应于"Movie"表中的行。</span><span class="sxs-lookup"><span data-stu-id="07070-154">Each instance of a "Movie" class will correspond to a row within the "Movie" table.</span></span>

<span data-ttu-id="07070-155">如果您不喜欢默认命名和映射实体框架使用的约定，可以使用实体框架设计器更改或自定义它们。</span><span class="sxs-lookup"><span data-stu-id="07070-155">If you don't like the default naming and mapping conventions used by the Entity Framework, you can use the Entity Framework designer to change or customize them.</span></span> <span data-ttu-id="07070-156">为此应用程序中，我们将使用默认值并只需将该文件作为-是。</span><span class="sxs-lookup"><span data-stu-id="07070-156">For this application we'll use the defaults and just save the file as-is.</span></span>

<span data-ttu-id="07070-157">现在，让我们使用一些真实数据 ！</span><span class="sxs-lookup"><span data-stu-id="07070-157">Now, let's work with some real data!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="07070-158">[上一页](getting-started-with-mvc-part3.md)
> [下一页](getting-started-with-mvc-part5.md)</span><span class="sxs-lookup"><span data-stu-id="07070-158">[Previous](getting-started-with-mvc-part3.md)
[Next](getting-started-with-mvc-part5.md)</span></span>
