---
name: initialize-project-structure
description: 僅在空白目錄建立固定、技術無關的專案骨架與私有文件忽略規則；不撰寫文件內容、不產生程式碼或初始化 Git。
---

# 初始化專案架構

以目前工作目錄為根目錄，除非使用者指定其他位置。先檢查含隱藏項目的全部內容；僅允許既有 `.git/`、`.DS_Store`、`Thumbs.db`、`desktop.ini`。存在其他內容就停止，列出阻擋項目並說明「未修改」。重複執行同樣適用，不用刪除、reset 或 clean 清空目錄。

## 固定產物

```text
.
├── README.md
├── README.en.md
├── TODO.md
├── .gitignore
├── docs/
│   ├── .gitkeep
│   ├── PRD.md
│   └── private/
└── src/
    └── .gitkeep
```

通過檢查後建立骨架。除 `.gitignore` 外，所有檔案完全空白，不含標題、模板、註解或空白字元。`docs/private/` 保持空白且不放 `.gitkeep`；clone 後可能不存在，寫入私有文件時才補建。

`.gitignore` 預設內容：

```gitignore
# 本機專案規劃與私有文件
TODO.md
docs/PRD.md
docs/private/

# 環境變數與本機機密
.env
.env.*
!.env.example

# 作業系統中繼資料
.DS_Store
Thumbs.db
desktop.ini

# 編輯器暫存檔
*.swp
*.swo
*~
*.tmp
*.temp

# 日誌
*.log

# 通用產生輸出
dist/
build/
coverage/
.cache/
```

三個私有路徑使用獨立規則；只有使用者明確要求公開特定 PRD／TODO 且經敏感內容檢查後，才可調整該規則。`docs/private/` 不直接公開。不得忽略整個 `docs/`、README、`src/` 或公開的 `.gitkeep`。

不選框架、語言或授權，不建立原始碼、套件設定或 LICENSE，不安裝套件、初始化 Git、暫存、提交或推送。

## 驗證與回報

確認固定產物齊全、空白檔案大小為零、私有目錄沒有 `.gitkeep`、忽略規則正確且沒有非預期變更。已有 Git 時可用 `git check-ignore` 核對私有路徑與公開保留檔，不為檢查而初始化 Git。

成功時簡短列出骨架，明確告知 TODO、PRD 與私有目錄預設被排除、不隨一般提交上傳，並說明 clone 的目錄限制。若有明確公開例外，回報精確路徑與檢查結果。建立失敗時如實回報部分產物；只有尚未寫入時才能說「未修改」。
