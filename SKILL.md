---
name: php-style-check
description: "檢查 PHP 檔案是否符合 PER Coding Style 3.0 或 PSR-12 風格規範。當用戶要求 PHP coding style 檢查、風格檢查、格式規範、PER style、PSR-12、程式碼格式化檢查時觸發。支援檢查當前檔案、指定 git commit、或 git 分支內的 PHP 檔案。支援報告模式（僅列出問題）與修復模式（直接修正檔案）。"
---

# PHP Coding Style Check

檢查 PHP 檔案是否符合 PER Coding Style 3.0 或 PSR-12 風格規範。

## 執行流程

### 步驟一：確認檢查範圍

根據 ARGUMENTS 或詢問用戶，確定檢查來源：

| 來源 | 取得方式 |
|------|----------|
| 當前檔案 | 直接 Read 指定路徑的 PHP 檔案 |
| Git commit | `git show <commit>:<file>` 取得檔案內容；`git diff-tree --no-commit-id --name-only -r <commit> -- '*.php'` 取得變更清單 |
| Git branch | `git diff <base>...<branch> --name-only -- '*.php'` 取得差異清單，Read 工作目錄檔案 |

若未提供參數，詢問用戶：
```
請選擇檢查範圍：
1. 指定檔案路徑
2. 指定 git commit（檢查該 commit 變更的 PHP 檔案）
3. 指定 git branch（檢查該分支與 base branch 的差異 PHP 檔案）
```

多檔案時列出清單讓用戶確認，或全部檢查。

### 步驟二：確認規範版本

詢問用戶（或從參數取得）：
```
請選擇風格規範：
1. [預設] PER Coding Style 3.0（涵蓋 PHP 8.x 特性）
2. PSR-12（適用 PHP 7.x 專案）
```

選擇後讀取對應的規範參考文件：
- PER 3.0 → 讀取 `references/per-coding-style.md`
- PSR-12 → 讀取 `references/psr-12.md`

### 步驟三：確認執行模式

```
請選擇執行模式：
1. [預設] 報告模式（僅列出風格問題，不修改檔案）
2. 修復模式（直接修正風格問題，修復後輸出變更摘要）
```

### 步驟四：取得檔案內容

根據步驟一的來源讀取檔案：
- **當前檔案**：直接 Read
- **Git commit**：使用 `git show <commit>:<filepath>` 取得該版本內容
- **Git branch**：Read 工作目錄中的檔案

### 步驟五：逐規則檢查

讀取對應規範文件後，按章節逐項比對：

**檢查優先順序**（從高到低）：
1. 縮排與空格（最常見的風格問題）
2. 大括號位置（控制結構、類別、方法）
3. 關鍵字與型別大小寫
4. 行長度與空行
5. 宣告順序（declare/namespace/use）
6. 參數列表與返回型別格式
7. 運算子空格
8. Trailing commas（僅 PER 3.0）
9. PHP 8.x 特性格式（僅 PER 3.0：enum、match、attributes、property hooks）

**嚴重性分級**：
- **Error**：違反 MUST / MUST NOT 規則（必須修正）
- **Warning**：違反 SHOULD / SHOULD NOT 規則（建議修正）

### 步驟六：產出報告或執行修復

- **報告模式**：按 `templates/style-report.md` 格式輸出完整報告
- **修復模式**：
  1. 使用 Edit 工具逐項修正風格問題
  2. 優先修正 Error，再修正 Warning
  3. 修復完成後輸出變更摘要（哪些行做了什麼改動）
  4. 若有無法自動修復的問題，在摘要中標註

### 步驟七：詢問存檔

報告完成後詢問：
```
是否需要存檔風格檢查報告？
1. 存檔至預設路徑：docs/report/style-check-{ClassName}-{date}.md
2. 自訂路徑
3. 不存檔
```

## 注意事項

- 此 skill 聚焦**格式風格**（縮排、空格、大括號位置、行長度等），不涉及程式碼品質（架構、命名、邏輯）
- 每個問題必須標明**具體行號**，方便定位
- 即使全部通過，也要列出「符合規範亮點」，讓用戶知道哪些做得好
- Git commit/branch 模式下，僅檢查 `.php` 副檔名的檔案
