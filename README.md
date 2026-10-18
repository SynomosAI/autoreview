# autoreview

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE.md)
[![Agent Skill](https://img.shields.io/badge/Agent%20Skill-SKILL.md-blue.svg)](SKILL.md)
[![AI Review](https://img.shields.io/badge/AI-code%20review-brightgreen.svg)](SKILL.md)
[![Security Scan](https://img.shields.io/badge/security-scan-2ea44f.svg)](SKILL.md)

SynomosAI 四支柱体系：**身份（Identity）· 溯源（Traceability）· 治理（Governance）· 共生（Symbiosis）**——当 AI 进入商业，可信是唯一的硬通货。

> 本仓库属于 [SynomosAI](https://github.com/SynomosAI) 生态技能包的一员。生态全景见 [`synomosai-skills`](https://github.com/SynomosAI/synomosai-skills)，理论站位见 [`traceability-audit`](https://github.com/SynomosAI/traceability-audit)。

**关键词 / Keywords**：自动代码审查 · AI review · PR review · 安全漏洞扫描 · 结构化审查报告 · automated code review

## 🚀 快速开始 / Quick Start

本仓是一个 **Agent Skill 发布包**（遵循 SKILL.md 规范），不是可运行的 SDK。

```bash
# 1. 克隆本仓
git clone https://github.com/SynomosAI/autoreview.git
cd autoreview

# 2. 查看技能主文件（审查流程 / 提示词 / 报告格式）
cat SKILL.md
```

```bash
# 3. 获取变更内容（GitHub PR 模式）
gh pr view <PR号> --json files,title,body
gh pr diff <PR号>

# 4. 获取变更内容（本地变更模式）
git diff main...HEAD
```

## 仓库内容

自动评审循环

本技能使用 AI 能力对代码变更进行深度审查，生成结构化报告，覆盖：安全漏洞（注入、XSS、权限绕过、敏感信息泄露）、代码规范（命名、复杂度、重复代码）、性能问题（N+1 查询、不必要计算、内存泄漏）、可维护性（注释、测试覆盖、错误处理）。对每个问题给出具体位置（文件名+行号）、风险等级（🔴/🟡/💭）和修复建议。

## 元信息

- **技能名**：`autoreview`
- **版本**：1.0.0
- **署名**：SynomosAI
- **许可**：MIT（详见仓库 LICENSE）

## 使用方式

1. 克隆本仓库或将该技能目录放入你的 Agent 技能目录（如 `~/.workbuddy/skills/`）；
2. 在 Agent 中按 `SKILL.md` 的描述触发对应能力；
3. 需要审计/合规证据的场景，参考 `SKILL.md` 内模板产出工件。

## 审查流程概览

```text
获取变更（PR diff / git diff）
  → 分文件审查（安全 / 规范 / 性能 / 可维护性）
  → 生成结构化报告（位置 + 风险等级 + 修复建议）
  → 开发者按建议修改
```

## 审查报告示例

```text
文件：src/auth/login.js
  🔴 [安全] 第 42 行：SQL 拼接注入风险
     风险：攻击者可通过用户名参数执行任意 SQL
     建议：改用参数化查询 db.query("SELECT * FROM users WHERE id = ?", [userId])
  🟡 [性能] 第 88 行：循环内发起数据库查询（N+1）
     建议：改为批量查询后内存匹配
  💭 [可维护性] 第 120 行：函数超过 50 行，建议拆分
```

## 仓库结构 / Repository layout

```text
autoreview/
├── README.md              # 本文件
├── README.en.md           # 英文版说明
├── SKILL.md               # 技能主文件（审查流程 / 提示词 / 报告格式）
├── LICENSE.md             # MIT License
├── llms.txt               # 给 AI 的最小索引
├── llms-full.txt          # 给 AI 的完整文本
├── AGENTS.md              # 给 AI Agent 的工作指引
├── SECURITY.md            # 安全策略
└── .github/CODEOWNERS      # 代码所有者
```

## License / 许可

本项目以 **MIT** 许可发布，详见仓库根目录 [LICENSE.md](LICENSE.md)。版权：© 2026 注册老炮@MedXpert。

---

## 免责声明

本仓库内容为 SynomosAI 的**理论站位与工具化探索**，不代表任何已获认证、已商业化交付或已服务特定客户的声明；文中涉及的 ISO/IEC 42001、NIST AI RMF、GB/Z 185 等外部标准与条款信息为公开资料转述，正式引用前请**独立核实**。API、授权码与形象大使等为路线图（roadmap）事项，尚未上线。
