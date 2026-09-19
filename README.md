# Software Testing Skill · 软件测试全流程

> 一句话：把"帮我测一下"变成可复现的工程流程——从需求质疑、用例设计、自动化脚本，到缺陷单和测试报告，一次跑通并落地成文件。

## 它解决什么问题

通用 AI 做测试常见的三种翻车：

1. **拍脑袋写用例** —— 想到哪写到哪，覆盖靠灵感，边界全靠运气
2. **产出停在对话里** —— 一大段 Markdown 表格，没人能拿去用
3. **谎报结果** —— "已测试通过"，其实压根没执行过

这个 skill 用**六段工作流 + 七条铁律 + 可运行脚本**把这三件事钉死：用例必须按方法设计、产出必须落文件、没跑过的必须标注"未实际执行"。

## 你会得到什么

| 交付物 | 形态 | 说明 |
|---|---|---|
| 测试计划与策略 | Markdown | 范围、策略、环境、准入准出标准、风险 |
| 测试用例集 | Markdown / **Excel** | 35 条级用例表，含覆盖度矩阵，可一键转 xlsx |
| 自动化测试代码 | 可运行工程 | pytest 骨架一键生成；纯前端项目走 Node + jsdom |
| 缺陷报告 | Markdown | S1~S4 分级、复现步骤、根因、修复建议 |
| 测试报告 | Markdown | 执行数据、缺陷分布、根因归类、发布建议 |

## 触发词（说这些就会自动启用）

软件测试 · 测试用例 · 测试计划 · 测试策略 · 自动化脚本 · pytest · 接口测试 · API 测试 · UI 测试 · Playwright · 回归测试 · 冒烟测试 · 覆盖率 · 缺陷报告 · Bug 报告 · 测试报告 · 帮我测一下 X · 找 bug · 质量风险评估

## 真实案例（不是 Demo，是真跑出来的）

对一个 **纯前端数据可视化项目**（Chart.js + 303 条医疗数据，无 Python 后端）执行本 skill：

- 产出 **35 条用例**，执行 33 条，**通过 20 / 失败 13**
- 揪出 **12 个缺陷**（S1×1、S2×3、S3×6、S4×2）
- 最严重的一个：数据集没有时间字段，页面上的"月度趋势"和"热力图"是**总数÷12 反推出来的**，实测 12 个月取值恒为 14，三张图结论全部无效
- 其余：id 重复导致报告锚点失效、"康复率 56%"实为未患病占比、散点图静默丢弃 67% 数据、筛选后热力图不刷新

完整案例见 `examples/biomed-frontend-case/`。

> 注：这个案例也暴露了纯前端项目硬套 pytest 的尴尬，因此本 skill 内置了 Node + jsdom 降级路径（`references/frontend-testing.md`）。

## 安装

### 方式一：直接解压（通用）

```bash
# Claude Code / Codex CLI
unzip software-testing-1.0.0.zip -d ~/.claude/skills/     # Codex: ~/.codex/skills/
```

### 方式二：WorkBuddy

在对话里说"安装 software-testing 技能"，或把解压后的目录放进 `~/.workbuddy/skills/`。

### 方式三：从市场安装

```bash
skillhq install software-testing        # SkillHQ
npx skills add <你的仓库> --skill software-testing
```

## 目录结构

```
software-testing/
├── SKILL.md                 触发路由 + W1~W6 六段工作流 + 七条铁律
├── README.md                本文件（买家读这个）
├── LICENSE.txt              MIT
├── CHANGELOG.md             版本记录
├── references/
│   ├── test-design-techniques.md   七大用例设计方法 + 字段规范 + 覆盖度矩阵
│   ├── pytest-guide.md             目录/fixture/参数化/断言/接口7维/CI/flaky
│   ├── frontend-testing.md         纯前端 Node+jsdom 路径与三个坑
│   ├── defect-and-severity.md      S1~S4 分级、状态流转、被拒自检
│   └── checklists.md               九大类测试点 + 需求质疑清单
├── assets/                  四类交付物模板（用例/计划/报告/缺陷）
├── scripts/
│   ├── scaffold_pytest.py  一键生成 pytest 工程骨架（api|ui|both）
│   └── cases_to_xlsx.py    用例 Markdown 表 → Excel（多 sheet）
└── examples/                实战案例（bio-med 前端项目完整测试过程）
```

## 环境要求

- **Python 3.9+**（可选，走 pytest 路径时需要；`cases_to_xlsx.py` 需要 `openpyxl`，缺失时自动降级输出 CSV）
- **Node 18+ / jsdom**（可选，走纯前端路径时需要）
- 无网络依赖、无 API Key、不上传任何数据

## 常见问题

**Q：我不用 pytest 怎么办？**
A：SKILL.md 里有技术栈降级铁律。Java/JS 项目保留结构与策略，语法换 JUnit5/TestNG 或 Playwright/Jest（`references/pytest-guide.md` 末尾有对照表）；纯前端项目走 Node + jsdom。

**Q：会替我编造测试结果吗？**
A：不会。铁律第 5 条明确禁止谎报：无法真实执行时必须标注"未实际执行"并说明原因。案例报告里就有 2 条这样的标注。

**Q：能改吗？**
A：MIT 协议，随便改。建议改完在 `CHANGELOG.md` 记一笔。

## 版本与维护

当前版本 **v1.0.0**（2026-09-19）。已在真实项目上完整跑通一轮，后续会随实战反馈迭代。
发现问题的同学欢迎提 issue，会优先修影响"结论正确性"的那类缺陷。

## 许可

MIT —— 可商用、可修改、可分发，保留署名即可。
