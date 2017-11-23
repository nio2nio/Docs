### bash 會將使用者執行過的歷史指令都儲存在 .bash_history 這個檔案中，由於 bash 並不會即時將新的指令寫入 .bash_history，所以這個只能查看使用者過去執行過的指令。
```shell
$ sudo cat /home/user/.bash_profile
```

### w 指令可以列出 Linux 系統上目前有哪些使用者登入，並且顯示每個使用者正在執行的指令。
```shell
$ w
```
