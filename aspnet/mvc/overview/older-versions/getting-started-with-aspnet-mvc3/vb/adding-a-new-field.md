---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
title: 将新字段添加到电影模型和数据库表 (VB) |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: aspnetcontent
ms.date: 01/12/2011
ms.assetid: 28970e1b-1845-4015-86ef-121e52a6c397
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: cd178b36e1554c9521e0a001568ba41ec13fcef0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839659"
---
<a name="adding-a-new-field-to-the-movie-model-and-database-table-vb"></a><span data-ttu-id="51550-103">将新字段添加到电影模型和数据库表 (VB)</span><span class="sxs-lookup"><span data-stu-id="51550-103">Adding a New Field to the Movie Model and Database Table (VB)</span></span>
====================
<span data-ttu-id="51550-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="51550-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="51550-105">本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="51550-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="51550-106">在开始之前，请确保已安装以下列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="51550-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="51550-107">可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="51550-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="51550-108">或者，可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="51550-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="51550-109">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="51550-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="51550-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="51550-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="51550-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）</span><span class="sxs-lookup"><span data-stu-id="51550-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="51550-112">如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="51550-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="51550-113">可随附于此项目具有 VB.NET 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="51550-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="51550-114">[下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="51550-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="51550-115">如果您愿意 C#，切换到[C# 版本](../cs/adding-a-new-field.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="51550-115">If you prefer C#, switch to the [C# version](../cs/adding-a-new-field.md) of this tutorial.</span></span>


