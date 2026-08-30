---
name: autoreview
description: 自动化代码审查技能。使用 Codex/AI 自动审查代码，检测安全漏洞、代码规范违规、性能问题，生成结构化审查报告。触发词：代码审查、code review、自动审查、PR review、安全审查、review代码。
version: 1.0.0
author: 注册老炮@MedXpert
license: MIT
category: 代码评审
platforms: [windows, macos, linux]
displayName: 自动化代码评审
title: 自动化代码评审
tags: [代码评审, 自动化评审, AI评审, 代码质量, 自动化]
---

# 自动化代码审查 (autoreview)

## 概述

使用 AI 能力对代码变更进行深度审查，生成结构化报告，覆盖：安全漏洞、代码规范、性能问题、可维护性。

## 审查流程

### 1. 获取变更内容

**GitHub PR 模式：**
```bash
gh pr view <PR号> --json files,title,body
gh pr diff <PR号>
```

**本地变更模式：**
```bash
git diff main...HEAD
git diff --cached
```

### 2. 分文件审查

对 each changed file 执行：

```
请审查以下代码变更（文件：<文件名>）：

<diff内容>

请从以下维度审查：
1. 🔴 安全漏洞（注入、XSS、权限绕过、敏感信息泄露）
2. 🟡 代码规范（命名、复杂度、重复代码）
3. 🟡 性能问题（N+1查询、不必要的计算、内存泄漏）
4. 💭 可维护性（注释、测试覆盖、错误处理）

对每个问题给出：
- 具体位置（文件名+行号）
- 风险等级（🔴/🟡/💭）
- 修复建议（含示例代码）
```

### 3. 生成审查报告

输出格式：

```markdown
## 代码审查报告

**审查时间：** 2026-05-31
**审查范围：** PR #123 - <标题>
**文件数量：** 8 个文件，+256 -89

---

### 🔴 必须修复（2处）

**1. SQL注入风险** (src/models/user.py:42)
```python
# 风险代码
query = f"SELECT * FROM users WHERE id = '{user_id}'"
```
**修复建议：**
```python
# 使用参数化查询
query = "SELECT * FROM users WHERE id = %s"
cursor.execute(query, (user_id,))
```

**2. 敏感信息泄露** (config/settings.py:8)
```python
SECRET_KEY = "my-secret-key-12345"  # ❌ 硬编码
```
**修复建议：** 使用环境变量 `os.getenv("SECRET_KEY")`

---

### 🟡 建议修复（3处）

（略）

---

### 💭 优化建议（2处）

（略）

---

### ✅ 总体评价

- 安全：⚠️ 需修复2处高危漏洞
- 规范：✅ 整体良好
- 性能：⚠️ 存在N+1查询风险
- 测试：❌ 新增代码无测试覆盖

**建议：** 修复🔴问题后重试合并。
```

## 审查标准参考

### 安全审查清单

- [ ] SQL注入（拼接SQL、ORM不当使用）
- [ ] XSS（未转义的用户输入）
- [ ] CSRF（缺少token验证）
- [ ] 权限绕过（缺少鉴权检查）
- [ ] 敏感信息（密钥、密码、token硬编码）
- [ ] 不安全的反序列化
- [ ] SSRF / 路径遍历

### 代码规范清单

- [ ] 命名规范（变量、函数、类名）
- [ ] 函数复杂度（不超过20行，cyclomatic complexity < 10）
- [ ] 重复代码（DRY原则）
- [ ] 注释充分（公共API必须有docstring）
- [ ] 错误处理（异常捕获不能吞掉错误）

### 性能审查清单

- [ ] N+1查询问题
- [ ] 大O复杂度（避免O(n²)）
- [ ] 不必要的内存分配
- [ ] 缺少索引的数据库查询
- [ ] 大文件/大数据集的内存溢出风险

## 快捷命令

```bash
# 审查当前分支相对于main的变更
git diff main...HEAD | clip   # 复制diff后粘贴给AI

# 审查GitHub PR
gh pr diff 123 | clip

# 审查指定文件
cat src/main.py | clip
```

## 与 GitHub PR 集成

在 PR 评论中调用 AI 审查：

```bash
gh pr review 123 --body "$(cat review_report.md)" --approve/--request-changes
```

## 注意事项

- 审查报告必须具体（文件名+行号+代码示例），不能只说"有安全问题"
- 对误报要说明为什么不是问题
- 对设计问题（架构、模式）要单独标注，不跟代码规范混在一起
- 审查意见要对事不对人，用"这段代码"而不是"你的代码"


## 版权与许可

© 2026 注册老炮@MedXpert。本作品基于 MIT 协议开源（详见 LICENSE.md）。

本作品按「现状」（AS IS）提供，作者不作任何明示或暗示担保，亦不保证适用于任何特定用途。