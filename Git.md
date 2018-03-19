#### **`git status`**
> 查詢當前工作目錄的詳細狀態
> -s 來顯示較為精簡的版本
#### **`git reset`** 
> 重設工作目錄的索引狀態
> **`--hard`** 工作目錄還原到目前的最新版
#### **`git add .`** 
> 自動將所有檔案(含子目錄的檔案)加入到工作目錄索引中，有時候我們只想讓特定目錄或特定檔案加入版本，這時你也可以指定特定目錄，或利用萬用字元來加入檔案
#### **`git commit -m "版本紀錄"`**
> 提交變更 / 建立版本
#### **`git rm [file_name]`**
> **`git rm 'Gruntfile.js'`**
> 1. 刪除工作目錄快取的 'Gruntfile.js' 這個檔案 (用來標示這個刪除檔案的動作要列入版本控管)
> 2. 刪除工作目錄下的 'Gruntfile.js' 這個實體檔案 (代表真的把這個實體檔案給刪除)
#### **`git mv test unit-teest`**
> 變更檔案或目錄的名稱
#### **`git checkout [branch_name] [file_name]`**
> **`git checkout master Grunefile.js`**
> 把 master 分支中最新版的 Grunefile.js 給還原

#### **`git branch [branch_name]`**
> 建立分支，但目前工作目錄維持在自己的分支
#### **`git checkout -b [branch_name]`**
> 建立分支，並將目前工作目錄切換到新的分支
#### **`git checkout [branch_name]`**
> 切換分支
#### **`git branch -d [branch_name]`**
> 刪除分支
#### **`git checkout [commit_id]`**
> 把工作目錄的狀態切換成某個版本了

#### **`git diff`**
> 比對的是「工作目錄」與「索引」之間的差異
#### **`git diff [commit_id]`**
> 「工作目錄」與「指定 commit 物件裡的那個 tree 物件」
> **`git diff HEAD`**
> 拿「工作目錄」與「當前分支的最新版」進行比對
#### **`git diff --cached [commit_id]`**
> 比對「當前的索引狀態」與「指定 commit 物件裡的那個 tree 物件」<br />
> **`git diff --cached HEAD`**
> 比對「當前的索引狀態」與「當前分支的最新版」進行比對
#### **`git diff [commit_id1] [commit_id2]`**
> 透過兩個不同的版本 ( commit id ) 來比對其差異 <br />
> **`git diff HEAD^ HEAD`**
> 比較【最新版的前一版】與【最新版】之間的差異

#### **`git log -10`**
> 查詢歷史紀錄<br />
> --pretty=oneline 取得較為精簡的歷史紀錄<br />
> ----abbrev-commit 僅輸出部分的「絕對名稱」
#### **`git cat-file -p [commit_id]`**
> 取得 commit 物件的詳細資訊
<br />
#### **`~`**
> 代表「第一個上層 commit 物件」<br />
> 如果你有一個「參照名稱」為 C，若要找到它的第一個上層 commit 物件，你可以有以下表達方式：<br />
> **`C^`**
> **`C^1`**
> **`C~`**
> **`C~1`**
#### **`^`**
> 「擁有多個上層 commit 物件時，要代表第幾個第一代的上層物件」


