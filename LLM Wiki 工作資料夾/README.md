# LLM Wiki — 大模型研究個人知識庫

> 基於 **Andrej Karpathy LLM Wiki 範式** 構建的持續演化、具複利效應（Compounding）的長效大語言模型研究知識庫。

---

## 💡 核心理念：超越傳統 RAG 的知識複利架構

大多數人使用 LLM 處理文獻時多採用 RAG（檢索增強生成）：每次提問，LLM 從大量片段中重新拼湊答案。這種模式**沒有知識累積**，每次查詢都在從零發現知識。

**LLM Wiki 則完全不同**：
- **知識是編譯沉澱的**：新文獻進入時，LLM 研讀、精煉、更新實體與概念頁、標註新舊觀點衝突、維護全局綜合。
- **Obsidian 是 IDE；LLM 是工程師；Wiki 是 Codebase**。
- **人類負責提出假說、尋找文獻、把關方向；LLM 負責所有繁瑣的頁面撰寫、交叉引用與格式整理**。

---

## 📂 目錄架構

```
.
├── AGENTS.md                  # LLM Agent 的最高執行規範手冊 (繁體中文版)
├── README.md                  # 本指引文件
├── index.md                   # 全局 Wiki 目錄索引 (分類檢索導航)
├── log.md                     # 操作日誌 (Ingest / Query / Lint 事件紀錄)
│
├── raw/                       # 【第一層：原始資料層】(Immutable，只讀不改)
│   ├── papers/                # 原始學術論文 (PDF, Markdown)
│   ├── articles/              # 技術部落格、專欄文章、技術發布說明
│   ├── notes/                 # 研究員個人隨筆、靈感、討論速記
│   └── assets/                # 剪藏圖片與附件 (Obsidian 剪藏圖片存放區)
│
├── wiki/                      # 【第二層：知識資產層】(由 LLM 全權維護與交叉連結)
│   ├── syntheses/             # 演化中的研究綜合論述 (如 llm-research-landscape.md)
│   ├── concepts/              # 核心技術概念 (如 test-time-compute.md, kv-cache.md)
│   ├── models/                # 模型家族與具體模型 (如 deepseek-r1.md, llama-3.md)
│   ├── architectures/         # 模型架構演進 (如 transformer.md, mixture-of-experts.md)
│   ├── methods/               # 訓練、微調與後訓練演算法 (如 grpo.md, dpo.md)
│   ├── agents/                # 自主 Agent、工具調用與 MCP 協議
│   ├── evaluations/           # 基準評測集 (如 swe-bench.md, gpqa.md)
│   ├── organizations/         # 頂尖實驗室與研究機構 (如 openai.md, deepseek.md)
│   └── comparisons/           # 橫向評比與專題對比 (如 reasoning-models-comparison.md)
│
└── templates/                 # 頁面標準模板 (供 Agent 與研究員統一規格)
    ├── source-summary-template.md
    ├── concept-template.md
    ├── model-template.md
    └── comparison-template.md
```

---

## 🚀 快速上手工作流 (Quick Start)

### 步驟 1：在 Obsidian 中開啟工作目錄
1. 打開 **Obsidian** 筆記軟體。
2. 點擊「開啟既有資料夾作為筆記倉庫 (Open folder as vault)」，選取本資料夾：`LLM Wiki 工作資料夾`。
3. 你將立刻看見美麗的雙向連結星系圖（Graph View），以及已為你初始化的種子頁面。

### 步驟 2：文獻攝入 (Ingest)
1. 將你感興趣的論文或文章放入 `raw/papers/` 或 `raw/articles/`。
2. 在 LLM Agent（Antigravity、Claude Code、Codex 等）中下達指令：
   > 「我已將《xxx.pdf》放入 raw/papers/，請依據 AGENTS.md 執行 Ingest 流程，萃取核心亮點並聯動更新相關 Wiki 頁面。」
3. Agent 會自動研讀論文、萃取重點、新建/更新 3~10 個相關概念與模型頁面，並同步登錄至 `index.md` 與 `log.md`。

### 步驟 3：深度提問與知識回流 (Query & Compound)
1. 向 Agent 提出跨文獻的深度研究問題：
   > 「請比對當前主流的後訓練強化學習演算法（如 PPO, DPO, GRPO）在顯存開銷與獎勵穩定性上的取捨，並將分析成果沉澱為一篇橫向對比頁面。」
2. Agent 會調閱 Wiki 中的頁面合成深度分析，並將高價值回答沉澱至 `wiki/comparisons/` 或 `wiki/syntheses/`，更新目錄與日誌。

### 步驟 4：知識庫體檢巡檢 (Lint)
1. 定期下達巡檢指令：
   > 「請對目前的 Wiki 執行 Lint 健康檢查，尋找孤島頁面、潛在矛盾論述，並提出下一步建議探索的研究缺口。」
2. Agent 會梳理連結拓撲、標註斷鏈與未建頁概念，保持知識庫高度整潔健全。

---

## 🛠️ 推薦工具與 Obsidian 插件

- **Obsidian Web Clipper**：瀏覽器插件，一鍵將 arXiv、Substack 或技術部落格完整轉為乾淨的 Markdown 存入 `raw/articles/`。
- **Obsidian Dataview**：根據各頁面 Frontmatter（tags、status、created）動態生成自定義篩選表格。
- **Marp Slides**：直接將 Wiki 綜述頁面轉化為簡報投影片。
- **Git**：本知識庫本質純為文字檔與 Markdown，可直接使用 Git 作為版本控制與分支協同。
