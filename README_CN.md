[English](README.md) | 简体中文 | [繁體中文](README_TW.md) | [日本語](README_JP.md) | [한국어](README_KR.md)

# PHP 编码风格检查

一个 VS Code Copilot 技能，用于检查 PHP 文件是否符合 **PER Coding Style 3.0** 或 **PSR-12** 风格规范。支持报告模式（仅列出问题）和修复模式（直接修正文件）。

## 功能特点

- 检查当前文件、指定 git commit 或 git 分支中的风格违规
- 支持 **PER Coding Style 3.0**（涵盖 PHP 8.x 特性）和 **PSR-12**（适用于 PHP 7.x 项目）
- 两种执行模式：**报告**（列出问题）和 **修复**（自动修正）
- 严重性分级：**Error**（违反 MUST / MUST NOT 规则）和 **Warning**（违反 SHOULD / SHOULD NOT 规则）
- 详细报告，每个问题标注具体行号

## 触发关键词

当用户提及以下内容时触发此技能：
- PHP 编码风格检查
- 风格检查 / 格式检查
- PER style / PSR-12
- 代码格式化检查

## 工作流程

### 步骤一：确定检查范围

| 来源 | 获取方式 |
|------|----------|
| 当前文件 | 直接读取指定路径的 PHP 文件 |
| Git commit | 使用 `git show <commit>:<file>` 获取文件内容；`git diff-tree` 获取变更清单 |
| Git branch | 使用 `git diff <base>...<branch>` 获取差异清单，读取工作目录文件 |

### 步骤二：选择风格规范

| 选项 | 说明 |
|------|------|
| PER Coding Style 3.0（默认） | 涵盖 PHP 8.x 特性（enum、match、attributes、property hooks） |
| PSR-12 | 适用于 PHP 7.x 项目 |

### 步骤三：选择执行模式

| 模式 | 说明 |
|------|------|
| 报告（默认） | 列出所有风格问题，不修改文件 |
| 修复 | 自动修正风格问题，并输出变更摘要 |

### 步骤四至六：检查与输出

技能读取对应的规范参考文件，按章节优先顺序逐项检查规则，并输出报告或执行修复。

**检查优先顺序（从高到低）：**

1. 缩进与空格
2. 大括号位置（控制结构、类、方法）
3. 关键字与类型大小写
4. 行长度与空行
5. 声明顺序（declare/namespace/use）
6. 参数列表与返回类型格式
7. 运算符空格
8. 尾随逗号（仅 PER 3.0）
9. PHP 8.x 特性格式（仅 PER 3.0）

### 步骤七：保存报告

完成后，用户可选择将报告保存至默认路径或自定义路径。

## 项目结构

```
php-style-check/
├── SKILL.md                         # 技能定义
├── references/
│   ├── per-coding-style.md          # PER Coding Style 3.0 参考文件
│   └── psr-12.md                    # PSR-12 参考文件
└── templates/
    └── style-report.md              # 报告输出模板
```

## 注意事项

- 此技能聚焦于**格式风格**（缩进、空格、大括号位置、行长度等），不涉及代码质量（架构、命名、逻辑）
- 每个问题均标注**具体行号**，方便定位
- 即使全部通过，报告也会列出「符合规范亮点」，让用户了解哪些做得好
- 在 git commit/branch 模式下，仅检查 `.php` 扩展名的文件
