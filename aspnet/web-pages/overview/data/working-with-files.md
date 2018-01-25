---
uid: web-pages/overview/data/working-with-files
title: "使用 ASP.NET Web 页 (Razor) 站点中的文件 |Microsoft 文档"
author: tfitzmac
description: "本章介绍如何读取、 写入、 追加、 删除和上载文件。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: eee916e4-ba4c-439a-a24e-68df7d45a569
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/data/working-with-files
msc.type: authoredcontent
ms.openlocfilehash: 0f119f8fb4873e55292203f21a2efd8f26793ae4
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="dd7fa-103">使用 ASP.NET Web 页 (Razor) 站点中的文件</span><span class="sxs-lookup"><span data-stu-id="dd7fa-103">Working with Files in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="dd7fa-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="dd7fa-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="dd7fa-105">此文章介绍了如何读取、 写入、 追加、 删除和将 ASP.NET Web 页 (Razor) 站点中的文件上载。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-105">This article explains how to read, write, append, delete, and upload files in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="dd7fa-106">如果你想要将图像上载并对其进行处理 （例如，翻转或调整其大小），请参阅[处理 ASP.NET Web Pages 站点中的映像](https://go.microsoft.com/fwlink/?LinkId=202897)。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-106">If you want to upload images and manipulate them (for example, flip or resize them), see [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).</span></span>
> 
> 
> <span data-ttu-id="dd7fa-107">**你将学习：**</span><span class="sxs-lookup"><span data-stu-id="dd7fa-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="dd7fa-108">如何创建一个文本文件，并向其中写入数据。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-108">How to create a text file and write data to it.</span></span>
> - <span data-ttu-id="dd7fa-109">如何将数据追加到现有文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-109">How to append data to an existing file.</span></span>
> - <span data-ttu-id="dd7fa-110">如何读取文件并从它将显示。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-110">How to read a file and display from it.</span></span>
> - <span data-ttu-id="dd7fa-111">如何从网站中删除文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-111">How to delete files from a website.</span></span>
> - <span data-ttu-id="dd7fa-112">如何让用户上载一个文件或多个文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-112">How to let users upload one file or multiple files.</span></span>
> 
> <span data-ttu-id="dd7fa-113">这些是 ASP.NET 编程文章中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-113">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="dd7fa-114">`File`对象，它提供了如何管理文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-114">The `File` object, which provides a way to manage files.</span></span>
> - <span data-ttu-id="dd7fa-115">`FileUpload`帮助器。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-115">The `FileUpload` helper.</span></span>
> - <span data-ttu-id="dd7fa-116">`Path`对象，它提供可用于操作路径和文件名的方法。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-116">The `Path` object, which provides methods that let you manipulate path and file names.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="dd7fa-117">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="dd7fa-117">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="dd7fa-118">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="dd7fa-118">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="dd7fa-119">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="dd7fa-119">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="dd7fa-120">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-120">This tutorial also works with WebMatrix 3.</span></span>


<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a><span data-ttu-id="dd7fa-121">创建文本文件并向其中写入数据</span><span class="sxs-lookup"><span data-stu-id="dd7fa-121">Creating a Text File and Writing Data to It</span></span>

<span data-ttu-id="dd7fa-122">除了你的网站中使用的数据库，你可能会处理文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-122">In addition to using a database in your website, you might work with files.</span></span> <span data-ttu-id="dd7fa-123">例如，你可以将文本文件用作一种简单的方式来存储站点数据。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-123">For example, you might use text files as a simple way to store data for the site.</span></span> <span data-ttu-id="dd7fa-124">(用于存储数据的文本文件有时称为*平面文件*。)文本文件可以采用不同格式，如*.txt*， *.xml*，或*.csv* （以逗号分隔值）。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-124">(A text file that's used to store data is sometimes called a *flat file*.) Text files can be in different formats, like *.txt*, *.xml*, or *.csv* (comma-delimited values).</span></span>

<span data-ttu-id="dd7fa-125">如果你想要将数据存储在文本文件中，你可以使用`File.WriteAllText`方法来指定要创建的文件并对其进行写入的数据。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-125">If you want to store data in a text file, you can use the `File.WriteAllText` method to specify the file to create and the data to write to it.</span></span> <span data-ttu-id="dd7fa-126">在此过程中，你将创建页面，其中包含有三个简单的表单`input`元素 （名字、 姓氏和电子邮件地址） 和一个**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-126">In this procedure, you'll create a page that contains a simple form with three `input` elements (first name, last name, and email address) and a **Submit** button.</span></span> <span data-ttu-id="dd7fa-127">当用户提交表单时，你将在文本文件中存储用户的输入。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-127">When the user submits the form, you'll store the user's input in a text file.</span></span>

