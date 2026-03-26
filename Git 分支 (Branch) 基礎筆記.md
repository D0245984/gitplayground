Git 分支 (Branch) 基礎筆記
---

1. 核心概念：什麼是分支？
分支就像是遊戲的「平行世界」或是「存檔點」。你可以在分支上開發新功能，如果不滿意，直接刪除分支，主線完全不會受到影響。

2. 查看分支：git branch
這不只是取得位置，還能管理分支。

git branch：列出本地所有分支（目前所在的分支前會標註 * 號）。

git branch -a：列出所有分支（包含遠端伺服器上的分支）。

git branch [新分支名稱]：建立一個新的分支，但「不會」自動切換過去。

git branch -d [分支名稱]：刪除已合併的分支。

git branch -M [新名稱]：強制重新命名目前的分支（常用於將 master 改名為 main）。

3. 切換位置：git checkout
這是你在不同平行時空移動的指令。

git checkout [分支名稱]：切換到指定的分支。

git checkout -b [新分支名稱]：最強常用組合。等於「建立分支」+「直接切換過去」。

git checkout [檔案名稱]：(進階用法) 復原單一檔案到最後一次提交的狀態。

💡 注意：新版的 Git 建議使用 git switch 來專門負責切換分支，功能更單純安全。

4. 合併分支：git merge (重要補充)
當你在分支做完新功能，想把它帶回主線時：

先切換回主線：git checkout main

執行合併：git merge [新功能分支名稱]

5. 實戰流程範例
假設你要開發一個「登入功能」：

git checkout -b dev-login (建立並前往新分支)

(在 Vim 編輯檔案、git add、git commit)

git checkout main (回到主線)

git merge dev-login (把登入功能併入主線)

💡 筆記小撇步：如何看「位置」？
雖然 git branch 可以看你在哪個分支，但如果你想看「圖形化」的歷史軌跡，請記住這行指令：
git log --oneline --graph --all
這會用文字畫出一條漂亮的分支樹圖給你。

你需要我補充關於「解決衝突 (Conflict)」的處理筆記嗎？這是合併分支時最常遇到的問題。

---
Git 分支 (Branch) 基礎筆記
---

1. 核心概念：什麼是分支？
分支就像是遊戲的「平行世界」或是「存檔點」。你可以在分支上開發新功能，如果不滿意，直接刪除分支，主線完全不會受到影響。

2. 查看分支：git branch
這不只是取得位置，還能管理分支

git branch：列出本地所有分支（目前所在的分支前會標註 * 號）。

git branch -a：列出所有分支（包含遠端伺服器上的分支）。

git branch [新分支名稱]：建立一個新的分支，但「不會」自動切換過去。

git branch -d [分支名稱]：刪除已合併的分支。

git branch -M [新名稱]：強制重新命名目前的分支（常用於將 master 改名為 main）。

3. 切換位置：git checkout
這是你在不同平行時空移動的指令。

git checkout [分支名稱]：切換到指定的分支。

git checkout -b [新分支名稱]：最強常用組合。等於「建立分支」+「直接切換過去」。

git checkout [檔案名稱]：(進階用法) 復原單一檔案到最後一次提交的狀態。

💡 注意：新版的 Git 建議使用 git switch 來專門負責切換分支，功能更單純安全。

4. 合併分支：git merge (重要補充)
當你在分支做完新功能，想把它帶回主線時：

先切換回主線：git checkout main

執行合併：git merge [新功能分支名稱]

5. 實戰流程範例
假設你要開發一個「登入功能」：

git checkout -b dev-login (建立並前往新分支)

(在 Vim 編輯檔案、git add、git commit)

git checkout main (回到主線)

git merge dev-login (把登入功能併入主線)

💡 筆記小撇步：如何看「位置」？
雖然 git branch 可以看你在哪個分支，但如果你想看「圖形化」的歷史軌跡，請記住這行指令：
git log --oneline --graph --all
這會用文字畫出一條漂亮的分支樹圖給你。

你需要我補充關於「解決衝突 (Conflict)」的處理筆記嗎？這是合併分支時最常遇到的問題。

---