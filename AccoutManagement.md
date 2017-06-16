### /etc/passwd
>帳號名稱:密碼:UID:GID:使用者資訊欄位說明:家目錄:Shell<br>
>UID: 0(root), 1~999(系統帳號)

### /etc/shadow
>帳號名稱:密碼:最近更動密碼的日期:密碼不可被更動的天數:密碼需要重新變更的天數:密碼需要變更期限前的警告天數:密碼過期後的帳號寬限時間(密碼失效日):帳號失效日期:保留

> **root密碼忘記**
>> 重新開機進入單人維護模式後，系統會主動的給予 root 權限的 bash 介面， 此時再以 passwd 修改密碼即可；或以 Live CD 開機後掛載根目錄去修改 /etc/shadow，將裡面的 root 的密碼欄位清空， 再重新開機後 root 將不用密碼即可登入。

> **shadow 是使用哪種加密的機制**
>> authconfig --test | grep hashing

### /etc/group
>群組名稱:群組密碼:GID:此群組支援的帳號名稱<br>
>如果我想要讓 dmtsai 與 alex 也加入 root 這個群組，那麼在第一行的最後面加上『dmtsai,alex』，注意不要有空格。
