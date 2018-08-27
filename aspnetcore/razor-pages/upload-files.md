---
title: 将文件上传到 ASP.NET Core 中的 Razor 页面
author: guardrex
description: 了解如何将文件上传至 Razor 页面。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 07/11/2018
uid: razor-pages/upload-files
ms.openlocfilehash: 4b2f80cd5644cf21d5d8452aff6df4eb5591d41b
ms.sourcegitcommit: 19cbda409bdbbe42553dc385ea72d2a8e246509c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "42909253"
---
# <a name="upload-files-to-a-razor-page-in-aspnet-core"></a><span data-ttu-id="98062-103">将文件上传到 ASP.NET Core 中的 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="98062-103">Upload files to a Razor Page in ASP.NET Core</span></span>

<span data-ttu-id="98062-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="98062-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="98062-105">本主题是基于[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample)中<xref:tutorials/razor-pages/razor-pages-start>。</span><span class="sxs-lookup"><span data-stu-id="98062-105">This topic builds upon the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample) in <xref:tutorials/razor-pages/razor-pages-start>.</span></span>

<span data-ttu-id="98062-106">本主题演示如何使用简单的模型绑定来上传文件，这非常适合上传小文件。</span><span class="sxs-lookup"><span data-stu-id="98062-106">This topic shows how to use simple model binding to upload files, which works well for uploading small files.</span></span> <span data-ttu-id="98062-107">有关流式传输大文件的信息，请参阅[通过流式传输上传大文件](xref:mvc/models/file-uploads#uploading-large-files-with-streaming)。</span><span class="sxs-lookup"><span data-stu-id="98062-107">For information on streaming large files, see [Uploading large files with streaming](xref:mvc/models/file-uploads#uploading-large-files-with-streaming).</span></span>

<span data-ttu-id="98062-108">在下列步骤中，向示例应用添加电影计划文件上传功能。</span><span class="sxs-lookup"><span data-stu-id="98062-108">In the following steps, a movie schedule file upload feature is added to the sample app.</span></span> <span data-ttu-id="98062-109">每个电影计划由一个 `Schedule` 类表示。</span><span class="sxs-lookup"><span data-stu-id="98062-109">A movie schedule is represented by a `Schedule` class.</span></span> <span data-ttu-id="98062-110">该类包括两个版本的计划。</span><span class="sxs-lookup"><span data-stu-id="98062-110">The class includes two versions of the schedule.</span></span> <span data-ttu-id="98062-111">其中一个版本 (`PublicSchedule`) 提供给客户。</span><span class="sxs-lookup"><span data-stu-id="98062-111">One version is provided to customers, `PublicSchedule`.</span></span> <span data-ttu-id="98062-112">另一个版本 (`PrivateSchedule`) 用于公司员工。</span><span class="sxs-lookup"><span data-stu-id="98062-112">The other version is used for company employees, `PrivateSchedule`.</span></span> <span data-ttu-id="98062-113">每个版本作为单独的文件进行上传。</span><span class="sxs-lookup"><span data-stu-id="98062-113">Each version is uploaded as a separate file.</span></span> <span data-ttu-id="98062-114">本教程演示如何通过单个 POST 将两个文件上传至服务器。</span><span class="sxs-lookup"><span data-stu-id="98062-114">The tutorial demonstrates how to perform two file uploads from a page with a single POST to the server.</span></span>

## <a name="security-considerations"></a><span data-ttu-id="98062-115">安全注意事项</span><span class="sxs-lookup"><span data-stu-id="98062-115">Security considerations</span></span>

<span data-ttu-id="98062-116">向用户提供向服务器上传文件的功能时，必须格外小心。</span><span class="sxs-lookup"><span data-stu-id="98062-116">Caution must be taken when providing users with the ability to upload files to a server.</span></span> <span data-ttu-id="98062-117">攻击者可能对系统执行[拒绝服务](/windows-hardware/drivers/ifs/denial-of-service)和其他攻击。</span><span class="sxs-lookup"><span data-stu-id="98062-117">Attackers may execute [denial of service](/windows-hardware/drivers/ifs/denial-of-service) and other attacks on a system.</span></span> <span data-ttu-id="98062-118">一些降低成功攻击可能性的安全措施如下：</span><span class="sxs-lookup"><span data-stu-id="98062-118">Some security steps that reduce the likelihood of a successful attack are:</span></span>

* <span data-ttu-id="98062-119">将文件上传到系统上的专用文件上传区域，这样可以更轻松地对上传内容实施安全措施。</span><span class="sxs-lookup"><span data-stu-id="98062-119">Upload files to a dedicated file upload area on the system, which makes it easier to impose security measures on uploaded content.</span></span> <span data-ttu-id="98062-120">如果允许文件上传，请确保在上传位置禁用执行权限。</span><span class="sxs-lookup"><span data-stu-id="98062-120">When permitting file uploads, make sure that execute permissions are disabled on the upload location.</span></span>
* <span data-ttu-id="98062-121">使用由应用确定的安全文件名，而不是采用用户输入或已上传文件的文件名。</span><span class="sxs-lookup"><span data-stu-id="98062-121">Use a safe file name determined by the app, not from user input or the file name of the uploaded file.</span></span>
* <span data-ttu-id="98062-122">仅允许使用一组特定的已批准文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="98062-122">Only allow a specific set of approved file extensions.</span></span>
* <span data-ttu-id="98062-123">验证是否在服务器上执行了客户端检查。</span><span class="sxs-lookup"><span data-stu-id="98062-123">Verify client-side checks are performed on the server.</span></span> <span data-ttu-id="98062-124">客户端检查很容易规避。</span><span class="sxs-lookup"><span data-stu-id="98062-124">Client-side checks are easy to circumvent.</span></span>
* <span data-ttu-id="98062-125">检查上传文件大小，防止上传比预期大的文件。</span><span class="sxs-lookup"><span data-stu-id="98062-125">Check the size of the upload and prevent larger uploads than expected.</span></span>
* <span data-ttu-id="98062-126">对上传的内容运行病毒/恶意软件扫描程序。</span><span class="sxs-lookup"><span data-stu-id="98062-126">Run a virus/malware scanner on uploaded content.</span></span>

> [!WARNING]
> <span data-ttu-id="98062-127">将恶意代码上传到系统通常是执行代码的第一步，这些代码可以：</span><span class="sxs-lookup"><span data-stu-id="98062-127">Uploading malicious code to a system is frequently the first step to executing code that can:</span></span>
> * <span data-ttu-id="98062-128">完全接管系统。</span><span class="sxs-lookup"><span data-stu-id="98062-128">Completely takeover a system.</span></span>
> * <span data-ttu-id="98062-129">重载系统，导致系统完全崩溃。</span><span class="sxs-lookup"><span data-stu-id="98062-129">Overload a system with the result that the system completely fails.</span></span>
> * <span data-ttu-id="98062-130">泄露用户或系统数据。</span><span class="sxs-lookup"><span data-stu-id="98062-130">Compromise user or system data.</span></span>
> * <span data-ttu-id="98062-131">将涂鸦应用于公共接口。</span><span class="sxs-lookup"><span data-stu-id="98062-131">Apply graffiti to a public interface.</span></span>

## <a name="add-a-fileupload-class"></a><span data-ttu-id="98062-132">添加 FileUpload 类</span><span class="sxs-lookup"><span data-stu-id="98062-132">Add a FileUpload class</span></span>

<span data-ttu-id="98062-133">创建 Razor 页以处理一对文件上传。</span><span class="sxs-lookup"><span data-stu-id="98062-133">Create a Razor Page to handle a pair of file uploads.</span></span> <span data-ttu-id="98062-134">添加 `FileUpload` 类（此类与页面绑定以获取计划数据）。</span><span class="sxs-lookup"><span data-stu-id="98062-134">Add a `FileUpload` class, which is bound to the page to obtain the schedule data.</span></span> <span data-ttu-id="98062-135">右键单击“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="98062-135">Right click the *Models* folder.</span></span> <span data-ttu-id="98062-136">选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="98062-136">Select **Add** > **Class**.</span></span> <span data-ttu-id="98062-137">将类命名为“FileUpload”，并添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="98062-137">Name the class **FileUpload** and add the following properties:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](upload-files/samples/2.x/RazorPagesMovie/Models/FileUpload.cs)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](upload-files/samples/1.x/RazorPagesMovie/Models/FileUpload.cs)]

