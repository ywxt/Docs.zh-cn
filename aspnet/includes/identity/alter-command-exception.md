> <span data-ttu-id="50ce9-101">如果应用使用 SQLite 作为其标识数据存储区，某些命令不受支持。</span><span class="sxs-lookup"><span data-stu-id="50ce9-101">Some commands aren't supported if the app uses SQLite as its Identity data store.</span></span> <span data-ttu-id="50ce9-102">由于数据库引擎中的限制`Alter`命令将引发以下异常：</span><span class="sxs-lookup"><span data-stu-id="50ce9-102">Due to limitations in the database engine, `Alter` commands throw the following exception:</span></span>
>
> <span data-ttu-id="50ce9-103">"System.NotSupportedException: SQLite 不支持此迁移操作。"</span><span class="sxs-lookup"><span data-stu-id="50ce9-103">"System.NotSupportedException: SQLite does not support this migration operation."</span></span> 
>
> <span data-ttu-id="50ce9-104">作为替代，若要更改表的数据库运行 Code First 迁移。</span><span class="sxs-lookup"><span data-stu-id="50ce9-104">As a work around, run Code First migrations on the database to change the tables.</span></span>
