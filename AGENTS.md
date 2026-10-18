# AGENTS.md — 给 AI Agent 的工作指引

本文件面向自动化 AI Agent。人类读者请看 [README.md](README.md)。

## 这个仓库是什么

`autoreview` 是一个 **Agent Skill 发布包**，核心资产是 `SKILL.md`。把本目录放入 Agent 的技能目录即可获得「自动代码审查」能力。

## 可用的工作命令

```bash
head -15 SKILL.md
cat SKILL.md
```

## 约定（Do）

- 修改 `SKILL.md` 时保持 YAML frontmatter 字段兼容。
- 新增审查维度时同步更新报告格式模板。

## 禁止（Don't）

- 不要改动 `LICENSE.md` 的版权主体（© 2026 注册老炮@MedXpert）。
- 不要在仓库内提交任何密钥或真实客户数据。

## 边界

本技能专注代码变更审查；不覆盖安全审计、合规审计等独立技能域。