<span data-ttu-id="51550-116">在本部分将对模型类进行一些更改，并了解如何更新数据库架构以匹配的模型更改。</span><span class="sxs-lookup"><span data-stu-id="51550-116">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="51550-117">向电影模型添加分级属性</span><span class="sxs-lookup"><span data-stu-id="51550-117">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="51550-118">首先，通过添加一个新`Rating`属性设置为现有`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="51550-118">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="51550-119">打开*Movie.cs*文件，并添加`Rating`如下属性：</span><span class="sxs-lookup"><span data-stu-id="51550-119">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample1.vb)]

<span data-ttu-id="51550-120">完整`Movie`类现在看起来如以下代码：</span><span class="sxs-lookup"><span data-stu-id="51550-120">The complete `Movie` class now looks like the following code:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample2.vb)]

<span data-ttu-id="51550-121">重新编译应用程序中使用**调试** &gt;**构建电影**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="51550-121">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="51550-122">现在，已更新`Model`类，您还需要更新*\Views\Movies\Index.vbhtml*并*\Views\Movies\Create.vbhtml*查看模板以支持新`Rating`属性。</span><span class="sxs-lookup"><span data-stu-id="51550-122">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.vbhtml* and *\Views\Movies\Create.vbhtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="51550-123">打开<em>\Views\Movies\Index.vbhtml</em>文件，并添加`<th>Rating</th>`列标题之后<strong>价格</strong>列。</span><span class="sxs-lookup"><span data-stu-id="51550-123">Open the<em>\Views\Movies\Index.vbhtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="51550-124">然后添加`<td>`快要结束的模板来呈现列`@item.Rating`值。</span><span class="sxs-lookup"><span data-stu-id="51550-124">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="51550-125">下面是哪些更新<em>Index.vbhtml</em>视图模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="51550-125">Below is what the updated <em>Index.vbhtml</em> view template looks like:</span></span>

[!code-vbhtml[Main](adding-a-new-field/samples/sample3.vbhtml)]

<span data-ttu-id="51550-126">接下来，打开*\Views\Movies\Create.vbhtml*文件，并添加以下标记窗体的结尾附近。</span><span class="sxs-lookup"><span data-stu-id="51550-126">Next, open the *\Views\Movies\Create.vbhtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="51550-127">这会使文本框中，以便创建新电影时，可以指定一个级别。</span><span class="sxs-lookup"><span data-stu-id="51550-127">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="51550-128">管理模型和数据库架构差异</span><span class="sxs-lookup"><span data-stu-id="51550-128">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="51550-129">现已更新以支持新的应用程序代码`Rating`属性。</span><span class="sxs-lookup"><span data-stu-id="51550-129">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="51550-130">现在，运行该应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="51550-130">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="51550-131">执行此操作，不过，将看到以下错误：</span><span class="sxs-lookup"><span data-stu-id="51550-131">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="51550-132">之所以看到此错误，因为已更新`Movie`应用程序中的 model 类现在与不同的架构`Movie`现有数据库表。</span><span class="sxs-lookup"><span data-stu-id="51550-132">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="51550-133">（数据库表中没有 `Rating` 列。）</span><span class="sxs-lookup"><span data-stu-id="51550-133">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="51550-134">默认情况下，当您使用 Entity Framework Code First 自动创建数据库，就像前面在本教程中，代码优先将表添加到数据库来帮助跟踪数据库的架构是否与从其中生成它的模型类同步。</span><span class="sxs-lookup"><span data-stu-id="51550-134">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="51550-135">如果它们不同步，实体框架将引发错误。</span><span class="sxs-lookup"><span data-stu-id="51550-135">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="51550-136">这使得更轻松地在开发时，你可能会否则仅发现 （通过奇怪的错误） 在运行时跟踪问题。</span><span class="sxs-lookup"><span data-stu-id="51550-136">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="51550-137">同步检查功能是哪些因素会导致要显示的错误消息，你刚才看到的。</span><span class="sxs-lookup"><span data-stu-id="51550-137">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="51550-138">有两种方法解决此错误：</span><span class="sxs-lookup"><span data-stu-id="51550-138">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="51550-139">让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="51550-139">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="51550-140">这种方法是非常方便时执行活动开发上测试数据库，因为它允许您一起快速改进模型和数据库架构。</span><span class="sxs-lookup"><span data-stu-id="51550-140">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="51550-141">缺点，不过，是会丢失数据库中的现有数据，因此您*不*需要生产数据库上使用此方法 ！</span><span class="sxs-lookup"><span data-stu-id="51550-141">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="51550-142">对现有数据库架构进行显式修改，使它与模型类相匹配。</span><span class="sxs-lookup"><span data-stu-id="51550-142">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="51550-143">此方法的优点是可以保留数据。</span><span class="sxs-lookup"><span data-stu-id="51550-143">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="51550-144">可以手动或通过创建数据库更改脚本进行此更改。</span><span class="sxs-lookup"><span data-stu-id="51550-144">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="51550-145">对于本教程中，我们将使用第一种方法，您必须 Entity Framework Code First 每当模型发生更改自动重新创建该数据库。</span><span class="sxs-lookup"><span data-stu-id="51550-145">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="51550-146">自动重新创建模型的更改上的数据库</span><span class="sxs-lookup"><span data-stu-id="51550-146">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="51550-147">让我们更新该应用程序，以便 Code First 自动删除并重新创建数据库，只要您更改应用程序的模型。</span><span class="sxs-lookup"><span data-stu-id="51550-147">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="51550-148">**警告**应该启用的自动删除并重新创建数据库，仅当你正在使用开发或测试数据库，这种方法和*永远不会*包含实际数据的生产数据库上。</span><span class="sxs-lookup"><span data-stu-id="51550-148">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="51550-149">使用生产服务器上可能会导致数据丢失。</span><span class="sxs-lookup"><span data-stu-id="51550-149">Using it on a production server can lead to data loss.</span></span>


<span data-ttu-id="51550-150">在中**解决方案资源管理器**，右键单击*模型*文件夹，选择**添加**，然后选择**类**。</span><span class="sxs-lookup"><span data-stu-id="51550-150">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="51550-151">将类命名&quot;MovieInitializer&quot;。</span><span class="sxs-lookup"><span data-stu-id="51550-151">Name the class &quot;MovieInitializer&quot;.</span></span> <span data-ttu-id="51550-152">更新`MovieInitializer`类，以包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="51550-152">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample5.vb)]

<span data-ttu-id="51550-153">`MovieInitializer`类指定应删除并自动重新创建如果发生变化的模型类使用该模型的数据库。</span><span class="sxs-lookup"><span data-stu-id="51550-153">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="51550-154">该代码包括`Seed`方法，以便指定一些默认数据会自动向数据库添加任何时间它具有创建 （或重新创建）。</span><span class="sxs-lookup"><span data-stu-id="51550-154">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="51550-155">这提供了有用的方式来使用填充数据库一些示例数据，而无需手动填充它每次进行更改的模型。</span><span class="sxs-lookup"><span data-stu-id="51550-155">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="51550-156">现在，已定义`MovieInitializer`类，您需要其绑定，以便每次应用程序运行时，它检查是否不同于数据库中架构的模型类。</span><span class="sxs-lookup"><span data-stu-id="51550-156">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="51550-157">如果是，您可以运行初始值设定项来重新创建数据库以匹配该模型，然后使用示例数据在数据库中填充。</span><span class="sxs-lookup"><span data-stu-id="51550-157">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="51550-158">打开*Global.asax*文件的根目录处`MvcMovies`项目：</span><span class="sxs-lookup"><span data-stu-id="51550-158">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

<span data-ttu-id="51550-159">*Global.asax*文件包含的类定义整个应用程序项目，并包含`Application_Start`运行该应用程序首次启动时的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="51550-159">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="51550-160">查找`Application_Start`方法，并添加到调用`Database.SetInitializer`开头的方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="51550-160">Find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample6.vb)]

<span data-ttu-id="51550-161">`Database.SetInitializer`刚添加的语句指示的数据库由`MovieDBContext`应自动删除并重新创建如果不匹配的架构和数据库实例。</span><span class="sxs-lookup"><span data-stu-id="51550-161">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="51550-162">如您所看到的它还会填充使用示例数据中指定的数据库和`MovieInitializer`类。</span><span class="sxs-lookup"><span data-stu-id="51550-162">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="51550-163">关闭*Global.asax*文件。</span><span class="sxs-lookup"><span data-stu-id="51550-163">Close the *Global.asax* file.</span></span>

<span data-ttu-id="51550-164">重新运行该应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="51550-164">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="51550-165">应用程序启动时，它会检测模型结构不能再与数据库架构相匹配。</span><span class="sxs-lookup"><span data-stu-id="51550-165">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="51550-166">自动重新创建数据库，以匹配新的模型结构，并填充该数据库示例电影：</span><span class="sxs-lookup"><span data-stu-id="51550-166">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image3.png)

<span data-ttu-id="51550-168">单击**创建新**链接以添加新电影。</span><span class="sxs-lookup"><span data-stu-id="51550-168">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="51550-169">请注意，您可以添加一个级别。</span><span class="sxs-lookup"><span data-stu-id="51550-169">Note that you can add a rating.</span></span>

<span data-ttu-id="51550-170">[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="51550-170">[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)</span></span>

<span data-ttu-id="51550-171">单击 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="51550-171">Click **Create**.</span></span> <span data-ttu-id="51550-172">新电影，包括分级，现在显示在列表的电影：</span><span class="sxs-lookup"><span data-stu-id="51550-172">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image6.png)

<span data-ttu-id="51550-174">在本部分中您将看到如何修改模型对象并使数据库所做的更改同步。</span><span class="sxs-lookup"><span data-stu-id="51550-174">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="51550-175">你还了解了一种方法来填充新创建的数据库使用示例数据，这样您可以试用方案。</span><span class="sxs-lookup"><span data-stu-id="51550-175">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="51550-176">接下来，让我们看看如何将更丰富的验证逻辑添加到模型类并启用某些业务规则以强制实施。</span><span class="sxs-lookup"><span data-stu-id="51550-176">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="51550-177">[上一页](examining-the-edit-methods-and-edit-view.md)
> [下一页](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="51550-177">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
