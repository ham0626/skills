# Skills

我给 WorkBuddy（AI 助理）写的一批工作流 —— 每个 skill 都是一个**有明确触发条件、明确流程、明确验收标准**的目录。

不是提示词收藏夹，不是教程笔记。是可以直接丢给 AI 助理、它照着就能把活干完的东西。

---

## 这里面有什么

| Skill | 一句话 | 状态 |
|---|---|---|
| [`course-report`](skills/course-report/) | 课程汇报 / 翻转课堂演示：只深挖一个问题点，不把课堂内容横向重讲一遍 | ✅ 可用 |

> 每个 skill 目录下都有 `SKILL.md`（说明书）、`references/`（按需加载的详细资料）、`assets/`（可直接复用的模板文件）。

---

## 为什么要做成 skill，而不是每次都重新说一遍

做第一份课程汇报的时候，我踩了这些坑：

- 做到一半才发现**方向选错了** —— 主题、钩子、深挖点没对齐就开工，返工重来
- 内容越做越长，最后变成**把课本从头念一遍** —— 评审一问「这和上课讲的有什么区别」，就答不上来
- 视觉是硬编码的，换个学科就用不了

所以这套 skill 干的核心事情是三件：

1. **先定后做** —— 开工前先把约束摆出来确认，任何一项没确认不动手
2. **纵深优先** —— 强制只选一个问题点深挖，其余明确划为「不重复边界」
3. **不编造** —— 数据、引用、时间线必须来自材料或联网核实，核不实就标「需核实」

---

## 怎么用

### 本机已装好（目录联接）

本机的 skill 安装位置已经指向这个仓库：

```
C:\Users\15328\.workbuddy\skills\course-report
  →（junction）→ D:\03coding\myskill\skills\course-report
```

所以**改这个仓库，WorkBuddy 立刻生效**，不存在"改了一份另一份没改"的两边打架。重新打开 WorkBuddy 或新建会话即可加载。

### 给别人用

```bash
# Windows Git Bash
git clone https://github.com/ham0626/skills.git
cp -r skills/skills/course-report ~/.workbuddy/skills/
```

装完重启 WorkBuddy 或新建会话，skill 就会出现在技能列表里。

### 直接看

`skills/course-report/SKILL.md` 是纯 Markdown，直接读也能用。

---

## 一个 skill 长什么样

```
skills/course-report/
├── SKILL.md          # 说明书：什么时候用、怎么用、铁律、完整流程
├── references/       # 按需加载：分析框架库、代码范式
└── assets/           # 可直接复制的模板
```

这套结构不是我拍脑袋定的，是 WorkBuddy 官方 `skill-creator` 的规范：说明保持在 5k 词以内，细节丢 `references/`，模板丢 `assets/`，AI 助理按需加载 —— 上下文省着用。

---

## 开发约定

- **单一真源**：只改这个仓库（`D:\03coding\myskill`），本机安装位置是它的 junction，改完即生效。
- **一条 skill 一个目录**：`skills/<name>/`，目录名 = skill 名。
- **不改别人的 skill**：`~/.workbuddy/skills/` 下其他 skill 各自独立，不动。

---

## 写新 skill 的约定

- **一个 skill 解决一类问题**，不是一个具体任务
- **触发条件写清楚**（什么词、什么场景该用），AI 助理靠这个决定要不要加载
- **流程要有确认门** —— 关键节点停下来等确认，不要闷头往前跑
- **验收清单可勾选** —— 交付前逐条过
- **不编造** —— 涉及事实的内容要么可溯源，要么显式标注不确定

---

## 计划中

- [ ] `course-report` 补通用框架选型（让 SOP 能迁移到通选课 / 其他学科）
- [ ] 课程汇报 demo 的通用模板（脱开生物安全场景）
- [ ] 更多 skill

---

*这些 skill 大多是从真实作业里长出来的 —— 先踩坑，再把坑填成流程。*