::: moniker-end

<span data-ttu-id="98062-138">此类有一个属性对应计划标题，另各有一个属性对应计划的两个版本。</span><span class="sxs-lookup"><span data-stu-id="98062-138">The class has a property for the schedule's title and a property for each of the two versions of the schedule.</span></span> <span data-ttu-id="98062-139">3 个属性皆为必需属性，标题长度必须为 3-60 个字符。</span><span class="sxs-lookup"><span data-stu-id="98062-139">All three properties are required, and the title must be 3-60 characters long.</span></span>

## <a name="add-a-helper-method-to-upload-files"></a><span data-ttu-id="98062-140">添加用于上传文件的 helper 方法</span><span class="sxs-lookup"><span data-stu-id="98062-140">Add a helper method to upload files</span></span>

<span data-ttu-id="98062-141">为避免处理未上传计划文件时出现代码重复，请首先上传一个静态 helper 方法。</span><span class="sxs-lookup"><span data-stu-id="98062-141">To avoid code duplication for processing uploaded schedule files, add a static helper method first.</span></span> <span data-ttu-id="98062-142">在此应用中创建一个“Utilities”文件夹，然后在“FileHelpers.cs”文件中添加以下内容。</span><span class="sxs-lookup"><span data-stu-id="98062-142">Create a *Utilities* folder in the app and add a *FileHelpers.cs* file with the following content.</span></span> <span data-ttu-id="98062-143">helper 方法 `ProcessFormFile` 接受 [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) 和 [ModelStateDictionary](/api/microsoft.aspnetcore.mvc.modelbinding.modelstatedictionary)，并返回包含文件大小和内容的字符串。</span><span class="sxs-lookup"><span data-stu-id="98062-143">The helper method, `ProcessFormFile`, takes an [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) and [ModelStateDictionary](/api/microsoft.aspnetcore.mvc.modelbinding.modelstatedictionary) and returns a string containing the file's size and content.</span></span> <span data-ttu-id="98062-144">检查内容类型和长度。</span><span class="sxs-lookup"><span data-stu-id="98062-144">The content type and length are checked.</span></span> <span data-ttu-id="98062-145">如果文件未通过验证检查，将向 `ModelState` 添加一个错误。</span><span class="sxs-lookup"><span data-stu-id="98062-145">If the file doesn't pass a validation check, an error is added to the `ModelState`.</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](upload-files/samples/2.x/RazorPagesMovie/Utilities/FileHelpers.cs)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](upload-files/samples/1.x/RazorPagesMovie/Utilities/FileHelpers.cs)]

