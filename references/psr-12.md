# PSR-12: Extended Coding Style 規範要點

> 來源：https://www.php-fig.org/psr/psr-12/
> PSR-12 延伸並取代 PSR-2，要求遵守 PSR-1
> 每條規則標明等級：**MUST** / **MUST NOT** / **SHOULD** / **SHOULD NOT**

---

## 1. 通用規則

### 1.1 檔案格式
- **[MUST]** 使用 Unix LF 換行符
- **[MUST]** 檔案結尾為非空白行，以單一 LF 結束
- **[MUST]** 純 PHP 檔案省略結尾 `?>` 標籤

### 1.2 行長度
- **[MUST NOT]** 無硬性行長限制
- **[SHOULD]** 軟限制 120 字元
- **[SHOULD]** 超過 80 字元的行應拆分為多行（每段不超過 80 字元）

### 1.3 縮排
- **[MUST]** 使用 4 個空格縮排（不可使用 Tab）

### 1.4 空白
- **[MUST NOT]** 行尾不可有尾隨空白
- **[MAY]** 可加入空行提升可讀性
- **[MUST]** 每行最多一個陳述式

---

## 2. 關鍵字與型別

- **[MUST]** 所有 PHP 保留關鍵字和型別必須小寫
- **[MUST]** 使用短型別：`bool`（非 `boolean`）、`int`（非 `integer`）

---

## 3. 宣告、命名空間與 Import

### 3.1 檔案標頭順序
各區塊若存在，必須以單一空行分隔：

1. `<?php` 開始標籤
2. 檔案層級 docblock
3. 一個或多個 declare 陳述式
4. namespace 宣告
5. class-based use imports
6. function-based use imports
7. constant-based use imports
8. 其餘程式碼

### 3.2 Import 規則
- **[MUST]** import 陳述式不可以反斜線開頭（必須完全限定）
- **[MUST]** compound namespace 最多兩層深度

### 3.3 Declare 陳述式
- **[MUST]** 不可包含空格，必須為 `declare(strict_types=1)`
- **[MUST]** 含標記的檔案中：`<?php declare(strict_types=1) ?>`
- **[MUST]** 區塊 declare：`declare(ticks=1) { // code }`

---

## 4. 類別、屬性、方法

### 4.1 通用
- **[MUST NOT]** 結束大括號後同行不可有註解或陳述式
- **[MUST]** 實例化類別時必須加括號（即使無參數）

### 4.2 extends / implements
- **[MUST]** 關鍵字與類別名稱在同一行
- **[MUST]** 開始大括號獨立一行
- **[MUST]** 結束大括號在主體後獨立一行
- **[MUST NOT]** 開始大括號前後不可有空行
- **[MUST NOT]** 結束大括號前不可有空行
- **[MAY]** 列表可跨多行，每行一個介面
- **[MUST]** 多行時第一項在下一行

### 4.3 Traits
- **[MUST]** `use` 陳述式在開始大括號的下一行
- **[MUST]** 每個 trait 一個 `use` 陳述式
- **[MUST]** trait 後無其他內容時，結束大括號在下一行
- **[MUST]** trait 後有其他內容時需有空行
- **[MUST]** `insteadof` 和 `as` 運算子正確格式化

### 4.4 屬性與常數
- **[MUST]** 所有屬性必須宣告 visibility
- **[MUST]** PHP 7.1+ 時常數必須宣告 visibility
- **[MUST NOT]** 不可使用 `var` 關鍵字
- **[MUST]** 每個陳述式最多一個屬性
- **[SHOULD NOT]** 不應使用底線前綴表示 protected/private
- **[MUST]** 型別宣告與屬性名稱之間一個空格

### 4.5 方法與函式
- **[MUST]** 所有方法必須宣告 visibility
- **[SHOULD NOT]** 不應使用底線前綴表示 protected/private
- **[MUST NOT]** 方法名稱後不可有空格
- **[MUST]** 開始大括號獨立一行
- **[MUST]** 結束大括號在主體後獨立一行
- **[MUST NOT]** 開始括號後不可有空格
- **[MUST NOT]** 結束括號前不可有空格

### 4.6 方法與函式參數
- **[MUST NOT]** 逗號前不可有空格
- **[MUST]** 逗號後一個空格
- **[MUST]** 有預設值的參數放在列表末尾
- **[MAY]** 參數列表可跨多行，每行一個參數
- **[MUST]** 多行時第一個參數在下一行
- **[MUST]** 多行時結束括號和開始大括號在同一行，中間一個空格
- **[MUST]** 返回型別：冒號後一個空格，冒號與結束括號同行
- **[MUST NOT]** Nullable 型別 `?` 與型別之間不可有空格
- **[MUST NOT]** 參考運算子 `&` 後不可有空格
- **[MUST NOT]** 可變參數 `...` 與參數名稱之間不可有空格
- **[MUST NOT]** 參考與可變參數合用時無空格：`&...$parts`

