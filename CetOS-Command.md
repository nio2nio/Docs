### Yum
```shell
  yum install package
  # 升級全部套件
  yum update
  yum update package
  # 升級全部套件及發行版本
  yum upgrade
  yum remove package
  yum clean (/var/cache/yum)
  
  # 查詢
  yum info package
  yum search keyword
  yum list package
  # 查詢所有可更新的套件
  yum list updates
  # 查詢所有已安裝的套件
  yum list installed
  # 查詢特定檔案存在於什麼套件之中
  yum provides 檔案名稱
  yum provides */檔案名稱
  yum resolvedep 檔案名稱
  
  # 套件組
  yum grouplist
  yum groupinstall "Group Name"
  yum groupupdate "Group Name"
  yum groupremove "Group Name"
  yum groupinfo "Group Name"
  
  # 當安裝套件時出現錯誤訊息:pkgKey xxx doesn't exist in repo base
  yum clean metadata
```

### tar
  * 建立 .tar 壓縮檔
  ```shell
  # -c: create
  # -v: verbose
  # -f: archive file
  # -z: gzip
  tar -zcvf mpi.tar folder/
  ```
  * 驗證 .tar 壓縮檔案
  ```shell
  tar -zcvfW mpi.tar folder/
  ```
  * 解壓縮 .tar 壓縮檔案
  ```shell
  # -x: extract
  tar -zxvf mpi.tar
  # -C: 指定解壓縮後的檔案放置位置
  tar -zxvf mpi.tar -C /target/folder
  ```
  * 列出 .tar 壓縮檔案的內容
  ```shell
  tar -ztvf mpi.tar
  ```
  * 從 .tar 壓縮檔案中解壓縮指定的檔案
  ```shell
  tar -zxvf mpi.tar "mpi/mpi.R"
  tar -zxvf mpi.tar "mpi/mpi.R" "mpi/pi.c" "mpi/my_phi.c"
  # --wildcards 參數以萬用字元（wildcard）的方式來指定檔案
  tar -zxvf mpi.tar --wildcards "*.c"
  ```
  * 加入新的檔案或目錄到 .tar 壓縮檔案中
  ```shell
  # -r: append
  tar -zrvf mpi.tar test_append.txt
  ```

### nmcli
  * Show device
  ```shell
  nmcli d
  ```
  * Set IPv4 Address
  ```shell
  nmcli c modify eth0 ipv4.addresses 10.0.0.30/24
  ```
  * Set default gateway
  ```shell
  nmcli c modify eth0 ipv4.gateway 10.0.0.1
  ```
  * Set DNS
  ```shell
  nmcli c modify eth0 ipv4.dns 10.0.0.1 
  ```
  * Set DHCP (auto) Or Static (manual)
  ```shell
  nmcli c modify eth0 ipv4.method manual
  ```
  * Reload configuration
  ```shell
  nmcli c down eth0; nmcli c up eth0 
  ```
  * Show configuration
  ```shell
  nmcli d show eth0 
  ```
  * Show status
  ```shell
  ip addr show
  ```
  
### nohup 讓程式可以在離線或登出系統後繼續執行
  * 當 Linux 使用者登出系統時，其所執行的每一個程式都會接收到一個**`SIGHUP（hangup）`**這個信號，正常的程式收到這個信號之後，就會馬上停止執行。如果想讓程式可以在離線或登出之後繼續執行，可以使用 nohup 這個指令來執行程式，這個指令可以讓程式忽略 SIGHUP 這個信號，所以當使用者登出或是斷線後，程式也可以正常執行，不會受到任何影響。
  ```shell
  nohup /path/command &
  ```
  * nohup 在執行程式時，會將所有的輸出訊息導入 **`nohup.out`** 這個文字檔
  * 即時顯示最新
  ```shell
  tail -f nohup.out
  ```
  * 指定輸出檔案
  ```shell
  nohup /path/command &> my_log.txt &
  ```
  * 正常的訊息與錯誤訊息分開
  ```shell
  nohup /path/command > log.txt 2> err.txt &
  ```
  * 降低執行優先權 使用 nice 時若不指定其 niceness 值，則預設為 10
  ```shell
  nohup nice /path/command &
  ```

### scp
  * 要在不同的 Linux 主機之間複製檔案，最常用的方法就是使用 scp 指令，它可以透過 SSH 安全加密傳輸的方式，將本地端的檔案或目錄複製到遠端，或是將遠端的資料複製到本地端，而這個指令在 Mac OS X 中也同樣可以使用。在不同 Linux 主機之間使用 scp 指令複製檔案時，遠端的 Linux 主機必須要開啟 SSH 遠端登入服務，否則無法使用 scp 指令複製檔案。   
  ```shell
  scp [帳號@來源主機]:來源檔案 [帳號@目的主機]:目的檔案
  ```
  * 從本地端複製到遠端
  ```shell
  scp /path/file1 myuser@192.168.0.1:/path/file2
  ```
  * 從遠端複製到本地端
  ```shell
  scp myuser@192.168.0.1:/path/file2 /path/file1
  ```
  * 複製目錄
  ```shell
  scp -r /path/folder1 myuser@192.168.0.1:/path/folder2
  ```
  * 保留檔案時間與權限
  ```shell
  scp -p /path/file1 myuser@192.168.0.1:/path/file2
  ```
  * 資料壓縮
  ```shell
  scp -C /path/file1 myuser@192.168.0.1:/path/file2
  ```
  * 限制傳輸速度為 400 Kbit/s
  ```shell
  scp -l 400 /path/file1 myuser@192.168.0.1:/path/file2
  ```
