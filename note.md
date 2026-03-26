Linux 常用指令筆記
1. ls (List) - 列出檔案與目錄
用於查看當前目錄下的內容。
---
常用參數：

ls -a：顯示所有檔案，包含以 . 開頭的隱藏檔（如 .gitignore）。

ls -l：以詳細清單格式顯示（包含權限、擁有者、檔案大小、修改日期）。

ls -h：與 -l 搭配（ls -lh），將檔案大小以易讀格式（如 KB, MB）顯示。

ls -R：遞迴列出所有子目錄內的檔案。
---
2. rm (Remove) - 刪除檔案或目錄
注意： Linux 中刪除後通常無法從回收桶找回。

常用參數：

rm -i：刪除前先詢問確認（較安全）。

rm -f：強制刪除，忽略不存在的檔案且不詢問。

rm -r (或 -R)：遞迴刪除，用於刪除整個目錄及其內容。

rm -rf：最常用的組合，強制刪除整個目錄（使用時需極度小心）。

3. touch - 新增檔案 / 更新時間戳記
主要用於快速建立一個空檔案。

用法範例：

touch index.html：建立一個名為 index.html 的空檔案。

如果檔案已存在，touch 會更新該檔案的「最後修改時間」而不會更動內容。

4. pwd (Print Working Directory) - 顯示目前所在目錄
說明： 你的筆記中提到 "print word document" 是不正確的誤植。其全稱是 Print Working Directory，意即「印出目前的工作目錄」。

它會顯示從根目錄 (/) 開始的完整路徑。

Git 設定 (Git Config)
Git 設定主要分為三個層級：--system（系統）、--global（使用者）、--local（單一專案）。

使用者識別設定 (Global)
這是安裝 Git 後必須執行的首要設定，這些資訊會出現在你的 Commit（提交）紀錄中。

設定使用者名稱：
git config --global user.name "eeff5049"

設定電子郵件：
git config --global user.email "eeff5049@gmail.com"

常用管理指令
列出目前所有設定：
git config --list
（這可以讓你確認目前的 user.name 與 user.email 是否正確）

編輯設定檔：
git config --global --edit
（會開啟文字編輯器讓你直接修改設定檔）

💡 學習小撇步
在 Linux 中，如果你想查詢任何指令的詳細完整參數，可以輸入：
man [指令名稱] (例如 man ls)
這會開啟該指令的 Manual page (說明手冊)。

