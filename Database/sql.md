### Backup MySQL
```shell
# 匯出
mysqldump -u user -h 192.168.1.200 -p database table > backup.sql

# 匯出所有資料庫
mysqldump --user=root -p --all-database > /backup/mysql.sql

# 匯入 mysql -u user -p database < backup.sql

# 參數說明
> 匯出
< 匯入
-u mysql user
-h Host IP或Domain Name
-d 只需匯出Table Schema，若沒有此參數，會將Table結構跟資料一起匯出
-p password
```