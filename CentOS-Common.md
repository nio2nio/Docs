### NodeJs
  * Install EPEL-Release
  ```shell
  sudo yum install epel-release
  ```
  * Bug: Error: Package: 1:nodejs-6.11.1-1.el7.x86_64 (epel) Requires: libhttp_parser.so.2()(64bit)
  ```shell
  rpm -ivh https://kojipkgs.fedoraproject.org//packages/http-parser/2.7.1/3.el7/x86_64/http-parser-2.7.1-3.el7.x86_64.rpm
  ```
  * Install nodeJs/npm
  ```shell
  sudo yum install nodejs
  sudo yum install npm
  ```
  
### Zip
  * Installation
  ```shell
  yum install zip unzip
  ```
  * Zip
  ```shell
  # 壓縮目錄 (將data目錄下的所有檔案壓縮到file.zip，指令無須加上zip副檔名)
  zip file data/*
  # 將data目錄下所有檔案及子目錄壓縮到file.zip
  zip -r file data/*
  ```
  * Unzip
  ```shell
  # 將file.zip解壓縮到當前目錄
  unzip file.zip
  # 解壓縮檔內其中一個檔案
  unzip file.zip test.php
  # 解壓縮到指定目錄
  unzip file.zip -d /home/phpini
  ```
  
### nmon
  * Installation
  ```shell
  sudo yum install nmon
  ```
  * Usage
  ```shell
  # t = Top Process Stats
  # c = CPU by Processor
  # l = Longer term CPU Averages
  # m = Memory and Swap Stats
  # j = JFS Usage Stats
  # h = Help Information
  # n = Network Stats
  # d = Disk I/O Stats
  # o = Disk Busy Map
  # k = Kernel Stats and Load average
  # v = Virtual Memory Stats
  # g = User defined disk groups
  # v = Verbose Simple Checks
  # b = Black and White Mode
  # N = NFS
  ```
  
