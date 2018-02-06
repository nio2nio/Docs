### Backup MySQL
  * Export
  ```shell
  mysqldump -u user -h 192.168.1.200 -p database table > backup.sql
  mysqldump --user=root -p --all-database > /backup/mysql.sql
  ```
  * 匯入 
  ```shell
  mysql -u user -p database < backup.sql
  ```
  * 參數說明
  ```shell
  > 匯出
  < 匯入
  -u mysql user
  -h Host IP或Domain Name
  -d 只需匯出Table Schema，若沒有此參數，會將Table結構跟資料一起匯出
  -p password
  ```
  
### Reset MySQL Root Password
  * Stop MySQL Service
  ```shell
  sudo systemctl stop mariadb.service
  sudo mysqld_safe --skip-grant-tables &
  ```
  * Login as root without password
  ```shell
  sudo mysql -u root
  ```
  * Reset Root Password
  ```sql
  > use mysql;
  > UPDATE user set Password=PASSWORD("P@ssw0rd") WHERE User='root';
  > Flush Privileges;
  > quit
  ```
  * Restart MySQL Service
  ```shell
  sudo systemctl stop mariadb.service
  sudo systemctl start mariadb.service
  ```
