#### `nohup` 讓程式可以在離線或登出系統後繼續執行。
> 當 Linux 使用者登出系統時，其所執行的每一個程式都會接收到一個 `SIGHUP（hangup）`這個信號，正常的程式收到這個信號之後，就會馬上停止執行。
> 如果想讓程式可以在離線或登出之後繼續執行，可以使用 nohup 這個指令來執行程式，這個指令可以讓程式忽略 SIGHUP 這個信號，所以當使用者登出或是斷線後，程式也可以正常執行，不會受到任何影響。
```shell
$ nohup /path/command &
```

> nohup 在執行程式時，會將所有的輸出訊息導入 `nohup.out` 這個文字檔
```shell
$ cat nohup.out

# 即時顯示最新
$ tail -f nohup.out

# 指定輸出檔案
$ nohup /path/command &> my_log.txt &

# 正常的訊息與錯誤訊息分開
$ nohup /path/command > log.txt 2> err.txt &

# 降低執行優先權
# 使用 nice 時若不指定其 niceness 值，則預設為 10。
$ nohup nice /path/command &
```

