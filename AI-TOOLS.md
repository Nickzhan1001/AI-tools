# AI-tools

AI 協作工具與技能集合，用於在 Claude / Cursor 等環境中擴充 AI 代理能力，包含技能（Skills）、MCP 相關說明與專案規則。

## 專案結構

```
AI-tools/
├── AGENTS.md          # 代理技能清單與使用說明（供 AI 讀取）
├── AI-TOOLS.md        # 本說明檔（專案概覽與結構）
├── .agents/           # Cursor Agent 技能（僅供 Cursor 讀取）
│   └── skills/
│       ├── find-skills/         # 探索與安裝 Agent 技能
│       └── powershell-windows/  # PowerShell 語法與錯誤處理
├── .claude/           # OpenSkills 技能（SKILL.md 與資源，供 npx openskills 使用）
│   └── skills/        # 各技能子目錄（algorithmic-art, docx, pdf, pptx, xlsx, …）
├── .cursor/           # Cursor 規則與設定
│   └── rules/         # .mdc 規則檔
│       ├── exa-search-fetch.mdc  # Exa 搜尋優先、fetch 權限說明
│       ├── no-reasoning.mdc      # 不顯示思考過程
│       └── powershell-only.mdc   # 終端僅用 PowerShell
└── docs/              # 文件
    ├── mcp_doc/       # MCP 相關說明
    │   └── mcp_recommend.md
    └── skills_doc/    # 技能安裝、排名、Anthropic 技能等說明
        ├── agent_skill_install.md
        ├── agent_skill_ranking.md
        └── anthropic_skill.md
```

## 技能（Skills）

專案內建多種技能，供 AI 在執行任務時依情境選用，例如：

| 類別       | 技能範例                                                                                   |
| ---------- | ------------------------------------------------------------------------------------------ |
| 設計與前端 | `frontend-design`、`canvas-design`、`algorithmic-art`、`theme-factory`、`brand-guidelines` |
| 文件與簡報 | `docx`、`pdf`、`pptx`、`xlsx`、`doc-coauthoring`                                           |
| 開發與整合 | `mcp-builder`、`webapp-testing`、`web-artifacts-builder`                                   |
| 內容與溝通 | `internal-comms`、`slack-gif-creator`                                                      |
| 擴充能力   | `skill-creator`、`find-skills`                                                             |

完整清單與觸發情境請見 [AGENTS.md](./AGENTS.md)。

### 使用技能（OpenSkills）

在 shell 中可透過 OpenSkills 讀取技能內容：

```bash
npx openskills read <skill-name>
# 多個技能：npx openskills read skill-one,skill-two
```

## 文件

- **MCP**：`docs/mcp_doc/mcp_recommend.md` — MCP 建議與使用方式
- **技能**：`docs/skills_doc/` — 技能安裝、排名、Anthropic 技能等說明

## 授權與貢獻

依專案實際授權與貢獻方式另行補充。
