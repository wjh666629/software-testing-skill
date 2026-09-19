# Software Testing Skill

> One line: turn "test this for me" into a repeatable engineering process — from requirement challenges, case design, and automation scripts, all the way to defect tickets and test reports — run once and delivered as files.

## Problems it solves

Three ways generic AI testing usually goes wrong:

1. **Cases from the gut** — write whatever comes to mind, coverage by inspiration, boundaries by luck.
2. **Output stuck in the chat** — a big Markdown table nobody can actually use.
3. **Fabricated results** — "all tests passed", when nothing was ever executed.

This skill nails all three down with a **six-stage workflow + seven ground rules + runnable scripts**: cases must be designed by method, output must land in files, and anything not actually run must be marked "NOT EXECUTED".

## What you get

| Deliverable | Form | Notes |
|---|---|---|
| Test plan & strategy | Markdown | scope, strategy, environment, entry/exit criteria, risks |
| Test case set | Markdown / **Excel** | case-level table with coverage matrix, one-click to xlsx |
| Automation code | Runnable project | one-shot pytest scaffold; pure-frontend projects use Node + jsdom |
| Defect report | Markdown | S1~S4 grading, repro steps, root cause, fix suggestion |
| Test report | Markdown | execution data, defect distribution, RCA, release recommendation |

## Trigger words (say these and it activates)

software testing · test cases · test plan · test strategy · automation · pytest · API testing · UI testing · Playwright · bug report · defect · regression · smoke test · coverage · test report · test X for me · find bugs · quality risk assessment

## Real case (not a demo — actually run)

Running this skill against a **pure-frontend data-visualization project** (Chart.js + 303 medical records, no Python backend):

- Produced **35 cases**, executed 33, **20 passed / 13 failed**
- Found **12 defects** (S1×1, S2×3, S3×6, S4×2)
- The most severe: the dataset has no time field, yet the page's "monthly trend" and "heatmap" were **inferred from total ÷ 12** — measured values were a constant 14 across all 12 months, so all three charts' conclusions were invalid
- Others: duplicate `id` broke report anchors, "56% recovery rate" was actually the share of non-diseased, the scatter plot silently dropped 67% of data, heatmap not refreshed after filtering

Full case in `examples/biomed-frontend-case/`.

> Note: this case also exposed the awkwardness of forcing pytest onto a pure-frontend project, which is why the skill ships a Node + jsdom fallback path (`references/frontend-testing.md`).

## Install

### Option 1: Unzip directly (universal)

```bash
# Claude Code / Codex CLI
unzip software-testing-1.0.0.zip -d ~/.claude/skills/     # Codex: ~/.codex/skills/
```

### Option 2: WorkBuddy

Say "install software-testing skill" in chat, or drop the unzipped directory into `~/.workbuddy/skills/`.

### Option 3: From a marketplace

```bash
skillhq install software-testing        # SkillHQ
npx skills add <your-repo> --skill software-testing
```

## Directory structure

```
software-testing/
├── SKILL.md                  trigger routing + W1~W6 workflow + seven ground rules
├── README.md                 this file (read by buyers)
├── LICENSE.txt              MIT
├── CHANGELOG.md             version history
├── references/
│   ├── test-design-techniques.md   seven case-design methods + field spec + coverage matrix
│   ├── pytest-guide.md             layout / fixtures / parametrize / assertions / 7 API dims / CI / flaky
│   ├── frontend-testing.md        pure-frontend Node+jsdom path and three pitfalls
│   ├── defect-and-severity.md     S1~S4 grading, status flow, rejection self-check
│   └── checklists.md              nine categories of test points + requirement challenge list
├── assets/                  four deliverable templates (case / plan / report / defect)
├── scripts/
│   ├── scaffold_pytest.py  one-shot pytest project scaffold (api|ui|both)
│   └── cases_to_xlsx.py    case Markdown table → Excel (multi-sheet)
└── examples/               real case (bio-med frontend project, full test run)
```

## Environment requirements

- **Python 3.9+** (optional; needed for the pytest path; `cases_to_xlsx.py` needs `openpyxl`, degrades to CSV when missing)
- **Node 18+ / jsdom** (optional; needed for the pure-frontend path)
- No network dependency, no API key, no data uploaded

## FAQ

**Q: I don't use pytest — what then?**
A: SKILL.md has a stack-degradation ground rule. For Java/JS projects keep the structure and strategy but swap the syntax to JUnit5/TestNG or Playwright/Jest (mapping table at the end of `references/pytest-guide.md`); pure-frontend projects use Node + jsdom.

**Q: Will it fabricate test results for me?**
A: No. Ground Rule 5 explicitly forbids faking results: when tests cannot actually be executed, mark "NOT EXECUTED" with a reason. The case report itself has 2 such annotations.

**Q: Can I modify it?**
A: MIT — modify freely. Suggest recording the change in `CHANGELOG.md`.

## Version & maintenance

Current version **v1.0.0** (2026-09-19). Fully run on a real project; will iterate with field feedback.
Issues welcome; defects that affect "correctness of conclusions" get priority.

## License

MIT — commercial use, modification, and redistribution allowed; keep the attribution.
