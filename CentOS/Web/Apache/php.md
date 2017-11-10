### Install PHP
```shell
$ sudo yum install -y php php-mbstring php-pear
```

### Configure PHP
```shell
$ sudo vi /etc/php.ini

# Line 878
date.timezone = "Asia/Taipei"

# Restart httpd service
$ sudo systemctl restart httpd.service
```

### Create a PHP test page
```shell
$ sudo vi /var/www/html/index.php
<html>
  <body>
    <div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">
      <?php
        print Date("Y/m/d");
      ?>
    </div>
  </body>
</html>
```
