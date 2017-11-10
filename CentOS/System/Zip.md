### Installation
```bash
# REHL / CentOS / Fedora
$ yum install zip upzip

# Debian / Ubuntu / Mint
$ apt-get zip upzip
```

### Zip
```shell
# 壓縮目錄 (將data目錄下的所有檔案壓縮到file.zip，指令無須加上zip副檔名)
$ zip file data/*

# 將data目錄下所有檔案及子目錄壓縮到file.zip
$ zip -r file data/*
```

### Unzip
```shell
# 將file.zip解壓縮到當前目錄
$ unzip file.zip

# 解壓縮檔內其中一個檔案
$ unzip file.zip test.php

# 解壓縮到指定目錄
$ unzip file.zip -d /home/phpini
```
