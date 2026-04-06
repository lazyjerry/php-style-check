[English](README.md) | [简体中文](README_CN.md) | 繁體中文 | [日本語](README_JP.md) | [한국어](README_KR.md)

# PHP 程式碼風格檢查

一個 VS Code Copilot 技能，用於檢查 PHP 檔案是否符合 **PER Coding Style 3.0** 或 **PSR-12** 風格規範。支援報告模式（僅列出問題）與修復模式（直接修正檔案）。

## 功能特色

- 檢查當前檔案、指定 git commit 或 git 分支中的風格違規
- 支援 **PER Coding Style 3.0**（涵蓋 PHP 8.x 特性）與 **PSR-12**（適用於 PHP 7.x 專案）
- 兩種執行模式：**報告**（列出問題）與 **修復**（自動修正）
- 嚴重性分級：**Error**（違反 MUST / MUST NOT 規則）與 **Warning**（違反 SHOULD / SHOULD NOT 規則）
- 詳細報告，每個問題標註具體行號

## 觸發關鍵詞

當使用者提及以下內容時觸發此技能：
- PHP 程式碼風格檢查
- 風格檢查 / 格式檢查
- PER style / PSR-12
- 程式碼格式化檢查

## 工作流程

### 步驟一：確認檢查範圍

| 來源 | 取得方式 |
|------|----------|
| 當前檔案 | 直接讀取指定路徑的 PHP 檔案 |
| Git commit | 使用 `git show <commit>:<file>` 取得檔案內容；`git diff-tree` 取得變更清單 |
| Git branch | 使用 `git diff <base>...<branch>` 取得差異清單，讀取工作目錄檔案 |

### 步驟二：選擇風格規範

| 選項 | 說明 |
|------|------|
| PER Coding Style 3.0（預設） | 涵蓋 PHP 8.x 特性（enum、match、attributes、property hooks） |
| PSR-12 | 適用於 PHP 7.x 專案 |

### 步驟三：選擇執行模式

| 模式 | 說明 |
|------|------|
| 報告（預設） | 列出所有風格問題，不修改檔案 |
| 修復 | 自動修正風格問題，並輸出變更摘要 |

### 步驟四至六：檢查與輸出

技能讀取對應的規範參考檔案，按章節優先順序逐項檢查規則，並輸出報告或執行修復。

**檢查優先順序（從高到低）：**

1. 縮排與空格
2. 大括號位置（控制結構、類別、方法）
3. 關鍵字與型別大小寫
4. 行長度與空行
5. 宣告順序（declare/namespace/use）
6. 參數列表與回傳型別格式
7. 運算子空格
8. 尾隨逗號（僅 PER 3.0）
9. PHP 8.x 特性格式（僅 PER 3.0）

### 步驟七：存檔報告

完成後，使用者可選擇將報告存檔至預設路徑或自訂路徑。

## 專案結構

```
php-style-check/
├── SKILL.md                         # 技能定義
├── references/
│   ├── per-coding-style.md          # PER Coding Style 3.0 參考檔案
│   └── psr-12.md                    # PSR-12 參考檔案
└── templates/
    └── style-report.md              # 報告輸出範本
```

## 注意事項

- 此技能聚焦於**格式風格**（縮排、空格、大括號位置、行長度等），不涉及程式碼品質（架構、命名、邏輯）
- 每個問題均標註**具體行號**，方便定位
- 即使全部通過，報告也會列出「符合規範亮點」，讓使用者瞭解哪些做得好
- 在 git commit/branch 模式下，僅檢查 `.php` 副檔名的檔案
