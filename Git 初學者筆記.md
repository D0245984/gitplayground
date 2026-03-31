Git 初學者筆記
---

1. 什麼是 Git？
Git 是一套「版本控制系統」，簡單來說就是幫你的專案做「時光機」。每一次的提交 (Commit) 都是一個存檔點，你可以隨時回到過去的任何一個版本。

為什麼要用 Git？
- 不再需要「報告_final_final_真的最終版.docx」這種命名方式。
- 多人協作時不會互相覆蓋對方的程式碼。
- 出了錯可以快速回到上一個正確的版本。

---

2. 建立 Git 倉庫：git init
在你想要開始版本控制的資料夾中執行：

git init

這會在資料夾中建立一個隱藏的 .git 目錄，Git 的所有紀錄都存放在裡面。

💡 注意：只需要在專案「第一次」初始化時執行一次就好。

---

3. 查看目前狀態：git status
這是你最常用的指令之一，用來查看目前的工作狀態。

git status

它會告訴你：
- 哪些檔案被修改了（紅色 = 尚未加入暫存區）。
- 哪些檔案已加入暫存區（綠色 = 準備被提交）。
- 哪些檔案是全新的、尚未被 Git 追蹤的。

---

4. Git 的三個區域（核心概念）
這是理解 Git 最重要的觀念：

工作目錄 (Working Directory)：你正在編輯的檔案所在之處。

暫存區 (Staging Area)：你「挑選」好、準備提交的檔案會放在這裡。

儲存庫 (Repository)：正式提交後的紀錄，也就是你的存檔點。

流程：編輯檔案 → git add（放入暫存區）→ git commit（正式存檔）

---

5. 加入暫存區：git add
把修改過的檔案「挑選」出來，準備提交。

git add [檔案名稱]：加入指定檔案。

git add .：加入目前目錄下所有變更的檔案（方便但要小心，避免加入不該提交的檔案）。

💡 小技巧：用 git status 確認你要加入的檔案是否正確，再執行 git add。

---

6. 正式提交：git commit
把暫存區的檔案正式存檔，並附上一段說明訊息。

git commit -m "你的提交訊息"

好的提交訊息範例：
- git commit -m "add: 新增登入頁面 HTML 結構"
- git commit -m "fix: 修正首頁圖片無法顯示的問題"
- git commit -m "update: 更新 README 說明文件"

💡 提交訊息很重要！未來回頭看紀錄時，好的訊息能讓你一眼看出這次改了什麼。

---

7. 查看提交歷史：git log
查看過去所有的提交紀錄。

git log：顯示完整的提交歷史（包含作者、日期、訊息）。

git log --oneline：精簡模式，每個提交只顯示一行（推薦日常使用）。

git log --oneline --graph --all：圖形化顯示所有分支的歷史軌跡。

---

8. 比較差異：git diff
查看檔案被修改了哪些內容。

git diff：比較工作目錄與暫存區的差異（你改了什麼但還沒 add）。

git diff --staged：比較暫存區與最後一次提交的差異（你 add 了什麼但還沒 commit）。

---

9. 復原操作
不小心改錯了？Git 提供了幾種「後悔藥」：

git checkout [檔案名稱]：放棄工作目錄中該檔案的修改，回到上次提交的狀態。

git reset HEAD [檔案名稱]：把已加入暫存區的檔案移回工作目錄（取消 git add）。

git reset --soft HEAD~1：撤銷最近一次提交，但保留修改在暫存區。

💡 注意：git reset --hard 會永久丟失未提交的修改，使用前請三思！

---

10. 忽略檔案：.gitignore
有些檔案不需要被 Git 追蹤（例如密碼設定檔、暫存檔、套件目錄等）。在專案根目錄建立 .gitignore 檔案：

常見的 .gitignore 內容：
node_modules/
.env
*.log
.DS_Store

每行寫一個要忽略的檔案或目錄名稱，Git 就不會再追蹤它們。

---

11. 遠端倉庫基礎：git remote / push / pull
當你想把本地的程式碼上傳到 GitHub 等平台時：

git remote add origin [遠端倉庫網址]：將本地倉庫連結到遠端倉庫（第一次設定）。

git push -u origin main：將本地的 main 分支推送到遠端（第一次推送需加 -u）。

git push：之後推送只需要這樣即可。

git pull：從遠端拉取最新的程式碼到本地（建議每次開始工作前先執行）。

git clone [遠端倉庫網址]：複製一份完整的遠端倉庫到你的電腦（第一次取得專案時使用）。

---

12. 完整實戰流程
假設你從零開始一個新專案：

mkdir my-project（建立專案資料夾）

cd my-project（進入資料夾）

git init（初始化 Git）

touch index.html（建立檔案）

vim index.html（用 Vim 編輯檔案）

git add index.html（加入暫存區）

git commit -m "add: 建立首頁 HTML"（提交）

git remote add origin https://github.com/你的帳號/my-project.git（連結遠端）

git push -u origin main（推送到 GitHub）

---

💡 學習小撇步
- 不確定的時候就用 git status，它是你最好的朋友。
- 養成「小步提交」的習慣：每完成一個小功能就提交一次，不要等全部做完才提交。
- 提交訊息用動詞開頭：add、fix、update、remove、refactor。
- 搭配本倉庫的「Git 分支 (Branch) 基礎筆記」一起學習，效果更好！

---
