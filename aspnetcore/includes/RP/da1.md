# <a name="update-the-generated-pages"></a><span data-ttu-id="1a638-101">更新生成的页面</span><span class="sxs-lookup"><span data-stu-id="1a638-101">Update the generated pages</span></span>

<span data-ttu-id="1a638-102">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1a638-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="1a638-103">我们的电影应用有个不错的开始，但是展示效果还不够理想。</span><span class="sxs-lookup"><span data-stu-id="1a638-103">We have a good start to the movie app, but the presentation isn't ideal.</span></span> <span data-ttu-id="1a638-104">我们不希望看到时间（如下图所示的 12:00:00 AM），并且“ReleaseDate”应为“Release Date”（两个词）。</span><span class="sxs-lookup"><span data-stu-id="1a638-104">We don't want to see the time (12:00:00 AM in the image below) and **ReleaseDate** should be **Release Date** (two words).</span></span>

![在 Chrome 中打开的显示电影数据的电影应用程序](../../tutorials/razor-pages/sql/_static/m55.png)

## <a name="update-the-generated-code"></a><span data-ttu-id="1a638-106">更新生成的代码</span><span class="sxs-lookup"><span data-stu-id="1a638-106">Update the generated code</span></span>

<span data-ttu-id="1a638-107">打开 Models/Movie.cs 文件，并添加以下代码中突出显示的行：</span><span class="sxs-lookup"><span data-stu-id="1a638-107">Open the *Models/Movie.cs* file and add the highlighted lines shown in the following code:</span></span>

[!code-csharp[](code/Models/Movie.cs?highlight=2,11-12)]