::: moniker-end

### <a name="save-the-file-to-disk"></a><span data-ttu-id="98062-146">将文件保存到磁盘</span><span class="sxs-lookup"><span data-stu-id="98062-146">Save the file to disk</span></span>

<span data-ttu-id="98062-147">示例应用将已上传的文件保存到数据库字段中。</span><span class="sxs-lookup"><span data-stu-id="98062-147">The sample app saves uploaded files into database fields.</span></span> <span data-ttu-id="98062-148">要将文件保存到磁盘，请使用 [FileStream](/dotnet/api/system.io.filestream)。</span><span class="sxs-lookup"><span data-stu-id="98062-148">To save a file to disk, use a [FileStream](/dotnet/api/system.io.filestream).</span></span> <span data-ttu-id="98062-149">以下示例将 `FileUpload.UploadPublicSchedule` 所保存的文件复制到 `OnPostAsync` 方法中的 `FileStream`。</span><span class="sxs-lookup"><span data-stu-id="98062-149">The following example copies a file held by `FileUpload.UploadPublicSchedule` to a `FileStream` in an `OnPostAsync` method.</span></span> <span data-ttu-id="98062-150">`FileStream` 将文件写入 `<PATH-AND-FILE-NAME>` 提供的磁盘：</span><span class="sxs-lookup"><span data-stu-id="98062-150">The `FileStream` writes the file to disk at the `<PATH-AND-FILE-NAME>` provided:</span></span>

```csharp
public async Task<IActionResult> OnPostAsync()
{
    // Perform an initial check to catch FileUpload class attribute violations.
    if (!ModelState.IsValid)
    {
        return Page();
    }

    var filePath = "<PATH-AND-FILE-NAME>";

    using (var fileStream = new FileStream(filePath, FileMode.Create))
    {
        await FileUpload.UploadPublicSchedule.CopyToAsync(fileStream);
    }

    return RedirectToPage("./Index");
}
```

