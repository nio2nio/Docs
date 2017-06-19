### /etc/passwd
>帳號名稱:密碼:UID:GID:使用者資訊欄位說明:家目錄:Shell<br>
>UID: 0(root), 1~999(系統帳號)

### /etc/shadow
>帳號名稱:密碼:最近更動密碼的日期:密碼不可被更動的天數:密碼需要重新變更的天數:密碼需要變更期限前的警告天數:密碼過期後的帳號寬限時間(密碼失效日):帳號失效日期:保留

> **Q: root密碼忘記**
>> 重新開機進入單人維護模式後，系統會主動的給予 root 權限的 bash 介面， 此時再以 passwd 修改密碼即可；或以 Live CD 開機後掛載根目錄去修改 /etc/shadow，將裡面的 root 的密碼欄位清空， 再重新開機後 root 將不用密碼即可登入

> **Q: shadow 是使用哪種加密的機制**
>> authconfig --test | grep hashing

### /etc/group
>群組名稱:群組密碼:GID:此群組支援的帳號名稱<br>
>如果我想要讓 dmtsai 與 alex 也加入 root 這個群組，那麼在第一行的最後面加上『dmtsai,alex』，注意不要有空格

### /etc/gshadow
>群組名稱:密碼欄:群組管理員的帳號:有加入該群組支援的所屬帳號

### useradd
>-u UID<br>
>-g initial group (該群組的GID會放到/etc/passwd第四個欄位)<br>
>-M 不要建立使用者家目錄(系統帳號預設值)<br>
>-m 要建立使用者家目錄(一般帳號預設值)<br>
>-d 指定某個目錄成為家目錄，而不要使用預設值。(絕對路徑)<br>
>-r 建立一個系統的帳號(不會主動建立家目錄)，這個帳號的 UID 會有限制(參考 /etc/login.defs)<br>
>-s 後面接一個 shell，若沒有指定則預設是/bin/bash<br>
>-e 帳號失效日<br>
>-f 指定密碼是否會失效。0為立刻失效，-1為永遠不失效

>**useradd 參考檔**
>>useradd -D<br>
>>GROUP=100 預設的群組<br>
>>HOME=/home 預設的家目錄所在目錄<br>
>>INACTIVE=-1 密碼失效日，在 shadow 內的第 7 欄<br>
>>EXPIRE=	帳號失效日，在 shadow 內的第 8 欄<br>
>>SHELL=/bin/bash	預設的 shell<br>
>>SKEL=/etc/skel 使用者家目錄的內容資料參考目錄<br>
>>CREATE_MAIL_SPOOL=yes 是否主動幫使用者建立郵件信箱(mailbox)

### passwd
>-1 是 Lock 的意思，會將 /etc/shadow 第二欄最前面加上!使密碼失效<br>
>-u unlock<br>
>-n 多久不可修改密碼天數<br>
>-x 多久內必須要更動密碼<br>
>-w 密碼過期前的警告天數<br>
>-i 密碼失效天數

### chage
>-l 列出該帳號的詳細密碼參數<br>
>-d 最近一次更改密碼的日期 (yyyy-MM-dd)<br>
>-E 帳號失效日<br>
>-I 密碼失效日期<br>
>-m 密碼最短保留天數<br>
>-M 密碼多久需要進行變更<br>
>-W 密碼過期前警告日期

>**使用者在第一次登入時， 強制她們一定要更改密碼後才能夠使用系統資源**
>> useradd demouser
>> echo "demopass" | passwd --stdin demouser
>> chage -d 0 demouser
