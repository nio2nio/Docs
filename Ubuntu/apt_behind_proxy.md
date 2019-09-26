## Behind Proxy Configuration
```bash
$ sudo vi /etc/apt/apt.conf
Acquire::http::Proxy "http://10.1.1.117:8088";
Acquire::https::Proxy "http://10.1.1.117:8088";

## Fix "Hash sum mismatch"
$ sudo vi /etc/apt/apt.conf.d/99fixbadproxy
Acquire::http::Pipeline-Depth 0;
Acquire::http::No-Cache true;
Acquire::BrokenProxy    true;
```
