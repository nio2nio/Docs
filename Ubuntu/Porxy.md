### 全域變數
```bash
# 暫時生效，重開機proxy就會失效
$ export http_proxy=http://10.1.1.117:8088
 
# https用https_proxy
$ export https_proxy=https://10.1.1.117:8088
```

### 永久變數
* 僅在目前使用者
> 永久變數可以寫在登入後會讀取的 ~/.bash_profile , ~/.bashrc
```bash
$ echo "export http_proxy=http://10.1.1.117:8088" >> ~/.bashrc
$ echo "export https_proxy=https://10.1.1.117:8088" >> ~/.bashrc

# 立即套用設定
. ~/.bashrc
```

* 針對所有使用者
> 如果要讓這台主機的所有 http / https 都走 proxy 就設定在 /etc/profile
```bash
$ echo "export http_proxy=http://proxy.example.com" >> /etc/profile
$ echo "export https_proxy=https://proxy.example.com" >> /etc/profile
```

* 僅 apt or yum 使用時才用 proxy
```bash
# YUM setting
$ vim /etc/yum.conf
proxy=http://proxy.example.com
 
# APT setting
$ vim /etc/apt/apt.conf
Acquire::http::Proxy "http://proxy.example.com";
```
