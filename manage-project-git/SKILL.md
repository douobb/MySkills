---
name: manage-project-git
description: 依風險分級安全管理專案 Git 初始化、提交與推送。用於第一次 git init、設定初始分支與遠端、建立初始提交，或在既有儲存庫檢查變更、同步文件、掃描敏感資訊與多餘檔案、驗證、精確暫存、提交及上傳。低風險變更採一般模式；首次初始化、不明檔案或高風險變更採加強模式；遇到版本差異、衝突、失敗、機密或混合暫存內容時切換停止模式並由使用者選擇方案。
---

# 管理專案 Git

依風險載入足夠且不重複的流程。主檔只負責模式選擇與共通底線；各模式完整程序位於 `references/`。

## 核心原則

- 先確認只初始化、只提交、只推送或提交並推送，不擴大外部變更。
- 明確要求「上傳」代表授權通過檢查後執行一般暫存、commit 與非強制 push；正常階段不重複詢問。
- 只處理本次範圍，保留無關修改、分支、tag、remote 與 staged 狀態；只以精確路徑暫存。
- 掃描只能降低風險，不得保證沒有機密或輸出完整機密值。
- 不得自動執行 `reset --hard`、`clean`、捨棄修改、刪除分支、`commit --amend`、重寫歷史或強制推送。

## 選擇流程與模式

先解析 Git 根目錄。不是儲存庫或要求首次初始化時走流程 A，否則走流程 B。巢狀儲存庫、submodule、worktree 或目標不明時先釐清範圍。

| 模式 | 適用條件 |
|---|---|
| 一般模式 | 既有儲存庫、小型且單一目的的文字或原始碼變更、remote 與 upstream 明確，沒有異常 staged 內容或高風險訊號 |
| 加強模式 | 首次初始化、大量且來源未確認的 untracked 或其他內容不明檔案、二進位／大型／產生檔、環境或認證設定、私有文件、高風險或跨領域程式碼、混合目的變更、未審查 outgoing commits、remote／upstream 不明 |
| 停止模式 | 疑似機密、無關的既有 staged 內容、detached HEAD、進行中的 Git 操作、衝突、重要驗證失敗、remote 不符、本機落後或雙方分歧，以及認證、權限、hook 或 push 錯誤 |

採用符合任一條件的最高風險模式。不要只因 untracked 檔案的存在或數量自動採加強模式；由本次工作建立、來源與用途明確、內容已檢查且大小正常的小型文字檔，可維持一般模式。其他情況依類型、來源、任務關聯與風險判斷。只要求檢查或準備提交時，在提交前報告後停止。

## 必要 Reference

模式選定後，在執行該模式檢查或任何改變 Git 狀態的動作前，必須完整讀取：

- 一般模式：[`references/normal-mode.md`](references/normal-mode.md)
- 加強模式或流程 A：[`references/enhanced-mode.md`](references/enhanced-mode.md)
- 任何停止條件：立即停止擴大影響，完整讀取 [`references/stop-mode.md`](references/stop-mode.md) 後回報。

Reference 不是選讀摘要。執行中模式改變時先讀取新模式檔案；不要載入未觸發模式的 reference。

## 共通安全與文件底線

至少檢查 `.env`、憑證、私鑰、雲端認證、cookie、session、連線字串、含帳密 URL、API key、token、password、個人或客戶資料、內部端點、商業規劃、未公開 PRD／TODO 與 `docs/private/`。疑似機密立即切換停止模式。

將 `TODO.md`、`docs/PRD.md` 與 `docs/private/` 視為受保護路徑：每次暫存前確認其 ignored／tracked／staged／outgoing 狀態。一般的「全部上傳」不等於公開這些路徑；只有使用者明確指定精確 PRD 或 TODO，且通過內容檢查後才可納入。`docs/private/` 與 `HANDOFF.md` 不得直接上傳，應改寫成去除私有脈絡的公開文件。受保護內容意外已追蹤、暫存或存在於待推送 commit 時切換停止模式。

依條件使用其他可用 Skill：

- 已驗證的功能、指令、設定、限制、版本或結構改變：使用 `$write-project-readme`。
- `docs/` 含開發紀錄、重複或私有內容：使用 `$manage-project-docs`；需要確認時暫停 Git 流程。
- 本機 `TODO.md` 狀態改變：使用 `$write-project-todo`，維持忽略且不因同步而上傳。
- 產品需求確實改變且使用者要求更新：使用 `$write-project-prd`；PRD 預設維持私有與忽略。
- 空白目錄同時需要專案骨架：先使用 `$initialize-project-structure`，再回到流程 A。
- 大範圍或高風險程式碼需交付前審查：使用 `$code-review` 產生唯讀結果。

只執行儲存庫既有且與變更相關的驗證。執行 `git diff --check`，提交前另執行 `git diff --cached --check`。不得自行安裝相依套件、變更工具鏈或以 `--no-verify` 掩蓋錯誤。

## 流程路由與檢查失效

- **流程 A**：一律選加強模式；初始化不自動包含骨架、授權、遠端建立、commit 或 push。
- **流程 B**：先建立精確變更清單，再選一般或加強模式；發現停止條件即切換停止模式。
- 同一狀態只執行一次相同檢查。只有檔案、index、HEAD、branch、remote 改變，其他 Skill 修改內容、整合或解決衝突、經過較長時間，或外部程序可能改動時，才重新分類並重跑受影響檢查。

## 完成回報

簡潔列出模式與動作、branch／remote、新 commit 與納入檔案、敏感及多餘檔案檢查範圍、文件同步、成功或未執行的驗證、push 與本機／遠端一致性，以及剩餘變更或風險。只有已授權動作成功、需要 push 時已驗證遠端一致性，且沒有隱藏風險時才回報完成。