### 4.7 abstract / final / static
- **[MUST]** `abstract` 和 `final` 在 visibility 之前
- **[MUST]** `static` 在 visibility 之後

### 4.8 方法與函式呼叫
- **[MUST NOT]** 方法/函式名稱與開始括號之間不可有空格
- **[MUST NOT]** 開始括號後不可有空格
- **[MUST NOT]** 結束括號前不可有空格
- **[MUST NOT]** 逗號前不可有空格
- **[MUST]** 逗號後一個空格
- **[MAY]** 引數列表可跨多行，每行一個引數
- **[MUST]** 多行時第一項在下一行

---

## 5. 控制結構

### 5.1 通用規則
- **[MUST]** 關鍵字後一個空格
- **[MUST NOT]** 開始括號後不可有空格
- **[MUST NOT]** 結束括號前不可有空格
- **[MUST]** 結束括號與開始大括號之間一個空格
- **[MUST]** 結構主體縮排一次
- **[MUST]** 主體在開始大括號的下一行
- **[MUST]** 結束大括號獨立一行
- **[MUST]** 所有控制結構主體必須用大括號包裹

### 5.2 if / elseif / else
- **[SHOULD]** 優先使用 `elseif`（而非 `else if`）
- **[MUST]** `else` 和 `elseif` 與前一個結束大括號在同一行
- **[MAY]** 條件表達式可跨行，每行一個條件
- **[MUST]** 布林運算子在行首或行尾（不可混用）

### 5.3 switch / case
- **[MUST]** `case` 相對 `switch` 縮排一次
- **[MUST]** `break` 與 case 主體同層級縮排
- **[MUST]** 刻意 fall-through 時必須加註解 `// no break`
- **[MAY]** 表達式可跨多行
- **[MUST]** 布林運算子在行首或行尾（不可混用）

### 5.4 while / do-while
- **[MUST]** 標準空格與大括號規則
- **[MAY]** 表達式可跨多行
- **[MUST]** do-while 的 `while` 與結束大括號在同一行

### 5.5 for
- **[MUST]** 標準空格與大括號規則
- **[MAY]** 表達式可跨多行

### 5.6 foreach
- **[MUST]** 標準空格與大括號規則

### 5.7 try / catch / finally
- **[MUST]** 標準空格與大括號規則
- **[MAY]** catch 可使用 union 型別：`catch (FirstType | SecondType $e)`

---

## 6. 運算子

### 6.1 一元運算子
- **[MUST NOT]** 遞增/遞減：運算子與運算元之間不可有空格
- **[MUST NOT]** 型別轉換括號內不可有空格：`(int) $input`

### 6.2 二元運算子
- **[MUST]** 所有二元運算子（算術、比較、賦值、位元、邏輯、字串、型別）前後至少一個空格

### 6.3 三元運算子
- **[MUST]** `?` 和 `:` 前後都需要空格
- **[MUST]** Elvis 運算子 `?:` 遵循二元運算子空格規則

---

## 7. 閉包（Closures）

- **[MUST]** `function` 關鍵字後一個空格
- **[MUST]** `use` 關鍵字前後各一個空格
- **[MUST]** 開始大括號在同一行
- **[MUST]** 結束大括號在主體後的下一行
- **[MUST NOT]** 開始括號後不可有空格
- **[MUST NOT]** 結束括號前不可有空格
- **[MUST NOT]** 逗號前不可有空格
- **[MUST]** 逗號後一個空格
- **[MUST]** 預設值參數放在列表末尾
- **[MUST]** 返回型別遵循方法/函式規則
- **[MUST]** 有返回型別時，冒號接在 `use` 列表結束括號後，無空格
- **[MAY]** 引數和變數列表可跨多行，每行一個
- **[MUST]** 多行時結束括號和開始大括號在同一行，中間一個空格
- **[MUST]** 作為函式/方法引數的閉包遵循相同規則

---

## 8. 匿名類別

- **[MUST]** 遵循與閉包相同的指引
- **[MAY]** implements 列表未包裹時，開始大括號可在 `class` 同行
- **[MUST]** implements 列表包裹時，開始大括號在下一行
