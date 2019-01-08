# <a name="how-to-buildrun-secure-user-data-sample"></a><span data-ttu-id="a18ea-101">如何生成/运行安全的用户数据示例</span><span class="sxs-lookup"><span data-stu-id="a18ea-101">How to build/run Secure user data sample</span></span>

* <span data-ttu-id="a18ea-102">使用机密管理器工具设置密码：</span><span class="sxs-lookup"><span data-stu-id="a18ea-102">Set password with the Secret Manager tool:</span></span>

  `dotnet user-secrets set SeedUserPW <pw>`

* <span data-ttu-id="a18ea-103">更新数据库：</span><span class="sxs-lookup"><span data-stu-id="a18ea-103">Update the database:</span></span>

    `dotnet ef database update`

* <span data-ttu-id="a18ea-104">在项目中启用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="a18ea-104">Enable HTTPS in the project</span></span>
