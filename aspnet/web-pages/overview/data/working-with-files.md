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
<a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET Web Pages (Razor) 站点中使用文件
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 此文章介绍了如何读取、 写入、 追加、 删除和将 ASP.NET Web Pages (Razor) 站点中的文件上传。
> 
> > [!NOTE]
> > 如果你想要将图像上传并对其进行处理 （例如，翻转或调整其大小），请参阅[使用 ASP.NET Web Pages 站点中的图像](https://go.microsoft.com/fwlink/?LinkId=202897)。
> 
> 
> **你将学习：** 
> 
> - 了解如何创建一个文本文件并向其写入数据。
> - 如何将数据追加到现有文件。
> - 了解如何读取文件并从其显示。
> - 如何从网站中删除文件。
> - 如何让用户上传一个或多个文件。
> 
> 这些是 ASP.NET 编程一文中引入的功能：
> 
> - `File`对象，它提供一种方法来管理文件。
> - `FileUpload`帮助器。
> - `Path`对象，它提供可用于操作路径和文件名的方法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 2
> - WebMatrix 2
>   
> 
> 本教程还适用于 WebMatrix 3。


<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a>创建一个文本文件并向其中写入数据

除了在你的网站中使用的数据库，您可能会处理文件。 例如，你可能会使用文本文件作为存储站点数据的简单方法。 (有时称为用来存储数据的文本文件*平面文件*。)文本文件可以采用不同格式，如 *.txt*， *.xml*，或 *.csv* （以逗号分隔值）。

如果你想要将数据存储在文本文件中，则可以使用`File.WriteAllText`方法，以指定要创建的文件和要向其中写入的数据。 在此过程中，你将创建包含具有三个简单的窗体的页面`input`元素 （名字、 姓氏和电子邮件地址） 和一个**提交**按钮。 当用户提交窗体时，想要在文本文件中保存用户的输入。

1. 创建一个名为的新文件夹*应用程序\_数据*，如果它尚未存在。
2. 在你的网站的根目录，创建名为的新文件*UserData.cshtml*。
3. 使用以下内容替换现有内容： 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    HTML 标记创建具有三个文本框中的窗体。 在代码中，您使用`IsPost`属性来确定页是否已提交之前开始处理。

    第一个任务是获取用户输入，并将其分配给变量。 代码然后将不同的变量的值连接成一个以逗号分隔的字符串，然后存储在不同的变量。 请注意，逗号分隔符是包含在引号中的字符串 （"，"），因为按字面意思逗号嵌入到你要创建的大字符串。 在串联在一起的数据结束时，您将添加`Environment.NewLine`。 这会添加一个分行符 （换行符）。 您创建此连接是一个字符串，如下所示：

    [!code-css[Main](working-with-files/samples/sample2.css)]

    （使用一个不可见的换行符结束时。）

    然后创建一个变量 (`dataFile`)，其中包含的位置和存储中的数据的文件的名称。 将位置设置需要一些特殊的处理。 在网站中它是个好办法在代码中引用为绝对路径，如*C:\Folder\File.txt* web 服务器上的文件。 如果移动网站，则会不正确的绝对路径。 此外，为托管站点 （与用于在你自己的计算机上） 通常不甚至知道正确的路径是当您编写的代码。

    但有时 （例如 now，用于写入一个文件)，则需要完整路径。 解决方法是使用`MapPath`方法的`Server`对象。 这将返回到你的网站的完整路径。 若要获取网站根目录，你的用户的路径`~`运算符 (站点来表示您的虚拟根) 到`MapPath`。 (你还可以传递一个子文件夹名称到它，如 *~/App\_数据 /*，以获取此子文件夹的路径。)然后可以连接到任何方法返回若要创建的完整路径上的其他信息。 在此示例中，添加的文件名称。 (您可以阅读更多有关如何处理中的文件和文件夹路径[ASP.NET Web Pages 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)。)

    该文件保存在*应用程序\_数据*文件夹。 此文件夹是用于存储数据文件中所述的 ASP.NET 中的特殊文件夹[使用 ASP.NET Web Pages 站点中的数据库简介](https://go.microsoft.com/fwlink/?LinkId=195209)。

    `WriteAllText`方法的`File`对象将数据写入该文件。 此方法采用两个参数： 要写入的文件和要写入的实际数据 （包括路径） 的名称。 请注意，第一个参数的名称具有`@`字符作为前缀。 这告诉的 ASP.NET，您要提供逐字字符串文本，并且字符如"/"不应采用专门方法来解释。 (有关详细信息，请参阅[ASP.NET Web 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)。)

    > [!NOTE]
    > 为你的代码来保存文件的顺序*应用程序\_数据*文件夹中，应用程序需要读写该文件夹的权限。 在开发计算机上这不是通常出现问题。 但是，当将您的网站发布到宿主提供程序的 web 服务器，您可能需要显式设置这些权限。 如果托管提供商的服务器上运行此代码，并出现错误，请与宿主提供程序中，若要了解如何设置这些权限。

- 在浏览器中运行页。 

    ![](working-with-files/_static/image1.jpg)
- 在字段中输入值，然后单击**提交**。
- 关闭浏览器。
- 返回到该项目并刷新视图。
- 打开*data.txt*文件。 在窗体中提交的数据是在文件中。 

    ![[image]](working-with-files/_static/image2.jpg)
- 关闭*data.txt*文件。

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a>将数据追加到现有文件

在上述示例中，您使用`WriteAllText`创建在其中有只是一段数据的文本文件。 如果再次调用该方法并将其传递相同的文件名称，是完全覆盖现有文件。 但是，创建一个文件后你通常想要将新数据添加到文件末尾。 您可以执行操作，使用`AppendAllText`方法的`File`对象。

1. 在网站中，制作一份*UserData.cshtml*文件并将命名该副本*UserDataMultiple.cshtml*。
2. 将打开之前的代码块为`<!DOCTYPE html>`下面的代码块的标记： 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    此代码从前一示例中有一项更改。 而不是使用`WriteAllText`，它使用`the AppendAllText`方法。 方法非常相似，只不过`AppendAllText`将数据添加到该文件的末尾。 如同`WriteAllText`，`AppendAllText`创建该文件，如果它尚不存在。
3. 在浏览器中运行页。
4. 输入字段的值，然后单击**提交**。
5. 添加更多数据并再次提交该窗体。
6. 返回到你的项目，右键单击项目文件夹，然后单击**刷新**。
7. 打开*data.txt*文件。 它现在包含刚才输入的新数据。 

    ![[image]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a>读取和显示文件中的数据

即使您不需要将数据写入到一个文本文件，有时可能需要从一个读取数据。 若要执行此操作，可以再次使用`File`对象。 可以使用`File`对象来单独读取每一行 （由换行符分隔） 或读取无论分隔方式的单个项。

此过程说明了如何将读取并显示在上一示例中创建的数据。

1. 在你的网站的根目录，创建名为的新文件*DisplayData.cshtml*。
2. 使用以下内容替换现有内容： 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    代码首先读取到变量名为上一示例中创建的文件`userData`，使用此方法调用：

    [!code-css[Main](working-with-files/samples/sample5.css)]

    若要执行此操作的代码位于`if`语句。 当你想要读取的文件时，它是使用一个好办法`File.Exists`方法，以首先确定文件是否可用。 该代码还检查文件是否为空。

    页的正文包含两个`foreach`循环，嵌套在另一个。 外部`foreach`循环从数据文件一次获取一行。 行由换行符的文件中的定义在这种情况下，&#8212;也就是说，每个数据项是在其对应行。 外部循环创建新项 (`<li>`元素) 内的排序列表 (`<ol>`元素)。

    内部循环将每个数据行拆分成使用逗号作为分隔符的项 （字段）。 (根据前面的示例，这意味着每个行包含三个字段&#8212;名字、 姓氏和电子邮件地址，每个用逗号分隔。)内部循环还会创建`<ul>`列表并显示一个列表项为数据行中的每个字段。

    该代码演示如何使用两种数据类型、 数组和`char`数据类型。 该数组是必需的因为`File.ReadAllLines`方法返回为数组的数据。 `char`数据类型是必需的因为`Split`方法将返回`array`其中每个元素的类型均`char`。 (有关数组的信息，请参阅[ASP.NET Web 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects)。)
3. 在浏览器中运行页。 显示您为前面的示例输入的数据。 

    ![[image]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> **显示 Microsoft Excel 以逗号分隔文件中的数据**
> 
> 您可以使用 Microsoft Excel 保存为逗号分隔的文件的电子表格中包含的数据 (*.csv*文件)。 执行操作时，该文件保存在纯文本，不以 Excel 格式。 由逗号分隔每个数据项，并且该电子表格中的每一行分隔文本文件，在一个分行符。 在前面的示例所示的代码可用于读取 Excel 以逗号分隔文件，只需通过更改在代码中的数据文件的名称。


<a id="Deleting_Files"></a>
## <a name="deleting-files"></a>正在删除文件

若要从你的网站中删除文件，可以使用`File.Delete`方法。 此过程说明如何以使用户可以删除图像 (*.jpg*文件) 从*映像*文件夹，如果他们知道文件的名称。

> [!NOTE] 
> 
> **重要**在生产网站，您通常限制谁有权对数据进行更改。 有关如何设置成员资格以及方法可用来授予用户在站点上执行任务的信息，请参阅[添加安全性和 ASP.NET Web Pages 站点的成员身份](https://go.microsoft.com/fwlink/?LinkId=202904)。


1. 在网站中，创建名为的子*映像*。
2. 复制一个或多个 *.jpg*文件到*映像*文件夹。
3. 在该网站的根目录中创建名为的新文件*FileDelete.cshtml*。
4. 使用以下内容替换现有内容： 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    此页包含窗体用户可以在其中输入图像文件的名称。 请勿输入 *.jpg*文件扩展名; 通过限制此类的文件名称，来帮助阻止用户删除你的站点上的任意文件。

    代码中读取的文件名称，用户已输入，然后，将构造的完整路径。 若要创建该路径，该代码使用当前的网站路径 (如返回的`Server.MapPath`方法)，则*映像*文件夹名称、 用户提供的名称和作为文字字符串".jpg"。

    若要删除的文件，该代码调用`File.Delete`方法，并向其传递你刚构建的完整路径。 在结束标记时，代码将显示该文件已删除一条确认消息。
5. 在浏览器中运行页。 

    ![[image]](working-with-files/_static/image5.jpg)
6. 输入要删除，然后单击的文件的名称**提交**。 如果删除了该文件，在页面底部显示的文件的名称。

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a>让用户上传文件

`FileUpload`帮助器，用户将文件上传到你的网站。 下面的过程演示如何让用户上载的单个文件。

1. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果您以前未将其添加。
2. 在中*应用程序\_数据*文件夹中，创建一个新文件夹并将其命名*UploadedFiles*。
3. 在根目录中创建名为的新文件*FileUpload.cshtml*。
4. 在页中的现有内容替换为以下： 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    此页面的正文部分使用`FileUpload`帮助器来创建上传框和按钮，您可能熟悉：

    ![[image]](working-with-files/_static/image6.jpg)

    有关设置的属性的`FileUpload`帮助器指定你希望提交按钮来读取和你想要上载的文件的单个框**上传**。 （你将添加更多框本文后面的部分。）

    当用户单击**上传**，在页面顶部的代码获取文件，并将其保存。 `Request`通常用于从窗体字段中获取值的对象还具有`Files`数组，其中包含文件 （或文件） 的已上传。 可以获取从数组中的特定位置的单个文件&#8212;例如，若要获取的第一个已上传的文件，则获取`Request.Files[0]`，以获得第二个文件，您获得`Request.Files[1]`，依次类推。 （请记住，在编程中，计数通常从零开始）。

    当提取已上载的文件时，您将其放在变量中 (在这里， `uploadedFile`)，以便可以对其进行操作。 若要确定已上传文件的名称，只需获取其`FileName`属性。 但是，当用户将文件上传，`FileName`包含用户的原始名称，其中包括完整路径。 它可能如下所示：

    *C:\Users\Public\Sample.txt*

    但是，因为这是用户的计算机，不适用于你的服务器上的路径，您不希望所有该路径信息。 你只是想实际文件名称 (*Sample.txt*)。 可以去除使用的只是从路径文件`Path.GetFileName`方法，如下：

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    `Path`对象是一个实用工具，有许多可用于去除路径、 合并路径，而其他操作的此类方法。

    一旦您已经看到了上传的文件的名称，您可以构建你想要将上传的文件存储在你的网站的新路径。 在这种情况下，你将结合`Server.MapPath`，文件夹名称 (*应用程序\_数据/UploadedFiles*)，并要创建新的路径的新去除的文件名称。 然后，可以调用已上传的文件的`SaveAs`方法要实际保存该文件。
5. 在浏览器中运行页。 

    ![[image]](working-with-files/_static/image7.jpg)
6. 单击**浏览**，然后选择要上载的文件。 

    ![[image]](working-with-files/_static/image8.jpg)

    下一步的文本框**浏览**按钮将包含路径和文件位置。

    ![[image]](working-with-files/_static/image9.jpg)
7. 单击“上载” 。
8. 在网站中，右键单击项目文件夹，然后依次**刷新**。
9. 打开*UploadedFiles*文件夹。 已上传的文件的文件夹中。 

    ![[image]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a>让用户上载多个文件

在上一示例中，您可以让用户上载一个文件。 但您可以使用`FileUpload`帮助器一次上传多个文件。 这非常方便的方案，例如上传的照片，其中一次上载一个文件是枯燥乏味。 (您可以阅读有关上传中的照片[使用 ASP.NET Web Pages 站点中的图像](https://go.microsoft.com/fwlink/?LinkId=202897)。)此示例演示如何以使用户可以上传两个时，虽然可以使用相同的技术来上传更多。

1. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未准备好。
2. 创建一个名为的新页*FileUploadMultiple.cshtml*。
3. 在页中的现有内容替换为以下：  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    在此示例中，`FileUpload`配置页的正文中的帮助程序默认情况下为让用户上载两个文件。 因为`allowMoreFilesToBeAdded`设置为`true`，帮助器将呈现一个允许用户将多个上传框添加链接：

    ![[image]](working-with-files/_static/image11.jpg)

    若要处理在用户上传的文件，该代码使用上一示例中使用的相同基本方法&#8212;获取文件从`Request.Files`然后将其保存。 （包括各种内容需要执行操作以获取正确的文件名称和路径。）这一次的创新是用户可能多个文件上传并不知道很多。 若要了解，可以获取`Request.Files.Count`。

    使用此数字后，您可以循环访问`Request.Files`、 依次提取每个文件并将其保存。 当你想要循环通过一组已知的次数时，可以使用`for`循环，如下：

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    该变量`i`是只是临时计数器，它会从零到任何你设置的上限。 在这种情况下，上限为的文件数。 但由于该计数器从零，因为是典型的计数在 ASP.NET 中的方案开始的上限值实际是一个小于该文件数。 （如果三个文件上传时，计数为零到 2。）

    `uploadedCount`变量进行合计已成功上传并保存的所有文件。 此代码帐户所需的文件可能无法上传的可能性。
4. 在浏览器中运行页。 在浏览器显示页面和其上传两个框。
5. 选择要上传的两个文件。
6. 单击**添加另一个文件**。 该页将显示一个新的上传框。 

    ![[image]](working-with-files/_static/image12.jpg)
7. 单击“上载” 。
8. 在网站中，右键单击项目文件夹，然后依次**刷新**。
9. 打开*UploadedFiles*文件夹，以查看已成功上传的文件。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源


[使用 ASP.NET Web Pages 站点中的图像](https://go.microsoft.com/fwlink/?LinkId=202897)

[导出到 CSV 文件](https://msdn.microsoft.com/library/ms155919.aspx)
