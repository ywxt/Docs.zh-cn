> 如果应用使用 SQLite 作为其标识数据存储区，不支持一些命令。 由于数据库引擎中的限制`Alter`命令将引发以下异常：
>
> "System.NotSupportedException: SQLite 不支持此迁移操作。" 
>
> 作为替代，若要更改的表在数据库上运行 Code First 迁移。