1. <span data-ttu-id="dd7fa-128">创建一个名为的新文件夹*应用\_数据*，如果它已不存在。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-128">Create a new folder named *App\_Data*, if it doesn't exist already.</span></span>
2. <span data-ttu-id="dd7fa-129">在你的网站的根目录，创建一个名为的新文件*UserData.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-129">At the root of your website, create a new file named *UserData.cshtml*.</span></span>
3. <span data-ttu-id="dd7fa-130">将现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-130">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    <span data-ttu-id="dd7fa-131">HTML 标记创建具有三个文本框的窗体。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-131">The HTML markup creates the form with the three text boxes.</span></span> <span data-ttu-id="dd7fa-132">在代码中，你使用`IsPost`属性来确定开始处理之前是否已提交页面。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-132">In the code, you use the `IsPost` property to determine whether the page has been submitted before you start processing.</span></span>

    <span data-ttu-id="dd7fa-133">第一个任务是获取用户输入并将其分配给变量。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-133">The first task is to get the user input and assign it to variables.</span></span> <span data-ttu-id="dd7fa-134">然后，代码会将单独的变量的值串联成一个逗号分隔的字符串，然后存储在一个不同的变量。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-134">The code then concatenates the values of the separate variables into one comma-delimited string, which is then stored in a different variable.</span></span> <span data-ttu-id="dd7fa-135">请注意，逗号分隔符是包含用引号引起来的字符串 （"，"），因为要按其原义嵌入到你要创建的大字符串的逗号。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-135">Notice that the comma separator is a string contained in quotation marks (","), because you're literally embedding a comma into the big string that you're creating.</span></span> <span data-ttu-id="dd7fa-136">在你将连接在一起的数据结束时，你将添加`Environment.NewLine`。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-136">At the end of the data that you concatenate together, you add `Environment.NewLine`.</span></span> <span data-ttu-id="dd7fa-137">这将添加一个分行符 （换行符）。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-137">This adds a line break (a newline character).</span></span> <span data-ttu-id="dd7fa-138">你要创建的用于此串联是一个字符串，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-138">What you're creating with all this concatenation is a string that looks like this:</span></span>

    [!code-css[Main](working-with-files/samples/sample2.css)]

    <span data-ttu-id="dd7fa-139">（通过结束时不可见的行中断。）</span><span class="sxs-lookup"><span data-stu-id="dd7fa-139">(With an invisible line break at the end.)</span></span>

    <span data-ttu-id="dd7fa-140">然后创建一个变量 (`dataFile`)，其中包含的位置和要存储中的数据的文件的名称。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-140">You then create a variable (`dataFile`) that contains the location and name of the file to store the data in.</span></span> <span data-ttu-id="dd7fa-141">设置位置需要某些特殊处理。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-141">Setting the location requires some special handling.</span></span> <span data-ttu-id="dd7fa-142">在网站中，它是不好的做法，在代码中引用为绝对路径，如*C:\Folder\File.txt* web 服务器上的文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-142">In websites, it's a bad practice to refer in code to absolute paths like *C:\Folder\File.txt* for files on the web server.</span></span> <span data-ttu-id="dd7fa-143">如果移动网站，绝对路径将会不正确。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-143">If a website is moved, an absolute path will be wrong.</span></span> <span data-ttu-id="dd7fa-144">此外，为托管站点 （如而非你自己的计算机上） 您通常不知道正确的路径是在你编写代码时。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-144">Moreover, for a hosted site (as opposed to on your own computer) you typically don't even know what the correct path is when you're writing the code.</span></span>

    <span data-ttu-id="dd7fa-145">但有时 （例如 now，进行写入的文件)，你需要的完整路径。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-145">But sometimes (like now, for writing a file) you do need a complete path.</span></span> <span data-ttu-id="dd7fa-146">解决方案是使用`MapPath`方法`Server`对象。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-146">The solution is to use the `MapPath` method of the `Server` object.</span></span> <span data-ttu-id="dd7fa-147">这将返回到你的网站的完整路径。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-147">This returns the complete path to your website.</span></span> <span data-ttu-id="dd7fa-148">若要获取的网站根目录中，你的用户的路径`~`运算符 (站点来表示您的虚拟根) 到`MapPath`。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-148">To get the path for the website root, you user the `~` operator (to represen the site's virtual root) to `MapPath`.</span></span> <span data-ttu-id="dd7fa-149">(你还可以传递子文件夹名称给它，如*~/App\_数据 /*，以获取该子文件夹的路径。)然后可以连接到任何该方法返回若要创建的完整路径的其他信息。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-149">(You can also pass a subfolder name to it, like *~/App\_Data/*, to get the path for that subfolder.) You can then concatenate additional information onto whatever the method returns in order to create a complete path.</span></span> <span data-ttu-id="dd7fa-150">在此示例中，你可以添加文件名称。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-150">In this example, you add a file name.</span></span> <span data-ttu-id="dd7fa-151">(你可以阅读更多有关如何使用中的文件和文件夹路径[ASP.NET 网页编程使用 Razor 语法的简介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)。)</span><span class="sxs-lookup"><span data-stu-id="dd7fa-151">(You can read more about how to work with file and folder paths in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    <span data-ttu-id="dd7fa-152">该文件保存在*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-152">The file is saved in the *App\_Data* folder.</span></span> <span data-ttu-id="dd7fa-153">此文件夹是用于存储数据文件中所述的 ASP.NET 中的特殊文件夹[使用 ASP.NET Web Pages 站点中的数据库的简介](https://go.microsoft.com/fwlink/?LinkId=195209)。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-153">This folder is a special folder in ASP.NET that's used to store data files, as described in [Introduction to Working with a Database in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=195209).</span></span>

    <span data-ttu-id="dd7fa-154">`WriteAllText`方法`File`对象将数据写入该文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-154">The `WriteAllText` method of the `File` object writes the data to the file.</span></span> <span data-ttu-id="dd7fa-155">此方法采用两个参数： 写入的文件及要写入的实际数据 （包括路径） 的名称。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-155">This method takes two parameters: the name (with path) of the file to write to, and the actual data to write.</span></span> <span data-ttu-id="dd7fa-156">请注意，第一个参数的名称具有`@`字符作为前缀。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-156">Notice that the name of the first parameter has an `@` character as a prefix.</span></span> <span data-ttu-id="dd7fa-157">这是告诉的 ASP.NET 你提供的文本，原义字符串且字符，例如"/"不应以特殊方式解释。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-157">This tells ASP.NET that you're providing a verbatim string literal, and that characters like "/" should not be interpreted in special ways.</span></span> <span data-ttu-id="dd7fa-158">(有关详细信息，请参阅[ASP.NET Web 编程使用 Razor 语法的简介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)。)</span><span class="sxs-lookup"><span data-stu-id="dd7fa-158">(For more information, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd7fa-159">为了使你的代码以将文件保存于*应用\_数据*文件夹中，应用程序需要读写权限为该文件夹。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-159">In order for your code to save files in the *App\_Data* folder, the application needs read-write permissions for that folder.</span></span> <span data-ttu-id="dd7fa-160">你的开发计算机上这是不通常问题。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-160">On your development computer this is not typically an issue.</span></span> <span data-ttu-id="dd7fa-161">但是，当你的站点发布到宿主提供程序的 web 服务器时，你可能需要显式设置这些权限。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-161">However, when you publish your site to a hosting provider's web server, you might need to explicitly set those permissions.</span></span> <span data-ttu-id="dd7fa-162">如果你在托管提供商的服务器上运行此代码，并获取错误，请与宿主提供程序中，若要了解如何设置这些权限。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-162">If you run this code on a hosting provider's server and get errors, check with the hosting provider to find out how to set those permissions.</span></span>

- <span data-ttu-id="dd7fa-163">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-163">Run the page in a browser.</span></span> 

    ![](working-with-files/_static/image1.jpg)
- <span data-ttu-id="dd7fa-164">到的字段中输入值，然后单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-164">Enter values into the fields and then click **Submit**.</span></span>
- <span data-ttu-id="dd7fa-165">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-165">Close the browser.</span></span>
- <span data-ttu-id="dd7fa-166">返回到该项目并刷新视图。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-166">Return to the project and refresh the view.</span></span>
- <span data-ttu-id="dd7fa-167">打开*data.txt*文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-167">Open the *data.txt* file.</span></span> <span data-ttu-id="dd7fa-168">在窗体中提交的数据位于文件中。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-168">The data you submitted in the form is in the file.</span></span> 

    ![[image]](working-with-files/_static/image2.jpg)
- <span data-ttu-id="dd7fa-170">关闭*data.txt*文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-170">Close the *data.txt* file.</span></span>

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a><span data-ttu-id="dd7fa-171">将数据追加到现有文件</span><span class="sxs-lookup"><span data-stu-id="dd7fa-171">Appending Data to an Existing File</span></span>

<span data-ttu-id="dd7fa-172">在前面的示例中，你使用`WriteAllText`创建一个文本文件，在其中有一条数据。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-172">In the previous example, you used `WriteAllText` to create a text file that's got just one piece of data in it.</span></span> <span data-ttu-id="dd7fa-173">如果你再次调用该方法，并将其传递的相同的文件名称，完全覆盖现有文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-173">If you call the method again and pass it the same file name, the existing file is completely overwritten.</span></span> <span data-ttu-id="dd7fa-174">但是，创建一个文件后你通常想要将新数据添加到文件末尾。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-174">However, after you've created a file you often want to add new data to the end of the file.</span></span> <span data-ttu-id="dd7fa-175">你可以执行，使用`AppendAllText`方法`File`对象。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-175">You can do that using the `AppendAllText` method of the `File` object.</span></span>

1. <span data-ttu-id="dd7fa-176">在网站中，请一份*UserData.cshtml*文件并将副本命名*UserDataMultiple.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-176">In the website, make a copy of the *UserData.cshtml* file and name the copy *UserDataMultiple.cshtml*.</span></span>
2. <span data-ttu-id="dd7fa-177">将代码块在打开之前`<!DOCTYPE html>`标记中使用下面的代码块：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-177">Replace the code block before the opening `<!DOCTYPE html>` tag with the following code block:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    <span data-ttu-id="dd7fa-178">此代码从前面的示例中有一项更改。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-178">This code has one change in it from the previous example.</span></span> <span data-ttu-id="dd7fa-179">而不是使用`WriteAllText`，它使用`the AppendAllText`方法。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-179">Instead of using `WriteAllText`, it uses `the AppendAllText` method.</span></span> <span data-ttu-id="dd7fa-180">方法非常相似，只不过`AppendAllText`将数据添加到文件末尾。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-180">The methods are similar, except that `AppendAllText` adds the data to the end of the file.</span></span> <span data-ttu-id="dd7fa-181">与`WriteAllText`，`AppendAllText`创建文件，如果它尚不存在。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-181">As with `WriteAllText`, `AppendAllText` creates the file if it doesn't already exist.</span></span>
3. <span data-ttu-id="dd7fa-182">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-182">Run the page in a browser.</span></span>
4. <span data-ttu-id="dd7fa-183">用于字段输入值，然后单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-183">Enter values for the fields and then click **Submit**.</span></span>
5. <span data-ttu-id="dd7fa-184">添加更多的数据，并再次提交窗体。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-184">Add more data and submit the form again.</span></span>
6. <span data-ttu-id="dd7fa-185">返回到你的项目，右键单击项目文件夹，然后单击**刷新**。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-185">Return to your project, right-click the project folder, and then click **Refresh**.</span></span>
7. <span data-ttu-id="dd7fa-186">打开*data.txt*文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-186">Open the *data.txt* file.</span></span> <span data-ttu-id="dd7fa-187">它现在包含您刚才输入的新数据。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-187">It now contains the new data that you just entered.</span></span> 

    ![[image]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a><span data-ttu-id="dd7fa-189">读取和显示文件中的数据</span><span class="sxs-lookup"><span data-stu-id="dd7fa-189">Reading and Displaying Data from a File</span></span>

<span data-ttu-id="dd7fa-190">即使你不需要将数据写入到文本文件，有时可能需要从一个读取数据。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-190">Even if you don't need to write data to a text file, you'll probably sometimes need to read data from one.</span></span> <span data-ttu-id="dd7fa-191">若要执行此操作，可以再次使用`File`对象。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-191">To do this, you can again use the `File` object.</span></span> <span data-ttu-id="dd7fa-192">你可以使用`File`对象来单独读取每个行 （换行分隔） 或读取无论分隔方式的单个项。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-192">You can use the `File` object to read each line individually (separated by line breaks) or to read individual item no matter how they're separated.</span></span>

<span data-ttu-id="dd7fa-193">此过程演示了如何读取，并显示你在前面的示例中创建的数据。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-193">This procedure shows you how to read and display the data that you created in the previous example.</span></span>

1. <span data-ttu-id="dd7fa-194">在你的网站的根目录，创建一个名为的新文件*DisplayData.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-194">At the root of your website, create a new file named *DisplayData.cshtml*.</span></span>
2. <span data-ttu-id="dd7fa-195">将现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-195">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    <span data-ttu-id="dd7fa-196">通过读取上一示例中创建到一个名为变量的文件来启动代码`userData`，使用此方法调用：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-196">The code starts by reading the file that you created in the previous example into a variable named `userData`, using this method call:</span></span>

    [!code-css[Main](working-with-files/samples/sample5.css)]

    <span data-ttu-id="dd7fa-197">要执行此操作的代码位于`if`语句。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-197">The code to do this is inside an `if` statement.</span></span> <span data-ttu-id="dd7fa-198">如果你想要读取的文件，它是一个好办法使用`File.Exists`方法，以首先确定文件是否可用。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-198">When you want to read a file, it's a good idea to use the `File.Exists` method to determine first whether the file is available.</span></span> <span data-ttu-id="dd7fa-199">代码还将检查文件是否为空。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-199">The code also checks whether the file is empty.</span></span>

    <span data-ttu-id="dd7fa-200">页面的正文包含两个`foreach`循环，嵌套在另一个。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-200">The body of the page contains two `foreach` loops, one nested inside the other.</span></span> <span data-ttu-id="dd7fa-201">外部`foreach`循环从数据文件一次获取一行。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-201">The outer `foreach` loop gets one line at a time from the data file.</span></span> <span data-ttu-id="dd7fa-202">在这种情况下，行定义中的文件 &#8212; 换行也就是说，每个数据项是在其对应行。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-202">In this case, the lines are defined by line breaks in the file &#8212; that is, each data item is on its own line.</span></span> <span data-ttu-id="dd7fa-203">外部循环创建新项 (`<li>`元素) 的有序列表内 (`<ol>`元素)。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-203">The outer loop creates a new item (`<li>` element) inside an ordered list (`<ol>` element).</span></span>

    <span data-ttu-id="dd7fa-204">内部循环将每个数据行拆分为使用逗号作为分隔符的项 （字段）。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-204">The inner loop splits each data line into items (fields) using a comma as a delimiter.</span></span> <span data-ttu-id="dd7fa-205">（根据前面的示例，这意味着每个行包含三个字段和 #8212; 名字、 姓氏和电子邮件地址，每个以逗号分隔）。内部循环还会创建`<ul>`列表和显示一个列表项为每个数据行中的字段。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-205">(Based on the previous example, this means that each line contains three fields &#8212; the first name, last name, and email address, each separated by a comma.) The inner loop also creates a `<ul>` list and displays one list item for each field in the data line.</span></span>

    <span data-ttu-id="dd7fa-206">代码演示了如何使用两种数据类型、 数组和`char`数据类型。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-206">The code illustrates how to use two data types, an array and the `char` data type.</span></span> <span data-ttu-id="dd7fa-207">该数组是必需的因为`File.ReadAllLines`方法返回的数组形式的数据。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-207">The array is required because the `File.ReadAllLines` method returns data as an array.</span></span> <span data-ttu-id="dd7fa-208">`char`数据类型是必需的因为`Split`方法返回`array`其中每个元素的类型均`char`。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-208">The `char` data type is required because the `Split` method returns an `array` in which each element is of the type `char`.</span></span> <span data-ttu-id="dd7fa-209">(有关数组的信息，请参阅[ASP.NET Web 编程使用 Razor 语法的简介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects)。)</span><span class="sxs-lookup"><span data-stu-id="dd7fa-209">(For information about arrays, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)</span></span>
3. <span data-ttu-id="dd7fa-210">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-210">Run the page in a browser.</span></span> <span data-ttu-id="dd7fa-211">将显示为前面的示例输入的数据。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-211">The data you entered for the previous examples is displayed.</span></span> 

    ![[image]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="dd7fa-213">**显示 Microsoft Excel 以逗号分隔文件中的数据**</span><span class="sxs-lookup"><span data-stu-id="dd7fa-213">**Displaying Data from a Microsoft Excel Comma-Delimited File**</span></span>
> 
> <span data-ttu-id="dd7fa-214">您可以使用 Microsoft Excel 保存电子表格作为以逗号分隔文件中包含的数据 (*.csv*文件)。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-214">You can use Microsoft Excel to save the data contained in a spreadsheet as a comma-delimited file (*.csv* file).</span></span> <span data-ttu-id="dd7fa-215">执行操作时，该文件将保存在不采用 Excel 格式的纯文本。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-215">When you do, the file is saved in plain text, not in Excel format.</span></span> <span data-ttu-id="dd7fa-216">在电子表格中的每个行分隔的文本文件中以换行符结尾的用逗号分隔每个数据项。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-216">Each row in the spreadsheet is separated by a line break in the text file, and each data item is separated by a comma.</span></span> <span data-ttu-id="dd7fa-217">在前面的示例所示的代码可用于读取 Excel 以逗号分隔文件，只需通过更改你的代码中的数据文件的名称。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-217">You can use the code shown in the previous example to read an Excel comma-delimited file just by changing the name of the data file in your code.</span></span>


<a id="Deleting_Files"></a>
## <a name="deleting-files"></a><span data-ttu-id="dd7fa-218">删除文件</span><span class="sxs-lookup"><span data-stu-id="dd7fa-218">Deleting Files</span></span>

<span data-ttu-id="dd7fa-219">若要从你的网站中删除文件，可以使用`File.Delete`方法。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-219">To delete files from your website, you can use the `File.Delete` method.</span></span> <span data-ttu-id="dd7fa-220">此过程演示如何使用户可以删除映像 (*.jpg*文件) 从*映像*文件夹，如果他们知道文件的名称。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-220">This procedure shows how to let users delete an image (*.jpg* file) from an *images* folder if they know the name of the file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dd7fa-221">**重要**在生产网站中，你通常限制允许哪些人具有对数据进行更改。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-221">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="dd7fa-222">有关如何将成员资格设置以及如何授权用户的站点上执行任务的信息，请参阅[添加安全和 ASP.NET Web Pages 站点的成员资格](https://go.microsoft.com/fwlink/?LinkId=202904)。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-222">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>


1. <span data-ttu-id="dd7fa-223">在网站中，创建名为的子*映像*。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-223">In the website, create a subfolder named *images*.</span></span>
2. <span data-ttu-id="dd7fa-224">复制一个或多个*.jpg*文件到*映像*文件夹。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-224">Copy one or more *.jpg* files into the *images* folder.</span></span>
3. <span data-ttu-id="dd7fa-225">在网站的根目录，创建一个名为的新文件*FileDelete.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-225">In the root of the website, create a new file named *FileDelete.cshtml*.</span></span>
4. <span data-ttu-id="dd7fa-226">将现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-226">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    <span data-ttu-id="dd7fa-227">此页包含窗体用户可以在其中输入图像文件的名称。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-227">This page contains a form where users can enter the name of an image file.</span></span> <span data-ttu-id="dd7fa-228">他们不输入*.jpg*文件扩展名; 通过限制如下的文件名称，则帮助阻止用户删除你的站点上的任意文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-228">They don't enter the *.jpg* file-name extension; by restricting the file name like this, you help prevents users from deleting arbitrary files on your site.</span></span>

    <span data-ttu-id="dd7fa-229">该代码读取用户已输入，然后构造的完整路径的文件名称。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-229">The code reads the file name that the user has entered and then constructs a complete path.</span></span> <span data-ttu-id="dd7fa-230">若要创建路径，该代码使用当前的网站路径 (如返回`Server.MapPath`方法)，则*映像*文件夹名称、 用户已提供的名称和作为文字字符串的".jpg"。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-230">To create the path, the code uses the current website path (as returned by the `Server.MapPath` method), the *images* folder name, the name that the user has provided, and ".jpg" as a literal string.</span></span>

    <span data-ttu-id="dd7fa-231">若要删除的文件，该代码调用`File.Delete`方法，将其传递你刚构建的完整路径。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-231">To delete the file, the code calls the `File.Delete` method, passing it the full path that you just constructed.</span></span> <span data-ttu-id="dd7fa-232">在结束标记时，代码将显示确认消息的文件被删除。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-232">At the end of the markup, code displays a confirmation message that the file was deleted.</span></span>
5. <span data-ttu-id="dd7fa-233">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-233">Run the page in a browser.</span></span> 

    ![[image]](working-with-files/_static/image5.jpg)
6. <span data-ttu-id="dd7fa-235">输入要删除，然后单击的文件的名称**提交**。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-235">Enter the name of the file to delete and then click **Submit**.</span></span> <span data-ttu-id="dd7fa-236">如果该文件已删除，文件的名称被显示在页面底部。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-236">If the file was deleted, the name of the file is displayed at the bottom of the page.</span></span>

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a><span data-ttu-id="dd7fa-237">让用户上载一个文件</span><span class="sxs-lookup"><span data-stu-id="dd7fa-237">Letting Users Upload a File</span></span>

<span data-ttu-id="dd7fa-238">`FileUpload`帮助器允许用户将文件上载到你的网站。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-238">The `FileUpload` helper lets users upload files to your website.</span></span> <span data-ttu-id="dd7fa-239">下面的过程演示了如何让用户上载单个文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-239">The procedure below shows you how to let users upload a single file.</span></span>

1. <span data-ttu-id="dd7fa-240">将 ASP.NET Web 帮助程序库添加到你的网站中所述[安装 ASP.NET 网页站点中的帮助器](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你以前未将其添加。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-240">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you didn't add it previously.</span></span>
2. <span data-ttu-id="dd7fa-241">在*应用\_数据*文件夹中，创建一个新文件夹并将其命名*UploadedFiles*。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-241">In the *App\_Data* folder, create a new a folder and name it *UploadedFiles*.</span></span>
3. <span data-ttu-id="dd7fa-242">在根中，创建一个名为的新文件*FileUpload.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-242">In the root, create a new file named *FileUpload.cshtml*.</span></span>
4. <span data-ttu-id="dd7fa-243">在页中的现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-243">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    <span data-ttu-id="dd7fa-244">此页面的正文部分使用`FileUpload`帮助器创建上载框和你可能熟悉的按钮：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-244">The body portion of the page uses the `FileUpload` helper to create the upload box and buttons that you're probably familiar with:</span></span>

    ![[image]](working-with-files/_static/image6.jpg)

    <span data-ttu-id="dd7fa-246">有关设置的属性的`FileUpload`帮助器指定你希望提交按钮以读取和你想要上载的文件的单个框**上载**。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-246">The properties that you set for the `FileUpload` helper specify that you want a single box for the file to upload and that you want the submit button to read **Upload**.</span></span> <span data-ttu-id="dd7fa-247">（你将添加多个框本文后面的部分。）</span><span class="sxs-lookup"><span data-stu-id="dd7fa-247">(You'll add more boxes later in the article.)</span></span>

    <span data-ttu-id="dd7fa-248">当用户单击**上载**，在页面顶部的代码获取文件，并将其保存。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-248">When the user clicks **Upload**, the code at the top of the page gets the file and saves it.</span></span> <span data-ttu-id="dd7fa-249">`Request`你通常使用从窗体字段中获取值的对象还具有`Files`数组，其中包含的文件 （或文件） 的已上载。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-249">The `Request` object that you normally use to get values from form fields also has a `Files` array that contains the file (or files) that have been uploaded.</span></span> <span data-ttu-id="dd7fa-250">你可以超出数组 #8212; 中的特定位置的单个文件例如，若要获取第一个上载的文件，你获得`Request.Files[0]`，若要获取第二个文件，你获得`Request.Files[1]`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-250">You can get individual files out of specific positions in the array &#8212; for example, to get the first uploaded file, you get `Request.Files[0]`, to get the second file, you get `Request.Files[1]`, and so on.</span></span> <span data-ttu-id="dd7fa-251">（记住，在编程中，计数通常从零开始）。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-251">(Remember that in programming, counting usually starts at zero.)</span></span>

    <span data-ttu-id="dd7fa-252">当提取已上载的文件时，你将其放入变量 (在这里， `uploadedFile`)，以便可以对其进行操作。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-252">When you fetch an uploaded file, you put it in a variable (here, `uploadedFile`) so that you can manipulate it.</span></span> <span data-ttu-id="dd7fa-253">若要确定已上载的文件的名称，您只会收到其`FileName`属性。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-253">To determine the name of the uploaded file, you just get its `FileName` property.</span></span> <span data-ttu-id="dd7fa-254">但是，当用户上载一个文件时，才`FileName`包含用户的原始名称，包括完整路径。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-254">However, when the user uploads a file, `FileName` contains the user's original name, which includes the entire path.</span></span> <span data-ttu-id="dd7fa-255">它可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-255">It might look like this:</span></span>

    <span data-ttu-id="dd7fa-256">*C:\Users\Public\Sample.txt*</span><span class="sxs-lookup"><span data-stu-id="dd7fa-256">*C:\Users\Public\Sample.txt*</span></span>

    <span data-ttu-id="dd7fa-257">不过，因为这是用户的计算机，不是针对你的服务器上的路径，你不希望所有该路径信息。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-257">You don't want all that path information, though, because that's the path on the user's computer, not for your server.</span></span> <span data-ttu-id="dd7fa-258">你只是想实际文件名 (*Sample.txt*)。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-258">You just want the actual file name (*Sample.txt*).</span></span> <span data-ttu-id="dd7fa-259">可以通过使用剥离出只需从路径文件`Path.GetFileName`方法，如下：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-259">You can strip out just the file from a path by using the `Path.GetFileName` method, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    <span data-ttu-id="dd7fa-260">`Path`对象是一个实用工具，具有大量如下可以使用条带路径、 合并路径，等的方法。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-260">The `Path` object is a utility that has a number of methods like this that you can use to strip paths, combine paths, and so on.</span></span>

    <span data-ttu-id="dd7fa-261">一旦你已收到已上载的文件的名称，你可以构建你想要将上载的文件存储在你的网站的新路径。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-261">Once you've gotten the name of the uploaded file, you can build a new path for where you want to store the uploaded file in your website.</span></span> <span data-ttu-id="dd7fa-262">在这种情况下，你将结合`Server.MapPath`，文件夹名称 (*应用\_数据/UploadedFiles*)，以及要创建一个新路径的新提取的文件名称。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-262">In this case, you combine `Server.MapPath`, the folder names (*App\_Data/UploadedFiles*), and the newly stripped file name to create a new path.</span></span> <span data-ttu-id="dd7fa-263">然后，你可以调用已上载的文件的`SaveAs`方法以实际将保存该文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-263">You can then call the uploaded file's `SaveAs` method to actually save the file.</span></span>
5. <span data-ttu-id="dd7fa-264">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-264">Run the page in a browser.</span></span> 

    ![[image]](working-with-files/_static/image7.jpg)
6. <span data-ttu-id="dd7fa-266">单击**浏览**，然后选择要上载的文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-266">Click **Browse** and then select a file to upload.</span></span> 

    ![[image]](working-with-files/_static/image8.jpg)

    <span data-ttu-id="dd7fa-268">下一步的文本框**浏览**按钮将包含的路径和文件位置。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-268">The text box next to the **Browse** button will contain the path and file location.</span></span>

    ![[image]](working-with-files/_static/image9.jpg)
7. <span data-ttu-id="dd7fa-270">单击“上载” 。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-270">Click **Upload**.</span></span>
8. <span data-ttu-id="dd7fa-271">在网站中，右击项目文件夹，然后单击**刷新**。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-271">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="dd7fa-272">打开*UploadedFiles*文件夹。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-272">Open the *UploadedFiles* folder.</span></span> <span data-ttu-id="dd7fa-273">你上载的文件位于文件夹中。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-273">The file that you uploaded is in the folder.</span></span> 

    ![[image]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a><span data-ttu-id="dd7fa-275">让用户上载多个文件</span><span class="sxs-lookup"><span data-stu-id="dd7fa-275">Letting Users Upload Multiple Files</span></span>

<span data-ttu-id="dd7fa-276">在前面的示例中，你可以让用户上载一个文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-276">In the previous example, you let users upload one file.</span></span> <span data-ttu-id="dd7fa-277">但你可以使用`FileUpload`帮助器一次上载多个文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-277">But you can use the `FileUpload` helper to upload more than one file at a time.</span></span> <span data-ttu-id="dd7fa-278">此方法非常方便和上载的照片，其中一次上载一个文件单调乏味一样的方案。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-278">This is handy for scenarios like uploading photos, where uploading one file at a time is tedious.</span></span> <span data-ttu-id="dd7fa-279">(你可以阅读上载照片[处理 ASP.NET Web Pages 站点中的映像](https://go.microsoft.com/fwlink/?LinkId=202897)。)此示例演示如何以使用户可以上载两个一次，不过可以使用相同的技术来上载多个程序。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-279">(You can read about uploading photos in [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).) This example shows how to let users upload two at a time, although you can use the same technique to upload more than that.</span></span>

1. <span data-ttu-id="dd7fa-280">将 ASP.NET Web 帮助程序库添加到你的网站中所述[安装 ASP.NET 网页站点中的帮助器](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-280">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="dd7fa-281">创建一个名为的新页*FileUploadMultiple.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-281">Create a new page named *FileUploadMultiple.cshtml*.</span></span>
3. <span data-ttu-id="dd7fa-282">在页中的现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-282">Replace the existing content in the page with the following:</span></span>  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    <span data-ttu-id="dd7fa-283">在此示例中，`FileUpload`页的正文中的帮助器以使用户可以将两个文件上载默认配置。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-283">In this example, the `FileUpload` helper in the body of the page is configured to let users upload two files by default.</span></span> <span data-ttu-id="dd7fa-284">因为`allowMoreFilesToBeAdded`设置为`true`，帮助器呈现一个链接，允许用户添加更多上载框：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-284">Because `allowMoreFilesToBeAdded` is set to `true`, the helper renders a link that lets user add more upload boxes:</span></span>

    ![[image]](working-with-files/_static/image11.jpg)

    <span data-ttu-id="dd7fa-286">若要处理用户上载的文件，该代码使用在前面的示例和 #8212; 中使用的相同基本技术获取从文件`Request.Files`然后将其保存。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-286">To process the files that the user uploads, the code uses the same basic technique that you used in the previous example &#8212; get a file from `Request.Files` and then save it.</span></span> <span data-ttu-id="dd7fa-287">（包括各种内容需要操作，以正确的文件名和路径。）这一次的创新是用户可能会上载多个文件，并且你不知道许多。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-287">(Including the various things you need to do to get the right file name and path.) The innovation this time is that the user might be uploading multiple files and you don't know many.</span></span> <span data-ttu-id="dd7fa-288">若要了解，你可以获取`Request.Files.Count`。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-288">To find out, you can get `Request.Files.Count`.</span></span>

    <span data-ttu-id="dd7fa-289">与现有此数字，则可以遍历`Request.Files`，反过来，提取每个文件并将其保存。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-289">With this number in hand, you can loop through `Request.Files`, fetch each file in turn, and save it.</span></span> <span data-ttu-id="dd7fa-290">如果你想要循环访问集合的已知的次数，你可以使用`for`循环，如下：</span><span class="sxs-lookup"><span data-stu-id="dd7fa-290">When you want to loop a known number of times through a collection, you can use a `for` loop, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    <span data-ttu-id="dd7fa-291">变量`i`是只会从零到您设置任何上限的临时计数器。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-291">The variable `i` is just a temporary counter that will go from zero to whatever upper limit you set.</span></span> <span data-ttu-id="dd7fa-292">在这种情况下，上限为的文件数。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-292">In this case, the upper limit is the number of files.</span></span> <span data-ttu-id="dd7fa-293">但由于计数器开始从零开始，适用于计数在 ASP.NET 中的方案的典型的上限值实际是一个小于该文件数。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-293">But because the counter starts at zero, as is typical for counting scenarios in ASP.NET, the upper limit is actually one less than the file count.</span></span> <span data-ttu-id="dd7fa-294">（如果三个文件上载，计数为零为 2。）</span><span class="sxs-lookup"><span data-stu-id="dd7fa-294">(If three files are uploaded, the count is zero to 2.)</span></span>

    <span data-ttu-id="dd7fa-295">`uploadedCount`变量进行合计已成功上载并保存的所有文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-295">The `uploadedCount` variable totals all the files that are successfully uploaded and saved.</span></span> <span data-ttu-id="dd7fa-296">此代码中占了预期的文件可能无法要上载的可能性。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-296">This code accounts for the possibility that an expected file may not be able to be uploaded.</span></span>
4. <span data-ttu-id="dd7fa-297">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-297">Run the page in a browser.</span></span> <span data-ttu-id="dd7fa-298">浏览器显示页和其两个上载框。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-298">The browser displays the page and its two upload boxes.</span></span>
5. <span data-ttu-id="dd7fa-299">选择要上载的两个文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-299">Select two files to upload.</span></span>
6. <span data-ttu-id="dd7fa-300">单击**添加另一个文件**。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-300">Click **Add another file**.</span></span> <span data-ttu-id="dd7fa-301">该页显示一个新的上载框。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-301">The page displays a new upload box.</span></span> 

    ![[image]](working-with-files/_static/image12.jpg)
7. <span data-ttu-id="dd7fa-303">单击“上载” 。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-303">Click **Upload**.</span></span>
8. <span data-ttu-id="dd7fa-304">在网站中，右击项目文件夹，然后单击**刷新**。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-304">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="dd7fa-305">打开*UploadedFiles*文件夹以查看已成功上载的文件。</span><span class="sxs-lookup"><span data-stu-id="dd7fa-305">Open the *UploadedFiles* folder to see the successfully uploaded files.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="dd7fa-306">其他资源</span><span class="sxs-lookup"><span data-stu-id="dd7fa-306">Additional Resources</span></span>


[<span data-ttu-id="dd7fa-307">使用 ASP.NET Web 页站点中的图像</span><span class="sxs-lookup"><span data-stu-id="dd7fa-307">Working with Images in an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkId=202897)

[<span data-ttu-id="dd7fa-308">将导出到 CSV 文件</span><span class="sxs-lookup"><span data-stu-id="dd7fa-308">Exporting to a CSV File</span></span>](https://msdn.microsoft.com/library/ms155919.aspx)
