### android.database.sqlite.SQLiteBlobTooBigException: Row too big to fit into CursorWindow requiredPos=0, totalRows=1...


**解决方法：** 数据库表字段值如果超过**2M**，那么就把值存在文件中，然后把文件路径存在此字段中。 

数据库存储“二进制数据”不能超过**2M** 。
