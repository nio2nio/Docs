## Behind Proxy
```bash
$ sudo vi /etc/apt/apt.conf
Acquire::http::Proxy "http://10.1.1.117:8088";
Acquire::https::Proxy "http://10.1.1.117:8088";
```
