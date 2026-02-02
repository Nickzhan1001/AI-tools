# Agent Skills (OpenSkills) 安裝指南（照做即可用）

適用：Cursor、Claude Code、Windsurf、Aider、Codex、Trae、Qoder 等「會讀取 `AGENTS.md`」的 Coding Agent。

本指南基於 [OpenSkills](https://github.com/numman-ali/openskills)（numman-ali/openskills）：Universal skills loader for AI coding agents，格式與 Claude Code 的 SKILL.md 相容。

## 快速開始（兩行指令）

在專案根目錄執行：

```bash
npx openskills install anthropics/skills
npx openskills sync
```

預設為專案本機安裝（`./.claude/skills`）；使用 `--universal` 則安裝到 `./.agent/skills/`；使用 `--global` 則安裝到 `~/.claude/skills`。

## 前置條件（缺一會失敗）

1. **Node.js 20.6+**（建議 20 LTS 或更新）
2. **Git** 已安裝且在 PATH 中（`git --version` 能執行）
3. 你有一個「專案根目錄」（後續命令都在這個目錄執行）

## 目標狀態（做到這些才算安裝成功）

- 專案裡存在技能目錄：預設 `./.claude/skills/`，或使用 `--universal` 時為 `./.agent/skills/`
- 專案根目錄存在 `AGENTS.md`，且裡面包含 `<available_skills>` 區塊
- 在專案目錄執行 `npx openskills list` 能看到已安裝的 skills

## 技能解析優先順序（由高到低）

Agent 載入 skill 時，會依下列順序尋找（先找到者優先）：

1. `./.agent/skills/`
2. `~/.agent/skills/`
3. `./.claude/skills/`
4. `~/.claude/skills/`

若同時使用 Claude Code 與其他 agent 且共用一個 `AGENTS.md`，建議用 `--universal` 裝到 `./.agent/skills/` 避免與 Claude 外掛市集衝突。

## 安裝步驟（推薦：Universal 模式，相容性最好）

### 步驟 1：安裝 skills 到專案

**從 Anthropic 官方 skills（GitHub）：**

```bash
npx openskills install anthropics/skills --universal
```

**其他來源範例：**

```bash
# 任意 GitHub 倉庫
npx openskills install your-org/your-skills

# 本機路徑
npx openskills install ./local-skills/my-skill

# 私人 Git 倉庫
npx openskills install git@github.com:your-org/private-skills.git
```

- `--universal`：安裝到 `./.agent/skills/`，適合多種 agent 共用。
- `--global`：安裝到 `~/.claude/skills`（全域，非專案專用）。

### 步驟 2：產生/更新 AGENTS.md（讓各類 agent 「發現」 skills）

在專案根目錄執行：

```bash
npx openskills sync
```

會出現互動式選擇：用 Space 選擇要暴露給 agent 的 skills，Enter 確認。

- 跳過提示（例如 CI）：`npx openskills sync -y`
- 自訂輸出檔：`npx openskills sync -o AGENTS.md`（預設即為 `AGENTS.md`，多數工具預設讀專案根目錄的 `AGENTS.md`，一般不建議改名。）

### 步驟 3：驗證安裝（強烈建議做一次）

```bash
npx openskills list
```

並確認存在：`AGENTS.md`、以及 `./.agent/skills/`（使用 `--universal`）或 `./.claude/skills/`（預設）。

## 在 Cursor / Claude Code / Windsurf 等工具中的呼叫方式

多數工具不會自動載入 skill 內容，需讓 agent 先將 skill 讀進上下文。

### 方式 A（推薦）：讓 agent 執行 openskills read，再依指引完成任務

把下面這段提示詞貼給 agent（將 skill 名稱換成你要的）：

```text
請先在專案根目錄執行：npx openskills read frontend-design
然後把讀到的 SKILL 內容載入進上下文，並嚴格按該 skill 的步驟完成：<你的任務>
```

- `npx openskills read <skill-name>` 會輸出該 skill 的完整 SKILL.md 內容（步驟、約束、資源路徑）。
- 多個 skill 可用逗號分隔：`npx openskills read foo,bar`。

### 方式 B：工具無法執行終端機命令時

1. 你在終端機手動執行：`npx openskills read <skill-name>`
2. 將輸出整段複製到對話裡
3. 再讓 agent 依該 skill 執行

## 常用指令一覽

| 指令                                        | 說明                                    |
| ------------------------------------------- | --------------------------------------- |
| `npx openskills install <source> [options]` | 從 GitHub、本機路徑或私人 repo 安裝     |
| `npx openskills sync [-y] [-o <path>]`      | 更新 AGENTS.md（或自訂輸出檔）          |
| `npx openskills list`                       | 列出已安裝的 skills                     |
| `npx openskills read <name>`                | 載入 skill 內容（給 agent 用）          |
| `npx openskills update [name...]`           | 更新已安裝的 skills（不指定則全部更新） |
| `npx openskills manage`                     | 互動式移除 skills                       |
| `npx openskills remove <name>`              | 移除指定 skill                          |

常用選項：`--global`、`--universal`、`-y`/`--yes`（略過提示）、`-o`/`--output <path>`（sync 輸出檔）。

## 更新已安裝的 skills

若 skills 是從 git 倉庫安裝的，可隨時更新：

```bash
npx openskills update
```

只更新特定 skills（逗號分隔）：

```bash
npx openskills update git-workflow,check-branch-first
```

若某個 skill 是在「更新追蹤」功能加入前安裝的，可重新安裝一次以記錄來源，之後即可用 `update` 更新。

## 建立自己的 skill

### 最簡結構

```
my-skill/
└── SKILL.md
```

### 含資源的結構

```
my-skill/
├── SKILL.md
├── references/
├── scripts/
└── assets/
```

安裝自訂 skill：

```bash
npx openskills install ./my-skill
```

撰寫指引可先安裝官方 skills，再讀取 `skill-creator`：

```bash
npx openskills install anthropics/skills
npx openskills read skill-creator
```

## 常見變體

### 全域安裝（不推薦作為唯一方案）

```bash
npx openskills install anthropics/skills --global
```

注意：全域安裝不等於所有工具自動可用，多數工具仍依賴專案內的 `AGENTS.md`；若要在某專案使用，仍建議在該專案執行一次 `npx openskills sync`。

## 故障排查（按順序做）

1. **Node 版本不符**：升級到 Node.js 20.6+
2. **Git 不可用**：確認 `git --version` 能執行
3. **不在專案根目錄**：切到含 `AGENTS.md` 的目錄再執行
4. **AGENTS.md 沒更新**：重新執行 `npx openskills sync` 並確認有勾選 skills
5. **工具看不到 skills**：確認工具會讀取專案根目錄的 `AGENTS.md`；不確定時用「方式 A」強制載入（`npx openskills read <skill-name>`）

## 參考連結

- [OpenSkills 倉庫](https://github.com/numman-ali/openskills)
- [Anthropic skills（anthropics/skills）](https://github.com/anthropics/skills)