<span data-ttu-id="98062-151">工作进程必须对 `filePath` 指定的位置具有写入权限。</span><span class="sxs-lookup"><span data-stu-id="98062-151">The worker process must have write permissions to the location specified by `filePath`.</span></span>

> [!NOTE]
> <span data-ttu-id="98062-152">`filePath` 必须包含文件名。</span><span class="sxs-lookup"><span data-stu-id="98062-152">The `filePath` *must* include the file name.</span></span> <span data-ttu-id="98062-153">如果未提供文件名，则会在运行时引发 [UnauthorizedAccessException](/dotnet/api/system.unauthorizedaccessexception)。</span><span class="sxs-lookup"><span data-stu-id="98062-153">If the file name isn't provided, an [UnauthorizedAccessException](/dotnet/api/system.unauthorizedaccessexception) is thrown at runtime.</span></span>

> [!WARNING]
> <span data-ttu-id="98062-154">切勿将上传的文件保存在与应用相同的目录树中。</span><span class="sxs-lookup"><span data-stu-id="98062-154">Never persist uploaded files in the same directory tree as the app.</span></span>
>
> <span data-ttu-id="98062-155">代码示例不提供针对恶意文件上传的服务器端保护。</span><span class="sxs-lookup"><span data-stu-id="98062-155">The code sample provides no server-side protection against malicious file uploads.</span></span> <span data-ttu-id="98062-156">有关在接受用户文件时减少攻击外围应用的信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="98062-156">For information on reducing the attack surface area when accepting files from users, see the following resources:</span></span>
>
> * <span data-ttu-id="98062-157">[Unrestricted File Upload](https://www.owasp.org/index.php/Unrestricted_File_Upload)（不受限制的文件上传）</span><span class="sxs-lookup"><span data-stu-id="98062-157">[Unrestricted File Upload](https://www.owasp.org/index.php/Unrestricted_File_Upload)</span></span>
> * [<span data-ttu-id="98062-158">Azure 安全性：确保在接受用户文件时采取适当的控制措施</span><span class="sxs-lookup"><span data-stu-id="98062-158">Azure Security: Ensure appropriate controls are in place when accepting files from users</span></span>](/azure/security/azure-security-threat-modeling-tool-input-validation#controls-users)

### <a name="save-the-file-to-azure-blob-storage"></a><span data-ttu-id="98062-159">将文件保存到 Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="98062-159">Save the file to Azure Blob Storage</span></span>

<span data-ttu-id="98062-160">若要将文件内容上传到 Azure Blob 存储，请参阅[使用 .NET 的 Azure Blob 存储入门](/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。</span><span class="sxs-lookup"><span data-stu-id="98062-160">To upload file content to Azure Blob Storage, see [Get started with Azure Blob Storage using .NET](/azure/storage/blobs/storage-dotnet-how-to-use-blobs).</span></span> <span data-ttu-id="98062-161">本主题演示如何使用 [UploadFromStream](/dotnet/api/microsoft.windowsazure.storage.file.cloudfile.uploadfromstreamasync) 将[文件流](/dotnet/api/system.io.filestream)保存到 blob 存储。</span><span class="sxs-lookup"><span data-stu-id="98062-161">The topic demonstrates how to use [UploadFromStream](/dotnet/api/microsoft.windowsazure.storage.file.cloudfile.uploadfromstreamasync) to save a [FileStream](/dotnet/api/system.io.filestream) to blob storage.</span></span>

## <a name="add-the-schedule-class"></a><span data-ttu-id="98062-162">添加 Schedule 类</span><span class="sxs-lookup"><span data-stu-id="98062-162">Add the Schedule class</span></span>

<span data-ttu-id="98062-163">右键单击“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="98062-163">Right click the *Models* folder.</span></span> <span data-ttu-id="98062-164">选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="98062-164">Select **Add** > **Class**.</span></span> <span data-ttu-id="98062-165">将类命名为“Schedule”，并添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="98062-165">Name the class **Schedule** and add the following properties:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](upload-files/samples/2.x/RazorPagesMovie/Models/Schedule.cs)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](upload-files/samples/1.x/RazorPagesMovie/Models/Schedule.cs)]

