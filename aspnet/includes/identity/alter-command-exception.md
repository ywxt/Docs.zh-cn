> 如果应用使用 SQLite 作为其标识数据存储区，某些命令不受支持。 由于数据库引擎中的限制`Alter`命令将引发以下异常：
>
> "System.NotSupportedException: SQLite 不支持此迁移操作。" 
>
> 作为替代，若要更改表的数据库运行 Code First 迁移。
