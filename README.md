English | [简体中文](README_CN.md) | [繁體中文](README_TW.md) | [日本語](README_JP.md) | [한국어](README_KR.md)

# PHP Coding Style Check

A VS Code Copilot skill that checks whether PHP files comply with **PER Coding Style 3.0** or **PSR-12** style specifications. Supports report mode (list issues only) and fix mode (auto-correct files directly).

## Features

- Check the current file, a specific git commit, or a git branch for style violations
- Support for **PER Coding Style 3.0** (PHP 8.x features) and **PSR-12** (PHP 7.x projects)
- Two execution modes: **Report** (list issues) and **Fix** (auto-correct)
- Severity classification: **Error** (MUST/MUST NOT violations) and **Warning** (SHOULD/SHOULD NOT violations)
- Detailed reports with specific line numbers for every issue

## Trigger Keywords

This skill is activated when users mention:
- PHP coding style check
- Style check / format check
- PER style / PSR-12
- Code formatting inspection

## Workflow

### Step 1: Determine Check Scope

| Source | Method |
|--------|--------|
| Current file | Read the specified PHP file directly |
| Git commit | `git show <commit>:<file>` to get file content; `git diff-tree` to get changed file list |
| Git branch | `git diff <base>...<branch>` to get diff list, read files from working directory |

### Step 2: Select Style Specification

| Option | Description |
|--------|-------------|
| PER Coding Style 3.0 (default) | Covers PHP 8.x features (enum, match, attributes, property hooks) |
| PSR-12 | Suitable for PHP 7.x projects |

### Step 3: Select Execution Mode

| Mode | Description |
|------|-------------|
| Report (default) | List all style issues without modifying files |
| Fix | Auto-correct style issues and output a change summary |

### Step 4–6: Check and Output

The skill reads the corresponding specification reference file, checks rules by section in priority order, and outputs a report or performs fixes.

**Check Priority (high to low):**

1. Indentation and spaces
2. Brace placement (control structures, classes, methods)
3. Keyword and type casing
4. Line length and blank lines
5. Declaration order (declare/namespace/use)
6. Parameter list and return type formatting
7. Operator spacing
8. Trailing commas (PER 3.0 only)
9. PHP 8.x feature formatting (PER 3.0 only)

### Step 7: Save Report

After completion, the user can choose to save the report to a default or custom path.

## Project Structure

```
php-style-check/
├── SKILL.md                         # Skill definition
├── references/
│   ├── per-coding-style.md          # PER Coding Style 3.0 reference
│   └── psr-12.md                    # PSR-12 reference
└── templates/
    └── style-report.md              # Report output template
```

## Notes

- This skill focuses on **formatting style** (indentation, spacing, brace placement, line length, etc.), not code quality (architecture, naming, logic)
- Every issue includes a **specific line number** for easy identification
- Even if all checks pass, the report lists "compliance highlights" to show what was done well
- In git commit/branch mode, only `.php` files are checked