::: moniker-end

<span data-ttu-id="98062-166">此类使用 `Display` 和 `DisplayFormat` 特性，呈现计划数据时，这些特性会生成友好型的标题和格式。</span><span class="sxs-lookup"><span data-stu-id="98062-166">The class uses `Display` and `DisplayFormat` attributes, which produce friendly titles and formatting when the schedule data is rendered.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="update-the-razorpagesmoviecontext"></a><span data-ttu-id="98062-167">更新 RazorPagesMovieContext</span><span class="sxs-lookup"><span data-stu-id="98062-167">Update the RazorPagesMovieContext</span></span>

<span data-ttu-id="98062-168">在 `RazorPagesMovieContext` (Data/RazorPagesMovieContext.cs) 中为计划指定 `DbSet`：</span><span class="sxs-lookup"><span data-stu-id="98062-168">Specify a `DbSet` in the `RazorPagesMovieContext` (*Data/RazorPagesMovieContext.cs*) for the schedules:</span></span>

[!code-csharp[](upload-files/samples/2.x/RazorPagesMovie/Data/RazorPagesMovieContext.cs?highlight=17)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

## <a name="update-the-moviecontext"></a><span data-ttu-id="98062-169">更新 MovieContext</span><span class="sxs-lookup"><span data-stu-id="98062-169">Update the MovieContext</span></span>

<span data-ttu-id="98062-170">在 `MovieContext` (*Models/MovieContext.cs*) 中为计划指定 `DbSet`：</span><span class="sxs-lookup"><span data-stu-id="98062-170">Specify a `DbSet` in the `MovieContext` (*Models/MovieContext.cs*) for the schedules:</span></span>

[!code-csharp[](upload-files/samples/1.x/RazorPagesMovie/Models/MovieContext.cs?highlight=13)]

::: moniker-end

## <a name="add-the-schedule-table-to-the-database"></a><span data-ttu-id="98062-171">将 Schedule 表添加到数据库</span><span class="sxs-lookup"><span data-stu-id="98062-171">Add the Schedule table to the database</span></span>

<span data-ttu-id="98062-172">打开包管理器控制台 (PMC)：“工具” > “NuGet 包管理器” > “包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="98062-172">Open the Package Manger Console (PMC): **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

![PMC 菜单](upload-files/_static/pmc.png)

<span data-ttu-id="98062-174">在 PMC 中执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="98062-174">In the PMC, execute the following commands.</span></span> <span data-ttu-id="98062-175">这些命令将向数据库添加 `Schedule` 表：</span><span class="sxs-lookup"><span data-stu-id="98062-175">These commands add a `Schedule` table to the database:</span></span>

```powershell
Add-Migration AddScheduleTable
Update-Database
```

## <a name="add-a-file-upload-razor-page"></a><span data-ttu-id="98062-176">添加文件上传 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="98062-176">Add a file upload Razor Page</span></span>

<span data-ttu-id="98062-177">在“Pages”文件夹中创建“Schedules”文件夹。</span><span class="sxs-lookup"><span data-stu-id="98062-177">In the *Pages* folder, create a *Schedules* folder.</span></span> <span data-ttu-id="98062-178">在“Schedules”文件夹中，创建名为“Index.cshtml”的页面，用于上传具有如下内容的计划：</span><span class="sxs-lookup"><span data-stu-id="98062-178">In the *Schedules* folder, create a page named *Index.cshtml* for uploading a schedule with the following content:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-cshtml[](upload-files/samples/2.x/RazorPagesMovie/Pages/Schedules/Index.cshtml)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-cshtml[](upload-files/samples/1.x/RazorPagesMovie/Pages/Schedules/Index.cshtml)]

::: moniker-end

