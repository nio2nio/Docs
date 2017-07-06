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

### 基本指令
```shell
# 安裝套件
$ yum install 套件名稱

# 升級套件
$ yum update 套件名稱

# 升級全部套件
$ yum update

# 升級全部套件及發行版本
$ yum upgrade

# 移除套件
$ yum remove 套件名稱

# 清除暫存檔 (/var/cache/yum)
$ yum clean
```

### 查詢功能
```shell
# 查詢套件資訊
$ yum info 套件名稱

# 搜尋套件
$ yum search 關鍵字

# 查詢套件
$ yum list 套件名稱

# 查詢所有可更新的套件
$ yum list updates

# 查詢所有已安裝的套件
$ yum list installed

# 查詢特定檔案存在於什麼套件之中
$ yum provides 檔案名稱
$ yum provides */檔案名稱
$ yum resolvedep 檔案名稱
# example
$ yum provides libz.*
$ yum provides */nslookup
$ yum resolvedep libz.so.1
```

### 套件組
```shell
# 查看已安裝與可安裝的套件組
$ yum grouplist

# 安裝套件組
$ yum groupinstall "套件組名稱"

# 升級套件組
$ yum groupupdate "套件組名稱"

# 移除套件組
$ yum groupremove "套件組名稱"

# 查看套件組資訊
$ yum groupinfo "套件組名稱"
```

### 錯誤處理
```shell
# 當安裝套件時出現錯誤訊息:pkgKey xxx doesn't exist in repo base
$ yum clean metadata
```
