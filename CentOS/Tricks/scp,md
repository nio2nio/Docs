#### scp
> 要在不同的 Linux 主機之間複製檔案，最常用的方法就是使用 scp 指令，它可以透過 SSH 安全加密傳輸的方式，將本地端的檔案或目錄複製到遠端，或是將遠端的資料複製到本地端，而這個指令在 Mac OS X 中也同樣可以使用。

> 在不同 Linux 主機之間使用 scp 指令複製檔案時，遠端的 Linux 主機必須要開啟 `SSH 遠端登入服務，否則無法使用 scp 指令複製檔案`。

```shell
$ scp [帳號@來源主機]:來源檔案 [帳號@目的主機]:目的檔案

# 從本地端複製到遠端
$ scp /path/file1 myuser@192.168.0.1:/path/file2

# 從遠端複製到本地端
scp myuser@192.168.0.1:/path/file2 /path/file1

# 複製目錄
scp -r /path/folder1 myuser@192.168.0.1:/path/folder2

# 保留檔案時間與權限
scp -p /path/file1 myuser@192.168.0.1:/path/file2

# 資料壓縮
scp -C /path/file1 myuser@192.168.0.1:/path/file2

# 限制傳輸速度為 400 Kbit/s
scp -l 400 /path/file1 myuser@192.168.0.1:/path/file2
```