<span data-ttu-id="98062-179">每个窗体组包含一个 \<label>，它显示每个类属性的名称。</span><span class="sxs-lookup"><span data-stu-id="98062-179">Each form group includes a **\<label>** that displays the name of each class property.</span></span> <span data-ttu-id="98062-180">`FileUpload` 模型中的 `Display` 特性提供这些标签的显示值。</span><span class="sxs-lookup"><span data-stu-id="98062-180">The `Display` attributes in the `FileUpload` model provide the display values for the labels.</span></span> <span data-ttu-id="98062-181">例如，`UploadPublicSchedule` 特性的显示名称通过 `[Display(Name="Public Schedule")]` 进行设置，因此呈现窗体时会在此标签中显示“Public Schedule”。</span><span class="sxs-lookup"><span data-stu-id="98062-181">For example, the `UploadPublicSchedule` property's display name is set with `[Display(Name="Public Schedule")]` and thus displays "Public Schedule" in the label when the form renders.</span></span>

<span data-ttu-id="98062-182">每个窗体组包含一个验证 \<span>。</span><span class="sxs-lookup"><span data-stu-id="98062-182">Each form group includes a validation **\<span>**.</span></span> <span data-ttu-id="98062-183">如果用户输入未能满足 `FileUpload` 类中设置的属性特性，或者任何 `ProcessFormFile` 方法文件检查失败，则模型验证会失败。</span><span class="sxs-lookup"><span data-stu-id="98062-183">If the user's input fails to meet the property attributes set in the `FileUpload` class or if any of the `ProcessFormFile` method file validation checks fail, the model fails to validate.</span></span> <span data-ttu-id="98062-184">模型验证失败时，会向用户呈现有用的验证消息。</span><span class="sxs-lookup"><span data-stu-id="98062-184">When model validation fails, a helpful validation message is rendered to the user.</span></span> <span data-ttu-id="98062-185">例如，`Title` 属性带有 `[Required]` 和 `[StringLength(60, MinimumLength = 3)]` 注释。</span><span class="sxs-lookup"><span data-stu-id="98062-185">For example, the `Title` property is annotated with `[Required]` and `[StringLength(60, MinimumLength = 3)]`.</span></span> <span data-ttu-id="98062-186">用户若未提供标题，会接收到一条指示需要提供值的消息。</span><span class="sxs-lookup"><span data-stu-id="98062-186">If the user fails to supply a title, they receive a message indicating that a value is required.</span></span> <span data-ttu-id="98062-187">如果用户输入的值少于 3 个字符或多于 60 个字符，则会接收到一条指示值长度不正确的消息。</span><span class="sxs-lookup"><span data-stu-id="98062-187">If the user enters a value less than three characters or more than sixty characters, they receive a message indicating that the value has an incorrect length.</span></span> <span data-ttu-id="98062-188">如果提供不含内容的文件，则会显示一条指示文件为空的消息。</span><span class="sxs-lookup"><span data-stu-id="98062-188">If a file is provided that has no content, a message appears indicating that the file is empty.</span></span>

## <a name="add-the-page-model"></a><span data-ttu-id="98062-189">添加页面模型</span><span class="sxs-lookup"><span data-stu-id="98062-189">Add the page model</span></span>

<span data-ttu-id="98062-190">将页面模型 (Index.cshtml.cs) 添加到“Schedules”文件夹中：</span><span class="sxs-lookup"><span data-stu-id="98062-190">Add the page model (*Index.cshtml.cs*) to the *Schedules* folder:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](upload-files/samples/2.x/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](upload-files/samples/1.x/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs)]

::: moniker-end

<span data-ttu-id="98062-191">页面模型（Index.cshtml.cs 中的 `IndexModel`）绑定 `FileUpload` 类：</span><span class="sxs-lookup"><span data-stu-id="98062-191">The page model (`IndexModel` in *Index.cshtml.cs*) binds the `FileUpload` class:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](upload-files/snapshot_samples/2.x/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](upload-files/snapshot_samples/1.x/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="98062-192">此模型还使用计划列表 (`IList<Schedule>`) 在页面上显示数据库中存储的计划：</span><span class="sxs-lookup"><span data-stu-id="98062-192">The model also uses a list of the schedules (`IList<Schedule>`) to display the schedules stored in the database on the page:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](upload-files/snapshot_samples/2.x/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet2)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](upload-files/snapshot_samples/1.x/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet2)]

::: moniker-end

<span data-ttu-id="98062-193">页面加载 `OnGetAsync` 时，会从数据库填充 `Schedules`，用于生成已加载计划的 HTML 表：</span><span class="sxs-lookup"><span data-stu-id="98062-193">When the page loads with `OnGetAsync`, `Schedules` is populated from the database and used to generate an HTML table of loaded schedules:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](upload-files/snapshot_samples/2.x/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet3)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](upload-files/snapshot_samples/1.x/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet3)]

