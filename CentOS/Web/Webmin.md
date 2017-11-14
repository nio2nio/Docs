### Install Webmin
```shell
$ sudo vi /etc/yum.repos.d/webmin.repo
[Webmin]
name=Webmin Distribution Neutral
#baseurl=http://download.webmin.com/download/yum
mirrorlist=http://download.webmin.com/download/yum/mirrorlist
enabled=1

# Add the Webmin author's PGP key
wget http://www.webmin.com/jcameron-key.asc
sudo rpm --import jcameron-key.asc

$ sudo yum install -y webmin

# Navigate to https://your_domain:10000
```

### Change webmin root password
```shell
$ sudo /usr/libexec/webmin/changepass.pl /etc/webmin root newpassword
```
