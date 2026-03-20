# PER Coding Style 3.0 規範要點

> 來源：https://www.php-fig.org/per/coding-style/
> 每條規則標明等級：**MUST** / **MUST NOT** / **SHOULD** / **SHOULD NOT**

---

## 1. 通用規則

### 1.1 檔案格式
- **[MUST]** 使用 Unix LF 換行符
- **[MUST]** 檔案結尾為非空白行，以單一 LF 結束
- **[MUST]** 純 PHP 檔案省略結尾 `?>` 標籤
- **[MUST]** 使用 UTF-8 無 BOM 編碼

### 1.2 行長度
- **[MUST NOT]** 無硬性行長限制
- **[SHOULD]** 軟限制 120 字元
- **[SHOULD]** 超過 80 字元的行應拆分為多行

### 1.3 縮排
- **[MUST]** 使用 4 個空格縮排（不可使用 Tab）

### 1.4 空白
- **[MUST NOT]** 行尾不可有尾隨空白
- **[MUST]** 每行最多一個陳述式

---

## 2. 關鍵字與型別

### 2.1 關鍵字
- **[MUST]** 所有 PHP 保留關鍵字和型別必須小寫

### 2.2 型別宣告
- **[MUST]** 使用短型別：`bool`（非 `boolean`）、`int`（非 `integer`）

### 2.3 複合型別
- **[MUST NOT]** Union（`|`）和 Intersection（`&`）符號前後不可有空格
- **[MUST NOT]** 括號內不可有前後空格
- **[MUST]** 多行拆分時，每行一個型別，符號在行首
- **[MUST]** `null` 必須放在 union 型別的最後
- **[SHOULD]** 單一型別加 null 時，優先使用 `?T` 語法

---

## 3. Trailing Commas（尾隨逗號）

- **[MUST NOT]** 單行列表不可有尾隨逗號
- **[MUST]** 多行列表必須有尾隨逗號

---

## 4. 檔案標頭結構

區塊必須按以下順序排列，各區塊間以單一空行分隔：

1. `<?php` 開始標籤
2. 檔案層級 docblock
3. declare 陳述式
4. namespace 宣告
5. class-based use imports
6. function-based use imports
7. constant-based use imports
8. 其餘程式碼

### 4.1 Import 規則
- **[MUST NOT]** import 陳述式不可以反斜線開頭
- **[MUST]** compound namespace 最多兩層子命名空間
- **[MUST]** declare 陳述式不可包含空格，必須為 `declare(strict_types=1)`

---

## 5. 類別、屬性、方法

### 5.1 類別宣告
- **[MUST]** `extends` 和 `implements` 關鍵字與類別名稱在同一行
- **[MUST]** 開始大括號獨立一行
- **[MAY]** implements 列表可跨多行，每行一個，縮排一次
- **[MUST]** 多行時第一項在下一行

### 5.2 Traits
- **[MUST]** `use` 陳述式在開始大括號的下一行
- **[MUST]** 每個 trait 一個 `use` 陳述式
- **[MUST]** trait 後無其他內容時，結束大括號在下一行
- **[MUST]** trait 後有其他內容時，trait 後需有空行

### 5.3 屬性與常數
- **[MUST]** 所有屬性必須宣告 visibility
- **[MUST NOT]** 不可使用 `var` 關鍵字宣告屬性
- **[MUST]** 每個陳述式只宣告一個屬性/常數
- **[MUST]** 型別與屬性名稱之間需有空格
- **[SHOULD NOT]** 不應使用底線前綴表示 protected/private visibility

### 5.4 方法宣告
- **[MUST]** 所有方法必須宣告 visibility
- **[MUST NOT]** 方法名稱與開始括號之間不可有空格
- **[MUST]** 開始大括號獨立一行
- **[MUST NOT]** 開始括號後不可有空格
- **[MUST NOT]** 結束括號前不可有空格
- **[MAY]** 空方法可使用行內 `{}` 語法

### 5.5 建構子屬性提升（Constructor Promotion）
- **[MUST]** 實例化時必須加括號：`new Foo()`
- **[MAY]** 可直接存取成員：`new Foo()->method()`

---

## 6. Modifier 關鍵字順序

**[MUST]** 按以下順序排列：
1. `abstract` 或 `final`（繼承）
2. `public`、`protected`、`private`（可見性）
3. `public(set)` 等（Set-visibility）
4. `static`（範圍）
5. `readonly`（不可變）
6. 型別宣告
7. 名稱

**[MUST]** 全部小寫，單行，以空格分隔

---

## 7. 方法與函式參數

- **[MUST NOT]** 逗號前不可有空格
- **[MUST]** 逗號後一個空格
- **[MUST]** 有預設值的參數放在參數列表末尾
- **[MUST]** 多行參數列表：第一項在下一行，每行一個參數
- **[MUST]** 多行時結束括號和開始大括號在同一行，中間一個空格
- **[MUST]** 返回型別：冒號後一個空格，冒號與結束括號同行
- **[MUST NOT]** Nullable 型別 `?` 與型別之間不可有空格
- **[MUST NOT]** 參考運算子 `&` 後不可有空格
- **[MUST NOT]** 可變參數 `...` 後不可有空格

---

## 8. 控制結構

### 8.1 通用規則
- **[MUST]** 關鍵字後一個空格
- **[MUST NOT]** 開始括號後不可有空格
- **[MUST NOT]** 結束括號前不可有空格
- **[MUST]** 結束括號與開始大括號之間一個空格
- **[MUST]** 結構主體縮排一次
- **[MUST]** 主體在開始大括號的下一行
- **[MUST]** 結束大括號獨立一行
- **[MUST]** 所有控制結構主體必須用大括號包裹