::: moniker-end

<span data-ttu-id="98062-194">将窗体发布到服务器时，会检查 `ModelState`。</span><span class="sxs-lookup"><span data-stu-id="98062-194">When the form is posted to the server, the `ModelState` is checked.</span></span> <span data-ttu-id="98062-195">如果无效，会重新生成 `Schedule`，且页面会呈现一个或多个验证消息，陈述页面验证失败的原因。</span><span class="sxs-lookup"><span data-stu-id="98062-195">If invalid, `Schedule` is rebuilt, and the page renders with one or more validation messages stating why page validation failed.</span></span> <span data-ttu-id="98062-196">如果有效，`FileUpload` 属性将用于“OnPostAsync”中，以完成两个计划版本的文件上传，并创建一个用于存储数据的新 `Schedule` 对象。</span><span class="sxs-lookup"><span data-stu-id="98062-196">If valid, the `FileUpload` properties are used in *OnPostAsync* to complete the file upload for the two versions of the schedule and to create a new `Schedule` object to store the data.</span></span> <span data-ttu-id="98062-197">然后会将此计划保存到数据库：</span><span class="sxs-lookup"><span data-stu-id="98062-197">The schedule is then saved to the database:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](upload-files/snapshot_samples/2.x/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet4)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](upload-files/snapshot_samples/1.x/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet4)]

::: moniker-end

## <a name="link-the-file-upload-razor-page"></a><span data-ttu-id="98062-198">链接文件上传 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="98062-198">Link the file upload Razor Page</span></span>

<span data-ttu-id="98062-199">打开“Pages/Shared/_Layout.cshtml”，然后向导航栏添加一个链接以访问“计划”页面：</span><span class="sxs-lookup"><span data-stu-id="98062-199">Open *Pages/Shared/_Layout.cshtml* and add a link to the navigation bar to reach the Schedules page:</span></span>

```cshtml
<div class="navbar-collapse collapse">
    <ul class="nav navbar-nav">
        <li><a asp-page="/Index">Home</a></li>
        <li><a asp-page="/Schedules/Index">Schedules</a></li>
        <li><a asp-page="/About">About</a></li>
        <li><a asp-page="/Contact">Contact</a></li>
    </ul>
</div>
```

## <a name="add-a-page-to-confirm-schedule-deletion"></a><span data-ttu-id="98062-200">添加计划删除确认页面</span><span class="sxs-lookup"><span data-stu-id="98062-200">Add a page to confirm schedule deletion</span></span>

<span data-ttu-id="98062-201">用户单击删除计划时，为其提供取消此操作的机会。</span><span class="sxs-lookup"><span data-stu-id="98062-201">When the user clicks to delete a schedule, a chance to cancel the operation is provided.</span></span> <span data-ttu-id="98062-202">向“Schedules”文件夹添加删除确认页面 (Delete.cshtml)：</span><span class="sxs-lookup"><span data-stu-id="98062-202">Add a delete confirmation page (*Delete.cshtml*) to the *Schedules* folder:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-cshtml[](upload-files/samples/2.x/RazorPagesMovie/Pages/Schedules/Delete.cshtml)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-cshtml[](upload-files/samples/1.x/RazorPagesMovie/Pages/Schedules/Delete.cshtml)]

::: moniker-end

<span data-ttu-id="98062-203">页面模型 (Delete.cshtml.cs) 在请求的路由数据中加载由 `id` 标识的单个计划。</span><span class="sxs-lookup"><span data-stu-id="98062-203">The page model (*Delete.cshtml.cs*) loads a single schedule identified by `id` in the request's route data.</span></span> <span data-ttu-id="98062-204">将“Delete.cshtml.cs”文件添加到“Schedules”文件夹：</span><span class="sxs-lookup"><span data-stu-id="98062-204">Add the *Delete.cshtml.cs* file to the *Schedules* folder:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](upload-files/samples/2.x/RazorPagesMovie/Pages/Schedules/Delete.cshtml.cs)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](upload-files/samples/1.x/RazorPagesMovie/Pages/Schedules/Delete.cshtml.cs)]

