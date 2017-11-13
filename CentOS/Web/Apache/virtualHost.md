### 安裝 Apache
```shell
$ sudo yum install -y httpd

# start httpd service and enable it to start automatically on boot
$ sudo systemctl start httpd.service
$ sudo systemctl enable httpd.service
```

### 設定虛擬主機
```shell
#  建立虛擬目錄
$ sudo makir -p /var/www/example.com/public_html

# 變更擁有權
$ sudo chown -R apache:apache /var/www/example.com/public_html

# 變更目錄權限
$ sudo chmod -R 755 /var/www
```

### 設定虛擬目錄
```shell
# 建立目錄
$ sudo mkdir /etc/httpd/sites-available
$ sudo mkdir /etc/httpd/sites-enabled

# 編輯Apache設定檔
$ sudo vi /etc/httpd/conf/httpd.conf
# 新增設定
IncludeOptional sites-enabled/*.conf
```

### 建立虛擬主機檔案
```shell
$ sudo vi /etc/httpd/sites-avialable/example.com.conf
<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host.example.com    
    ServerName www.coolexample.com
    ServerAlias coolexample.com 
    DocumentRoot /var/www/example.com/public_html 
    ErrorLog /var/www/example.com/error.log 
    CustomLog /var/www/example.com/requests.log combined 
</VirtualHost>

# 連結設定檔至site-enabled
$ sudo ln -S /etc/httpd/site-available/example.com.conf /etc/httpd/site-enabled/example.com.conf

# 重啟Apache
$ sudo systemctl restart httpd.service
```
