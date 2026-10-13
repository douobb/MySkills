---
name: manage-project-git
description: 安全處理首次 Git 初始化、指定範圍提交與推送，檢查差異、機密、私有路徑與待推送 commits；異常時停止並提供處理方案。
---

# 管理專案 Git

先確認只初始化、只提交、只推送或提交並推送。只有使用者明確授權才 commit／push；「上傳」已授權本次範圍的安全檢查、精確暫存、commit 與正常非強制 push，但提交前仍須確認訊息內容。這是內容決策，不是重新取得操作授權；其餘已授權正常步驟不重複詢問。只要求檢查／準備時到提交前回報。

## 提交訊息與方案確認

完成必要檢查後，在 commit 前展示建議 commit message，並列出精確提交範圍與推送目標作為背景（只提交時標示不推送）。已授權提交時，優先使用 `request_user_input` 詢問「要使用哪個 commit message？」並提供「採用建議訊息」「自行提供訊息」「稍後決定」與自由輸入；不要改問「是否允許 commit／push」，也不要僅因工具禁止權限請求就退回文字對話。

選擇調整但未提供新訊息時先取得完整內容；訊息未確認、回答為空、取消或選擇稍後決定時暫停提交，不把它們視為訊息已確認。取得有效內容後依既有授權接續執行，不再次詢問操作授權。使用者已明確指定本次訊息並要求執行時，視為已確認；只推送既有 commits 不另要求訊息確認。

衝突、分歧或目標不明時，先區分方案／內容選擇與新增操作授權：前者優先使用 `request_user_input`；後者依當前授權限制處理，系統命令批准另走權限流程。工具不可用或明確不允許內容確認時才退回一般對話等待。範圍或目標超出原授權時另取得授權；只有訊息內容改變時只確認新訊息，不重複要求提交／推送授權。

## 不可退讓的限制

- 保留使用者及無關 staged／unstaged 修改，只暫存本次精確範圍。同一檔案有混合修改時隔離本次 hunks；無法安全隔離就停止，不用整檔暫存納入他人修改。
- 不自動執行 `reset --hard`、`git clean`、捨棄修改、`commit --amend`、歷史重寫、強制推送、刪除分支或 `--no-verify`；不擅改 global 設定、remote、tag 或 release。
- `TODO.md`、`docs/PRD.md`、`docs/private/` 預設私有，核對 ignored／tracked／staged／outgoing 狀態。一般「全部上傳」不構成公開授權；特定 PRD／TODO 只有明確指定且通過內容檢查才可例外。`docs/private/` 與 HANDOFF 不直接上傳。
- `.gitignore` 不取消既有追蹤或清除歷史；敏感掃描不能保證發現全部洩漏，不輸出完整機密值。

## 正常提交與推送

1. 確認 Git root、branch／HEAD、狀態、差異、進行中的 Git 操作與目標 remote／upstream，界定本次檔案及 hunks。不是儲存庫時只在初始化已授權後讀取 [首次初始化](references/initialize-git.md)；目標不明先釐清。
2. 審查本次變更與預計納入檔案，檢查私有路徑、憑證、私鑰、API key、token、cookie／session、含帳密 URL／連線字串、個資、客戶資料、內部端點及未公開商業規劃；辨識多餘 log、匯出、備份、快取與產物。既有 secret scanner 優先，沒有時以檔名、模式及內容判讀，不擅自安裝。
3. 核對受影響的公開文件是否符合目前程式行為，執行相關既有測試／lint／build 與 `git diff --check`。只有使用者要求或交付正確性確實需要時才使用其他 Skill，不因提交全面更新 PRD、TODO、README 或交接。來源不明、二進位、大檔或高風險內容擴大檢查至受影響範圍，不掃描無關 ignored tree、不直接刪除多餘檔案。
4. 提交前核對有效的 Git 身分與專案簽署規範；精確暫存後審查完整 staged diff、檔案清單及 `git diff --cached --check`。非預期 staged 內容停止，不擅自 unstage 或一併提交。無變更不建立空 commit。commit message 遵循專案慣例，無慣例時使用簡潔繁體中文。
5. 推送前 fetch 目標 remote 一次，確認目標分支與 ahead／behind，檢查**所有待推送 commits 的差異與新增內容**，包含中間 commit 中曾加入又刪除的機密及私有檔案；不能只掃最終 diff。只推送既有 commit 同樣適用。本機落後、雙方分歧或目標不符時停止。
6. 檢查通過且遠端可正常 fast-forward 時 push；已有同名遠端分支但缺 upstream 時先確認它是正確目標，缺同名分支時可依明確上傳要求使用 `git push -u <remote> <branch>`。push 後核對遠端分支 HEAD 與本機 HEAD，回報剩餘工作樹。

狀態未變不重複掃描、驗證或 fetch；檔案、index、HEAD 或目標改變時只重跑失效檢查。

## 停止條件

疑似機密、私有文件意外 tracked／staged／outgoing、非預期暫存、detached HEAD、進行中的 Git 操作、衝突、分支分歧、重要驗證失敗、remote 不符、認證／權限／網路／hook／push 錯誤時停止擴大影響。需要處理方案時讀取 [異常處理](references/stop-mode.md)，提出證據、選項與建議，由使用者決定，不自行 pull／merge／rebase 或繞過檢查。

## 完成回報

列出已執行動作、branch／remote、commit、push 結果、敏感與文件檢查範圍、驗證限制及剩餘變更／風險。未成功推送或未核對遠端時不宣稱上傳完成。
