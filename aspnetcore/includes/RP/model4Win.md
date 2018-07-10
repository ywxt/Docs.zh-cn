<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="21804-101">搭建“电影”模型的基架</span><span class="sxs-lookup"><span data-stu-id="21804-101">Scaffold the Movie model</span></span>

* <span data-ttu-id="21804-102">从命令行（在包含 Program.cs、Startup.cs 和 .csproj 文件的项目目录中）中运行如下命令：</span><span class="sxs-lookup"><span data-stu-id="21804-102">Run the following from the command line (in the project directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files):</span></span>

  ```console
  dotnet restore
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

<span data-ttu-id="21804-103">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="21804-103">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="21804-104">当处于错误的目录时，会发生上述错误。</span><span class="sxs-lookup"><span data-stu-id="21804-104">The preceeding error happens when you are in the wrong directory.</span></span> <span data-ttu-id="21804-105">打开命令行界面，进入项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录），然后运行上述命令。</span><span class="sxs-lookup"><span data-stu-id="21804-105">Open a command shell to the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files), and then run the preceeding command.</span></span>

<span data-ttu-id="21804-106">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="21804-106">If you get the error:</span></span>
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

<span data-ttu-id="21804-107">退出 Visual Studio，然后重新运行命令。</span><span class="sxs-lookup"><span data-stu-id="21804-107">Exit Visual Studio and run the command again.</span></span>
