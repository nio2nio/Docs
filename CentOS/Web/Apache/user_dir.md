### Configure httpd
```shell
$ sudo vi /etc/httpd/conf.d/userdir.conf
# UserDir disabled
UserDir public_html

<Directory "/home/*/public_html">
  AllowOverride All
  Options None
  Require method GET POST OPTIONS
</Directory>

# Restart httpd service
$ sudo systemctl restart httpd.service
```

### Create a test page
```shell
$ cd ~
$ mkdir public_html
$ chmod 711 /home/cent
$ chmod 755 /home/cent/public_html
$ vi ./public_html/index.html
<html>
  <body>
    <div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">
      UserDir Test Page
    </div>
   </body>
</html>

# Visit http://your.domain/~cent/
```
