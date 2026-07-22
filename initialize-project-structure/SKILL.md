---
name: initialize-project-structure
description: 在空白目錄中建立最小化、與技術無關的專案初始架構，包含空白的中英文 README、PRD、TODO、文件與原始碼目錄、Git 目錄保留檔，以及一定排除 TODO.md 的通用 .gitignore。僅用於初始化空白目錄；不得修改既有專案、產生程式碼、安裝套件或初始化 Git。
---

# 初始化專案架構

只建立檔案與目錄；不得撰寫 README、PRD、TODO、原始碼或特定技術設定。

## 必要架構

在目前工作目錄建立：

```text
.
├── README.md
├── README.en.md
├── TODO.md
├── .gitignore
├── docs/
│   └── PRD.md
└── src/
    └── .gitkeep
```

除 `.gitignore` 外，下列檔案必須完全空白，不得加入標題、註解、模板、預留文字或空白字元：

```text
README.md
README.en.md
TODO.md
docs/PRD.md
src/.gitkeep
```

不要建立 `docs/.gitkeep`；`docs/PRD.md` 已能保留該目錄。

## 執行流程

### 1. 驗證目前目錄

將目前工作目錄視為專案根目錄；除非使用者明確要求，不要建立巢狀專案目錄。

建立任何內容前，檢查所有項目，包括隱藏項目。僅允許下列既有中繼資料：

```text
.git/
.DS_Store
Thumbs.db
desktop.ini
```

其他項目皆視為有意義的既有內容。若存在任何一項：

1. 立即停止，不建立任何內容。
2. 不得覆寫、刪除、移動或重新命名既有項目。
3. 列出阻止初始化的項目並回報目錄不是空白。

重複執行時，已產生的架構同樣算既有內容；不得修改或重設。

### 2. 建立架構

目錄通過驗證後，一次完成：

1. 建立 `docs/` 與 `src/`。
2. 建立所有必要空白檔案。
3. 建立以下 `.gitignore`：

```gitignore
# 本機專案規劃
TODO.md

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

`TODO.md` 必須是獨立且完全相符的忽略規則。不得忽略 `README.md`、`README.en.md`、`docs/`、`src/` 或 `.gitignore`，也不得加入語言或框架專用規則。

### 3. 驗證結果

確認：

- 必要目錄與檔案全部存在。
- 除 `.gitignore` 外，所有必要檔案大小皆為零。
- `.gitignore` 含獨立的 `TODO.md` 規則。
- 未建立任何未要求的項目，也未修改既有內容。

若 `.git/` 原本存在且 Git 可用，可選擇執行：

```bash
git check-ignore TODO.md
```

不得只為此檢查初始化 Git。

### 4. 回報

成功時列出必要架構，並確認空白檔案、`TODO.md` 忽略規則及未產生特定技術內容。可建議使用 README、PRD、TODO Skill 補充內容，或在公開散布前選擇授權；不得自動執行這些後續操作。

失敗時列出既有項目，並明確說明為避免混合或覆寫既有專案，本次未修改任何檔案。

## 安全界線

- 不得使用刪除或重設手段清空目錄，例如 `rm`、`Remove-Item`、`git clean` 或 `git reset --hard`。
- 不得選擇程式語言、框架或授權，也不得建立套件描述檔、技術設定、原始碼或空白 `LICENSE`。
- 不得安裝相依套件、初始化 Git，或暫存、提交、推送檔案。
- 只有使用者明確選擇或要求授權條款時，才能建立 `LICENSE`。

## 驗收條件

只有在目錄已先通過驗證、必要架構完全建立、空白檔案與 `.gitignore` 皆符合規格、未修改既有內容，且結果已驗證並回報時，才算完成。