::: moniker-end

<span data-ttu-id="98062-205">`OnPostAsync` 方法按 `id` 处理计划删除：</span><span class="sxs-lookup"><span data-stu-id="98062-205">The `OnPostAsync` method handles deleting the schedule by its `id`:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](upload-files/snapshot_samples/2.x/RazorPagesMovie/Pages/Schedules/Delete.cshtml.cs?name=snippet1&highlight=8,12-13)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](upload-files/snapshot_samples/1.x/RazorPagesMovie/Pages/Schedules/Delete.cshtml.cs?name=snippet1&highlight=8,12-13)]

::: moniker-end

<span data-ttu-id="98062-206">成功删除计划后，`RedirectToPage` 将返回到计划的“Index.cshtml”页面。</span><span class="sxs-lookup"><span data-stu-id="98062-206">After successfully deleting the schedule, the `RedirectToPage` sends the user back to the schedules *Index.cshtml* page.</span></span>

## <a name="the-working-schedules-razor-page"></a><span data-ttu-id="98062-207">有效的 Schedules Razor 页面</span><span class="sxs-lookup"><span data-stu-id="98062-207">The working Schedules Razor Page</span></span>

<span data-ttu-id="98062-208">页面加载时，计划标题、公用计划和专用计划的标签和输入将呈现提交按钮：</span><span class="sxs-lookup"><span data-stu-id="98062-208">When the page loads, labels and inputs for schedule title, public schedule, and private schedule are rendered with a submit button:</span></span>

![按初始加载所示计划 Razor 页面，其中不含验证错误和空字段](upload-files/_static/browser1.png)

<span data-ttu-id="98062-210">在不填充任何字段的情况下选择“上传”按钮会违反此模型上的 `[Required]` 特性。</span><span class="sxs-lookup"><span data-stu-id="98062-210">Selecting the **Upload** button without populating any of the fields violates the `[Required]` attributes on the model.</span></span> <span data-ttu-id="98062-211">`ModelState` 无效。</span><span class="sxs-lookup"><span data-stu-id="98062-211">The `ModelState` is invalid.</span></span> <span data-ttu-id="98062-212">会向用户显示验证错误消息：</span><span class="sxs-lookup"><span data-stu-id="98062-212">The validation error messages are displayed to the user:</span></span>

![验证错误消息显示在每个输入控件旁边](upload-files/_static/browser2.png)

<span data-ttu-id="98062-214">在“标题”字段中键入两个字母。</span><span class="sxs-lookup"><span data-stu-id="98062-214">Type two letters into the **Title** field.</span></span> <span data-ttu-id="98062-215">验证消息改为指示标题长度必须介于 3-60 个字符之间：</span><span class="sxs-lookup"><span data-stu-id="98062-215">The validation message changes to indicate that the title must be between 3-60 characters:</span></span>

![标题验证消息已更改](upload-files/_static/browser3.png)

<span data-ttu-id="98062-217">上传一个或多个计划时，“已加载计划”部分会显示已加载计划：</span><span class="sxs-lookup"><span data-stu-id="98062-217">When one or more schedules are uploaded, the **Loaded Schedules** section renders the loaded schedules:</span></span>

![已加载计划表，显示每个计划的标题、UTC 格式的上传日期、公用版本文件大小和专用版本文件大小](upload-files/_static/browser4.png)

<span data-ttu-id="98062-219">用户可单击该表中的“删除”链接以访问删除确认视图，并在其中选择确认或取消删除操作。</span><span class="sxs-lookup"><span data-stu-id="98062-219">The user can click the **Delete** link from there to reach the delete confirmation view, where they have an opportunity to confirm or cancel the delete operation.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="98062-220">疑难解答</span><span class="sxs-lookup"><span data-stu-id="98062-220">Troubleshooting</span></span>

<span data-ttu-id="98062-221">有关上传 `IFormFile` 的疑难解答信息，请参阅 [ASP.NET Core 中的文件上传：疑难解答](xref:mvc/models/file-uploads#troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="98062-221">For troubleshooting information with `IFormFile` uploading, see the [File uploads in ASP.NET Core: Troubleshooting](xref:mvc/models/file-uploads#troubleshooting).</span></span>
