## Behind Proxy Configuration
```bash
$ sudo vi /etc/apt/apt.conf
Acquire::http::Proxy "http://10.1.1.117:8088";
Acquire::https::Proxy "http://10.1.1.117:8088";
```

## APT Command Usage
+ Installing a package
```bash
sudo apt install package_name
```
+ Find location of installed package
```bash
sudo apt content package_name
```
