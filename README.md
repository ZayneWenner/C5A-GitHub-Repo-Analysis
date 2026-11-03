# C5A GitHub 入门与仓库理解 · 提交包

本仓库是 EduSeed 课程挑战 **C5A GitHub 入门与仓库理解** 的提交物：选一个真实的公开仓库，读它的目录结构、加载协议与授权边界，产出一份可复核的仓库分析。

## 提交信息

- 挑战：C5A GitHub 入门与仓库理解（challenge_id `ch-20260717031511-x5c6t1`，截止 2026-12-31 23:59）
- 分析对象：[`anthropics/skills`](https://github.com/anthropics/skills)
- 分析对象快照：默认分支 `main`，最近推送 `2026-10-28T19:20:39Z`，仓库体积约 5488 KB，Star 186881
- 分析日期：2026-11-03

## 交付物清单

| 文件 | 对应交付要求 | 内容 |
| --- | --- | --- |
| `仓库分析.md` | `*仓库分析*` | 十节完整分析：顶层结构、注册层、分发层、许可层、规范外置、工程量最大样本解剖、可迁移清单、五步读法、局限 |
| `README.md` | `README.md` | 本文件：提交说明、清单、复核方式 |
| `AI日志.md` | `*AI日志*` | 本次分析的真实协作记录：工具、关键提问、AI 出错与纠正、分工 |

## 为什么选这个仓库

C5A 要求的是「读懂别人的仓库」，而这个仓库本身就在讲**怎么组织一个可被工具加载的文件夹**——它既是被分析对象，也是方法样本。它同时具备三种可比性：

1. **体量跨度大**：最小技能 `template/SKILL.md` 只有 140 B，最大技能 `skill-creator/SKILL.md` 33168 B，差 230 倍，同一套规范下的上下限一目了然；
2. **有分层证据**：注册层（`.claude-plugin/marketplace.json`）、分发层（`skills/` 19 个目录）、执行层（各技能的 `scripts/`、`references/`、`agents/`）都能用文件体量直接验证；
3. **有反直觉陷阱**：GitHub API 的 `license` 字段返回 `null`，但仓库并非无授权，而是按技能分别授权（11345 B 与 1467 B 两种 LICENSE.txt）。这一条最能体现「不能只看一个字段就下结论」。

## 如何复核本文的每一个数字

所有数字都来自 GitHub 公开 API 与原始文件，任何人可复现：

```bash
# 仓库元信息（star / 体积 / 默认分支 / pushed_at / license）
curl -s -H "User-Agent: verify" https://api.github.com/repos/anthropics/skills

# 根目录清单
curl -s -H "User-Agent: verify" https://api.github.com/repos/anthropics/skills/contents/

# 单个技能内部的目录与文件体量
curl -s -H "User-Agent: verify" https://api.github.com/repos/anthropics/skills/contents/skills/skill-creator/scripts

# 模板与规范的原文（验证 140 B / 87 B 两个关键体量）
curl -s https://raw.githubusercontent.com/anthropics/skills/main/template/SKILL.md
curl -s https://raw.githubusercontent.com/anthropics/skills/main/spec/agent-skills-spec.md
```

`main` 分支会持续变动，若某个数字与你的复核结果不一致，说明仓库已更新，请以你自己那次 API 返回为准——这也是分析里「局限与不确定项」一节写明的前提。

## 已知限制

- 只抽样通读了 `skill-creator`、`pdf`、`docx`、`mcp-builder` 四个技能的内部结构，未逐个通读全部 19 个；
- 许可判断依据 LICENSE 文件体量与仓库 README 表述，未做逐字法律核对；
- 分析对象是公开第三方仓库，本提交包**不含**其源码副本，只含分析与元数据，遵守原仓库授权边界。
