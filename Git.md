#### 物件的符號參照名稱 (symref)
* **`HEAD`**
  * 永遠會指向「工作目錄」中所設定的「分支」當中的「最新版」。
  * 所以當你在這個分支執行 git commit 後，這個 HEAD 符號參照也會更新成該分支最新版的那個 commit 物件。
* **`ORIG_HEAD`**
  * HEAD 這個 commit 物件的「前一版」，經常用來復原上一次的版本變更。
* **`FETCH_HEAD`**
  * 使用遠端儲存庫時，可能會使用 git fetch 指令取回所有遠端儲存庫的物件。這個 FETCH_HEAD 符號參考則會記錄遠端儲存庫中每個分支的 HEAD (最新版) 的「絕對名稱」。
* **`MERGE_HEAD`**
  * 當你執行合併工作時，「合併來源｣的 commit 物件絕對名稱會被記錄在 MERGE_HEAD 這個符號參照中。
#### 相對名稱表示法 ^ 與 ~ 的差異
**`~`** 代表「第一個上層 commit 物件」


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
#### **`git commit --amend`**
> 重新提交一次最後一個版本 (即 HEAD 版本)
#### **`git rm [file_name]`**
> **`git rm 'Gruntfile.js'`**
> 1. 刪除工作目錄快取的 'Gruntfile.js' 這個檔案 (用來標示這個刪除檔案的動作要列入版本控管)
> 2. 刪除工作目錄下的 'Gruntfile.js' 這個實體檔案 (代表真的把這個實體檔案給刪除)
#### **`git mv test unit-teest`**
> 變更檔案或目錄的名稱
#### **`git checkout [branch_name] [file_name]`**
> **`git checkout master Grunefile.js`**
> 把 master 分支中最新版的 Grunefile.js 給還原
#### **`git revert [command_id]`**
> 「還原」某個版本 (其實是透過「新增一個版本」的方式把變更的內容改回來，而且透過這種方式，你可以透過版本歷史紀錄中明確找出你到底是針對哪幾個版本進行還原的)

#### **`git branch [branch_name]`**
> 建立分支，但目前工作目錄維持在自己的分支
#### **`git checkout -b [branch_name]`**
> 建立分支，並將目前工作目錄切換到新的分支
#### **`git checkout [branch_name]`**
> 切換分支
#### **`git branch -d [branch_name]`**
> 刪除分支<br />
> 只要沒有執行過「合併」的分支，必須用 **`git branch -D feature`** 才能刪除該分支
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
#### **`git reflog`**
> 列印出所有「歷史紀錄」的版本變化<br />
> 這裡有個特殊的「參考名稱」為 HEAD@{0}，這裡每個版本都會有一個歷史紀錄都會有個編號，代表著這個版本的在記錄檔中的順位。如果是 HEAD@{0} 的話，永遠代表目前分支的「最新版」<br />
> **`git reset HEAD@{1} --hard`**
> **`git reset ORIG_HEAD --hard`**
> 刪除最近一次的版本，但保留最後一次的變更
> **`git reset "HEAD^" --soft`**
> 刪除最近一次的版本紀錄，但留下最後一次版本變更的異動內容
> **`git reflog expire --expire=now --all`**
> 立即清除所有歷史紀錄
#### **`git cat-file -p [commit_id]`**
> 取得 commit 物件的詳細資訊

> 如果你有一個「參照名稱」為 C，若要找到它的第一個上層 commit 物件，你可以有以下表達方式：<br />
> **`C^`**
> **`C^1`**
> **`C~`**
> **`C~1`**
#### **`^`**
> 「擁有多個上層 commit 物件時，要代表第幾個第一代的上層物件」<br />
> 如果你要找到它的第二個上層 commit 物件 (在沒有合併的狀況下)，你可以有以下表達方式：<br />
> **`C^^`**
> **`C^1^1`**
> **`C~2`**
> **`C~~`**
> **`C~1~1`**<br />
> 但你不能用 C^2 來表達「第二個上層 commit 物件」！原因是在沒有合併的情況下，這個 C 只有一個上層物件而已，你只能用 C^2 代表｢上一層物件的第二個上層物件」

#### **`git clone`**
> 將遠端儲存庫複製到本地，並建立工作目錄與本地儲存庫 (就是 .git 資料夾)
#### **`git pull`**
> 將遠端儲存庫的最新版下載回來，下載的內容包含完整的物件儲存庫(object storage)。並且將遠端分支合併到本地分支。 (將 origin/master 遠端分支合併到 master 本地分支)<br />
> 所以一個 git pull 動作，完全相等於以下兩段指令：<br />
> **`git fetch`**
> **`git merge origin/master`**
#### **`git push`**
> 將本地儲存庫中目前分支的所有相關物件推送到遠端儲存庫中。
#### **`git fetch`**
> 將遠端儲存庫的最新版下載回來，下載的內容包含完整的物件儲存庫(object storage)。 這個命令不包含「合併」分支的動作。
#### **`git ls-remote`**
> 顯示特定遠端儲存庫的參照名稱。包含遠端分支與遠端標籤。
#### **`git remote add origin [remote_git]`**
> 註冊遠端儲存庫
#### **`git push origin --delete [remote_branch_name]`**
> 刪除遠端分支
#### **`git blame [file_name]`**
#### **`git blame -L [start-line],[end-line] [file-name]`**
> 找出改壞程式的兇手
