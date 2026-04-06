# Git 初學者筆記

## 前言
這份筆記是為完全沒有 Git 經驗的初學者設計的。Git 是最流行的版本控制系統，能幫助你管理程式碼的歷史版本、與團隊協作，並避免遺失重要檔案。本筆記將從基礎概念開始，逐步介紹實用命令和最佳實踐。

---

## 1. 什麼是 Git？
Git 是一套**分散式版本控制系統**，由 Linux 創始人 Linus Torvalds 開發。它就像一個「時間機器」，記錄你專案的每一次變更，讓你可以隨時回到過去的任何狀態。

### 為什麼需要版本控制？
- **追蹤變更**：知道什麼時候改了什麼，為什麼改
- **多人協作**：避免覆蓋彼此的程式碼
- **備份與恢復**：出了錯可以快速回到正確版本
- **分支開發**：同時開發多個功能而不互相干擾

### Git vs GitHub
- **Git**：版本控制軟體
- **GitHub**：線上平台，存放 Git 倉庫，提供協作功能

---

## 2. 安裝與設定 Git
### 安裝
- **Windows**：下載 Git for Windows (https://git-scm.com/download/win)
- **macOS**：`brew install git` 或下載安裝包
- **Linux**：`sudo apt install git` (Ubuntu/Debian)

### 基本設定
```bash
# 設定使用者名稱和郵箱（全域設定）
git config --global user.name "你的名字"
git config --global user.email "你的郵箱@example.com"

# 檢查設定
git config --list
```

💡 **提示**：郵箱會顯示在提交歷史中，使用真實郵箱以便聯繫。

---

## 3. Git 核心概念：三個區域
理解 Git 的三個區域是學習 Git 的關鍵：

1. **工作目錄 (Working Directory)**：你正在編輯的檔案
2. **暫存區 (Staging Area)**：準備提交的檔案集合
3. **儲存庫 (Repository)**：已提交的歷史記錄

### 工作流程
```
編輯檔案 → git add → git commit → 儲存庫
     ↑           ↑
     └─ 工作目錄  └─ 暫存區
```

---

## 4. 建立 Git 倉庫
### 初始化新倉庫
```bash
# 在專案資料夾中執行
git init
```
這會建立 `.git` 隱藏資料夾，存放所有 Git 資料。

### 複製現有倉庫
```bash
git clone https://github.com/user/repo.git
```

---

## 5. 基本操作命令
### 查看狀態
```bash
git status
```
顯示：
- 未追蹤的檔案 (Untracked)
- 已修改但未暫存 (Modified)
- 已暫存等待提交 (Staged)

### 加入暫存區
```bash
# 加入特定檔案
git add filename.txt

# 加入所有變更
git add .

# 互動式加入
git add -p
```

### 提交變更
```bash
# 提交並加上訊息
git commit -m "新增登入功能"

# 修改最後一次提交訊息
git commit --amend -m "新訊息"
```

💡 **提交訊息寫法**：
- 使用英文或中文，保持一致
- 第一行簡短描述（50字內）
- 詳細說明用空行分隔
- 範例：`feat: add user authentication`

### 查看歷史
```bash
# 完整歷史
git log

# 簡潔模式
git log --oneline

# 圖形化分支歷史
git log --oneline --graph --all
```

### 比較差異
```bash
# 工作目錄 vs 暫存區
git diff

# 暫存區 vs 最後提交
git diff --staged

# 比較兩個提交
git diff commit1 commit2
```

---

## 6. 分支管理
分支讓你可以同時開發多個功能。

### 基本分支操作
```bash
# 查看分支
git branch

# 建立分支
git branch feature/login

# 切換分支
git checkout feature/login

# 建立並切換
git checkout -b feature/login

# 刪除分支
git branch -d feature/login
```

### 合併分支
```bash
# 切換到主分支
git checkout main

# 合併功能分支
git merge feature/login
```

### 合併衝突解決
當合併時發生衝突：
1. Git 會標記衝突檔案
2. 編輯檔案選擇保留的內容
3. 移除衝突標記 (`<<<<<<<`, `=======`, `>>>>>>>`)
4. 加入並提交

```bash
git add conflicted-file.txt
git commit  # 無需 -m，Git 會自動產生訊息
```

💡 **避免衝突**：頻繁提交，及時同步。

---

## 7. 遠程倉庫操作
### 連接遠程倉庫
```bash
# 新增遠程
git remote add origin https://github.com/user/repo.git

# 查看遠程
git remote -v
```

### 推送與拉取
```bash
# 推送分支
git push -u origin main

# 拉取更新
git pull

# 僅獲取（不合併）
git fetch
```

### 常見遠程操作
```bash
# 複製倉庫
git clone https://github.com/user/repo.git

# 推送新分支
git push -u origin feature/new-feature

# 刪除遠程分支
git push origin --delete feature/old
```

---

## 8. 復原與修正
### 取消變更
```bash
# 放棄工作目錄變更
git checkout -- file.txt

# 取消暫存
git reset HEAD file.txt

# 取消最後一次提交（保留檔案）
git reset --soft HEAD~1

# 取消最後一次提交（刪除檔案變更）
git reset --hard HEAD~1
```

### 建立修復提交
```bash
# 取消特定提交（建立新提交）
git revert commit-hash
```

### 暫存工作
```bash
# 暫存目前工作
git stash

# 恢復並刪除暫存
git stash pop

# 查看暫存列表
git stash list
```

---

## 9. .gitignore 檔案
告訴 Git 忽略哪些檔案。

建立 `.gitignore` 檔案，內容範例：
```
# 依賴套件
node_modules/
__pycache__/

# 系統檔案
.DS_Store
Thumbs.db

# IDE 設定
.vscode/
.idea/

# 敏感檔案
.env
secrets.json

# 建構輸出
dist/
build/
```

💡 **提示**：可以從 https://gitignore.io 產生適合的 .gitignore 檔案。

---

## 10. 進階技巧
### 互動式 rebase
整理提交歷史：
```bash
git rebase -i HEAD~3
```

### 標籤版本
```bash
# 建立輕量標籤
git tag v1.0

# 建立附註標籤
git tag -a v1.0 -m "版本 1.0"

# 推送標籤
git push origin v1.0
```

### 子模組
管理外部專案：
```bash
git submodule add https://github.com/user/library.git libs/library
```

---

## 11. 常見錯誤與解決
### 常見問題
1. **"fatal: not a git repository"**
   - 確認在正確資料夾，或執行 `git init`

2. **"Changes not staged for commit"**
   - 記得先 `git add` 再 `git commit`

3. **合併衝突**
   - 編輯衝突檔案，移除標記，然後 `git add` 和 `git commit`

4. **"Permission denied"**
   - 檢查 SSH 金鑰設定，或使用 HTTPS URL

5. **"Detached HEAD"**
   - 切回分支：`git checkout main`

### 緊急救援
```bash
# 查看所有操作歷史
git reflog

# 找回丟失的提交
git checkout commit-hash
```

---

## 12. Git 工作流程
### 推薦的工作流程
1. **主分支 (main/master)**：保持穩定，只接受合併
2. **開發分支 (develop)**：整合各功能分支
3. **功能分支 (feature/)**：開發新功能
4. **修復分支 (hotfix/)**：緊急修復生產問題

### 日常開發流程
```bash
# 1. 同步最新程式碼
git checkout main
git pull

# 2. 建立功能分支
git checkout -b feature/new-feature

# 3. 開發並提交
git add .
git commit -m "實作新功能"

# 4. 推送分支
git push -u origin feature/new-feature

# 5. 建立 Pull Request/Merge Request
# 在 GitHub/GitLab 上操作
```

---

## 13. 最佳實踐
- **頻繁提交**：小步前進，避免大提交
- **清晰訊息**：寫有意義的提交訊息
- **分支策略**：使用適當的分支命名和流程
- **定期同步**：避免與遠程差太多
- **不要提交**：大檔案、二進位檔案、敏感資訊
- **學習命令**：熟練基本命令後學習進階功能

---

## 14. 學習資源
### 官方資源
- [Git 官方文件](https://git-scm.com/doc)
- [Pro Git 書籍](https://git-scm.com/book/zh-tw) (免費線上閱讀)

### 互動式學習
- [Learn Git Branching](https://learngitbranching.js.org/) - 互動式遊戲
- [GitHub Learning Lab](https://lab.github.com/) - 實作課程

### 中文資源
- [Git 教學 - 為你自己學 Git](https://gitbook.tw/)
- [Git 學習筆記](https://hackmd.io/@eMP9zUQMS3O1zH6iKm9YFw/git-tutorial)

### 工具與視覺化
- [GitKraken](https://www.gitkraken.com/) - Git GUI 工具
- [SourceTree](https://www.sourcetreeapp.com/) - 免費 Git 客戶端

---

## 總結
Git 是一個強大的工具，但學習曲線稍陡。建議從基本命令開始練習，多使用 `git status` 和 `git log` 觀察狀態。熟練後，你會發現 Git 讓開發變得更有條理和安全。

記住：**不要害怕嘗試**，Git 的設計讓大多數操作都可以復原。持續練習，你很快就能掌握這個重要的開發工具！

---

*最後更新：2024年*  
*歡迎提出建議和修正！*

- 「Permission denied」：檢查 SSH 金鑰或權限設定。

- 「Detached HEAD」：切回分支：git checkout main。

---

16. Git 最佳實踐
- 頻繁 commit，小步前進。

- 寫清楚的提交訊息。

- 使用分支開發新功能。

- 定期 push 到遠程倉庫。

- 不要 commit 大檔案或敏感資訊。

- 學習使用 git rebase 整理提交歷史（進階）。

---

17. 學習資源
- 官方文件：https://git-scm.com/doc

- GitHub 教學：https://guides.github.com/

- 互動式學習：https://learngitbranching.js.org/

- 中文資源：Git 官方書《Pro Git》有中文版。

---

持續更新中... 有任何建議歡迎提出！

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
