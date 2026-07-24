# 加強模式

用於首次初始化、內容不明或風險較高的變更。本檔是完整流程，不需先讀一般模式；執行前仍須套用主 Skill 共通底線。

## 擴大盤點

- 完整確認 root、branch、HEAD、工作樹、staged／unstaged／untracked／ignored、remote／upstream、進行中的 Git 操作與本次範圍。
- 逐檔檢查 unfamiliar、binary、large、generated、archive、database、export、backup、log、cache、coverage、build、IDE／OS 中繼資料及無長期價值的紀錄。
- 確認 `.gitignore` 涵蓋不應追蹤項目且未誤排必要來源；不得以通用模板覆寫既有規則。
- 優先使用儲存庫既有 secret scanner；否則採檔名、內容模式與語意檢查，不自動安裝工具。
- 檢查完整 staged diff、必要 outgoing commits 與歷史暴露風險。只有 binary 或大小異常時才逐一回報大小並提出 Git LFS 等選項。
- 擴大文件一致性與既有驗證至所有受影響領域。其他 Skill 修改後重新分類，只重跑受影響檢查。

不得直接刪除多餘檔案；列出精確路徑、理由及忽略、保留、移除或改放位置等方案，由使用者決定。

## 流程 A：第一次初始化

1. 檢查所有一般與隱藏項目；已有 Git 儲存庫時改走流程 B。
2. 檢查敏感資訊、多餘檔案與 `.gitignore`。預設以完全相符的獨立規則排除 `TODO.md`、`docs/PRD.md`、`docs/private/`、真實 `.env` 與確認的產生物；保留既有規則且不重複。PRD／TODO 只有在使用者指定精確路徑並通過公開檢查後才可例外，`docs/private/` 不得例外直接上傳。
3. 未指定分支時使用 `main` 並說明；以 `git init -b <branch>` 初始化，舊版 Git 使用等價且非破壞性方式。
4. 只有使用者提供或確認 URL 時才新增 remote。建立託管儲存庫前確認平台、名稱、擁有者與 public／private，不推定公開性。
5. 只要求初始化時到此停止，不建立 commit 或 push。
6. 首次提交前確認 `user.name`、`user.email` 與簽署規範，不擅改 global 設定；精確暫存、審查完整 staged diff 與 `git diff --cached --check` 後提交。
7. 接近 push 時查詢遠端一次；沒有同名分支時可執行 `git push -u <remote> <branch>`。不相關遠端歷史切換停止模式。

初始化不等於建立骨架、選擇授權、建立遠端、commit 或 push。不得自動建立 `LICENSE`、合併不相關歷史或強制推送。

## 流程 B：既有儲存庫

1. 建立精確檔案清單；多個無關目的提出原子提交方案，由使用者決定是否拆分。
2. 檢查既有 staged 內容；混有範圍外檔案時切換停止模式，不擅自 unstage 或一併提交。
3. 完成擴大盤點、敏感資訊與文件同步，以及所有受影響領域的既有驗證；另確認受保護路徑沒有意外出現在 tracked、staged 或 outgoing 集合。
4. 不建立空 commit。精確暫存，審查完整 staged diff 與 `git diff --cached --check`，再建立單一目的 commit。
5. 需要 push 時，在內容穩定後 fetch 一次：本機僅領先則一般 push；缺 upstream 且遠端無同名分支時可依明確上傳要求設定；落後、分歧、remote 不符或 fetch 失敗則切換停止模式。
6. push 後比較本機 HEAD 與遠端追蹤分支，並檢查剩餘工作樹。

不得為略過檢查而降級模式。出現停止條件時，立即停止擴大影響並載入停止模式。
