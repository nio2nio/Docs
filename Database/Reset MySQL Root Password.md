### Reset MySQL Root Password
```shell
$ sudo systemctl stop mariadb.service
$ sudo mysqld_safe --skip-grant-tables &

# Login as root without password
$ sudo mysql -u root
> use mysql;
> UPDATE user set Password=PASSWORD("P@ssw0rd") WHERE User='root';
> Flush Privileges;
> quit

# Restart MySQL Service
$ sudo systemctl stop mariadb.service
$ sudo systemctl start mariadb.service
```
