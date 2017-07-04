### Yum Proxy 設定
```shell
$ vi /etc/yum.conf
proxy=http://ip:port
```

### Epel (Extra Packages for Enterprise Linux 7)
```shell
# yum
$ sudo yum install epel-release

# epel (http://dl.fedoraproject.org/pub/epel/)
$ wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
$ sudo rpm -Uvh epel-release-7*.rpm
```
