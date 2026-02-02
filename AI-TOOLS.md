# AI-tools

AI 協作工具與技能集合，用於在 Claude / Cursor 等環境中擴充 AI 代理能力，包含技能（Skills）、MCP 相關說明與專案規則。

## 專案結構

```
AI-tools/
├── AGENTS.md          # 代理技能清單與使用說明（供 AI 讀取）
├── README.md          # 本說明檔
├── .claude/           # OpenSkills 技能（SKILL.md 與資源）
├── .cursor/           # Cursor 規則與設定
│   └── rules/
└── docs/              # 文件
    ├── mcp_doc/       # MCP 相關說明
    └── skills_doc/    # 技能安裝、排名、Anthropic 技能等說明
```

## 技能（Skills）

專案內建多種技能，供 AI 在執行任務時依情境選用，例如：

| 類別       | 技能範例                                                                                   |
| ---------- | ------------------------------------------------------------------------------------------ |
| 設計與前端 | `frontend-design`、`canvas-design`、`algorithmic-art`、`theme-factory`、`brand-guidelines` |
| 文件與簡報 | `docx`、`pdf`、`pptx`、`xlsx`、`doc-coauthoring`                                           |
| 開發與整合 | `mcp-builder`、`webapp-testing`、`web-artifacts-builder`                                   |
| 內容與溝通 | `internal-comms`、`slack-gif-creator`                                                      |
| 擴充能力   | `skill-creator`                                                                            |

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