### 8.2 if / elseif / else
- **[SHOULD]** 優先使用 `elseif`（而非 `else if`）
- **[MUST]** 多行條件：第一個條件在下一行，運算子在行首
- **[MUST]** 多行時結束括號和開始大括號在同一行

### 8.3 switch / case
- **[MUST]** `case` 相對 `switch` 縮排一次
- **[MUST]** `break`/`return` 與 case 主體同層級縮排
- **[MUST]** 刻意 fall-through 時必須加註解 `// no break`

### 8.4 match 表達式
- **[MUST]** 遵循類似 switch 的格式規則
- **[MUST]** 支援 default 分支

### 8.5 while / do-while
- **[MUST]** 多行條件遵循標準規則
- **[MUST]** do-while 的條件在結束大括號後

### 8.6 for
- **[MUST]** 三個表達式以分號分隔
- **[MUST]** 多行時每個表達式獨立一行

### 8.7 foreach
- **[MUST]** 標準格式：`foreach ($iterable as $key => $value)`

### 8.8 try / catch / finally
- **[MUST]** 每個區塊在前一個區塊的結束大括號同行
- **[MAY]** catch 可使用 union 型別

---

## 9. 運算子

### 9.1 一元運算子
- **[MUST NOT]** 遞增/遞減：運算子與運算元之間不可有空格
- **[MUST]** 型別轉換：`(type)` 後一個空格

### 9.2 二元運算子
- **[MUST]** 所有二元運算子（算術、比較、賦值、位元、邏輯、字串、型別）前後至少一個空格

### 9.3 三元運算子
- **[MUST]** `?` 和 `:` 前後都需要空格
- **[MUST]** Elvis 運算子 `?:` 遵循二元運算子空格規則
- **[MUST]** 跨行的三元運算子用 3 行（不可 2 行），運算子在行首

---

## 10. 閉包（Closures）

### 10.1 長形式閉包
- **[MUST]** `function` 關鍵字後一個空格
- **[MUST]** `use` 關鍵字前後各一個空格
- **[MUST]** 開始大括號在同一行
- **[MUST NOT]** 開始括號後不可有空格
- **[MUST]** 逗號後一個空格
- **[MUST]** 預設值參數放在列表末尾
- **[MUST]** 結束大括號獨立一行
- **[MUST]** 多行列表：第一項在下一行，結束括號和開始大括號在同一行

### 10.2 短閉包（箭頭函式）
- **[MUST NOT]** `fn` 關鍵字後不可有空格
- **[MUST]** `=>` 前後各一個空格
- **[MUST NOT]** 分號前不可有空格

---

## 11. 匿名類別

- **[MUST]** 遵循與閉包相同的指引
- **[MAY]** 無介面包裹時，開始大括號可在 `class` 同行
- **[MUST]** 介面列表包裹時，大括號在下一行
- **[SHOULD]** 無建構參數時省略 `()`

---

## 12. 列舉（Enumerations）— PER 3.0 專屬

- **[MUST]** 遵循類別指引
- **[MUST]** 非 public 方法使用 `private`（enum 不支援繼承）
- **[MUST]** Backed enum：名稱與冒號之間無空格，冒號後一個空格
- **[MUST]** case 宣告使用 PascalCase，每行一個
- **[MAY]** 常數可使用 PascalCase 或 UPPER_CASE（推薦 PascalCase）

---

## 13. Attributes（屬性標註）— PER 3.0 專屬

- **[MUST]** 屬性名稱緊接 `#[`，無空格
- **[MUST]** 結束 `]` 前無空格
- **[SHOULD]** 無參數時省略 `()`
- **[MUST]** 類別/方法/函式/常數/屬性的 attribute 在結構上方獨立一行
- **[MUST]** 參數 attribute：單行時行內，多行時獨立一行
- **[MUST]** 順序：docblock → attributes → 結構（之間無空行）
- **[MAY]** 同一個 `#[]` 內以逗號分隔多個 attribute
- **[MUST]** 多行 attribute 參數遵循函式呼叫格式

---

## 14. Property Hooks — PER 3.0 專屬

### 14.1 長形式
- **[MUST]** 開始大括號在屬性同行，以空格分隔
- **[MUST]** 結束大括號獨立一行
- **[MUST]** 主體縮排一次
- **[MUST]** 多個 hook 之間至少一個空行

### 14.2 短形式（單一表達式）
- **[MUST]** `=>` 前後各一個空格
- **[MUST]** 主體在同行開始
- **[MAY]** 單一 hook + 短語法時可行內：`{ get => expr; }`

### 14.3 建構子提升
- **[MUST]** 行內僅允許單一短語法 hook
- **[MUST]** 複雜 hook 需使用完整屬性語法

---

## 15. Heredoc / Nowdoc — PER 3.0 專屬

- **[SHOULD]** 盡可能使用 Nowdoc
- **[MUST]** 宣告與上下文在同行開始
- **[MUST]** 後續行相對作用域縮排一次
- **[MUST]** 結束標識符獨立一行，在正確縮排位置

---

## 16. 陣列（Arrays）— PER 3.0 專屬

- **[MUST]** 使用短語法 `[]`（非 `array()`）
- **[MUST]** 遵循 trailing comma 規則（多行必須有尾隨逗號）
- **[MUST]** 多行時第一個值在下一行，每行一個值
- **[MUST]** 開始方括號與等號在同一行
- **[MUST]** 結束方括號在值之後的下一行
