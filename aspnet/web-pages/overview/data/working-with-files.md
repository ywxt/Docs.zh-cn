---
uid: web-pages/overview/data/working-with-files
title: 在 ASP.NET 网页 (Razor) 站点中使用文件 |Microsoft Docs
author: tfitzmac
description: 这一章介绍了如何读取、 写入、 追加、 删除和将文件上传。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: eee916e4-ba4c-439a-a24e-68df7d45a569
msc.legacyurl: /web-pages/overview/data/working-with-files
msc.type: authoredcontent
ms.openlocfilehash: 20fdbfda7d3e4b214a8e201c4a815a29c5bb7061
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825644"
---
<a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="be5c6-103">在 ASP.NET Web Pages (Razor) 站点中使用文件</span><span class="sxs-lookup"><span data-stu-id="be5c6-103">Working with Files in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="be5c6-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="be5c6-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="be5c6-105">此文章介绍了如何读取、 写入、 追加、 删除和将 ASP.NET Web Pages (Razor) 站点中的文件上传。</span><span class="sxs-lookup"><span data-stu-id="be5c6-105">This article explains how to read, write, append, delete, and upload files in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="be5c6-106">如果你想要将图像上传并对其进行处理 （例如，翻转或调整其大小），请参阅[使用 ASP.NET Web Pages 站点中的图像](https://go.microsoft.com/fwlink/?LinkId=202897)。</span><span class="sxs-lookup"><span data-stu-id="be5c6-106">If you want to upload images and manipulate them (for example, flip or resize them), see [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).</span></span>
> 
> 
> <span data-ttu-id="be5c6-107">**你将学习：**</span><span class="sxs-lookup"><span data-stu-id="be5c6-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="be5c6-108">了解如何创建一个文本文件并向其写入数据。</span><span class="sxs-lookup"><span data-stu-id="be5c6-108">How to create a text file and write data to it.</span></span>
> - <span data-ttu-id="be5c6-109">如何将数据追加到现有文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-109">How to append data to an existing file.</span></span>
> - <span data-ttu-id="be5c6-110">了解如何读取文件并从其显示。</span><span class="sxs-lookup"><span data-stu-id="be5c6-110">How to read a file and display from it.</span></span>
> - <span data-ttu-id="be5c6-111">如何从网站中删除文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-111">How to delete files from a website.</span></span>
> - <span data-ttu-id="be5c6-112">如何让用户上传一个或多个文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-112">How to let users upload one file or multiple files.</span></span>
> 
> <span data-ttu-id="be5c6-113">这些是 ASP.NET 编程一文中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="be5c6-113">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="be5c6-114">`File`对象，它提供一种方法来管理文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-114">The `File` object, which provides a way to manage files.</span></span>
> - <span data-ttu-id="be5c6-115">`FileUpload`帮助器。</span><span class="sxs-lookup"><span data-stu-id="be5c6-115">The `FileUpload` helper.</span></span>
> - <span data-ttu-id="be5c6-116">`Path`对象，它提供可用于操作路径和文件名的方法。</span><span class="sxs-lookup"><span data-stu-id="be5c6-116">The `Path` object, which provides methods that let you manipulate path and file names.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="be5c6-117">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="be5c6-117">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="be5c6-118">ASP.NET 网页 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="be5c6-118">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="be5c6-119">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="be5c6-119">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="be5c6-120">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="be5c6-120">This tutorial also works with WebMatrix 3.</span></span>


<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a><span data-ttu-id="be5c6-121">创建一个文本文件并向其中写入数据</span><span class="sxs-lookup"><span data-stu-id="be5c6-121">Creating a Text File and Writing Data to It</span></span>

<span data-ttu-id="be5c6-122">除了在你的网站中使用的数据库，您可能会处理文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-122">In addition to using a database in your website, you might work with files.</span></span> <span data-ttu-id="be5c6-123">例如，你可能会使用文本文件作为存储站点数据的简单方法。</span><span class="sxs-lookup"><span data-stu-id="be5c6-123">For example, you might use text files as a simple way to store data for the site.</span></span> <span data-ttu-id="be5c6-124">(有时称为用来存储数据的文本文件*平面文件*。)文本文件可以采用不同格式，如 *.txt*， *.xml*，或 *.csv* （以逗号分隔值）。</span><span class="sxs-lookup"><span data-stu-id="be5c6-124">(A text file that's used to store data is sometimes called a *flat file*.) Text files can be in different formats, like *.txt*, *.xml*, or *.csv* (comma-delimited values).</span></span>

<span data-ttu-id="be5c6-125">如果你想要将数据存储在文本文件中，则可以使用`File.WriteAllText`方法，以指定要创建的文件和要向其中写入的数据。</span><span class="sxs-lookup"><span data-stu-id="be5c6-125">If you want to store data in a text file, you can use the `File.WriteAllText` method to specify the file to create and the data to write to it.</span></span> <span data-ttu-id="be5c6-126">在此过程中，你将创建包含具有三个简单的窗体的页面`input`元素 （名字、 姓氏和电子邮件地址） 和一个**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="be5c6-126">In this procedure, you'll create a page that contains a simple form with three `input` elements (first name, last name, and email address) and a **Submit** button.</span></span> <span data-ttu-id="be5c6-127">当用户提交窗体时，想要在文本文件中保存用户的输入。</span><span class="sxs-lookup"><span data-stu-id="be5c6-127">When the user submits the form, you'll store the user's input in a text file.</span></span>

1. <span data-ttu-id="be5c6-128">创建一个名为的新文件夹*应用程序\_数据*，如果它尚未存在。</span><span class="sxs-lookup"><span data-stu-id="be5c6-128">Create a new folder named *App\_Data*, if it doesn't exist already.</span></span>
2. <span data-ttu-id="be5c6-129">在你的网站的根目录，创建名为的新文件*UserData.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="be5c6-129">At the root of your website, create a new file named *UserData.cshtml*.</span></span>
3. <span data-ttu-id="be5c6-130">使用以下内容替换现有内容：</span><span class="sxs-lookup"><span data-stu-id="be5c6-130">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    <span data-ttu-id="be5c6-131">HTML 标记创建具有三个文本框中的窗体。</span><span class="sxs-lookup"><span data-stu-id="be5c6-131">The HTML markup creates the form with the three text boxes.</span></span> <span data-ttu-id="be5c6-132">在代码中，您使用`IsPost`属性来确定页是否已提交之前开始处理。</span><span class="sxs-lookup"><span data-stu-id="be5c6-132">In the code, you use the `IsPost` property to determine whether the page has been submitted before you start processing.</span></span>

    <span data-ttu-id="be5c6-133">第一个任务是获取用户输入，并将其分配给变量。</span><span class="sxs-lookup"><span data-stu-id="be5c6-133">The first task is to get the user input and assign it to variables.</span></span> <span data-ttu-id="be5c6-134">代码然后将不同的变量的值连接成一个以逗号分隔的字符串，然后存储在不同的变量。</span><span class="sxs-lookup"><span data-stu-id="be5c6-134">The code then concatenates the values of the separate variables into one comma-delimited string, which is then stored in a different variable.</span></span> <span data-ttu-id="be5c6-135">请注意，逗号分隔符是包含在引号中的字符串 （"，"），因为按字面意思逗号嵌入到你要创建的大字符串。</span><span class="sxs-lookup"><span data-stu-id="be5c6-135">Notice that the comma separator is a string contained in quotation marks (","), because you're literally embedding a comma into the big string that you're creating.</span></span> <span data-ttu-id="be5c6-136">在串联在一起的数据结束时，您将添加`Environment.NewLine`。</span><span class="sxs-lookup"><span data-stu-id="be5c6-136">At the end of the data that you concatenate together, you add `Environment.NewLine`.</span></span> <span data-ttu-id="be5c6-137">这会添加一个分行符 （换行符）。</span><span class="sxs-lookup"><span data-stu-id="be5c6-137">This adds a line break (a newline character).</span></span> <span data-ttu-id="be5c6-138">您创建此连接是一个字符串，如下所示：</span><span class="sxs-lookup"><span data-stu-id="be5c6-138">What you're creating with all this concatenation is a string that looks like this:</span></span>

    [!code-css[Main](working-with-files/samples/sample2.css)]

    <span data-ttu-id="be5c6-139">（使用一个不可见的换行符结束时。）</span><span class="sxs-lookup"><span data-stu-id="be5c6-139">(With an invisible line break at the end.)</span></span>

    <span data-ttu-id="be5c6-140">然后创建一个变量 (`dataFile`)，其中包含的位置和存储中的数据的文件的名称。</span><span class="sxs-lookup"><span data-stu-id="be5c6-140">You then create a variable (`dataFile`) that contains the location and name of the file to store the data in.</span></span> <span data-ttu-id="be5c6-141">将位置设置需要一些特殊的处理。</span><span class="sxs-lookup"><span data-stu-id="be5c6-141">Setting the location requires some special handling.</span></span> <span data-ttu-id="be5c6-142">在网站中它是个好办法在代码中引用为绝对路径，如*C:\Folder\File.txt* web 服务器上的文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-142">In websites, it's a bad practice to refer in code to absolute paths like *C:\Folder\File.txt* for files on the web server.</span></span> <span data-ttu-id="be5c6-143">如果移动网站，则会不正确的绝对路径。</span><span class="sxs-lookup"><span data-stu-id="be5c6-143">If a website is moved, an absolute path will be wrong.</span></span> <span data-ttu-id="be5c6-144">此外，为托管站点 （与用于在你自己的计算机上） 通常不甚至知道正确的路径是当您编写的代码。</span><span class="sxs-lookup"><span data-stu-id="be5c6-144">Moreover, for a hosted site (as opposed to on your own computer) you typically don't even know what the correct path is when you're writing the code.</span></span>

    <span data-ttu-id="be5c6-145">但有时 （例如 now，用于写入一个文件)，则需要完整路径。</span><span class="sxs-lookup"><span data-stu-id="be5c6-145">But sometimes (like now, for writing a file) you do need a complete path.</span></span> <span data-ttu-id="be5c6-146">解决方法是使用`MapPath`方法的`Server`对象。</span><span class="sxs-lookup"><span data-stu-id="be5c6-146">The solution is to use the `MapPath` method of the `Server` object.</span></span> <span data-ttu-id="be5c6-147">这将返回到你的网站的完整路径。</span><span class="sxs-lookup"><span data-stu-id="be5c6-147">This returns the complete path to your website.</span></span> <span data-ttu-id="be5c6-148">若要获取网站根目录，你的用户的路径`~`运算符 (站点来表示您的虚拟根) 到`MapPath`。</span><span class="sxs-lookup"><span data-stu-id="be5c6-148">To get the path for the website root, you user the `~` operator (to represen the site's virtual root) to `MapPath`.</span></span> <span data-ttu-id="be5c6-149">(你还可以传递一个子文件夹名称到它，如 *~/App\_数据 /*，以获取此子文件夹的路径。)然后可以连接到任何方法返回若要创建的完整路径上的其他信息。</span><span class="sxs-lookup"><span data-stu-id="be5c6-149">(You can also pass a subfolder name to it, like *~/App\_Data/*, to get the path for that subfolder.) You can then concatenate additional information onto whatever the method returns in order to create a complete path.</span></span> <span data-ttu-id="be5c6-150">在此示例中，添加的文件名称。</span><span class="sxs-lookup"><span data-stu-id="be5c6-150">In this example, you add a file name.</span></span> <span data-ttu-id="be5c6-151">(您可以阅读更多有关如何处理中的文件和文件夹路径[ASP.NET Web Pages 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)。)</span><span class="sxs-lookup"><span data-stu-id="be5c6-151">(You can read more about how to work with file and folder paths in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    <span data-ttu-id="be5c6-152">该文件保存在*应用程序\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="be5c6-152">The file is saved in the *App\_Data* folder.</span></span> <span data-ttu-id="be5c6-153">此文件夹是用于存储数据文件中所述的 ASP.NET 中的特殊文件夹[使用 ASP.NET Web Pages 站点中的数据库简介](https://go.microsoft.com/fwlink/?LinkId=195209)。</span><span class="sxs-lookup"><span data-stu-id="be5c6-153">This folder is a special folder in ASP.NET that's used to store data files, as described in [Introduction to Working with a Database in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=195209).</span></span>

    <span data-ttu-id="be5c6-154">`WriteAllText`方法的`File`对象将数据写入该文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-154">The `WriteAllText` method of the `File` object writes the data to the file.</span></span> <span data-ttu-id="be5c6-155">此方法采用两个参数： 要写入的文件和要写入的实际数据 （包括路径） 的名称。</span><span class="sxs-lookup"><span data-stu-id="be5c6-155">This method takes two parameters: the name (with path) of the file to write to, and the actual data to write.</span></span> <span data-ttu-id="be5c6-156">请注意，第一个参数的名称具有`@`字符作为前缀。</span><span class="sxs-lookup"><span data-stu-id="be5c6-156">Notice that the name of the first parameter has an `@` character as a prefix.</span></span> <span data-ttu-id="be5c6-157">这告诉的 ASP.NET，您要提供逐字字符串文本，并且字符如"/"不应采用专门方法来解释。</span><span class="sxs-lookup"><span data-stu-id="be5c6-157">This tells ASP.NET that you're providing a verbatim string literal, and that characters like "/" should not be interpreted in special ways.</span></span> <span data-ttu-id="be5c6-158">(有关详细信息，请参阅[ASP.NET Web 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)。)</span><span class="sxs-lookup"><span data-stu-id="be5c6-158">(For more information, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    > [!NOTE]
    > <span data-ttu-id="be5c6-159">为你的代码来保存文件的顺序*应用程序\_数据*文件夹中，应用程序需要读写该文件夹的权限。</span><span class="sxs-lookup"><span data-stu-id="be5c6-159">In order for your code to save files in the *App\_Data* folder, the application needs read-write permissions for that folder.</span></span> <span data-ttu-id="be5c6-160">在开发计算机上这不是通常出现问题。</span><span class="sxs-lookup"><span data-stu-id="be5c6-160">On your development computer this is not typically an issue.</span></span> <span data-ttu-id="be5c6-161">但是，当将您的网站发布到宿主提供程序的 web 服务器，您可能需要显式设置这些权限。</span><span class="sxs-lookup"><span data-stu-id="be5c6-161">However, when you publish your site to a hosting provider's web server, you might need to explicitly set those permissions.</span></span> <span data-ttu-id="be5c6-162">如果托管提供商的服务器上运行此代码，并出现错误，请与宿主提供程序中，若要了解如何设置这些权限。</span><span class="sxs-lookup"><span data-stu-id="be5c6-162">If you run this code on a hosting provider's server and get errors, check with the hosting provider to find out how to set those permissions.</span></span>

- <span data-ttu-id="be5c6-163">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="be5c6-163">Run the page in a browser.</span></span> 

    ![](working-with-files/_static/image1.jpg)
- <span data-ttu-id="be5c6-164">在字段中输入值，然后单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="be5c6-164">Enter values into the fields and then click **Submit**.</span></span>
- <span data-ttu-id="be5c6-165">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="be5c6-165">Close the browser.</span></span>
- <span data-ttu-id="be5c6-166">返回到该项目并刷新视图。</span><span class="sxs-lookup"><span data-stu-id="be5c6-166">Return to the project and refresh the view.</span></span>
- <span data-ttu-id="be5c6-167">打开*data.txt*文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-167">Open the *data.txt* file.</span></span> <span data-ttu-id="be5c6-168">在窗体中提交的数据是在文件中。</span><span class="sxs-lookup"><span data-stu-id="be5c6-168">The data you submitted in the form is in the file.</span></span> 

    ![[image]](working-with-files/_static/image2.jpg)
- <span data-ttu-id="be5c6-170">关闭*data.txt*文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-170">Close the *data.txt* file.</span></span>

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a><span data-ttu-id="be5c6-171">将数据追加到现有文件</span><span class="sxs-lookup"><span data-stu-id="be5c6-171">Appending Data to an Existing File</span></span>

<span data-ttu-id="be5c6-172">在上述示例中，您使用`WriteAllText`创建在其中有只是一段数据的文本文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-172">In the previous example, you used `WriteAllText` to create a text file that's got just one piece of data in it.</span></span> <span data-ttu-id="be5c6-173">如果再次调用该方法并将其传递相同的文件名称，是完全覆盖现有文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-173">If you call the method again and pass it the same file name, the existing file is completely overwritten.</span></span> <span data-ttu-id="be5c6-174">但是，创建一个文件后你通常想要将新数据添加到文件末尾。</span><span class="sxs-lookup"><span data-stu-id="be5c6-174">However, after you've created a file you often want to add new data to the end of the file.</span></span> <span data-ttu-id="be5c6-175">您可以执行操作，使用`AppendAllText`方法的`File`对象。</span><span class="sxs-lookup"><span data-stu-id="be5c6-175">You can do that using the `AppendAllText` method of the `File` object.</span></span>

1. <span data-ttu-id="be5c6-176">在网站中，制作一份*UserData.cshtml*文件并将命名该副本*UserDataMultiple.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="be5c6-176">In the website, make a copy of the *UserData.cshtml* file and name the copy *UserDataMultiple.cshtml*.</span></span>
2. <span data-ttu-id="be5c6-177">将打开之前的代码块为`<!DOCTYPE html>`下面的代码块的标记：</span><span class="sxs-lookup"><span data-stu-id="be5c6-177">Replace the code block before the opening `<!DOCTYPE html>` tag with the following code block:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    <span data-ttu-id="be5c6-178">此代码从前一示例中有一项更改。</span><span class="sxs-lookup"><span data-stu-id="be5c6-178">This code has one change in it from the previous example.</span></span> <span data-ttu-id="be5c6-179">而不是使用`WriteAllText`，它使用`the AppendAllText`方法。</span><span class="sxs-lookup"><span data-stu-id="be5c6-179">Instead of using `WriteAllText`, it uses `the AppendAllText` method.</span></span> <span data-ttu-id="be5c6-180">方法非常相似，只不过`AppendAllText`将数据添加到该文件的末尾。</span><span class="sxs-lookup"><span data-stu-id="be5c6-180">The methods are similar, except that `AppendAllText` adds the data to the end of the file.</span></span> <span data-ttu-id="be5c6-181">如同`WriteAllText`，`AppendAllText`创建该文件，如果它尚不存在。</span><span class="sxs-lookup"><span data-stu-id="be5c6-181">As with `WriteAllText`, `AppendAllText` creates the file if it doesn't already exist.</span></span>
3. <span data-ttu-id="be5c6-182">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="be5c6-182">Run the page in a browser.</span></span>
4. <span data-ttu-id="be5c6-183">输入字段的值，然后单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="be5c6-183">Enter values for the fields and then click **Submit**.</span></span>
5. <span data-ttu-id="be5c6-184">添加更多数据并再次提交该窗体。</span><span class="sxs-lookup"><span data-stu-id="be5c6-184">Add more data and submit the form again.</span></span>
6. <span data-ttu-id="be5c6-185">返回到你的项目，右键单击项目文件夹，然后单击**刷新**。</span><span class="sxs-lookup"><span data-stu-id="be5c6-185">Return to your project, right-click the project folder, and then click **Refresh**.</span></span>
7. <span data-ttu-id="be5c6-186">打开*data.txt*文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-186">Open the *data.txt* file.</span></span> <span data-ttu-id="be5c6-187">它现在包含刚才输入的新数据。</span><span class="sxs-lookup"><span data-stu-id="be5c6-187">It now contains the new data that you just entered.</span></span> 

    ![[image]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a><span data-ttu-id="be5c6-189">读取和显示文件中的数据</span><span class="sxs-lookup"><span data-stu-id="be5c6-189">Reading and Displaying Data from a File</span></span>

<span data-ttu-id="be5c6-190">即使您不需要将数据写入到一个文本文件，有时可能需要从一个读取数据。</span><span class="sxs-lookup"><span data-stu-id="be5c6-190">Even if you don't need to write data to a text file, you'll probably sometimes need to read data from one.</span></span> <span data-ttu-id="be5c6-191">若要执行此操作，可以再次使用`File`对象。</span><span class="sxs-lookup"><span data-stu-id="be5c6-191">To do this, you can again use the `File` object.</span></span> <span data-ttu-id="be5c6-192">可以使用`File`对象来单独读取每一行 （由换行符分隔） 或读取无论分隔方式的单个项。</span><span class="sxs-lookup"><span data-stu-id="be5c6-192">You can use the `File` object to read each line individually (separated by line breaks) or to read individual item no matter how they're separated.</span></span>

<span data-ttu-id="be5c6-193">此过程说明了如何将读取并显示在上一示例中创建的数据。</span><span class="sxs-lookup"><span data-stu-id="be5c6-193">This procedure shows you how to read and display the data that you created in the previous example.</span></span>

1. <span data-ttu-id="be5c6-194">在你的网站的根目录，创建名为的新文件*DisplayData.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="be5c6-194">At the root of your website, create a new file named *DisplayData.cshtml*.</span></span>
2. <span data-ttu-id="be5c6-195">使用以下内容替换现有内容：</span><span class="sxs-lookup"><span data-stu-id="be5c6-195">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    <span data-ttu-id="be5c6-196">代码首先读取到变量名为上一示例中创建的文件`userData`，使用此方法调用：</span><span class="sxs-lookup"><span data-stu-id="be5c6-196">The code starts by reading the file that you created in the previous example into a variable named `userData`, using this method call:</span></span>

    [!code-css[Main](working-with-files/samples/sample5.css)]

    <span data-ttu-id="be5c6-197">若要执行此操作的代码位于`if`语句。</span><span class="sxs-lookup"><span data-stu-id="be5c6-197">The code to do this is inside an `if` statement.</span></span> <span data-ttu-id="be5c6-198">当你想要读取的文件时，它是使用一个好办法`File.Exists`方法，以首先确定文件是否可用。</span><span class="sxs-lookup"><span data-stu-id="be5c6-198">When you want to read a file, it's a good idea to use the `File.Exists` method to determine first whether the file is available.</span></span> <span data-ttu-id="be5c6-199">该代码还检查文件是否为空。</span><span class="sxs-lookup"><span data-stu-id="be5c6-199">The code also checks whether the file is empty.</span></span>

    <span data-ttu-id="be5c6-200">页的正文包含两个`foreach`循环，嵌套在另一个。</span><span class="sxs-lookup"><span data-stu-id="be5c6-200">The body of the page contains two `foreach` loops, one nested inside the other.</span></span> <span data-ttu-id="be5c6-201">外部`foreach`循环从数据文件一次获取一行。</span><span class="sxs-lookup"><span data-stu-id="be5c6-201">The outer `foreach` loop gets one line at a time from the data file.</span></span> <span data-ttu-id="be5c6-202">行由换行符的文件中的定义在这种情况下，&#8212;也就是说，每个数据项是在其对应行。</span><span class="sxs-lookup"><span data-stu-id="be5c6-202">In this case, the lines are defined by line breaks in the file &#8212; that is, each data item is on its own line.</span></span> <span data-ttu-id="be5c6-203">外部循环创建新项 (`<li>`元素) 内的排序列表 (`<ol>`元素)。</span><span class="sxs-lookup"><span data-stu-id="be5c6-203">The outer loop creates a new item (`<li>` element) inside an ordered list (`<ol>` element).</span></span>

    <span data-ttu-id="be5c6-204">内部循环将每个数据行拆分成使用逗号作为分隔符的项 （字段）。</span><span class="sxs-lookup"><span data-stu-id="be5c6-204">The inner loop splits each data line into items (fields) using a comma as a delimiter.</span></span> <span data-ttu-id="be5c6-205">(根据前面的示例，这意味着每个行包含三个字段&#8212;名字、 姓氏和电子邮件地址，每个用逗号分隔。)内部循环还会创建`<ul>`列表并显示一个列表项为数据行中的每个字段。</span><span class="sxs-lookup"><span data-stu-id="be5c6-205">(Based on the previous example, this means that each line contains three fields &#8212; the first name, last name, and email address, each separated by a comma.) The inner loop also creates a `<ul>` list and displays one list item for each field in the data line.</span></span>

    <span data-ttu-id="be5c6-206">该代码演示如何使用两种数据类型、 数组和`char`数据类型。</span><span class="sxs-lookup"><span data-stu-id="be5c6-206">The code illustrates how to use two data types, an array and the `char` data type.</span></span> <span data-ttu-id="be5c6-207">该数组是必需的因为`File.ReadAllLines`方法返回为数组的数据。</span><span class="sxs-lookup"><span data-stu-id="be5c6-207">The array is required because the `File.ReadAllLines` method returns data as an array.</span></span> <span data-ttu-id="be5c6-208">`char`数据类型是必需的因为`Split`方法将返回`array`其中每个元素的类型均`char`。</span><span class="sxs-lookup"><span data-stu-id="be5c6-208">The `char` data type is required because the `Split` method returns an `array` in which each element is of the type `char`.</span></span> <span data-ttu-id="be5c6-209">(有关数组的信息，请参阅[ASP.NET Web 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects)。)</span><span class="sxs-lookup"><span data-stu-id="be5c6-209">(For information about arrays, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)</span></span>
3. <span data-ttu-id="be5c6-210">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="be5c6-210">Run the page in a browser.</span></span> <span data-ttu-id="be5c6-211">显示您为前面的示例输入的数据。</span><span class="sxs-lookup"><span data-stu-id="be5c6-211">The data you entered for the previous examples is displayed.</span></span> 

    ![[image]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="be5c6-213">**显示 Microsoft Excel 以逗号分隔文件中的数据**</span><span class="sxs-lookup"><span data-stu-id="be5c6-213">**Displaying Data from a Microsoft Excel Comma-Delimited File**</span></span>
> 
> <span data-ttu-id="be5c6-214">您可以使用 Microsoft Excel 保存为逗号分隔的文件的电子表格中包含的数据 (*.csv*文件)。</span><span class="sxs-lookup"><span data-stu-id="be5c6-214">You can use Microsoft Excel to save the data contained in a spreadsheet as a comma-delimited file (*.csv* file).</span></span> <span data-ttu-id="be5c6-215">执行操作时，该文件保存在纯文本，不以 Excel 格式。</span><span class="sxs-lookup"><span data-stu-id="be5c6-215">When you do, the file is saved in plain text, not in Excel format.</span></span> <span data-ttu-id="be5c6-216">由逗号分隔每个数据项，并且该电子表格中的每一行分隔文本文件，在一个分行符。</span><span class="sxs-lookup"><span data-stu-id="be5c6-216">Each row in the spreadsheet is separated by a line break in the text file, and each data item is separated by a comma.</span></span> <span data-ttu-id="be5c6-217">在前面的示例所示的代码可用于读取 Excel 以逗号分隔文件，只需通过更改在代码中的数据文件的名称。</span><span class="sxs-lookup"><span data-stu-id="be5c6-217">You can use the code shown in the previous example to read an Excel comma-delimited file just by changing the name of the data file in your code.</span></span>


<a id="Deleting_Files"></a>
## <a name="deleting-files"></a><span data-ttu-id="be5c6-218">正在删除文件</span><span class="sxs-lookup"><span data-stu-id="be5c6-218">Deleting Files</span></span>

<span data-ttu-id="be5c6-219">若要从你的网站中删除文件，可以使用`File.Delete`方法。</span><span class="sxs-lookup"><span data-stu-id="be5c6-219">To delete files from your website, you can use the `File.Delete` method.</span></span> <span data-ttu-id="be5c6-220">此过程说明如何以使用户可以删除图像 (*.jpg*文件) 从*映像*文件夹，如果他们知道文件的名称。</span><span class="sxs-lookup"><span data-stu-id="be5c6-220">This procedure shows how to let users delete an image (*.jpg* file) from an *images* folder if they know the name of the file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="be5c6-221">**重要**在生产网站，您通常限制谁有权对数据进行更改。</span><span class="sxs-lookup"><span data-stu-id="be5c6-221">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="be5c6-222">有关如何设置成员资格以及方法可用来授予用户在站点上执行任务的信息，请参阅[添加安全性和 ASP.NET Web Pages 站点的成员身份](https://go.microsoft.com/fwlink/?LinkId=202904)。</span><span class="sxs-lookup"><span data-stu-id="be5c6-222">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>


1. <span data-ttu-id="be5c6-223">在网站中，创建名为的子*映像*。</span><span class="sxs-lookup"><span data-stu-id="be5c6-223">In the website, create a subfolder named *images*.</span></span>
2. <span data-ttu-id="be5c6-224">复制一个或多个 *.jpg*文件到*映像*文件夹。</span><span class="sxs-lookup"><span data-stu-id="be5c6-224">Copy one or more *.jpg* files into the *images* folder.</span></span>
3. <span data-ttu-id="be5c6-225">在该网站的根目录中创建名为的新文件*FileDelete.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="be5c6-225">In the root of the website, create a new file named *FileDelete.cshtml*.</span></span>
4. <span data-ttu-id="be5c6-226">使用以下内容替换现有内容：</span><span class="sxs-lookup"><span data-stu-id="be5c6-226">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    <span data-ttu-id="be5c6-227">此页包含窗体用户可以在其中输入图像文件的名称。</span><span class="sxs-lookup"><span data-stu-id="be5c6-227">This page contains a form where users can enter the name of an image file.</span></span> <span data-ttu-id="be5c6-228">请勿输入 *.jpg*文件扩展名; 通过限制此类的文件名称，来帮助阻止用户删除你的站点上的任意文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-228">They don't enter the *.jpg* file-name extension; by restricting the file name like this, you help prevents users from deleting arbitrary files on your site.</span></span>

    <span data-ttu-id="be5c6-229">代码中读取的文件名称，用户已输入，然后，将构造的完整路径。</span><span class="sxs-lookup"><span data-stu-id="be5c6-229">The code reads the file name that the user has entered and then constructs a complete path.</span></span> <span data-ttu-id="be5c6-230">若要创建该路径，该代码使用当前的网站路径 (如返回的`Server.MapPath`方法)，则*映像*文件夹名称、 用户提供的名称和作为文字字符串".jpg"。</span><span class="sxs-lookup"><span data-stu-id="be5c6-230">To create the path, the code uses the current website path (as returned by the `Server.MapPath` method), the *images* folder name, the name that the user has provided, and ".jpg" as a literal string.</span></span>

    <span data-ttu-id="be5c6-231">若要删除的文件，该代码调用`File.Delete`方法，并向其传递你刚构建的完整路径。</span><span class="sxs-lookup"><span data-stu-id="be5c6-231">To delete the file, the code calls the `File.Delete` method, passing it the full path that you just constructed.</span></span> <span data-ttu-id="be5c6-232">在结束标记时，代码将显示该文件已删除一条确认消息。</span><span class="sxs-lookup"><span data-stu-id="be5c6-232">At the end of the markup, code displays a confirmation message that the file was deleted.</span></span>
5. <span data-ttu-id="be5c6-233">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="be5c6-233">Run the page in a browser.</span></span> 

    ![[image]](working-with-files/_static/image5.jpg)
6. <span data-ttu-id="be5c6-235">输入要删除，然后单击的文件的名称**提交**。</span><span class="sxs-lookup"><span data-stu-id="be5c6-235">Enter the name of the file to delete and then click **Submit**.</span></span> <span data-ttu-id="be5c6-236">如果删除了该文件，在页面底部显示的文件的名称。</span><span class="sxs-lookup"><span data-stu-id="be5c6-236">If the file was deleted, the name of the file is displayed at the bottom of the page.</span></span>

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a><span data-ttu-id="be5c6-237">让用户上传文件</span><span class="sxs-lookup"><span data-stu-id="be5c6-237">Letting Users Upload a File</span></span>

<span data-ttu-id="be5c6-238">`FileUpload`帮助器，用户将文件上传到你的网站。</span><span class="sxs-lookup"><span data-stu-id="be5c6-238">The `FileUpload` helper lets users upload files to your website.</span></span> <span data-ttu-id="be5c6-239">下面的过程演示如何让用户上载的单个文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-239">The procedure below shows you how to let users upload a single file.</span></span>

1. <span data-ttu-id="be5c6-240">将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果您以前未将其添加。</span><span class="sxs-lookup"><span data-stu-id="be5c6-240">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you didn't add it previously.</span></span>
2. <span data-ttu-id="be5c6-241">在中*应用程序\_数据*文件夹中，创建一个新文件夹并将其命名*UploadedFiles*。</span><span class="sxs-lookup"><span data-stu-id="be5c6-241">In the *App\_Data* folder, create a new a folder and name it *UploadedFiles*.</span></span>
3. <span data-ttu-id="be5c6-242">在根目录中创建名为的新文件*FileUpload.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="be5c6-242">In the root, create a new file named *FileUpload.cshtml*.</span></span>
4. <span data-ttu-id="be5c6-243">在页中的现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="be5c6-243">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    <span data-ttu-id="be5c6-244">此页面的正文部分使用`FileUpload`帮助器来创建上传框和按钮，您可能熟悉：</span><span class="sxs-lookup"><span data-stu-id="be5c6-244">The body portion of the page uses the `FileUpload` helper to create the upload box and buttons that you're probably familiar with:</span></span>

    ![[image]](working-with-files/_static/image6.jpg)

    <span data-ttu-id="be5c6-246">有关设置的属性的`FileUpload`帮助器指定你希望提交按钮来读取和你想要上载的文件的单个框**上传**。</span><span class="sxs-lookup"><span data-stu-id="be5c6-246">The properties that you set for the `FileUpload` helper specify that you want a single box for the file to upload and that you want the submit button to read **Upload**.</span></span> <span data-ttu-id="be5c6-247">（你将添加更多框本文后面的部分。）</span><span class="sxs-lookup"><span data-stu-id="be5c6-247">(You'll add more boxes later in the article.)</span></span>

    <span data-ttu-id="be5c6-248">当用户单击**上传**，在页面顶部的代码获取文件，并将其保存。</span><span class="sxs-lookup"><span data-stu-id="be5c6-248">When the user clicks **Upload**, the code at the top of the page gets the file and saves it.</span></span> <span data-ttu-id="be5c6-249">`Request`通常用于从窗体字段中获取值的对象还具有`Files`数组，其中包含文件 （或文件） 的已上传。</span><span class="sxs-lookup"><span data-stu-id="be5c6-249">The `Request` object that you normally use to get values from form fields also has a `Files` array that contains the file (or files) that have been uploaded.</span></span> <span data-ttu-id="be5c6-250">可以获取从数组中的特定位置的单个文件&#8212;例如，若要获取的第一个已上传的文件，则获取`Request.Files[0]`，以获得第二个文件，您获得`Request.Files[1]`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="be5c6-250">You can get individual files out of specific positions in the array &#8212; for example, to get the first uploaded file, you get `Request.Files[0]`, to get the second file, you get `Request.Files[1]`, and so on.</span></span> <span data-ttu-id="be5c6-251">（请记住，在编程中，计数通常从零开始）。</span><span class="sxs-lookup"><span data-stu-id="be5c6-251">(Remember that in programming, counting usually starts at zero.)</span></span>

    <span data-ttu-id="be5c6-252">当提取已上载的文件时，您将其放在变量中 (在这里， `uploadedFile`)，以便可以对其进行操作。</span><span class="sxs-lookup"><span data-stu-id="be5c6-252">When you fetch an uploaded file, you put it in a variable (here, `uploadedFile`) so that you can manipulate it.</span></span> <span data-ttu-id="be5c6-253">若要确定已上传文件的名称，只需获取其`FileName`属性。</span><span class="sxs-lookup"><span data-stu-id="be5c6-253">To determine the name of the uploaded file, you just get its `FileName` property.</span></span> <span data-ttu-id="be5c6-254">但是，当用户将文件上传，`FileName`包含用户的原始名称，其中包括完整路径。</span><span class="sxs-lookup"><span data-stu-id="be5c6-254">However, when the user uploads a file, `FileName` contains the user's original name, which includes the entire path.</span></span> <span data-ttu-id="be5c6-255">它可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="be5c6-255">It might look like this:</span></span>

    <span data-ttu-id="be5c6-256">*C:\Users\Public\Sample.txt*</span><span class="sxs-lookup"><span data-stu-id="be5c6-256">*C:\Users\Public\Sample.txt*</span></span>

    <span data-ttu-id="be5c6-257">但是，因为这是用户的计算机，不适用于你的服务器上的路径，您不希望所有该路径信息。</span><span class="sxs-lookup"><span data-stu-id="be5c6-257">You don't want all that path information, though, because that's the path on the user's computer, not for your server.</span></span> <span data-ttu-id="be5c6-258">你只是想实际文件名称 (*Sample.txt*)。</span><span class="sxs-lookup"><span data-stu-id="be5c6-258">You just want the actual file name (*Sample.txt*).</span></span> <span data-ttu-id="be5c6-259">可以去除使用的只是从路径文件`Path.GetFileName`方法，如下：</span><span class="sxs-lookup"><span data-stu-id="be5c6-259">You can strip out just the file from a path by using the `Path.GetFileName` method, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    <span data-ttu-id="be5c6-260">`Path`对象是一个实用工具，有许多可用于去除路径、 合并路径，而其他操作的此类方法。</span><span class="sxs-lookup"><span data-stu-id="be5c6-260">The `Path` object is a utility that has a number of methods like this that you can use to strip paths, combine paths, and so on.</span></span>

    <span data-ttu-id="be5c6-261">一旦您已经看到了上传的文件的名称，您可以构建你想要将上传的文件存储在你的网站的新路径。</span><span class="sxs-lookup"><span data-stu-id="be5c6-261">Once you've gotten the name of the uploaded file, you can build a new path for where you want to store the uploaded file in your website.</span></span> <span data-ttu-id="be5c6-262">在这种情况下，你将结合`Server.MapPath`，文件夹名称 (*应用程序\_数据/UploadedFiles*)，并要创建新的路径的新去除的文件名称。</span><span class="sxs-lookup"><span data-stu-id="be5c6-262">In this case, you combine `Server.MapPath`, the folder names (*App\_Data/UploadedFiles*), and the newly stripped file name to create a new path.</span></span> <span data-ttu-id="be5c6-263">然后，可以调用已上传的文件的`SaveAs`方法要实际保存该文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-263">You can then call the uploaded file's `SaveAs` method to actually save the file.</span></span>
5. <span data-ttu-id="be5c6-264">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="be5c6-264">Run the page in a browser.</span></span> 

    ![[image]](working-with-files/_static/image7.jpg)
6. <span data-ttu-id="be5c6-266">单击**浏览**，然后选择要上载的文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-266">Click **Browse** and then select a file to upload.</span></span> 

    ![[image]](working-with-files/_static/image8.jpg)

    <span data-ttu-id="be5c6-268">下一步的文本框**浏览**按钮将包含路径和文件位置。</span><span class="sxs-lookup"><span data-stu-id="be5c6-268">The text box next to the **Browse** button will contain the path and file location.</span></span>

    ![[image]](working-with-files/_static/image9.jpg)
7. <span data-ttu-id="be5c6-270">单击“上载” 。</span><span class="sxs-lookup"><span data-stu-id="be5c6-270">Click **Upload**.</span></span>
8. <span data-ttu-id="be5c6-271">在网站中，右键单击项目文件夹，然后依次**刷新**。</span><span class="sxs-lookup"><span data-stu-id="be5c6-271">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="be5c6-272">打开*UploadedFiles*文件夹。</span><span class="sxs-lookup"><span data-stu-id="be5c6-272">Open the *UploadedFiles* folder.</span></span> <span data-ttu-id="be5c6-273">已上传的文件的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="be5c6-273">The file that you uploaded is in the folder.</span></span> 

    ![[image]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a><span data-ttu-id="be5c6-275">让用户上载多个文件</span><span class="sxs-lookup"><span data-stu-id="be5c6-275">Letting Users Upload Multiple Files</span></span>

<span data-ttu-id="be5c6-276">在上一示例中，您可以让用户上载一个文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-276">In the previous example, you let users upload one file.</span></span> <span data-ttu-id="be5c6-277">但您可以使用`FileUpload`帮助器一次上传多个文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-277">But you can use the `FileUpload` helper to upload more than one file at a time.</span></span> <span data-ttu-id="be5c6-278">这非常方便的方案，例如上传的照片，其中一次上载一个文件是枯燥乏味。</span><span class="sxs-lookup"><span data-stu-id="be5c6-278">This is handy for scenarios like uploading photos, where uploading one file at a time is tedious.</span></span> <span data-ttu-id="be5c6-279">(您可以阅读有关上传中的照片[使用 ASP.NET Web Pages 站点中的图像](https://go.microsoft.com/fwlink/?LinkId=202897)。)此示例演示如何以使用户可以上传两个时，虽然可以使用相同的技术来上传更多。</span><span class="sxs-lookup"><span data-stu-id="be5c6-279">(You can read about uploading photos in [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).) This example shows how to let users upload two at a time, although you can use the same technique to upload more than that.</span></span>

1. <span data-ttu-id="be5c6-280">将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未准备好。</span><span class="sxs-lookup"><span data-stu-id="be5c6-280">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="be5c6-281">创建一个名为的新页*FileUploadMultiple.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="be5c6-281">Create a new page named *FileUploadMultiple.cshtml*.</span></span>
3. <span data-ttu-id="be5c6-282">在页中的现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="be5c6-282">Replace the existing content in the page with the following:</span></span>  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    <span data-ttu-id="be5c6-283">在此示例中，`FileUpload`配置页的正文中的帮助程序默认情况下为让用户上载两个文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-283">In this example, the `FileUpload` helper in the body of the page is configured to let users upload two files by default.</span></span> <span data-ttu-id="be5c6-284">因为`allowMoreFilesToBeAdded`设置为`true`，帮助器将呈现一个允许用户将多个上传框添加链接：</span><span class="sxs-lookup"><span data-stu-id="be5c6-284">Because `allowMoreFilesToBeAdded` is set to `true`, the helper renders a link that lets user add more upload boxes:</span></span>

    ![[image]](working-with-files/_static/image11.jpg)

    <span data-ttu-id="be5c6-286">若要处理在用户上传的文件，该代码使用上一示例中使用的相同基本方法&#8212;获取文件从`Request.Files`然后将其保存。</span><span class="sxs-lookup"><span data-stu-id="be5c6-286">To process the files that the user uploads, the code uses the same basic technique that you used in the previous example &#8212; get a file from `Request.Files` and then save it.</span></span> <span data-ttu-id="be5c6-287">（包括各种内容需要执行操作以获取正确的文件名称和路径。）这一次的创新是用户可能多个文件上传并不知道很多。</span><span class="sxs-lookup"><span data-stu-id="be5c6-287">(Including the various things you need to do to get the right file name and path.) The innovation this time is that the user might be uploading multiple files and you don't know many.</span></span> <span data-ttu-id="be5c6-288">若要了解，可以获取`Request.Files.Count`。</span><span class="sxs-lookup"><span data-stu-id="be5c6-288">To find out, you can get `Request.Files.Count`.</span></span>

    <span data-ttu-id="be5c6-289">使用此数字后，您可以循环访问`Request.Files`、 依次提取每个文件并将其保存。</span><span class="sxs-lookup"><span data-stu-id="be5c6-289">With this number in hand, you can loop through `Request.Files`, fetch each file in turn, and save it.</span></span> <span data-ttu-id="be5c6-290">当你想要循环通过一组已知的次数时，可以使用`for`循环，如下：</span><span class="sxs-lookup"><span data-stu-id="be5c6-290">When you want to loop a known number of times through a collection, you can use a `for` loop, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    <span data-ttu-id="be5c6-291">该变量`i`是只是临时计数器，它会从零到任何你设置的上限。</span><span class="sxs-lookup"><span data-stu-id="be5c6-291">The variable `i` is just a temporary counter that will go from zero to whatever upper limit you set.</span></span> <span data-ttu-id="be5c6-292">在这种情况下，上限为的文件数。</span><span class="sxs-lookup"><span data-stu-id="be5c6-292">In this case, the upper limit is the number of files.</span></span> <span data-ttu-id="be5c6-293">但由于该计数器从零，因为是典型的计数在 ASP.NET 中的方案开始的上限值实际是一个小于该文件数。</span><span class="sxs-lookup"><span data-stu-id="be5c6-293">But because the counter starts at zero, as is typical for counting scenarios in ASP.NET, the upper limit is actually one less than the file count.</span></span> <span data-ttu-id="be5c6-294">（如果三个文件上传时，计数为零到 2。）</span><span class="sxs-lookup"><span data-stu-id="be5c6-294">(If three files are uploaded, the count is zero to 2.)</span></span>

    <span data-ttu-id="be5c6-295">`uploadedCount`变量进行合计已成功上传并保存的所有文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-295">The `uploadedCount` variable totals all the files that are successfully uploaded and saved.</span></span> <span data-ttu-id="be5c6-296">此代码帐户所需的文件可能无法上传的可能性。</span><span class="sxs-lookup"><span data-stu-id="be5c6-296">This code accounts for the possibility that an expected file may not be able to be uploaded.</span></span>
4. <span data-ttu-id="be5c6-297">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="be5c6-297">Run the page in a browser.</span></span> <span data-ttu-id="be5c6-298">在浏览器显示页面和其上传两个框。</span><span class="sxs-lookup"><span data-stu-id="be5c6-298">The browser displays the page and its two upload boxes.</span></span>
5. <span data-ttu-id="be5c6-299">选择要上传的两个文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-299">Select two files to upload.</span></span>
6. <span data-ttu-id="be5c6-300">单击**添加另一个文件**。</span><span class="sxs-lookup"><span data-stu-id="be5c6-300">Click **Add another file**.</span></span> <span data-ttu-id="be5c6-301">该页将显示一个新的上传框。</span><span class="sxs-lookup"><span data-stu-id="be5c6-301">The page displays a new upload box.</span></span> 

    ![[image]](working-with-files/_static/image12.jpg)
7. <span data-ttu-id="be5c6-303">单击“上载” 。</span><span class="sxs-lookup"><span data-stu-id="be5c6-303">Click **Upload**.</span></span>
8. <span data-ttu-id="be5c6-304">在网站中，右键单击项目文件夹，然后依次**刷新**。</span><span class="sxs-lookup"><span data-stu-id="be5c6-304">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="be5c6-305">打开*UploadedFiles*文件夹，以查看已成功上传的文件。</span><span class="sxs-lookup"><span data-stu-id="be5c6-305">Open the *UploadedFiles* folder to see the successfully uploaded files.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="be5c6-306">其他资源</span><span class="sxs-lookup"><span data-stu-id="be5c6-306">Additional Resources</span></span>


[<span data-ttu-id="be5c6-307">使用 ASP.NET Web Pages 站点中的图像</span><span class="sxs-lookup"><span data-stu-id="be5c6-307">Working with Images in an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkId=202897)

[<span data-ttu-id="be5c6-308">导出到 CSV 文件</span><span class="sxs-lookup"><span data-stu-id="be5c6-308">Exporting to a CSV File</span></span>](https://msdn.microsoft.com/library/ms155919.aspx)
