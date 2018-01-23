<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="8bfe1-101">搭建“电影”模型的基架</span><span class="sxs-lookup"><span data-stu-id="8bfe1-101">Scaffold the Movie model</span></span>

* <span data-ttu-id="8bfe1-102">从命令行（在包含 Program.cs、Startup.cs 和 .csproj 文件的项目目录中）中运行如下命令：</span><span class="sxs-lookup"><span data-stu-id="8bfe1-102">Run the following from the command line (in the project directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files):</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

<span data-ttu-id="8bfe1-103">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="8bfe1-103">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="8bfe1-104">打开一个到项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）的命令 shell。</span><span class="sxs-lookup"><span data-stu-id="8bfe1-104">Open a command shell to the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>

<span data-ttu-id="8bfe1-105">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="8bfe1-105">If you get the error:</span></span>
  ```
  The process cannot access the file
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll'
  because it is being used by another process.
  ```

<span data-ttu-id="8bfe1-106">退出 Visual Studio，然后重新运行命令。</span><span class="sxs-lookup"><span data-stu-id="8bfe1-106">Exit Visual Studio and run the command again.</span></span>
