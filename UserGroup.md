### /etc/group
>群組名稱:群組密碼:GID:此群組支援的帳號名稱<br>
>如果我想要讓 dmtsai 與 alex 也加入 root 這個群組，那麼在第一行的最後面加上『dmtsai,alex』，注意不要有空格

### /etc/gshadow
>群組名稱:密碼欄:群組管理員的帳號:有加入該群組支援的所屬帳號

### groupadd
>-g GID<br>
>-r 建立系統群組 

### groupmod
>-g GID<br>
>-n 修改既有的群組名稱

### groupdel

### gpasswd
>-A 將groupname的主控權交由後面的使用者管理<br>
>-M 將某些帳號加入這個群組當中<br>
>-r 將groupname的密碼移除<br>
>-R 讓groupname的密碼欄失效
