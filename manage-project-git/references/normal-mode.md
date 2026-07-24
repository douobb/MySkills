# 一般模式

用於既有儲存庫中範圍小、目的單一且沒有高風險訊號的變更。執行前必須套用主 Skill 的共通安全與文件底線。

## 執行流程

1. 一次確認 Git root、branch、HEAD、工作樹、staged／unstaged／untracked、remote／upstream、進行中的 Git 操作及本次範圍。
2. 檢查既有 staged 內容。若包含範圍外檔案，切換停止模式；不得擅自 unstage 或一併提交。
3. 只掃描預計提交的變更與檔案；若只推送既有 commit，亦檢查尚未存在於目標遠端的 outgoing commits，並確認 `TODO.md`、`docs/PRD.md`、`docs/private/` 沒有意外包含其中。
4. 套用敏感資訊與文件底線，只執行相關測試、lint、build 或 Skill 驗證。沒有實質變更時不得建立空 commit，除非使用者明確要求且理解用途。
5. 確認有效的 `user.name`、`user.email` 與簽署規範，不擅自修改 global 設定。
6. 以精確路徑暫存，檢查 staged 檔案、完整 staged diff 與 `git diff --cached --check`。
7. 依內容與既有慣例建立單一目的 commit；沒有慣例時使用簡潔繁體中文。不得自動 amend、簽署、建立 tag 或 release。
8. 需要 push 時，在內容穩定後執行一次 `git fetch --prune` 並比較目標分支：
   - 本機領先且未落後：執行一般 push。
   - upstream 缺失且遠端沒有同名分支：明確上傳要求可授權設定 upstream。
   - 本機落後、雙方分歧、remote 不符或 fetch 失敗：切換停止模式。
9. push 後比較本機 HEAD 與遠端追蹤分支，並檢查剩餘工作樹。

## 精簡與切換原則

- 不列出每個正常檔案大小、不掃描整個 ignored tree、不執行無關測試，也不在狀態未變時重複檢查。
- 正常流程只需簡短開始更新與完整最終回報；實質問題才追加更新。
- 發現不明檔案、二進位／大型產物、私有內容、高風險程式碼、混合目的、未審查 outgoing commits 或不明 remote／upstream 時，載入加強模式；任何停止條件則立即載入停止模式。
